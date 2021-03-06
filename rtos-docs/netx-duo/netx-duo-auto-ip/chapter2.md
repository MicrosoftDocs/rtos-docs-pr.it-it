---
title: Capitolo 2 - Installazione e uso di Azure RTOS AutoIP di NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del Azure RTOS NetX Duo AutoIP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 56bd8cd3cc361bbe0ec435012251e751af8c1566d01e8d52ff38d2eb9c381bfd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790514"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-autoip"></a>Capitolo 2 - Installazione e uso di Azure RTOS AutoIP di NetX Duo

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del Azure RTOS NetX Duo AutoIP.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS NetX AutoIP può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include tre file di origine, uno di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_auto_ip.h:** file di intestazione per NetX AutoIP
- **nx_auto_ip.c:** File di origine C per NetX AutoIP
- **demo_netx_auto_ip.c:** File di origine C per NetX AutoIP Demo
- **nx_auto_ip.pdf:** descrizione PDF di NetX AutoIP

## <a name="autoip-installation"></a>Installazione di AutoIP

Per usare NetX AutoIP, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_auto_ip.h*, *nx_auto_ip.c* e *demo_netx_auto_ip.c* devono essere copiati in questa directory.

## <a name="using-autoip"></a>Uso di AutoIP

L'uso di NetX AutoIP è semplice. Fondamentalmente, il codice dell'applicazione deve includere *nx_auto_ip.h* dopo aver incluso *tx_api.h* *e nx_api.h* per poter usare ThreadX e NetX. Dopo *nx_auto_ip.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione AutoIP specificate più avanti in questa guida. L'applicazione deve anche *includere nx_auto_ip.c* nel processo di compilazione. Questi file devono essere compilati nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX AutoIP.

> [!NOTE]
> Poiché AutoIP usa i servizi NetX ARP, ARP deve essere abilitato con la chiamata *nx_arp_enable* prima di usare AutoIP.

## <a name="small-example-system"></a>Small Example System

Un esempio della facilità d'uso di NetX AutoIP è descritto nella figura 1.1, illustrata di seguito. In questo esempio, il file di inclusione *AutoIP nx_auto_ip.h* viene portato alla riga 002. L'istanza di NetX AutoIP viene quindi creata in "*tx_application_define*" alla riga 090. Si noti che il blocco di controllo "auto_ip_0" di NetX AutoIP è stato definito in precedenza come variabile globale alla riga 015. Al termine della creazione, viene avviato NetX AutoIP alla riga 098. L'elaborazione della funzione di callback di modifica dell'indirizzo IP inizia dalla riga 105, usata per gestire i conflitti successivi o la possibile risoluzione degli indirizzi DHCP.

