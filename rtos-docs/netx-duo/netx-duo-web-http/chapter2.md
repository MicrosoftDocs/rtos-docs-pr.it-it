---
title: Capitolo 2 - Installazione e uso di HTTP e HTTPS
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP Web NetX.
author: philmea
ms.author: philmea
ms.date: 07/24/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fd8ab093d15c5413b0d5dac6d35b080674c3a332ec7a028fc462237135880d34
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783425"
---
# <a name="chapter-2---installation-and-use-of-http-and-https"></a>Capitolo 2 - Installazione e uso di HTTP e HTTPS

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP Web NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

HTTP per NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include tre file di origine, due file di inclusione e un file che contiene questo documento, come indicato di seguito:

- **nx_web_http_common.h** File di intestazione comune per NETX Web HTTP
- **nx_web_http_client.h** File di intestazione per il client HTTP per NetX Web
- **nx_web_http_server.h** File di intestazione per server HTTP per NetX Web
- **nx_web_http_client.c** File di origine C per il client HTTP per NetX Web
- **nx_web_http_server.c** File di origine C per il server HTTP per NetX Web
- **nx_tcpserver.c** File di origine C per più socket TCP
- **nx_tcpserver.h** File di intestazione per la definizione dei simboli del server HTTPS
- **nx_md5.c** Algoritmi digest MD5
- **filex_stub.h** File stub se FileX non è presente
- **nx_web_http.pdf** Descrizione di HTTP per NetX Web
- **demo_netx_web_http.c** Dimostrazione di HTTP Web NetX

## <a name="http-installation"></a>Installazione HTTP

Per usare NETX Web HTTP, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*\threadx\arm7\green*", *nx_web_http_client.h* e *nx_web_http_client.c* per le applicazioni client HTTP Web NetX e nx_web_http_server.h , nx_web_http_server.c, nx_tcpserver.c e nx_tcpserver.h per le applicazioni server *HTTP Web NetX. Per le applicazioni client e server, nx_web_http_common.h deve essere presente anche in questa directory. nx_md5.c* deve essere copiato anche in questa directory se viene usata l'autenticazione del digest. Per l'applicazione demo 'ram driver' i file http client e server devono essere copiati nella stessa directory.

Se si usa TLS, è necessario disporre di una directory NetX Secure separata contenente i file di origine TLS.

## <a name="using-http"></a>Uso di HTTP

L'uso di HTTP Web NetX è semplice. Fondamentalmente, il codice dell'applicazione deve includere *nx_web_http_client.h* e/o *nx_web_http_server.h* dopo aver *incluso tx_api.h, fx_api.h* e *nx_api.h* (*nx_web_http_common.h* viene incluso automaticamente). Queste intestazioni consentono all'applicazione di usare rispettivamente ThreadX, FileX e NetX Duo. Per il supporto HTTPS, le intestazioni devono essere incluse dopo che il file *nx_secure_tls.h* è stato incluso per includere il supporto TLS.

