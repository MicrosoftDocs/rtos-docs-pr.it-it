---
title: Capitolo 2-installazione e utilizzo del client SMTP NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client SMTP NetX Duo.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 86f324935ba32aab010b81f825be0a6564983a2e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821689"
---
# <a name="chapter-2---installation-and-use-of-netx-duo-smtp-client"></a>Capitolo 2-installazione e utilizzo del client SMTP NetX Duo

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client SMTP NetX Duo.

## <a name="netx-duo-smtp-client-installation"></a>Installazione client SMTP NetX Duo

Il client SMTP NetX Duo è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include i file seguenti:

- **nxd_smtp_client. c** File di origine C per l'API client SMTP NetX Duo
- **nxd_smtp_client. h** File di intestazione C per l'API client SMTP NetX Duo
- **demo_netxduo_smtp_client. c** Demo per il client SMTP NetX Duo
- **nxd_smtp_client.pdf manuale dell'utente per** API client SMTP NetX Duo

Per usare l'API client SMTP NetX Duo, l'intera distribuzione indicata in precedenza può essere copiata nella stessa directory in cui è installato NetX Duo. Se, ad esempio, NetX Duo è installato nella directory "c:*\Progetto nel*", i file *nxd_smtp_client. h e nxd_smtp_client. c* devono essere copiati in questa directory.

## <a name="using-netx-duo-smtp-client"></a>Uso del client SMTP NetX Duo

Per creare l'applicazione client SMTP NetX Duo, è necessario innanzitutto compilare le librerie ThreadX e NetX Duo e includerle nel progetto di compilazione. L'applicazione deve quindi includere TX *_api. h* e *nx_api. h nel codice sorgente dell'applicazione*. Questa operazione consentirà di abilitare i servizi ThreadX e NetX Duo. Deve inoltre includere *nxd_smtp_client. c* e *nxd_smtp_client. h* dopo *tx_api. h* e *nx_api. h per l'utilizzo dei servizi client SMTP.*

Questi file devono essere compilati in modo analogo agli altri file dell'applicazione e il codice oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per creare un'applicazione client SMTP NetX Duo.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di utilizzo del client SMTP NetX Duo è descritto nella figura 1 riportata di seguito. Il pool di pacchetti per l'istanza IP viene creato usando il servizio nx_packet_pool_create, alla riga 68 e ha un payload di pacchetti molto piccolo. Questo perché l'istanza IP invia solo pacchetti di controllo che non richiedono un payload molto elevato. Il pool di pacchetti client SMTP creato alla riga 84 e viene utilizzato per trasmettere messaggi client SMTP ai dati del server e del messaggio. Il payload del pacchetto è molto più grande. L'istanza IP viene creata nella riga 118 usando lo stesso pool di pacchetti. TCP, obbligatorio per il protocollo SMTP, è abilitato nell'istanza IP alla riga 130.

Nel thread dell'applicazione, il client SMTP viene creato usando il servizio *nxd_smtp_client_create* , alla riga 170. Il servizio *nxd_smtp_client_create* supporta le connessioni al server SMTP sia IPv4 che IPv6, sebbene questo esempio sia limitato a IPv4. Il messaggio di posta elettronica viene quindi inviato al client SMTP per la trasmissione alla riga 184 usando il servizio *nx_smtp_mail_send* . Si noti che la riga dell'oggetto con l'intestazione del contenuto della posta viene creata separatamente dal corpo del messaggio. Si noti inoltre che la richiesta invia messaggi accetta un solo indirizzo di posta elettronica destinatario che si presuppone sia sintatticamente corretto.

Quindi, l'applicazione termina il client SMTP alla riga 200. Il servizio *nx_smtp_client_delete* verifica che la connessione socket sia chiusa e che la porta non sia associata. Si noti che spetta all'applicazione client SMTP eliminare il pool di pacchetti se non è più usato.

