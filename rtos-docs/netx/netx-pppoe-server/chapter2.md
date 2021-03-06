---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX PPPoE Server
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS NetX PPPoE Server.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5e93d783299448301c4e79a324ccec01473dbcce3fb96d25d7be352384d4fa53
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796328"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-pppoe-server"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX PPPoE Server

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS NetX PPPoE Server.

## <a name="product-distribution"></a>Distribuzione del prodotto

PPPoE Server per NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_pppoe_server.h:** file di intestazione per PPPoE Server per NetX
- **nx_pppoe_server.c:** file di origine C per PPPoE Server per NetX
- **nx_pppoe_server.pdf:** descrizione PDF di PPPoE Server per NetX
- **demo_netx_pppoe_server.c:** Dimostrazione di NetX PPPoE Server

## <a name="pppoe-server-installation"></a>Installazione del server PPPoE

Per usare PPPoE Server per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_pppoe_server.h* e *nx_pppoe_server.c* devono essere copiati in questa directory.

## <a name="using-pppoe-server"></a>Uso del server PPPoE

L'uso di PPPoE Server per NetX è semplice. Fondamentalmente, il codice dell'applicazione deve includere *nx_pppoe_server.h* dopo aver incluso *tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX. Dopo *nx_pppoe_server.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione PPPoE Server specificate più avanti in questa guida. L'applicazione deve anche *includere nx_pppoe_server.c* nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX PPPoE Server.

## <a name="small-example-system"></a>Small Example System

Di seguito è riportato un esempio che illustra come usare NetX PPPoE Server è descritto nella figura 1.1. In questo esempio il file di inclusione PPPoE Server *nx_pppoe_server.h* viene portato alla riga 50. Il server PPPoE viene quindi creato in *"thread_0_entry*" alla riga 248. Si noti che il server PPPoE deve essere creato dopo la creazione dell'istanza IP. L'istanza IP viene creata e inizializzata nella riga 165. Il blocco di controllo del server PPPoE "*pppoe_server*" è stato definito in precedenza come variabile globale alla riga 79. Le funzioni di notifica vengono impostate alla riga 257. Si noti pppoe_session_data_receive la funzione notify deve essere impostata. Dopo la creazione di IP e PPPoE Server, il processo PPPoE Server di stabilire una sessione PPPoE alla chiamata a nx_pppoe_server_enable alla riga 272.

In generale, il modulo PPPoE deve essere usato con il modulo PPP. In questo esempio, il file di inclusione del server PPP *nx_ppp.h* viene portato alla riga 49. Successivamente, il server PPP viene creato alla riga 174. La riga 182 configura la funzione per l'invio di pacchetti PPP. La riga 188-200 configura gli indirizzi IP e definisce il protocollo pap. La riga 115-139 imposta il nome utente e la password per il protocollo pap.

Dopo aver stabilito la sessione PPPoE. L'applicazione può chiamare nx_pppoe_server_session_get per ottenere le informazioni sulla sessione (indirizzo MAC client e ID sessione) alla riga 281.

Quando l'applicazione non elabora più il traffico PPP, l'applicazione PppCloseInd o nx_pppoe_server_session_terminate terminare la sessione PPPoE.

> [!NOTE]
> In questo esempio il server PPPoE funziona contemporaneamente con lo stack IP normale e condivide un driver Ethernet. Passare lo stesso driver Ethernet per l'istanza IP normale alla riga 165 e l'istanza del server PPPoE alla riga 248.

> [!NOTE]
> Le funzioni vengono fornite dall'implementazione PPPoE per la chiamata da parte del software in base a NX_PPPoE_SERVER_SESSION_CONTROL_ENABELE.

Se definito, abilita la funzionalità che controlla la sessione PPPoE.

Il server PPPoE non risponde automaticamente alla richiesta fino a quando l'applicazione non chiama un'API specifica, se non è definita, il server PPPoE risponde automaticamente alla richiesta. Abilita per impostazione predefinita in nx_pppoe_server.h.

Si noti che ridefinire **NX_PHYSICAL_HEADER** 24 per garantire spazio sufficiente per il riempimento dell'intestazione fisica. Intestazione fisica:14(intestazione Ethernet) + 6 (intestazione PPPoE) + 2 (intestazione PPP) + 2 (aligment a quattro byte).