Dopo aver incluso i file di intestazione HTTP, il codice dell'applicazione è in grado di effettuare le chiamate di funzione HTTP specificate più avanti in questa guida. L'applicazione deve inoltre essere collegata a nx_web_http_client.c per i client *HTTP(S),* nx_web_http_server.c e nx_tcpserver.c per i server *HTTP(S)* e *nx_md5.c (per l'autenticazione digest)* nel processo di compilazione. Questi file devono essere compilati nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX Web HTTP.

> [!NOTE]
> Se NX_WEB_HTTP_DIGEST_ENABLE non è specificato nel processo di compilazione, non è necessario aggiungere il file *md5.c* all'applicazione. Analogamente, se non sono richieste funzionalità client HTTP, il file *nx_web_http_client.c* può essere omesso e, se non sono necessarie funzionalità del server HTTP, *nx_web_http_server.c* può essere omesso.
>
> A meno NX_WEB_HTTPS_ENABLE non sia definito per abilitare HTTPS (anziché usare solo HTTP in testo non crittografato), NetX Secure TLS non deve essere presente nella compilazione.
>
> Poiché HTTP utilizza i servizi TCP NetX, è necessario che TCP sia abilitato *con la chiamata nx_tcp_enable()* prima di usare HTTP.
>
> Quando si usa HTTPS con NetX Secure TLS, TLS deve essere inizializzato *con nx_secure_tls_initialize()* prima di chiamare routine HTTPS.

## <a name="small-example-system"></a>Small Example System

Un esempio di come usare HTTP Web NetX è descritto nella figura 1.1 riportata di seguito.

> [!CAUTION]
> Viene fornito solo a scopo dimostrativo e non è garantito per la compilazione e l'esecuzione così come sono.
>
> Fare riferimento alla distribuzione del codice di versione HTTPS di NetX Duo per i file di codice sorgente demo che verranno compilati correttamente nell'ambiente nativo per la logica Express.  Tenere anche presente che queste demo vengono mantenute intenzionalmente molto semplici perché sono progettate per introdurre l'applicazione HTTPS e/o NetX Duo HTTPS ai nuovi utenti.

In questo esempio i file di inclusione HTTP *nx_web_http_client.h e nx_web_http_server.h* vengono inseriti (*netx_web_http_common.h* viene incluso automaticamente). Successivamente, il server HTTP viene creato in "*tx_application_define*". Si noti che il blocco di controllo server HTTP "*Server*" è stato definito in precedenza come variabile globale. Al termine della creazione, viene avviato il server HTTPS. Viene quindi creato il client HTTPS. Scrive il file e lo legge nuovamente.

> [!NOTE]
> NX_WEB_HTTPS_ENABLE è definito in questo sistema.

```c
/* This is a small demo of HTTPS on the high-performance NetX Duo TCP/IP stack.
   This demo relies on ThreadX, NetX Duo, and FileX to show an HTML
   transfer from the client and then back from the server.  */

#include  "tx_api.h"
#include  "fx_api.h"
#include  "nx_api.h"
#include  “nx_crypto.h”
#include  “nx_secure_tls_api.h”
#include  “nx_secure_x509.h”
#include  "nx_web_http_client.h"
#include  "nx_web_http_server.h"
#define    DEMO_STACK_SIZE         4096


/* Define the ThreadX and NetX object control blocks...  */

TX_THREAD               thread_0;
TX_THREAD               thread_1;
NX_PACKET_POOL          pool_0;
NX_PACKET_POOL          pool_1;
NX_IP                   ip_0;
NX_IP                   ip_1;
FX_MEDIA                ram_disk;

/* Define HTTP objects.  */

NX_WEB_HTTP_SERVER      my_server;
NX_WEB_HTTP_CLIENT      my_client;

/* Define the counters used in the demo application...  */

ULONG                   error_counter;


/* Define the RAM disk memory.  */

UCHAR                   ram_disk_memory[32000];

/* Include cryptographic routines for TLS. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Define TLS data for HTTPS. */
CHAR crypto_metadata[8928 * NX_WEB_HTTP_SESSION_MAX];
UCHAR tls_packet_buffer[16500];

/* NX_WEB_HTTP_SERVER_SESSION_MAX defaults to 2 in nx_web_http_server.h */
UCHAR server_tls_packet_buffer[16500 * NX_WEB_HTTP_SERVER_SESSION_MAX];

/* Define certificate containers. The server certificate is used to identify the NetX
   Web HTTPS server and the trusted certificate is used by the client to verify the
   server’s identity certificate.  */
NX_SECURE_X509_CERT server_certificate;
NX_SECURE_X509_CERT trusted_certificate;

/* Remote certificates need both an NX_SECURE_X509_CERT container and an associated
   buffer. The number of certificates depends on the remote host, but usually at least
   two certificates will be sent – the identity certificate for the host and the
   certificate that issued the identity certificate. */
NX_SECURE_X509_CERT remote_certificate, remote_issuer;

UCHAR remote_cert_buffer[2000];
UCHAR remote_issuer_buffer[2000];

/* Certificate information for server and client (see NetX Secure TLS reference on X.509
    certificates for more information). Arrays are populated with binary versions Of
    certificates and keys and the corresponding “len” variables are assigned the lengths
    of that data. Trusted certificates do not need a private key. */
const UCHAR server_cert_der[] = { … };
const UINT  server_cert_derlen = … ;
const UCHAR server_cert_key_der[] = { … };
const UINT  server_cert_key_derlen = … ;

const UCHAR trusted_cert_der[] = { … };
const UINT  trusted_cert_derlen = … ;


/* Define function prototypes.  */

void    thread_0_entry(ULONG thread_input);
VOID    _fx_ram_driver(FX_MEDIA *media_ptr) ;
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
UINT    authentication_check(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
             CHAR *resource, CHAR **name, CHAR **password, CHAR **realm);
UINT tls_setup_callback(NX_WEB_HTTP_CLIENT *client_ptr,
   NX_SECURE_TLS_SESSION *tls_session);

/* Define the application's authentication check.  This is called by
   the HTTP server whenever a new request is received.  */
UINT  authentication_check(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
            CHAR *resource, CHAR **name, CHAR **password, CHAR **realm)
{
    /* Just use a simple name, password, and realm for all
       requests and resources.  */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Web HTTP demo";

    /* Request basic authentication.  */
    return(NX_WEB_HTTP_BASIC_AUTHENTICATE);
}

/* Define the TLS setup callback for HTTPS Client. This function is invoked when the
   HTTPS client is started – all TLS per-session initialization should go in here. */
UINT tls_setup_callback(NX_WEB_HTTP_CLIENT *client_ptr,
  NX_SECURE_TLS_SESSION *tls_session)
{
    UINT status;

    /* Initialize and create TLS session. */
    nx_secure_tls_session_create(tls_session, &nx_crypto_tls_ciphers,
        crypto_metadata, sizeof(crypto_metadata));

    /* Allocate space for packet reassembly. */
    nx_secure_tls_session_packet_buffer_set(tls_session, tls_packet_buffer,
        sizeof(tls_packet_buffer));


    /* Add a CA Certificate to our trusted store for verifying incoming server
        certificates. */
    nx_secure_x509_certificate_initialize(&trusted_certificate, trusted_cert_der,
        trusted_cert_der_len, NX_NULL, 0, NULL, 0,
        NX_SECURE_X509_KEY_TYPE_NONE);
    nx_secure_tls_trusted_certificate_add(tls_session, &trusted_certificate);

    /* Need to allocate space for the certificate coming in from the remote host. */
    nx_secure_tls_remote_certificate_allocate(tls_session, &remote_certificate,
        remote_cert_buffer, sizeof(remote_cert_buffer));
    nx_secure_tls_remote_certificate_allocate(tls_session,
        &remote_issuer, remote_issuer_buffer,
        sizeof(remote_issuer_buffer));

    return(NX_SUCCESS);
 }

/* Define main entry point.  */

 int main()
 {
     /* Enter the ThreadX kernel.  */
     tx_kernel_enter();
 }

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    CHAR    *pointer;

    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create the main thread.  */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create packet pool.  */
    nx_packet_pool_create(&pool_0, "NetX Packet Pool 0",
        600, pointer, 8192);
    pointer = pointer + 8192;

    /* Create an IP instance.  */
    nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(1, 2, 3, 4),
        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
        pointer, 4096, 1);
    pointer =  pointer + 4096;

    /* Create another packet pool. */
    nx_packet_pool_create(&pool_1, "NetX Packet Pool 1", 600, pointer, 8192);
    pointer = pointer + 8192;

    /* Create another IP instance.  */
    nx_ip_create(&ip_1, "NetX IP Instance 1", IP_ADDRESS(1, 2, 3, 5),
        0xFFFFFF00UL, &pool_1, _nx_ram_network_driver,
        pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable ARP and supply ARP cache memory for IP Instance 1.  */
    nx_arp_enable(&ip_1, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable TCP processing for both IP instances.  */
    nx_tcp_enable(&ip_0);
    nx_tcp_enable(&ip_1);

    /* Open the RAM disk.  */
    fx_media_open(&ram_disk, "RAM DISK",
        _fx_ram_driver, ram_disk_memory, pointer, 4096);
    pointer += 4096;

    /* Create the NetX Web HTTP Server.  */
    nx_web_http_server_create(&my_server, "My HTTP Server", &ip_1,
        NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
        pointer, 4096, &pool_1, authentication_check, NX_NULL);
    pointer = pointer + 4096;

    /* The TLS server needs an identity certificate which is imported as a binary DER-
        encoded X.509 certificate and its associated private key (e.g. DER-encoded PKCS#1
        RSA private key). */
    nx_secure_x509_certificate_initialize(&server_certificate, server_cert_der,
        server_cert_der_len, NX_NULL, 0,
        server_cert_key_der, server_cert_key_der_len,
        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Setup TLS session data for the TCP server.
        This enables TLS and HTTPS for the server.  */
    nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
        crypto_metadata, sizeof(crypto_metadata), server_tls_packet_buffer,
        sizeof(server_tls_packet_buffer), &server_certificate, NX_NULL, 0,
        NX_NULL, 0, NX_NULL, 0);

    /* Start the HTTP Server.  */
    nx_web_http_server_start(&my_server);
}

/* Define the test thread.  */
void    thread_0_entry(ULONG thread_input)
{
    NX_PACKET   *my_packet;
    UINT        status;

    /* Create an HTTP client instance.  */
    status = nx_web_http_client_create(&my_client, "My Client", &ip_0, &pool_0, 600);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Prepare to send the simple 103-byte HTML file to the Server over HTTPS.  */
    status = nx_web_http_client_put_secure_start(&my_client, IP_ADDRESS(1,2,3,5),
        NX_WEB_HTTPS_SERVER_PORT, "/test.htm", "name", "password", 103, tls_setup_callback, 50);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Allocate a packet.  */
     tatus = nx_web_http_client_request_packet_allocate(&pool_0, &my_packet,
        NX_TCP_PACKET, NX_WAIT_FOREVER);

    /* Check status.  */
    if (status != NX_SUCCESS)
        return;

    /* Build a simple 103-byte HTML page.  */
    nx_packet_data_append(my_packet, "<HTML>\r\n", 8,
        &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet,
        "<HEAD><TITLE>NetX HTTP Test</TITLE></HEAD>\r\n", 44,
        &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<BODY>\r\n", 8,
        &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<H1>NetX Test Page</H1>\r\n", 25,
        &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</BODY>\r\n", 9,
        &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</HTML>\r\n", 9,
        &pool_0, NX_WAIT_FOREVER);

    /* Complete the PUT by writing the total length.  */
    status =  nx_web_http_client_put_packet(&my_client, my_packet, 50);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Now GET the file back!  */
    status =  nx_web_http_client_get_secure_start(&my_client, IP_ADDRESS(1,2,3,5),
        NX_WEB_HTTPS_SERVER_PORT, "/test.htm",
        "name", "password", tls_setup_callback, 50);
 
    /* Check status.  */
    if (status)
        error_counter++;

    /* Get a packet.  */
    status =  nx_web_http_client_response_body_get(&my_client, &my_packet, 20);

    /* Check for an error.  */
    if ((status) || (my_packet -> nx_packet_length != 103))
        error_counter++;

    /* Check to see if we have a packet.  */
    if (status == NX_SUCCESS)
    {

        /* Yes, release it!  */
        nx_packet_release(my_packet);
    }

    /* Make sure TLS shuts down properly. */
    nx_web_http_client_delete(&my_client);

    /* Flush the media.  */
    fx_media_flush(&ram_disk);
}
```

**Figura 1.1 Esempio di uso di HTTPS con NetX e NetX Secure TLS**

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione di HTTP per NetX. Di seguito è riportato un elenco di tutte le opzioni, in cui ogni opzione è descritta in dettaglio. I valori predefiniti sono elencati, ma possono essere ridefinito prima dell'inclusione di *nx_web_http_client.h e nx_web_http_server.h*:

- **NX_DISABLE_ERROR_CHECKING** Definita, questa opzione rimuove il controllo degli errori HTTP di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_WEB_HTTP_DIGEST_ENABLE** Se definito, l'autenticazione tramite il digest MD5 è abilitata nel server HTTPS. Per impostazione predefinita, non è definito.
- **NX_WEB_HTTP_SERVER_PRIORITY** Priorità del thread del server HTTPS. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.
- **NX_WEB_HTTP_NO_FILEX** Definita, questa opzione fornisce uno stub per le dipendenze FileX. Il client HTTPS funzionerà senza alcuna modifica se questa opzione è definita. Il server HTTPS dovrà essere modificato o l'utente dovrà creare alcuni servizi FileX per funzionare correttamente.
- **NX_WEB_HTTP_TYPE_OF_SERVICE** Tipo di servizio necessario per le richieste TCP HTTPS. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio di pacchetti IP.
- **NX_WEB_HTTP_SERVER_THREAD_TIME_SLICE** Numero di tick del timer che il thread del server può eseguire prima di cedere ai thread con la stessa priorità. Il valore predefinito è 2. Si noti che questa opzione è deprecata.
- **NX_WEB_HTTP_FRAGMENT_OPTION** Frammento abilitato per le richieste TCP HTTP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT disabilitare la frammentazione TCP HTTP.
- **NX_WEB_HTTP_SERVER_WINDOW_SIZE** Dimensioni della finestra del socket del server. Per impostazione predefinita, questo valore è 2048 byte.
- **NX_WEB_HTTP_TIME_TO_LIVE** Specifica il numero di router che il pacchetto può superare prima di essere eliminato. Il valore predefinito è impostato su 0x80.
- **NX_WEB_HTTP_SERVER_TIMEOUT** Specifica il numero di tick ThreadX per cui i servizi interni verranno sospesi. Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).
- **NX_WEB_HTTP_SERVER_TIMEOUT_ACCEPT** Specifica il numero di tick ThreadX che i servizi interni sospenderanno per nelle *chiamate* nx_tcp_server_socket_accept(). Il valore predefinito è impostato su (10 \* *NX_IP_PERIODIC_RATE*).
- **NX_WEB_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifica il numero di tick ThreadX che i servizi interni sospenderanno per nelle chiamate *nx_tcp_socket_disconnect().* Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).
- **NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE** Specifica il numero di tick ThreadX che i servizi interni sospenderanno per nelle chiamate *nx_tcp_socket_receive().* Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).
- **NX_WEB_HTTP_SERVER_TIMEOUT_SEND** Specifica il numero di tick ThreadX che i servizi interni sospenderanno per nelle *chiamate nx_tcp_socket_send()* interne. Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).
- **NX_WEB_HTTP_MAX_HEADER_FIELD** **specifica la dimensione massima del campo di intestazione HTTP. Il valore predefinito è 256.**
- **NX_WEB_HTTP_MULTIPART_ENABLE ** **Se definito, consente al server HTTPS di supportare le richieste HTTP multiparte. **
- **NX_WEB_HTTP_SERVER_MAX_PENDING** Specifica il numero di connessioni che possono essere accodati per il server HTTPS. Il valore predefinito è impostato su due volte il numero massimo di sessioni del server.
- **NX_WEB_HTTP_MAX_RESOURCE** Specifica il numero di byte consentiti in un nome di risorsa *fornito dal* client. Il valore predefinito è impostato su 40.
- **NX_WEB_HTTP_MAX_NAME** Specifica il numero di byte consentiti in un nome utente *fornito* dal client. Il valore predefinito è impostato su 20.
- **NX_WEB_HTTP_MAX_PASSWORD** Specifica il numero di byte consentiti in una *password* fornita dal client. Il valore predefinito è impostato su 20.
- **NX_WEB_HTTP_SERVER_SESSION_MAX** Specifica il numero di sessioni simultanee per un server HTTP o HTTPS. Un socket TCP e una sessione TLS (se HTTPS è abilitato) vengono allocati per ogni sessione. Il valore predefinito è impostato su 2.
- **NX_WEB_HTTPS_ENABLE** Se definita, questa macro abilita TLS e HTTPS. Lasciare indefinito per liberare risorse se si desidera solo HTTP in testo non crittografato. Per impostazione predefinita, questa macro non è definita.
- **NX_WEB_HTTPS_KEEPALIVE_DISABLE** Se definita, questa macro disabilita la funzionalità keep-alive HTTP. Per impostazione predefinita, questa macro non è definita.
- **NX_WEB_HTTP_SERVER_MIN_PACKET_SIZE** Specifica le dimensioni minime dei pacchetti nel pool specificato al momento della creazione del server. Le dimensioni minime sono necessarie per garantire che l'intestazione HTTP completa possa essere contenuta in un pacchetto. Il valore predefinito è impostato su 600.
- **NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE** Specifica le dimensioni minime dei pacchetti nel pool specificato durante la creazione del client. Le dimensioni minime sono necessarie per garantire che l'intestazione HTTP completa possa essere contenuta in un pacchetto. Il valore predefinito è impostato su 600.
- **NX_WEB_HTTP_SERVER_RETRY_SECONDS** Impostare il timeout di ritrasmissione socket server in secondi. Il valore predefinito è impostato su 2.
- **NX_WEB_HTTP_ SERVER_RETRY_MAX** In questo modo viene impostato il numero massimo di ritrasmissioni nel socket del server. Il valore predefinito è impostato su 10.
- **NX_WEB_HTTP_ SERVER_RETRY_SHIFT** Questo valore viene usato per impostare il timeout di ritrasmissione successivo. Il timeout corrente viene moltiplicato per il numero di ritrasmissioni fino a questo momento, spostato per il valore dello spostamento del timeout del socket. Il valore predefinito è impostato su 1 per il raddoppio del timeout.
- **NX_WEB_HTTP_SERVER_RETRY_TRANSMIT_QUEUE_DEPTH** Specifica il numero massimo di pacchetti che possono essere accodati nella coda di ritrasmissione socket del server. Se il numero di pacchetti accodati raggiunge questo numero, non è possibile inviare altri pacchetti fino al rilascio di uno o più pacchetti accodati. Il valore predefinito è impostato su 20.