```c
/*
   demo_netxduo_smtp_client.c

   This is a small demo of the NetX Duo SMTP Client on the high-performance NetX
   Duo TCP/IP stack.  This demo relies on Thread, NetX Duo and SMTP Client API to
   perform simple SMTP mail transfers in an SMTP client application to an SMTP mail
   server.   */

#include "nx_api.h"
#include "nx_ip.h"
#include "nxd_smtp_client.h"


/* Define the host user name and mail box parameters */
#define USERNAME               "myusername"
#define PASSWORD               "mypassword"
#define FROM_ADDRESS           "my@mycompany.com"
#define RECIPIENT_ADDRESS      "your@yourcompany.com"
#define LOCAL_DOMAIN           "mycompany.com"

#define SUBJECT_LINE           "NetX Duo SMTP Client Demo"
#define MAIL_BODY              "NetX Duo SMTP client is an SMTP client \r\n" \
                               “implementation for embedded devices to send  \r\n" \
                               "email to SMTP servers. This feature is \r\n" \
                               "intended to allow a device to send simple \r\n " \
                               "status reports using the most universal \r\n " \
                               “Internet application, email.\r\n"

/* See the NetX Duo SMTP Client User Guide for how to set the authentication type.
   The most common authentication type is PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE 3


#define CLIENT_IP_ADDRESS  IP_ADDRESS(1,2,3,5)
#define SERVER_IP_ADDRESS  IP_ADDRESS(1,2,3,4)
#define SERVER_PORT        25


/* Define the NetX Duo and ThreadX structures for the SMTP client appliciation. */
NX_PACKET_POOL                  ip_packet_pool;
NX_PACKET_POOL                  client_packet_pool;
NX_IP                           client_ip;
TX_THREAD                       demo_client_thread;
static NX_SMTP_CLIENT           demo_client;


void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
void    demo_client_thread_entry(ULONG info);

/* Define main entry point.  */
int main()
{
    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    UINT    status;
    CHAR    *free_memory_pointer;


    /* Setup the pointer to unallocated memory.  */
    free_memory_pointer =  (CHAR *) first_unused_memory;

    /* Create IP default packet pool. */
    status =  nx_packet_pool_create(&ip_packet_pool, "Default IP Packet Pool",
                                    128, free_memory_pointer, 2048);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* Create SMTP Client packet pool. This is only for transmitting packets to the
       server. It need not be a separate packet pool than the IP default packet pool
       but for more efficient resource use, we use two different packet pools
       because the CLient SMTP messages generally require more payload than IP
       control packets.

       Packet payload depends on the SMTP Client application requirements.  Size of
       packet payload must include IP and TCP headers. For IPv6 connections, IP and
       TCP header data is 60 bytes. For IPv4 IP and TCP header data is 40 bytes (not
       including TCP options). */
    status |=  nx_packet_pool_create(&client_packet_pool, "SMTP Client Packet Pool",
                                     800, free_memory_pointer, (10*800));

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (10*800);

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the client thread */
    status = tx_thread_create(&demo_client_thread, "client_thread",
                              demo_client_thread_entry, 0, free_memory_pointer,
                              2048, 16, 16,
                              TX_NO_TIME_SLICE, TX_DONT_START);

    if (status != NX_SUCCESS)
    {

        printf("Error creating Client thread. Status 0x%x\r\n", status);
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + 4096;


    /* Create Client IP instance. Remember to replace the generic driver
       with a real ethernet driver to actually run this demo! */

    status = nx_ip_create(&client_ip, "SMTP Client IP Instance", CLIENT_IP_ADDRESS,
                          0xFFFFFF00UL, &ip_packet_pool, _nx_ram_network_driver,
                          free_memory_pointer, 2048, 1);


    free_memory_pointer =  free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    status =  nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1040);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1040;

    /* Enable TCP for client. */
    status =  nx_tcp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable ICMP for client. */
    status =  nx_icmp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Start the client thread. */
    tx_thread_resume(&demo_client_thread);

    return;
}


/* Define the smtp application thread task.   */
void    demo_client_thread_entry(ULONG info)
{

    UINT        status;
    UINT        error_counter = 0;
    NXD_ADDRESS server_ip_address;


    tx_thread_sleep(100);

    /* Set up the server IP address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;

    /* The demo client username and password is the authentication
       data used when the server attempts to authentication the client. */

    status =  nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
                                     USERNAME,
                                     PASSWORD,
                                     FROM_ADDRESS,
                                     LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
                                     &server_ip_address, SERVER_PORT);

    if (status != NX_SUCCESS)
    {
        printf("Error creating the client. Status: 0x%x.\n\r", status);
        return;
    }

    /* Create a mail instance with the above text message and recipient info. */
    status =  nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
                                TP_MAIL_PRIORITY_NORMAL,
                                SUBJECT_LINE, MAIL_BODY, sizeof(MAIL_BODY) - 1);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        /* Mail item was not sent. Note that we need not delete the client. The
           error status may be a failed authentication check or a broken connection.
           We can simply call nx_smtp_mail_send again.  */
        error_counter++;
    }

    /* Release resources used by client. Note that the transmit packet
       pool must be deleted by the application if it no longer has use for it.*/
    status = nx_smtp_client_delete(&demo_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    return;
}
```