> [!NOTE]
> L'esempio seguente presuppone che il dispositivo host sia un dispositivo a singola homed. Per un dispositivo multihomed, l'applicazione host può usare il servizio NetX AutoIP nx_auto_ip_interface_ impostato *per* specificare un'interfaccia di rete secondaria per il probe di un indirizzo IP. Per altre informazioni sulla configurazione di applicazioni multihomed, vedere il Manuale dell'utente di [NetX.](https://docs.microsoft.com/azure/rtos/netx/about-this-guide) Si noti inoltre che l'applicazione host deve usare l'API NetX *nx_status_ip_interface_check* verificare che AutoIP abbia ottenuto un indirizzo IP.

```c
#include "tx_api.h"
#include "nx_api.h"
#include "nx_auto_ip.h"

#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD              thread_0;
NX_PACKET_POOL         pool_0;
NX_IP                  ip_0;

/* Define the AUTO IP structures for the IP instance. */

NX_AUTO_IP             auto_ip_0;

/* Define the counters used in the demo application... */

ULONG                 thread_0_counter;
ULONG                 address_changes;
ULONG                 error_counter;

/* Define thread prototypes. */
void     thread_0_entry(ULONG thread_input);
void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    16, 16, 1, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
                                    pointer, 4096);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Create an IP instance. */
    status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 4096, 1);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
        error_counter++;

    /* Create the AutoIP instance for IP Instance 0. */
    status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Check AutoIP create status. */
    if (status)
        error_counter++;

    /* Start AutoIP instances. */
    status = **nx_auto_ip_start**(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);

    /* Check AutoIP start status. */
    if (status)
        error_counter++;

    /* Register an IP address change function for IP Instance 0. */
    status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
                                        (void *) &auto_ip_0);

    /* Check IP address change notify status. */
    if (status)
        error_counter++;
}

/* Define the test thread. */

void     thread_0_entry(ULONG thread_input)
{

UINT     status;
ULONG    actual_status;

    /* Wait for IP address to be resolved. */
    do
    {

        /* Call IP status check routine. */
        status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
            &actual_status, 10000);

    } while (status != NX_SUCCESS);

    /* Since the IP address is resolved at this point, the application can now fully utilize NetX! */

    while(1)
    {

        /* Increment thread 0's counter. */
        thread_0_counter++;

        /* Sleep... */
        tx_thread_sleep(10);
    }
}

void          ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
{

ULONG         ip_address;
ULONG         network_mask;
NX_AUTO_IP    *auto_ip_ptr;

    /* Setup pointer to auto IP instance. */
    auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;

    /* Pickup the current IP address. */
    nx_ip_address_get(ip_ptr, &ip_address, &network_mask);

    /* Determine if the IP address has changed back to zero. If so, make sure the AutoIP instance is started. */
    if (ip_address == 0)
    {

        /* Get the last AutoIP address for this node. */
        nx_auto_ip_get_address(auto_ip_ptr, &ip_address);

        /* Start this AutoIP instance. */
        nx_auto_ip_start(auto_ip_ptr, ip_address);
        }

    /* Determine if IP address has transitioned to a non local IP address. */
    else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
    {

        /* Stop the AutoIP processing. */
        nx_auto_ip_stop(auto_ip_ptr);
    }

    /* Increment a counter. */
    address_changes++;
}
```

Figura 1.1 Esempio di uso di AutoIP con NetX

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione di NetX AutoIP. Di seguito è riportato un elenco di tutte le opzioni, in cui ogni opzione è descritta in dettaglio:

- **NX_DISABLE_ERROR_CHECKING:** definita, questa opzione rimuove il controllo degli errori autoIP di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_AUTO_IP_PROBE_WAIT:** numero di secondi di attesa prima dell'invio del primo probe. Per impostazione predefinita, questo valore è definito come 1.
- **NX_AUTO_IP_PROBE_NUM:** numero di probe ARP da inviare. Per impostazione predefinita, questo valore è definito come 3.
- **NX_AUTO_IP_PROBE_MIN:** numero minimo di secondi di attesa tra l'invio dei probe. Per impostazione predefinita, questo valore è definito come 1.
- **NX_AUTO_IP_PROBE_MAX:** numero massimo di secondi di attesa tra l'invio dei probe. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_MAX_CONFLICTS:** numero di conflitti AutoIP prima di aumentare i ritardi di elaborazione. Per impostazione predefinita, questo valore è definito come 10.
- **NX_AUTO_IP_RATE_LIMIT_INTERVAL**: numero di secondi per estendere il periodo di attesa quando viene superato il numero totale di conflitti. Per impostazione predefinita, questo valore è definito come 60.
- **NX_AUTO_IP_ANNOUNCE_WAIT:** numero di secondi di attesa prima dell'invio dell'annuncio. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_ANNOUNCE_NUM:** numero di notifiche ARP da inviare. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_ANNOUNCE_INTERVAL:** numero di secondi di attesa tra l'invio delle notifiche. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_DEFEND_INTERVAL:** numero di secondi di attesa tra le comunicazioni di difesa. Per impostazione predefinita, questo valore è definito come 10.