```c
/**************************************************************************/
/**************************************************************************/
/**                                                                       */
/** NetX PPPoE Server stack Component                                     */
/**                                                                       */
/** This is a small demo of the high-performance NetX PPPoE Server        */
/** stack. This demo includes IP instance, PPPoE Server and PPP Server    */
/** stack. Create one IP instance includes two interfaces to support      */
/** for normal IP stack and PPPoE Server, PPPoE Server can use the        */
/** mutex of IP instance to send PPPoE message when share one Ethernet    */
/** driver. PPPoE Server work with normal IP instance at the same time.   */
/**                                                                       */
/** Note1: Substitute your Ethernet driver instead of                     */
/** _nx_ram_network_driver before run this demo                           */
/**                                                                       */
/** Note2: Prerequisite for using PPPoE.                                  */
/** Redefine NX_PHYSICAL_HEADER to 24 to ensure enough space for filling  */
/** in physical header. Physical header:14(Ethernet header)               */
/** + 6(PPPoE header) + 2(PPP header) + 2(four-byte aligment)             */
/**                                                                       */
/**************************************************************************/
/**************************************************************************/


/*****************************************************************/
/*                            NetX Stack                         */
/*****************************************************************/

                                      /***************************/
                                      /* PPP Server              */
                                      /***************************/

                                      /***************************/
                                      /* PPPoE Server            */
                                      /***************************/
/***************************/         /***************************/
/* Normal Ethernet Type    */         /* PPPoE Ethernet Type     */
/***************************/         /***************************/
/***************************/         /***************************/
/* Interface 0             */         /* Interface 1             */
/***************************/         /***************************/

/*****************************************************************/
/*                     Ethernet Dirver                           */
/*****************************************************************/

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nx_ppp.h"
#include     "nx_pppoe_server.h"

/* Defined NX_PPP_PPPOE_ENABLE if use Express Logic's PPP, since PPP module has been modified to match PPPoE moduler under this definition. */
#ifdef NX_PPP_PPPOE_ENABLE

/*   If the driver is not initialized in other module, define */
/*   NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE to initialize the driver in PPPoE module. */
/*   In this demo, the driver has been initialized in IP module. */

#ifdef NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE

/*   NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE: If defined, enables the feature that */
/*   controls the PPPoE session. PPPoE server does not automatically response to the */
/*   request until application call specific API. */

/* Define the block size. */
#define     NX_PACKET_POOL_SIZE     ((1536 + sizeof(NX_PACKET)) * 30)
#define     DEMO_STACK_SIZE         2048
#define     PPPOE_THREAD_SIZE       2048

/* Define the ThreadX and NetX object control blocks... */
TX_THREAD           thread_0;

/* Define the packet pool and IP instance for normal IP instnace. */
NX_PACKET_POOL      pool_0;
NX_IP               ip_0;

/* Define the PPP Server instance. */
NX_PPP              ppp_server;

/* Define the PPPoE Server instance. */
NX_PPPOE_SERVER     pppoe_server;

/* Define the counters. */
CHAR                *pointer;
ULONG               error_counter;

/* Define thread prototypes. */
void     thread_0_entry(ULONG thread_input);

/***** Substitute your PPP driver entry function here *********/
extern void     _nx_ppp_driver(NX_IP_DRIVER *driver_req_ptr);

/***** Substitute your Ethernet driver entry function here *********/
extern void     _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Define the callback functions. */
void     PppDiscoverReq(UINT interfaceHandle);
void     PppOpenReq(UINT interfaceHandle, ULONG length, UCHAR *data);
void     PppCloseRsp(UINT interfaceHandle);
void     PppCloseReq(UINT interfaceHandle);
void     PppTransmitDataReq(UINT interfaceHandle, ULONG length, UCHAR *data, UINT packet_id);
void     PppReceiveDataRsp(UINT interfaceHandle, UCHAR *data);

/* Define the porting layer function for Express Logic's PPP to simulate TTP's PPP. */
/* Functions to be provided by PPP for calling by the PPPoE Stack. */
void     ppp_server_packet_send(NX_PACKET *packet_ptr);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

UINT verify_login(CHAR *name, CHAR *password)
{

    if ((name[0] == 'm') &&
        (name[1] == 'y') &&
        (name[2] == 'n') &&
        (name[3] == 'a') &&
        (name[4] == 'm') &&
        (name[5] == 'e') &&
        (name[6] == (CHAR) 0) &&
        (password[0] == 'm') &&
        (password[1] == 'y') &&
        (password[2] == 'p') &&
        (password[3] == 'a') &&
        (password[4] == 's') &&
        (password[5] == 's') &&
        (password[6] == 'w') &&
        (password[7] == 'o') &&
        (password[8] == 'r') &&
        (password[9] == 'd') &&
        (password[10] == (CHAR) 0))
            return(NX_SUCCESS);
    else
        return(NX_PPP_ERROR);
}

/* Define what the initial system looks like. */

void tx_application_define(void *first_unused_memory)
{

    UINT status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool for normal IP instance. */
    status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool",
                                    (1536 + sizeof(NX_PACKET)),
                                    pointer, NX_PACKET_POOL_SIZE);
                                    pointer = pointer + NX_PACKET_POOL_SIZE;

    /* Check for error. */
    if (status)
        error_counter++;

    /* Create an normal IP instance. */
    status = nx_ip_create(&ip_0, "NetX IP Instance", IP_ADDRESS(192, 168, 100, 43),
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 2048, 1);
                        pointer = pointer + 2048;

    /* Check for error. */
    if (status)
        error_counter++;

    /* Create the PPP instance. */
    status = nx_ppp_create(&ppp_server, "PPP Instance", &ip_0, pointer, 2048, 1,
                            &pool_0, NX_NULL, NX_NULL);
    pointer = pointer + 2048;

    /* Check for PPP create error. */
    if (status)
        error_counter++;

    /* Set the PPP packet send function. */
    status = nx_ppp_packet_send_set(&ppp_server, ppp_server_packet_send);

    /* Check for PPP packet send function set error. */
    if (status)
        error_counter++;

    /* Define IP address. This PPP instance is effectively the server since it has both IP addresses. */
    status = nx_ppp_ip_address_assign(&ppp_server, IP_ADDRESS(192, 168, 10, 43),                                         IP_ADDRESS(192, 168, 10, 44));

    /* Check for PPP IP address assign error. */
    if (status)
        error_counter++;

    /* Setup PAP, this PPP instance is effectively the server since it will verify the name and password. */
    status = nx_ppp_pap_enable(&ppp_server, NX_NULL, verify_login);

    /* Check for PPP PAP enable error. */
    if (status)
        error_counter++;

    /* Attach an interface for PPP. */
    status = nx_ip_interface_attach(&ip_0, "Second Interface For PPP", 
                            IP_ADDRESS(0, 0, 0, 0), 0, nx_ppp_driver);

    /* Check for error. */
    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for Normal IP Instance. */
    status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
        error_counter++;

    /* Enable ICMP */
    status = nx_icmp_enable(&ip_0);
    if(status)
        error_counter++;

    /* Enable UDP traffic. */
    status = nx_udp_enable(&ip_0);
    if (status)
        error_counter++;

    /* Enable TCP traffic. */
    status = nx_tcp_enable(&ip_0);
    if (status)
        error_counter++;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
                    pointer = pointer + DEMO_STACK_SIZE;
}

/* Define the test threads. */

void     thread_0_entry(ULONG thread_input)
{
UINT     status;
ULONG    ip_status;

    /* Create the PPPoE instance. */
    status = nx_pppoe_server_create(&pppoe_server, (UCHAR *)"PPPoE Server", &ip_0, 0,
                    _nx_ram_network_driver, &pool_0, pointer, PPPOE_THREAD_SIZE, 4);
    pointer = pointer + PPPOE_THREAD_SIZE;
    if (status)
    {
        error_counter++;
        return;
    }

    /* Set the callback notify function. */
    status = nx_pppoe_server_callback_notify_set(&pppoe_server, PppDiscoverReq,
        PppOpenReq, PppCloseRsp, PppCloseReq, PppTransmitDataReq, PppReceiveDataRsp);

    if (status)
    {
        error_counter++;
        return;
    }

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call function function to set the default service Name. */
        /* PppInitInd(length, aData); */
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */

    /* Enable PPPoE Server. */
    status = nx_pppoe_server_enable(&pppoe_server);
    if (status)
    {
        error_counter++;
        return;
    }

    /* Get the PPPoE Client physical address and Session ID after establish PPPoE Session. */
    /*
        status = nx_pppoe_server_session_get(&pppoe_server, interfaceHandle, &client_mac_msw, &client_mac_lsw, &session_id);
        if (status)
            error_counter++;
    */

    /* Wait for the link to come up. */
    status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_ADDRESS_RESOLVED,
                                            &ip_status, NX_WAIT_FOREVER);
    if (status)
    {
        error_counter++;
        return;
    }

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to terminate the PPPoE Session. */
        /* PppCloseInd(interfaceHandle, causeCode); */
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */

}

void     PppDiscoverReq(UINT interfaceHandle)
{

    /* Receive the PPPoE Discovery Initiation Message. */
    
    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to allow TTP's software to define the Service Name field of the PADO packet. */
        PppDiscoverCnf(0, NX_NULL, interfaceHandle);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppOpenReq(UINT interfaceHandle, ULONG length, UCHAR *data)
{

    /* Get the notify that receive the PPPoE Discovery Request Message. */

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to allow TTP's software to accept the PPPoE session. */
        PppOpenCnf(NX_TRUE, interfaceHandle);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppCloseRsp(UINT interfaceHandle)
{

    /* Get the notify that receive the PPPoE Discovery Terminate Message. */

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to allow TTP's software to confirm that the handle has been freed. */
        PppCloseCnf(interfaceHandle);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppCloseReq(UINT interfaceHandle)
{

    /* Get the notify that PPPoE Discovery Terminate Message has been sent. */

}

void     PppTransmitDataReq(UINT interfaceHandle, ULONG length, UCHAR *data, UINT packet_id)
{

    NX_PACKET *packet_ptr;

    /* Get the notify that receive the PPPoE Session data. */

    /* Call PPP Server to receive the PPP data fame. */
    packet_ptr = (NX_PACKET *)(packet_id);
    nx_ppp_packet_receive(&ppp_server, packet_ptr);

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        /* Call PPPoE function to confirm that the data has been processed. */
        PppTransmitDataCnf(interfaceHandle, data, packet_id);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}

void     PppReceiveDataRsp(UINT interfaceHandle, UCHAR *data)
{

    /* Get the notify that the PPPoE Session data has been sent. */

}

/* PPP Server send function. */
void     ppp_server_packet_send(NX_PACKET *packet_ptr)
{

    /* For Express Logic's PPP test, the session should be the first session, so set interfaceHandle as 0. */
    UINT interfaceHandle = 0;

    #ifdef NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE
        while(packet_ptr)
        {

            /* Call functions to be provided by PPPoE for TTP. */
            PppReceiveDataInd(interfaceHandle, (packet_ptr -> nx_packet_append_ptr -
            packet_ptr -> nx_packet_prepend_ptr), packet_ptr -> nx_packet_prepend_ptr);

            /* Move to the next packet structure. */
            packet_ptr = packet_ptr -> nx_packet_next;
        }
    #else
        /* Directly Call PPPoE send function to send out the data through PPPoE module. */
        nx_pppoe_server_session_packet_send(&pppoe_server, interfaceHandle, packet_ptr);
    #endif /* NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE */
}
#endif /* NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE */

#endif /* NX_PPP_PPPOE_ENABLE */
```