**Figura 1. Esempio di utilizzo del client SMTP con NetX Duo**

## <a name="client-configuration-options"></a>Opzioni di configurazione client

Sono disponibili diverse opzioni di configurazione con l'API client SMTP NetX Duo. Di seguito è riportato un elenco di tutte le opzioni descritte in dettaglio:

- **NX_SMTP_CLIENT_TCP_WINDOW_SIZE** Questa opzione consente di impostare le dimensioni della finestra di ricezione TCP del client. Questo deve essere impostato su un numero inferiore alle dimensioni MTU dell'hardware Ethernet sottostante e consentire le intestazioni IP e TCP. La dimensione predefinita della finestra TCP del client SMTP NetX Duo è 1460.
- **NX_SMTP_CLIENT_PACKET_TIMEOUT** Questa opzione imposta il timeout per l'allocazione dei pacchetti NetX. Il timeout del pacchetto client SMTP NetX Duo predefinito è di 2 secondi.
- **NX_SMTP_CLIENT_CONNECTION_TIMEOUT** Questa opzione imposta il timeout di connessione socket TCP client. Il timeout di connessione del client SMTP NetX Duo predefinito è di 10 secondi.
- **NX_SMTP_CLIENT_DISCONNECT_TIMEOUT** Questa opzione imposta il timeout di disconnessione socket TCP client. Il timeout di disconnessione del client SMTP NetX Duo predefinito è 5 secondi *. Si noti che se il client SMTP rileva un errore interno, ad esempio una connessione interrotta, può terminare la connessione con un timeout di attesa zero.
- **NX_SMTP_GREETING_TIMEOUT** Questa opzione imposta il timeout per il client per ricevere la risposta del server al messaggio di saluto. Il valore predefinito del client SMTP NetX Duo è 10 secondi.
- **NX_SMTP_ENVELOPE_TIMEOUT** Questa opzione imposta il timeout per il client per ricevere la risposta del server a un comando client. Il valore predefinito del client SMTP NetX Duo è 10 secondi.
- **NX_SMTP_MESSAGE_TIMEOUT** Questa opzione imposta il timeout per il client per ricevere la risposta del server alla ricezione dei dati del messaggio di posta elettronica. Il valore predefinito del client SMTP NetX Duo è 30 secondi.
- **NX_SMTP_CLIENT_SEND_TIMEOUT** Questa opzione definisce l'opzione di attesa del buffer per archiviare la password dell'utente durante l'autenticazione SMTP con il server. Il valore predefinito è 20 byte.
- **NX_SMTP_SERVER_CHALLENGE_MAX_STRING** Questa opzione definisce la dimensione del buffer per l'estrazione della richiesta di verifica del server durante l'autenticazione SMTP. Il valore predefinito è 200 byte. Per l'accesso e l'autenticazione normale, il client SMTP può probabilmente usare un buffer più piccolo.
- **NX_SMTP_CLIENT_MAX_PASSWORD** Questa opzione definisce la dimensione del buffer in cui archiviare la password dell'utente durante l'autenticazione SMTP con il server. Il valore predefinito è 20 byte. 
- **NX_SMTP_CLIENT_MAX_USERNAME** Questa opzione definisce la dimensione del buffer in cui archiviare il nome utente dell'host durante l'autenticazione SMTP con il server. Il valore predefinito è 40 byte. 