Figura 1.1 Esempio di utilizzo del server PPPoE con NetX

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione di PPPoE Server per NetX. L'elenco seguente descrive ogni elemento in dettaglio:

- **NX_DISABLE_ERROR_CHECKING:** definita, questa opzione rimuove il controllo degli errori di base del server PPPoE. Viene in genere usato dopo il debug dell'applicazione.

- **NX_PPPOE_SERVER_SESSION_CONTROL_ENABLE:** se definito, abilita la funzionalità che controlla la sessione PPPoE. Il server PPPoE non risponde automaticamente alla richiesta fino a quando l'applicazione non chiama un'API specifica.

- **NX_PPPOE_SERVER_INITIALIZE_DRIVER_ENABLE:** se definito, consente alla funzionalità di inizializzare il driver Ethernet nel modulo PPPoE. Disabilita per impostazione predefinita.

- **NX_PPPOE_SERVER_THREAD_TIME_SLICE:** opzione Intervallo di tempo per il thread del server PPPoE. Per impostazione predefinita, questo valore è TX_NO_TIME_SLICE.

- **NX_PPPOE_SERVER_MAX_CLIENT_SESSION_NUMBER:** definisce il numero massimo di sessioni client simultanee. Per impostazione predefinita, questo valore è 10.

- **NX_PPPOE_SERVER_MAX_HOST_UNIQ_SIZE:** definisce le dimensioni massime di Host-Uniq. Per impostazione predefinita, questo valore è 32.

- **NX_PPPOE_SERVER_MAX_RELAY_SESSION_ID_SIZE:** definisce le dimensioni massime di Relay-Session-Id. Per impostazione predefinita, questo valore è 12.

- **NX_PPPOE_SERVER_MIN_PACKET_PAYLOAD_SIZE**: specifica le dimensioni minime del payload dei pacchetti per il server PPPoE. Se le dimensioni del payload del pacchetto sono maggiori di questo valore, è possibile evitare il concatenamento dei pacchetti. Per impostazione predefinita, questo valore è 1520 (dimensioni massime del payload di Ethernet 1500, intestazione Ethernet 14, CRC 2 e allineamento a quattro byte 4).

- **NX_PPPOE_SERVER_PACKET_TIMEOUT:** definisce la pozione di attesa (in tick del timer) per l'allocazione di pacchetti o l'aggiunta di dati in pacchetti. Per impostazione predefinita, questo valore **è NX_IP_PERIODIC_RATE** (100 tick).

- **NX_PPPOE_SERVER_START_SESSION_ID:** definisce l'ID sessione di avvio per l'assegnazione alla sessione PPPoE. Per impostazione predefinita, questo valore è 0X4944(valore ASCII per ID).