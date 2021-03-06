---
title: Capitolo 3 - Componenti funzionali di Azure RTOS NetX
description: Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS stack TCP/IP NetX dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4ebb002bc82d13210acf8db44cafb141d33a1b45fa8710295437e2dd15cbcf22
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784346"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx"></a>Capitolo 3 - Componenti funzionali di Azure RTOS NetX

Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS stack TCP/IP NetX dal punto di vista funzionale. 

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Esistono cinque tipi di esecuzione del programma all'interno di un'applicazione NetX: inizializzazione, chiamate all'interfaccia dell'applicazione, thread IP interno, timer periodici IP e driver di rete.

> [!IMPORTANT]
> NetX richiede l'installazione di ThreadX e dipende dall'esecuzione del thread, dalla sospensione, dai timer periodici e dalle funzionalità di esclusione reciproca.

### <a name="initialization"></a>Inizializzazione

Il servizio ***nx_system_initialize** _ deve essere chiamato prima che venga chiamato qualsiasi altro servizio NetX. L'inizializzazione del sistema può essere chiamata dalla routine ThreadX _ *_tx_application_define_** o dai thread dell'applicazione.

Dopo che *** nx_system_initialize** _ restituisce , il sistema è pronto per creare pool di pacchetti e istanze IP. Poiché la creazione di un'istanza IP richiede un pool di pacchetti predefinito, prima di creare un'istanza IP deve esistere almeno un pool di pacchetti NetX. La creazione di pool di pacchetti e istanze IP è consentita dalla funzione di *_inizializzazione_* ThreadX _ tx_application_define * e dai thread dell'applicazione.

Internamente, la creazione di un'istanza IP viene eseguita in due parti. La prima parte viene eseguita nel contesto del chiamante, tx_application_define ***o*** dal contesto di un thread dell'applicazione. Ciò include la configurazione della struttura dei dati IP e la creazione di varie risorse IP, incluso il thread IP interno. La seconda parte viene eseguita durante l'esecuzione iniziale dal thread IP interno. In questo caso viene chiamato per la prima volta il driver di rete, fornito durante la prima parte della creazione dell'indirizzo IP. La chiamata del driver di rete dal thread IP interno consente al driver di eseguire operazioni di I/O e sospendere durante l'elaborazione dell'inizializzazione. Quando il driver di rete viene restituito dall'elaborazione dell'inizializzazione, la creazione dell'indirizzo IP è stata completata.

> [!IMPORTANT]
> Il servizio NetX **nx_ip_status_check** disponibile per ottenere informazioni sull'istanza IP e sul relativo stato dell'interfaccia primaria. Tali informazioni sullo stato includono se il collegamento viene inizializzato, abilitato e l'indirizzo IP viene risolto. Queste informazioni vengono usate per sincronizzare i thread dell'applicazione che devono usare un'istanza IP appena creata. Per i sistemi multihome, vedere "Supporto multihome" di seguito. **nx_ip_interface_status_check** è disponibile per ottenere informazioni sull'interfaccia specificata.

### <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione

Le chiamate dall'applicazione vengono in gran parte effettuate da thread dell'applicazione in esecuzione nell'RTOS ThreadX. Tuttavia, alcuni servizi di inizializzazione, creazione e abilitazione possono essere chiamati ***da tx_application_define***. Le sezioni "Allowed From" del capitolo 4 indicano da quale può essere chiamato ogni servizio NetX.

Nella maggior parte dei casi, l'elaborazione di attività intensive come il calcolo dei checksum viene eseguita all'interno del contesto del thread chiamante, senza bloccare l'accesso di altri thread all'istanza IP. Durante la trasmissione, ad esempio, il calcolo del checksum UDP viene eseguito all'interno ***del servizio nx_udp_socket_send,*** prima di chiamare la funzione di invio IP sottostante. In un pacchetto ricevuto, il checksum UDP viene calcolato nel ***servizio nx_udp_socket_receive,*** eseguito nel contesto del thread dell'applicazione. Ciò consente di evitare lo stallo delle richieste di rete di thread con priorità più elevata a causa dell'elaborazione di calcoli di checksum intensivi nei thread con priorità inferiore.

I valori, ad esempio indirizzi IP e numeri di porta, vengono passati alle funzioni API nell'ordine dei byte dell'host. Internamente questi valori vengono archiviati anche nell'ordine dei byte dell'host. In questo modo gli sviluppatori possono visualizzare facilmente i valori tramite un debugger. Quando questi valori vengono programmati in un frame per la trasmissione, vengono convertiti nell'ordine dei byte di rete.

### <a name="internal-ip-thread"></a>Thread IP interno

Come accennato, ogni istanza IP in NetX ha un proprio thread. La priorità e le dimensioni dello stack del thread IP interno sono definite nel ***nx_ip_create*** servizio. Il thread IP interno viene creato in modalità ready-to-execute. Se il thread IP ha una priorità più alta rispetto al thread chiamante, la precedenza può verificarsi all'interno della chiamata di creazione IP.

Il punto di ingresso del thread IP interno si trova nella funzione interna ***_nx_ip_thread_entry***. All'avvio, il thread IP interno completa prima l'inizializzazione del driver di rete, che consiste nell'effettuare tre chiamate al driver di rete specifico dell'applicazione. La prima chiamata è connettere il driver di rete all'istanza IP, seguita da una chiamata di inizializzazione, che consente al driver di rete di eseguire il processo di inizializzazione. Dopo che il driver di rete è stato restituito dall'inizializzazione (potrebbe essere sospeso durante l'attesa della corretta configurazione dell'hardware), il thread IP interno chiama nuovamente il driver di rete per abilitare il collegamento. 

Dopo che il driver di rete è stato restituito dalla chiamata di abilitazione del collegamento, il thread IP interno entra in un ciclo infinito per verificare la presenza di vari eventi che necessitano di elaborazione per questa istanza IP. Gli eventi elaborati in questo ciclo includono la ricezione posticipata dei pacchetti IP, l'assembly del frammento di pacchetti IP, l'elaborazione ping ICMP, l'elaborazione IGMP, l'elaborazione della coda di pacchetti TCP, l'elaborazione periodica TCP, i timeout dell'assembly del frammento IP e l'elaborazione periodica IGMP. Gli eventi includono anche attività di risoluzione degli indirizzi: elaborazione di pacchetti ARP e elaborazione periodica ARP nella rete IP.

> [!NOTE]
> *Le funzioni di callback NetX, inclusi i callback di ascolto e disconnessione, vengono chiamate dal thread IP interno, non dal thread chiamante originale. L'applicazione deve fare attenzione a non sospendere all'interno di qualsiasi funzione di callback NetX.*

### <a name="ip-periodic-timers"></a>Timer periodici IP
Per ogni istanza IP vengono usati due timer periodici ThreadX. Il primo è un timer di un secondo per ARP, IGMP, timeout TCP e determina anche l'elaborazione del riassemblo dei frammenti IP. Il secondo timer è un timer di 100 ms per l'attivazione del timeout di ritrasmissione TCP.

### <a name="network-driver"></a>Driver di rete
Ogni istanza IP in NetX ha un'interfaccia primaria, identificata dal driver di dispositivo specificato nel ***nx_ip_create*** servizio. Il driver di rete è responsabile della gestione di varie richieste NetX, tra cui trasmissione di pacchetti, ricezione di pacchetti e richieste di stato e controllo.

Per un sistema multi-home, l'istanza IP ha più interfacce, ognuna con un driver di rete associato che esegue queste attività per la rispettiva interfaccia.

Il driver di rete deve anche gestire gli eventi asincroni che si verificano nel supporto. Gli eventi asincroni dai supporti includono la ricezione di pacchetti, il completamento della trasmissione di pacchetti e le modifiche di stato. NetX fornisce al driver di rete diverse funzioni di accesso per gestire vari eventi. Queste funzioni sono progettate per essere chiamate dalla parte di routine del servizio interrupt del driver di rete. Per le reti IP, il driver di rete deve inoltrare tutti i pacchetti ARP ricevuti alla funzione ***_nx_arp_packet_deferred_receive** _internal. Tutti i pacchetti RARP devono essere inoltrati a *_ _ _nx_rarp_packet_deferred_receive_* _ funzione interna. Sono disponibili due opzioni per i pacchetti IP. Se è necessario un invio rapido di pacchetti IP, i pacchetti IP in ingresso devono essere inoltrati a *_ _nx_ip_packet_receive_* _ per l'elaborazione immediata. Ciò migliora notevolmente le prestazioni di NetX nella gestione dei pacchetti IP. In caso contrario, il driver di rete deve inoltrare i pacchetti IP a _*_ _nx_ip_packet_deferred_receive_**. Questo servizio inserisce il pacchetto IP nella coda di elaborazione posticipata in cui viene quindi gestito dal thread IP interno, con il risultato della quantità minima di tempo di elaborazione ISR.

Il driver di rete può anche rinviare l'elaborazione dell'interrupt per l'esecuzione fuori dal contesto del thread IP. In questa modalità, l'ISR deve salvare le informazioni necessarie, chiamare la funzione interna ***_nx_ip_driver_deferred_processing*** e confermare il controller di interrupt. Questo servizio notifica al thread IP di pianificare un callback al driver di dispositivo per completare l'elaborazione dell'evento che causa l'interruzione.

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum dell'intestazione TCP/IP nell'hardware, senza occupare risorse preziose della CPU. Per sfruttare i vantaggi della funzionalità hardware, NetX offre opzioni per abilitare o disabilitare vari calcoli del checksum software in fase di compilazione, nonché per attivare o disattivare il calcolo del checksum in fase di esecuzione. Per informazioni[più dettagliate sulla scrittura di driver di rete NetX,](chapter5.md)vedere " Capitolo 5 Driver di rete NetX ".

### <a name="multihome-support"></a>Supporto multihome
NetX supporta i sistemi connessi a più dispositivi fisici usando una singola istanza IP. Ogni interfaccia fisica viene assegnata a un blocco di controllo dell'interfaccia nell'istanza IP. Le applicazioni che vogliono usare un sistema  multihome devono definire il valore per NX_MAX_PHSYCIAL_INTERFACES al numero di dispositivi fisici collegati al sistema e ricompilare la libreria NetX. Per impostazione **NX_MAX_PHYSICAL_INTERFACES** è impostato su uno, creando un blocco di controllo dell'interfaccia nell'istanza IP.

L'applicazione NetX crea una singola istanza IP per il dispositivo primario usando ***nx_ip_create** _service. Per ogni dispositivo di rete aggiuntivo, l'applicazione collega il dispositivo all'istanza IP usando il servizio _ *_nx_ip_interface_attach_**.

Ogni struttura dell'interfaccia di rete contiene un subset di informazioni di rete sull'interfaccia di rete contenute nel blocco di controllo IP, tra cui l'indirizzo IP dell'interfaccia, subnet mask, le dimensioni dell'MTU IP e le informazioni sull'indirizzo a livello MAC.

> [!IMPORTANT]
> *NetX con supporto multihome è compatibile con le versioni precedenti di NetX. Per impostazione predefinita, i servizi che non accettano informazioni esplicite sull'interfaccia sono il dispositivo di rete primario.*

L'interfaccia primaria ha indice zero nell'elenco di istanze IP. A ogni dispositivo successivo collegato all'istanza IP viene assegnato l'indice successivo.

Tutti i servizi di protocollo di livello superiore per cui è abilitata l'istanza IP, inclusi TCP, UDP, ICMP e IGMP, sono disponibili per tutti i dispositivi collegati.

Nella maggior parte dei casi, NetX può determinare l'indirizzo di origine migliore da usare durante la trasmissione di un pacchetto. La selezione dell'indirizzo di origine si basa sull'indirizzo di destinazione. I servizi NetX vengono forniti per consentire alle applicazioni di specificare un indirizzo di origine specifico da usare, nei casi in cui il più adatto non può essere determinato dall'indirizzo di destinazione. Ad esempio, in un sistema multihome un'applicazione deve inviare un pacchetto a un indirizzo di destinazione multicast o broadcast IP.

I servizi specifici per lo sviluppo di applicazioni multihome includono:

*nx_igmp_multicast_interface_join nx_ip_driver_interface_direct_command nx_ip_interface_address_get nx_ip_interface_address_set nx_ip_interface_attach nx_ip_interface_info_get nx_ip_interface_status_check nx_ip_raw_packet_interface_send nx_udp_socket_interface_send*

Questi servizi sono illustrati in modo più dettagliato in " Capitolo 4 - Descrizione[Azure RTOS NetX Services](chapter4.md)".

### <a name="loopback-interface"></a>Interfaccia di loopback
L'interfaccia di loopback è un'interfaccia di rete speciale senza un collegamento fisico collegato. L'interfaccia di loopback consente alle applicazioni di comunicare usando l'indirizzo di loopback IP 127.0.0.1

Per utilizzare un'interfaccia di loopback logico, assicurarsi che l'opzione configurabile ***NX_DISABLE_LOOPBACK_INTERFACE*** non sia impostata.

### <a name="interface-control-blocks"></a>Blocchi di controllo dell'interfaccia
Il numero di blocchi di controllo dell'interfaccia nell'istanza IP è il numero di interfacce fisiche (definite da ***NX_MAX_PHYSICAL_INTERFACES** _) più l'interfaccia di loopback, se abilitata. Il numero totale di interfacce è definito in __*_ NX_MAX_IP_INTERFACES **.

## <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TCP/IP implementato da NetX è un protocollo a più livelli, il che significa che i protocolli più complessi sono compilati in base a protocolli sottostanti più semplici. In TCP/IP il protocollo di livello più basso si trova a livello *di collegamento* e viene gestito dal driver di rete. Questo livello è in genere destinato a Ethernet, ma può anche essere in fibra ottica, seriale o praticamente qualsiasi supporto fisico.

Sopra il livello di collegamento è disponibile il *livello Rete*. In TCP/IP si tratta dell'ip, che è fondamentalmente responsabile dell'invio e della ricezione di pacchetti semplici attraverso la rete nel modo più efficiente possibile. I protocolli di tipo di gestione come ICMP e IGMP sono in genere anche classificati come livelli di rete, anche se si basano su IP per l'invio e la ricezione.

Il *livello Trasporto* si posiziona sopra il livello di rete. Questo livello è responsabile della gestione del flusso di dati tra gli host nella rete. NetX supporta due tipi di servizi di trasporto: UDP e TCP. I servizi UDP offrono il massimo sforzo per inviare e ricevere dati tra due host in modo senza connessione, mentre TCP offre un servizio orientato alla connessione affidabile tra due entità host.

Questo layering si riflette nei pacchetti di dati di rete effettivi. Ogni livello in TCP/IP contiene un blocco di informazioni denominato intestazione. Questa tecnica di dati circostante (ed eventualmente informazioni sul protocollo) con un'intestazione è in genere denominata incapsulamento dei dati. La figura 1 mostra un esempio di livelli NetX e la Figura 2 mostra l'incapsulamento dei dati risultante per i dati UDP inviati.

![Layering del protocollo](./media/user-guide/protocol-layering.png)

**FIGURA 1. Layering del protocollo**

![Incapsulamento dei dati UDP](./media/user-guide/udp-data-encapsulation.png)

**FIGURA 2. Incapsulamento dei dati UDP**

## <a name="packet-pools"></a>Pool di pacchetti

L'allocazione di pacchetti in modo rapido e deterministico è sempre una sfida nelle applicazioni di rete in tempo reale. A questo scopo, NetX offre la possibilità di creare e gestire più pool di pacchetti di rete di dimensioni fisse.

Poiché i pool di pacchetti NetX sono costituiti da blocchi di memoria di dimensioni fisse, non si verificano mai problemi di frammentazione interni. Naturalmente, la frammentazione causa un comportamento intrinsecamente non deterministico.

Inoltre, il tempo necessario per allocare e liberare un pacchetto NetX è necessario per la semplice manipolazione dell'elenco collegato. Inoltre, l'allocazione e la deallocazione dei pacchetti vengono eseguite all'inizio dell'elenco disponibile. In questo modo si garantisce la massima velocità di elaborazione dell'elenco collegato.

La mancanza di flessibilità è in genere lo svantaggio principale dei pool di pacchetti di dimensioni fisse. Determinare le dimensioni ottimali del payload dei pacchetti che gestisce anche il pacchetto in ingresso nel caso peggiore è un'attività difficile. I pacchetti NetX affrontano questo problema con una funzionalità facoltativa denominata *concatenamento di pacchetti*. Un pacchetto di rete effettivo può essere costituito da uno o più pacchetti NetX collegati tra loro. Inoltre, l'intestazione del pacchetto mantiene un puntatore all'inizio del pacchetto. Quando vengono aggiunti altri protocolli, questo puntatore viene semplicemente spostato indietro e la nuova intestazione viene scritta direttamente davanti ai dati. Senza la tecnologia dei pacchetti flessibile, lo stack dovrebbe allocare un altro buffer e copiare i dati in un nuovo buffer con la nuova intestazione, che richiede un'elaborazione intensiva.

Poiché le dimensioni di ogni payload del pacchetto sono fisse per un determinato pool di pacchetti, i dati dell'applicazione di dimensioni superiori a quelle del payload richiedono più pacchetti concatenati. Quando si compila un pacchetto con i dati utente, l'applicazione deve usare il servizio ***nx_packet_data_append***. Questo servizio sposta i dati dell'applicazione in un pacchetto. Nelle situazioni in cui un pacchetto non è sufficiente per contenere i dati utente, vengono allocati pacchetti aggiuntivi per archiviare i dati utente. Per usare il concatenamento dei pacchetti, il driver deve essere in grado di ricevere o trasmettere da pacchetti concatenati.

Ogni pool di memoria di pacchetti NetX è una risorsa pubblica. NetX non pone vincoli sulla modalità di utilizzo dei pool di pacchetti.

### <a name="packet-pool-memory-area"></a>Area di memoria del pool di pacchetti
L'area di memoria per il pool di pacchetti viene specificata durante la creazione. Analogamente ad altre aree di memoria per gli oggetti ThreadX e NetX, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. Si tratta di una funzionalità importante a causa della notevole flessibilità che offre all'applicazione. Si supponga, ad esempio, che un prodotto di comunicazione abbia un'area di memoria ad alta velocità per i buffer di rete. Questa area di memoria viene facilmente utilizzata rendendola in un pool di memoria di pacchetti NetX.

### <a name="creating-packet-pools"></a>Creazione di pool di pacchetti
I pool di pacchetti vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Non sono previsti limiti al numero di pool di memoria di pacchetti in un'applicazione NetX.

### <a name="packet-header-nx_packet"></a>Intestazione pacchetto NX_PACKET
Per impostazione predefinita, NetX inserisce l'intestazione del pacchetto immediatamente prima dell'area del payload del pacchetto. Il pool di memoria dei pacchetti è fondamentalmente una serie di pacchetti, ovvero intestazioni seguite immediatamente dal payload dei pacchetti. L'intestazione del ***pacchetto ( NX_PACKET***) e il layout del pool di pacchetti sono mostrati nella figura 3.

Per i driver di dispositivi di rete che sono in grado di eseguire zero operazioni di copia, in genere l'indirizzo iniziale dell'area del payload del pacchetto viene programmato nella logica DMA. Alcuni motori DMA hanno requisiti di allineamento nell'area del payload.

> [!IMPORTANT]
> *Il driver di rete a deve chiamare la funzione ***nx_packet_transmit_release** _ al termine della trasmissione di un pacchetto. Questa funzione verifica che il pacchetto non sia in una coda di output TCP prima di essere effettivamente inserito nuovamente nel pool disponibile. La mancata chiamata di questa funzione può causare problemi behavior._

![Layout dell'intestazione del pacchetto e del pool di pacchetti](./media/user-guide/packet-header-packet-pool-layout.png)

**FIGURA 3. Layout dell'intestazione del pacchetto e del pool di pacchetti**

I campi dell'intestazione del pacchetto sono definiti come illustrato nella tabella seguente. Si noti che questa tabella non è un elenco completo di tutti i membri nella *NX_PACKET* struttura .

| Intestazione del pacchetto          | Scopo                                                                                                                                                                                                                                                                                                                            |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *nx_packet_pool_owner*   | Questo campo punta al pool di pacchetti proprietario di questo particolare pacchetto. Quando il pacchetto viene rilasciato, viene rilasciato a questo pool specifico. Con la proprietà del pool all'interno di ogni pacchetto, è possibile che un datagramma si estendono su più pacchetti da più pool di pacchetti.                                                         |
| *nx_packet_next*         | Questo campo punta al pacchetto successivo all'interno dello stesso frame. Se NULL, non sono presenti pacchetti aggiuntivi che fanno parte del frame. |
| *nx_packet_last*         | Questo campo punta all'ultimo pacchetto all'interno dello stesso pacchetto di rete. Se NULL, questo pacchetto rappresenta l'intero pacchetto di rete.  |
| *nx_packet_length*       | Questo campo contiene il numero totale di byte nell'intero pacchetto di rete, incluso il totale di tutti i byte in tutti i pacchetti concatenati dal *nx_packet_next* di rete. |
| *nx_packet_ip_interface* | Questo campo è il blocco di controllo dell'interfaccia assegnato al pacchetto quando viene ricevuto dal driver di interfaccia e da NetX per i pacchetti in uscita. Un blocco di controllo dell'interfaccia descrive l'interfaccia, ad esempio l'indirizzo di rete, l'indirizzo MAC, l'indirizzo IP e lo stato dell'interfaccia, ad esempio il collegamento abilitato e il mapping fisico obbligatorio. |
| *nx_packet_data_start*   | Questo campo punta all'inizio dell'area del payload fisico di questo pacchetto. Non deve essere immediatamente dopo l'intestazione NX_PACKET, ma questa è l'impostazione predefinita per ***il nx_packet_pool_create*** servizio. |
| *nx_packet_data_end*     | Questo campo punta alla fine dell'area del payload fisico di questo pacchetto. La differenza tra questo campo e il campo nx_packet_data_start rappresenta le dimensioni del payload. |
| *nx_packet_prepend_ptr*  | Questo campo punta alla posizione in cui i dati del pacchetto, ovvero l'intestazione del protocollo o i dati effettivi, vengono aggiunti davanti ai dati del pacchetto esistenti (se presenti) nell'area del payload del pacchetto. Deve essere maggiore o uguale alla posizione del *puntatore nx_packet_data_start* e minore o uguale al puntatore *nx_packet_append_ptr.*  *Per motivi di prestazioni, NetX presuppone che, quando il pacchetto viene passato ai servizi NetX per la trasmissione, il puntatore anteposto punti all'indirizzo allineato alle parole lunghe.* |
| *nx_packet_append_ptr*    | Questo campo punta alla fine dei dati attualmente presenti nell'area del payload del pacchetto. Deve essere compreso tra la posizione di memoria a cui punta *nx_packet_prepend_ptr* e *nx_packet_data_end*. La differenza tra questo campo e *il campo nx_packet_prepend_ptr* rappresenta la quantità di dati in questo pacchetto. |
| *nx_packet_fragment_next* | Questo campo viene usato per contenere i pacchetti frammentati fino a quando l'intero pacchetto non può essere riassemblato. |
| *nx_packet_pad*           | Questo campo definisce la lunghezza del riempimento in parole a 4 byte per ottenere il requisito di allineamento desiderato. Questo campo viene rimosso *se NX_PACKET_HEADER_PAD* non è definito. |
|  |  |

### <a name="packet-header-offsets"></a>Offset dell'intestazione del pacchetto

Le dimensioni dell'intestazione del pacchetto vengono definite per consentire spazio sufficiente per contenere le dimensioni dell'intestazione. Il *nx_packet_allocate* viene usato per allocare un pacchetto e regola il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato. Il tipo di pacchetto indica a NetX l'offset necessario per inserire l'intestazione del protocollo (ad esempio UDP, TCP o ICMP) davanti ai dati del protocollo.

In NetX sono definiti i tipi seguenti per prendere in considerazione l'intestazione IP e l'intestazione del livello fisico (Ethernet) nel pacchetto. Nel secondo caso, si presuppone che siano 16 byte tenendo in considerazione l'allineamento a 4 byte richiesto. I pacchetti IP sono ancora definiti in NetX per l'allocazione di pacchetti per le reti IP da parte delle applicazioni. La tabella seguente mostra i simboli definiti:

| Tipo di pacchetto   | Valore |
|---------------|-------|
| NX_IP_PACKET  | 0x24  |
| NX_UDP_PACKET | 0x2c  |
| NX_TCP_PACKET | 0x38  |
|               |       |

### <a name="pool-capacity"></a>Capacità del pool
Il numero di pacchetti in un pool di pacchetti è una funzione delle dimensioni del payload e del numero totale di byte nell'area di memoria fornita al servizio di creazione del pool di pacchetti. La capacità del pool viene calcolata dividendo le dimensioni del pacchetto (incluse le dimensioni dell'intestazione NX_PACKET, le dimensioni del payload e l'allineamento appropriato) nel numero totale di byte nell'area di memoria fornita.

### <a name="thread-suspension"></a>Sospensione dei thread
I thread dell'applicazione possono essere sospesi durante l'attesa di un pacchetto da un pool vuoto. Quando un pacchetto viene restituito al pool, il thread sospeso viene assegnato e ripreso.

Se più thread vengono sospesi nello stesso pool di pacchetti, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

### <a name="pool-statistics-and-errors"></a>Statistiche ed errori del pool
Se abilitata, il software di gestione dei pacchetti NetX **Errors** tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per i pool di pacchetti vengono mantenute le statistiche e i report degli errori seguenti:

* Totale pacchetti nel pool
* Pacchetti liberi nel pool
* Richieste di allocazione vuote del pool
* Sospensioni di allocazione vuote del pool
* Versioni di pacchetti non valide

Tutte queste statistiche e segnalazioni errori, ad eccezione del numero totale e gratuito di pacchetti nel pool, sono incorporate nella libreria NetX, a meno che **non venga** definito * NX_DISABLE_PACKET_INFO _ . Questi dati sono disponibili per l'applicazione con il servizio _ *_nx_packet_pool_info_get_**.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Blocco di controllo del pool di pacchetti NX_PACKET_POOL

Le caratteristiche di ogni pool di memoria di pacchetti si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio l'elenco collegato di pacchetti gratuiti, il numero di pacchetti liberi e le dimensioni del payload per i pacchetti in questo pool. Questa struttura è definita nel file *nx_api.h.*

I blocchi di controllo del pool di pacchetti possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

## <a name="ip-protocol"></a>Protocollo IP

Il componente IP (Internet Protocol) di NetX è responsabile dell'invio e della ricezione di pacchetti IP su Internet. In NetX è il componente responsabile dell'invio e della ricezione di messaggi TCP, UDP, ICMP e IGMP, utilizzando il driver di rete sottostante.

NetX supporta il protocollo IP (RFC 791)

### <a name="ip-addresses"></a>Indirizzi IP

Ogni host su Internet ha un identificatore univoco a 32 bit denominato indirizzo IP. Esistono cinque classi di indirizzi IP, come descritto nella figura 4. Gli intervalli delle cinque classi di indirizzi IP sono i seguenti:

| Classe | Intervallo                        |
|-------|------------------------------|
| Una     | Da 0.0.0.0 a 127.255.255.255   |
| B     | Da 128.0.0.0 a 191.255.255.255 |
| C     | Da 192.0.0.0 a 223.255.255.255 |
| D     | Da 224.0.0.0 a 239.255.255.255 |
| E     | Da 240.0.0.0 a 247.255.255.255 |

**7 bit a 24 bit**

![Struttura degli indirizzi IP](./media/user-guide/ip-address-structure.png)

**FIGURA 4. Struttura degli indirizzi IP**

Esistono anche tre tipi di specifiche di indirizzo: *unicast,* *broadcast* e *multicast.* Gli indirizzi unicast sono gli indirizzi IP che identificano un host specifico su Internet. Gli indirizzi unicast possono essere un indirizzo IP di origine o di destinazione. Un indirizzo di trasmissione identifica tutti gli host in una rete o in una sotto rete specifica e può essere usato solo come indirizzi di destinazione. Gli indirizzi broadcast vengono specificati con la parte dell'ID host dell'indirizzo impostata su uno. Gli indirizzi multicast (classe D) specificano un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e uscire ogni volta che desiderano.

> [!IMPORTANT]
> *Solo i protocolli senza connessione come UDP su IP possono usare la trasmissione e la funzionalità di trasmissione limitata del gruppo multicast.*

> [!IMPORTANT]
> *Macro* IP_ADDRESS è *definito in*  * **nx_api.h** _. Consente di specificare facilmente gli indirizzi IP usando virgole anziché punti. Ad esempio, IP_ADDRESS(128,0,0,0) _specifies'indirizzo della prima classe B illustrato nella figura 4.*

### <a name="ip-gateway-address"></a>Indirizzo gateway IP

I gateway di rete assiste gli host nelle proprie reti per l'inoltro di pacchetti destinati a destinazioni esterne al dominio locale. Ogni nodo è a conoscenza dell'hop successivo a cui inviare, ovvero l'hop di destinazione di uno dei nodi adiacenti o tramite una tabella di routing statica pre-programmata. Tuttavia, se questi approcci hanno esito negativo, il nodo deve inoltrare il pacchetto al gateway predefinito, che contiene altre informazioni su come instradare il pacchetto alla destinazione. Si noti che il gateway predefinito deve essere accessibile direttamente tramite una delle interfacce fisiche collegate all'istanza IP. L'applicazione chiama ***nx_ip_gateway_address_set*** per configurare l'indirizzo IP predefinito del gateway.

### <a name="ip-header"></a>Intestazione IP

Per poter essere inviato su Internet, qualsiasi pacchetto IP deve avere un'intestazione IP. Quando i protocolli di livello superiore (UDP, TCP, ICMP o IGMP) chiamano il componente IP per inviare un pacchetto, il modulo di trasmissione IP inserisce un'intestazione IP davanti ai dati. Al contrario, quando i pacchetti IP vengono ricevuti dalla rete, il componente IP rimuove l'intestazione IP dal pacchetto prima del recapito ai protocolli di livello superiore. La figura 5 mostra il formato dell'intestazione IP.

![Formato intestazione IP](./media/user-guide/ip-header-format.png)

**FIGURA 5. Formato intestazione IP**

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in big endian formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso. Ad esempio, la versione a 4 bit e la lunghezza dell'intestazione a 4 bit dell'intestazione IP devono trovarsi sul primo byte dell'intestazione.*

I campi dell'intestazione IP sono definiti come segue:

**Scopo campo intestazione IP**

***Versione a 4 bit*** Questo campo contiene la versione dell'indirizzo IP rappresentato da questa intestazione. Per IP versione 4, che è ciò che Supporta NetX, il valore di questo campo è 4.

***Lunghezza dell'intestazione a 4 bit*** Questo campo specifica il numero di parole a 32 bit nell'intestazione IP. Se non sono presenti parole di opzione, il valore per questo campo è 5.

***Tipo di servizio (TOS)*** a 8 bit Questo campo specifica il tipo di servizio richiesto per questo pacchetto IP. Le richieste valide sono le seguenti:

| **Richiesta TOS**     | **Valore** |
| ------------------- | --------- |
| Normale              | 0x00      |
| Ritardo minimo       | 0x10      |
| Numero massimo di dati        | 0x08      |
| Affidabilità massima | 0x04      |
| Costo minimo        | 0x02      |

***Lunghezza totale a 16 bit*** Questo campo contiene la lunghezza totale del datagramma IP in byte, inclusa l'intestazione IP. Un datagramma IP è l'unità di base delle informazioni disponibili in una rete Internet TCP/IP. Contiene una destinazione e un indirizzo di origine oltre ai dati. Poiché si tratta di un campo a 16 bit, la dimensione massima di un datagramma IP è 65.535 byte.

***Identificazione a 16 bit*** Il campo è un numero usato per identificare in modo univoco ogni datagramma IP inviato da un host. Questo numero viene in genere incrementato dopo l'invio di un datagramma IP. È particolarmente utile per assemblare frammenti di pacchetti IP ricevuti.

***Flag a 3 bit*** Questo campo contiene informazioni sulla frammentazione IP. Il bit 14 è il bit "don't fragment". Se questo bit è impostato, il datagramma IP in uscita non verrà frammentato. Il bit 13 è il bit "più frammenti". Se questo bit è impostato, sono presenti più frammenti. Se questo bit è chiaro, questo è l'ultimo frammento del pacchetto IP.

**Scopo campo intestazione IP**

***Offset del frammento a 13 bit*** Questo campo contiene i 13 bit superiori dell'offset del frammento. Per questo problema, gli offset dei frammenti sono consentiti solo sui limiti a 8 byte. Il primo frammento di un datagramma IP frammentato avrà il bit "more fragments" impostato e un offset di 0.

***Durata (TTL)*** a 8 bit Questo campo contiene il numero di router che questo datagramma può superare, limitando la durata del datagramma.

***Protocollo a 8 bit*** Questo campo specifica il protocollo che usa il datagramma IP. Di seguito è riportato un elenco di protocolli validi e dei relativi valori:

| Protocollo | Valore |
|----------|-------|
| ICMP     | 0x01  |
| Igmp     | 0x02  |
| TCP      | 0X06  |
| UDP      | 0X11  |
|          |       |


***Checksum a 16 bit*** Questo campo contiene il checksum a 16 bit che copre solo l'intestazione IP. Sono disponibili checksum aggiuntivi nei protocolli di livello superiore che coprono il payload IP.

***Indirizzo IP di origine a 32 bit*** Questo campo contiene l'indirizzo IP del mittente ed è sempre un indirizzo host.

***Indirizzo IP di destinazione a 32 bit*** Questo campo contiene l'indirizzo IP del ricevitore o dei ricevitori se l'indirizzo è un indirizzo broadcast o multicast.

### <a name="creating-ip-instances"></a>Creazione di istanze IP

Le istanze IP vengono create durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. L'indirizzo IP iniziale, network mask, il pool di pacchetti predefinito, il driver multimediale e la memoria e la priorità del thread IP interno sono definiti dal *nx_ip_create* servizio. Se l'applicazione inizializza l'istanza IP con il relativo indirizzo IP impostato su un indirizzo non valido (0.0.0.0), si presuppone che l'indirizzo di interfaccia verrà risolto dalla configurazione manuale in un secondo momento, tramite RARP o tramite DHCP o protocolli simili.

Per i sistemi con più interfacce di rete, l'interfaccia primaria viene designata quando si *chiama nx_ip_create*. Ogni interfaccia aggiuntiva può essere collegata alla stessa istanza IP chiamando *nx_ip_interface_attach*. Questo servizio archivia le informazioni sull'interfaccia di rete (ad esempio indirizzo IP, network mask) nel blocco di controllo dell'interfaccia e associa l'istanza del driver al blocco di controllo dell'interfaccia nell'istanza IP. Quando il driver riceve un pacchetto di dati, deve archiviare le informazioni sull'interfaccia nella struttura NX_PACKET prima di inoltrarla alla logica di ricezione IP. Si noti che un'istanza IP deve essere già stata creata prima di collegare le interfacce.

 ### <a name="ip-send"></a>Invio IP
 L'elaborazione delle trasmissioni IP in NetX è molto semplificata.

Il puntatore anteposto nel pacchetto viene spostato indietro per contenere l'intestazione IP. L'intestazione IP viene completata (con tutte le opzioni specificate dal livello del protocollo chiamante), il checksum IP viene calcolato inline e il pacchetto viene inviato al driver di rete associato. Inoltre, la frammentazione in uscita viene coordinata anche dall'interno dell'elaborazione di invio IP.

Per IP, NetX avvia le richieste ARP se è necessario il mapping fisico per l'indirizzo IP di destinazione.

> [!IMPORTANT]
> Per la connettività IP, i pacchetti che richiedono la risoluzione degli indirizzi *IP (ad esempio, il mapping fisico)* vengono accodati nella coda ARP finché il numero di pacchetti in coda supera la profondità della coda ARP (definita dal simbolo ***NX_ARP_MAX_QUEUE_DEPTH**). Se viene* raggiunta la profondità della coda, NetX rimuoverà il pacchetto meno recente nella coda e continuerà ad attendere la risoluzione degli indirizzi per i *pacchetti rimanenti accodati. D'altra parte, se una voce ARP* non viene risolta, i pacchetti in sospeso nella voce ARP vengono rilasciati in caso di timeout della voce ARP.

Per i sistemi con più interfacce di rete, NetX sceglie un'interfaccia basata sull'indirizzo IP di destinazione. La procedura seguente si applica al processo di selezione:

1. Se un indirizzo di destinazione è broadcast IP o multicast e se viene specificata un'interfaccia in uscita valida, utilizzare tale interfaccia. In caso contrario, viene utilizzata la prima interfaccia fisica.

2. Se l'indirizzo di destinazione viene trovato nella tabella di routing statico, viene usata l'interfaccia associata al gateway.

3. Se la destinazione è on-link, viene usata l'interfaccia on-link.

4. Se l'indirizzo di destinazione è un indirizzo di loopback 127.0.0.1, viene usata l'interfaccia di loopback.

5. Se il gateway predefinito è configurato correttamente, usare l'interfaccia associata al gateway predefinito per trasmettere il pacchetto.

6. Il pacchetto di output viene eliminato se tutte le attività precedenti hanno esito negativo.

### <a name="ip-receive"></a>Ricezione IP

L'elaborazione della ricezione IP viene chiamata dal driver di rete o dal thread IP interno (per l'elaborazione dei pacchetti nella coda di pacchetti posticipata ricevuta). L'elaborazione della ricezione IP esamina il campo del protocollo e tenta di inviare il pacchetto al componente del protocollo appropriato. Prima che il pacchetto venga effettivamente inviato, l'intestazione IP viene rimossa spostando il puntatore anteposto oltre l'intestazione IP.

L'elaborazione della ricezione IP rileva anche i pacchetti IP frammentati ed esegue i passaggi necessari per riassemblarli se la frammentazione è abilitata. Se la frammentazione è necessaria ma non abilitata, il pacchetto viene eliminato.

NetX determina l'interfaccia di rete appropriata in base all'interfaccia specificata nel pacchetto. Se l'interfaccia del pacchetto è NULL, NetX imposta come predefinita l'interfaccia primaria. Questa operazione viene eseguita per garantire la compatibilità con i driver NetX Ethernet legacy.

### <a name="raw-ip-send"></a>Invio IP non elaborato

Un pacchetto IP non elaborato è un frame IP che contiene il payload del protocollo di livello superiore non supportato (ed elaborato) direttamente da NetX. Un pacchetto non elaborato consente agli sviluppatori di definire le proprie applicazioni basate su IP. Un'applicazione può inviare pacchetti IP non elaborati direttamente usando il servizio ***nx_ip_raw_packet_send** _ se l'elaborazione dei pacchetti IP non elaborati è stata abilitata _*_con il nx_ip_raw_packet_enabled_*_ servizio. Se l'indirizzo di destinazione è un indirizzo multicast o broadcast, tuttavia, NetX per impostazione predefinita viene impostata sulla prima interfaccia (primaria). Pertanto, per inviare tali pacchetti su interfacce secondarie, l'applicazione deve usare il servizio _ nx_ip_raw_packet_interface_send * per specificare l'indirizzo di origine da usare per il pacchetto *_in_* uscita.

### <a name="raw-ip-receive"></a>Ricezione IP non elaborato

Se è abilitata l'elaborazione di pacchetti IP non elaborati, l'applicazione può ricevere pacchetti IP non elaborati tramite il servizio ***nx_ip_raw_packet_receive** _. Tutti i pacchetti in ingresso vengono elaborati in base al protocollo specificato nell'intestazione IP. Se il protocollo specifica UDP, TCP, IGMP o ICMP, NetX eelaborare il pacchetto usando il gestore appropriato per il tipo di protocollo di pacchetto. Se il protocollo non è uno di questi protocolli e la ricezione IP non elaborata è abilitata, il pacchetto in ingresso verrà inserito nella coda di pacchetti non elaborati in attesa che l'applicazione lo riceva tramite il servizio _ *_nx_ip_raw_packet_receive_**. Inoltre, i thread dell'applicazione possono essere sospesi con un timeout facoltativo durante l'attesa di un pacchetto IP non elaborato.

### <a name="default-packet-pool"></a>Pool di pacchetti predefinito

A ogni istanza IP viene assegnato un pool di pacchetti predefinito durante la creazione. Questo pool di pacchetti viene usato per allocare pacchetti per ARP, RARP, ICMP, IGMP, vari pacchetti di controllo TCP (ad esempio SYN, ACK). Se il pool di pacchetti predefinito è vuoto quando NetX deve allocare un pacchetto, potrebbe essere necessario interrompere l'operazione specifica e, se possibile, restituirà un messaggio di errore.

### <a name="ip-helper-thread"></a>IP Helper Thread

Ogni istanza IP ha un thread helper. Questo thread è responsabile della gestione di tutte le elaborazioni di pacchetti posticipate e di tutte le elaborazioni periodiche. Il thread helper IP viene creato in ***nx_ip_create.*** Questo è il punto in cui al thread vengono dati lo stack e la priorità. Si noti che la prima elaborazione nel thread helper IP è il completamento dell'inizializzazione del driver di rete associata al servizio di creazione ip. Al termine dell'inizializzazione del driver di rete, il thread helper avvia un ciclo infinito per elaborare i pacchetti e le richieste periodiche.

> [!IMPORTANT]
> *Se viene visualizzato un comportamento inspiegabile all'interno del thread helper IP, l'aumento delle dimensioni dello stack durante il servizio di creazione dell'indirizzo IP è il primo passaggio di debug. Se lo stack è troppo piccolo, il thread helper IP potrebbe sovrascrivere la memoria, causando problemi insoliti.*

### <a name="thread-suspension"></a>Sospensione dei thread

I thread dell'applicazione possono essere sospesi durante il tentativo di ricevere pacchetti IP non elaborati. Dopo la ricezione di un pacchetto non elaborato, il nuovo pacchetto viene assegnato al primo thread sospeso e tale thread viene ripreso. I servizi NetX per la ricezione di pacchetti hanno tutti un timeout di sospensione facoltativo. Quando un pacchetto viene ricevuto o il timeout scade, il thread dell'applicazione viene ripreso con lo stato di completamento appropriato.

### <a name="ip-statistics-and-errors"></a>Statistiche ED errori IP

Se abilitato, NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti IP inviati
- Totale byte IP inviati
- Totale pacchetti IP ricevuti
- Totale byte IP ricevuti
- Totale pacchetti IP non validi
- Totale pacchetti di ricezione IP eliminati
- Totale errori di checksum di ricezione IP
- Totale pacchetti di invio IP eliminati
- Totale frammenti IP inviati
- Totale frammenti IP ricevuti

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con il ***nx_ip_info_get*** servizio.

### <a name="ip-control-block-nx_ip"></a>Blocco di controllo IP NX_IP

Le caratteristiche di ogni istanza IP si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio gli indirizzi IP e le network mask di ogni dispositivo di rete, e una tabella di mapping degli indirizzi IP adiacenti e hardware fisico. Questa struttura è definita nei blocchi di controllo dell'istanza IP ***nx_api.h*** che possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

### <a name="static-ip-routing"></a>Routing IP statico

La funzionalità di routing statico consente a un'applicazione di specificare una rete IP e un indirizzo hop successivo per indirizzi IP di destinazione fuori rete specifici. Se il routing statico è abilitato, NetX cerca nella tabella di routing statica una voce corrispondente all'indirizzo di destinazione del pacchetto da inviare. Se non viene trovata alcuna corrispondenza, NetX cerca nell'elenco delle interfacce fisiche e sceglie un indirizzo IP di origine e un indirizzo hop successivo in base all'indirizzo IP di destinazione e al network mask. Se la destinazione non corrisponde ad alcuno degli indirizzi IP dei driver di rete collegati all'istanza IP, NetX sceglie un'interfaccia direttamente connessa al gateway predefinito e usa l'indirizzo IP dell'interfaccia come indirizzo di origine e il gateway predefinito come hop successivo.

Le voci possono essere aggiunte e rimosse dalla tabella di routing statica ***usando*** rispettivamente i nx_ip_static_route_add e ***nx_ip_static_route_delete** _services. Per usare il routing statico, l'applicazione host deve abilitare questa funzionalità definendo _ *_NX_ENABLE_IP_STATIC_ROUTING_*.*

> [!IMPORTANT]
> *Quando si aggiunge una voce alla tabella di routing statico, NetX verifica la presenza di una voce corrispondente per l'indirizzo di destinazione specificato già presente nella tabella. Se ne esiste una, dà la preferenza alla voce con la rete più piccola (prefisso più lungo) nel network mask.*

### <a name="ip-fragmentation"></a>Frammentazione IP

Il dispositivo di rete può avere limiti alle dimensioni dei pacchetti in uscita. Questo limite è denominato MTU (Maximum Transmission Unit). L'MTU IP è la dimensione massima del frame IP che un driver del livello di collegamento è in grado di trasmettere senza frammentare il pacchetto IP. Durante una fase di inizializzazione del driver di dispositivo, il modulo driver deve configurare le dimensioni MTU IP tramite il servizio ***nx_ip_interface_mtu_set**.*

Sebbene non sia consigliabile, l'applicazione può generare datagrammi più grandi rispetto all'MTU IP sottostante supportato dal dispositivo. Prima di trasmettere tale datagramma IP, il livello IP deve frammentare questi pacchetti. Quando riceve frame IP frammentati, l'estremità ricevente deve archiviare tutti i frame IP frammentati con lo stesso ID frammentazione e riassemblarli nell'ordine indicato. Se la logica di ricezione IP non è in grado di raccogliere tutti i frammenti per ripristinare il frame IP originale nel tempo, vengono rilasciati tutti i frammenti. È il protocollo di livello superiore a rilevare tale perdita di pacchetti e a recuperarlo.

Per supportare la frammentazione IP e l'operazione di ***riassemblaggio,*** la finestra di progettazione del sistema deve abilitare la funzionalità di frammentazione IP in NetX usando il servizio nx_ip_fragment_enable ip. Se questa funzionalità non è abilitata, i pacchetti IP frammentati in ingresso vengono eliminati, nonché i pacchetti che superano la MTU del driver di rete.

> [!IMPORTANT]
> *La logica di frammentazione IP può essere rimossa completamente definendo*  * **NX_DISABLE_FRAGMENTATION** _ _when la libreriaNetX. Questa operazione consente di ridurre le dimensioni del codice di NetX.*

## <a name="address-resolution-protocol-arp-in-ip"></a>Protocollo ARP (Address Resolution Protocol) in IP

Il protocollo ARP (Address Resolution Protocol) è responsabile del mapping dinamico degli indirizzi IP a 32 bit a quelli dei supporti fisici sottostanti (RFC 826). Ethernet è il supporto fisico più tipico e supporta indirizzi a 48 bit. La necessità di ARP è determinata dal driver di rete fornito al ***nx_ip_create*** servizio. Se è necessario il mapping fisico, il driver di rete deve impostare il ***flag*** nx_interface_address_mapping_needed nell'interfaccia strcuture.

### <a name="arp-enable"></a>ARP Enable
Per il corretto funzionamento, ARP deve essere abilitato dall'applicazione con il ***nx_arp_enable*** servizio. Questo servizio configura varie strutture di dati per l'elaborazione ARP, inclusa la creazione di un'area della cache ARP dalla memoria fornita al servizio ARP enable.

### <a name="arp-cache"></a>ARP Cache
La cache ARP può essere visualizzata come una matrice di strutture di dati di mapping ARP interne. Ogni struttura interna è in grado di mantenere la relazione tra un indirizzo IP e un indirizzo hardware fisico. Inoltre, ogni struttura di dati ha puntatori di collegamento in modo che possa far parte di più elenchi collegati.

L'applicazione può cercare un indirizzo IP dalla cache ARP fornendo l'indirizzo MAC hardware usando il servizio ***nx_arp_ip_address_find** _ se il mapping esiste nella tabella ARP. Analogamente, il servizio _ *_nx_arp_hardware_address_find_** restituisce l'indirizzo MAC per un determinato indirizzo IP.


### <a name="arp-dynamic-entries"></a>Voci dinamiche ARP

Per impostazione predefinita, il servizio ARP enable inserisce tutte le voci nella cache ARP nell'elenco delle voci ARP dinamiche disponibili. Una voce ARP dinamica viene allocata da questo elenco da NetX quando viene rilevata una richiesta di invio a un indirizzo IP non mappato. Dopo l'allocazione, la voce ARP viene impostata e una richiesta ARP viene inviata al supporto fisico.

Una voce dinamica può essere creata anche dal servizio ***nx_arp_dynamic_entry_set***.

> [!IMPORTANT]
> *Se tutte le voci ARP dinamiche sono in uso, la voce ARP usata meno di recente viene sostituita con un nuovo mapping.*

### <a name="arp-static-entries"></a>Voci statiche ARP
L'applicazione può anche configurare il mapping ARP statico usando il ***nx_arp_static_entry_create*** servizio. Questo servizio alloca una voce ARP dall'elenco di voci ARP dinamiche e la inserisce nell'elenco statico con le informazioni di mapping fornite dall'applicazione. Le voci ARP statiche non sono soggette a riutilizzo o aging. L'applicazione può eliminare una voce statica usando il servizio ***nx_arp_static_entry_delete***.
Per rimuovere tutte le voci statiche nella tabella ARP, l'applicazione può usare il servizio ***nx_arp_static_entries_delete***.

### <a name="automatic-arp-entry"></a>Voce ARP automatica
NetX registra il mapping IP/MAC del peer dopo le risposte del peer alla richiesta ARP. NetX implementa anche la funzionalità di immissione automatica ARP in cui registra il mapping degli indirizzi IP/MAC peer in base alle richieste ARP non richieste dalla rete. Questa funzionalità consente alla tabella ARP di essere popolata con informazioni peer, riducendo il ritardo necessario per passare attraverso il ciclo di richiesta/risposta ARP. Tuttavia, lo svantaggio dell'abilitazione automatica di ARP è che la tabella ARP tende a riempirsi rapidamente in una rete occupata con molti nodi nel collegamento locale, che alla fine porterebbe alla sostituzione delle voci ARP.

Questa funzionalità è abilitata per impostazione predefinita. Per disabilitarla, la libreria NetX deve essere compilata con il ***simbolo NX_DISABLE_ARP_AUTO_ENTRY*** definito.

### <a name="arp-messages"></a>Messaggi ARP

Come accennato in precedenza, viene inviato un messaggio di richiesta ARP quando l'attività IP rileva che il mapping è necessario per un indirizzo IP. Le richieste ARP vengono inviate periodicamente (ogni ***NX_ARP_UPDATE_RATE** _ secondi) fino a quando non viene ricevuta una risposta ARP corrispondente. Un totale di _ *_NX_ARP_MAXIMUM_RETRIES_** richieste ARP vengono effettuate prima dell'abbandono del tentativo ARP. Quando viene ricevuta una risposta ARP, le informazioni sull'indirizzo fisico associato vengono archiviate nella voce ARP presente nella cache.

Per i sistemi multihome, NetX determina quale interfaccia inviare le richieste e le risposte ARP in base all'indirizzo di destinazione specificato.

> [!IMPORTANT]
> *I pacchetti IP in uscita vengono accodati mentre NetX attende la risposta ARP. Il numero di pacchetti IP in* uscita in coda è *definito* dalla costante  * **NX_ARP_MAX_QUEUE_DEPTH**.*

NetX risponde anche alle richieste ARP provenienti da altri nodi nella rete IP locale. Quando viene effettuata una richiesta ARP esterna che corrisponde all'indirizzo IP corrente dell'interfaccia che riceve la richiesta ARP, NetX compila un messaggio di risposta ARP che contiene l'indirizzo fisico corrente.

I formati delle richieste Ethernet ARP e delle risposte sono illustrati nella figura 6 e sono descritti di seguito:

| Campo di richiesta/risposta       | Scopo    |
|------------------------------|-----------------|
| Indirizzo di destinazione Ethernet | Questo campo a 6 byte contiene l'indirizzo di destinazione per la risposta ARP ed è una trasmissione (tutte) per le richieste ARP. Questo campo viene installato dal driver di rete. |
| Indirizzo di origine Ethernet      | Questo campo a 6 byte contiene l'indirizzo del mittente della richiesta o della risposta ARP ed è configurato dal driver di rete. |
| Tipo di frame                   | Questo campo a 2 byte contiene il tipo di frame Ethernet presente e, per le richieste e le risposte ARP, equivale a 0x0806. Questo è l'ultimo campo che il driver di rete è responsabile della configurazione. |
| Tipo di hardware                | Questo campo a 2 byte contiene il tipo di hardware, che 0x0001 per Ethernet. |
| Tipo di protocollo                | Questo campo a 2 byte contiene il tipo di protocollo, che 0x0800 per gli indirizzi IP. |
| Dimensioni hardware                | Questo campo a 1 byte contiene le dimensioni dell'indirizzo hardware, ovvero 6 per gli indirizzi Ethernet. |


![Formato pacchetto ARP](./media/user-guide/arp-packet-format.png)

**FIGURA 6. Formato pacchetto ARP**

| Campo richiesta/risposta | Scopo  |
|---|---|
| Dimensioni del protocollo | Questo campo a 1 byte contiene le dimensioni dell'indirizzo IP, ovvero 4 per gli indirizzi IP.  |
| Codice operazione | Questo campo a 2 byte contiene l'operazione per questo pacchetto ARP. Una richiesta ARP viene specificata con il valore 0x0001, mentre una risposta ARP è rappresentata da un valore di 0x0002.  |
| Indirizzo Ethernet mittente | Questo campo a 6 byte contiene l'indirizzo Ethernet del mittente. |
| Indirizzo IP mittente | Questo campo a 4 byte contiene l'indirizzo IP del mittente. |
| Indirizzo Ethernet di destinazione | Questo campo a 6 byte contiene l'indirizzo Ethernet della destinazione. |
| Indirizzo IP di destinazione | Questo campo a 4 byte contiene l'indirizzo IP della destinazione. |

> [!IMPORTANT]
> *Le richieste e le risposte ARP sono pacchetti a livello Ethernet. Tutti gli altri pacchetti TCP/IP sono incapsulati da un'intestazione di pacchetto IP.*

> [!IMPORTANT]
> *È previsto che tutti i messaggi ARP nell'implementazione TCP/IP siano in big endian formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso.*

### <a name="arp-aging"></a>ARP Aging

NetX supporta l'invalidamento automatico delle voci ARP dinamiche. ***NX_ARP_EXPIRATION_RATE** _specifies numero di secondi in cui un indirizzo IP stabilito per il mapping fisico rimane valido. Dopo la scadenza, la voce ARP viene rimossa dalla cache ARP. Il tentativo successivo di inviare all'indirizzo IP corrispondente comporta una nuova richiesta ARP. *_L'impostazione di_* _ NX_ARP_EXPIRATION_RATE * su zero disabilita la durata ARP, che è la configurazione predefinita.

### <a name="arp-defend"></a>Difesa ARP

Quando viene ricevuta una richiesta ARP o un pacchetto di risposta ARP e il mittente ha lo stesso indirizzo IP, che è in conflitto con l'indirizzo IP di questo nodo, NetX invia una richiesta ARP per tale indirizzo come difesa. Se il pacchetto ARP in conflitto viene ricevuto più di una volta in 10 secondi, NetX non invia più pacchetti di difesa. L'intervallo predefinito di 10 secondi può essere ridefinito da ***NX_ARP_DEFEND_INTERVAL** _. Questo comportamento segue i criteri specificati nella versione 2.4(c) di RFC5227. Poiché Windows XP ignora l'annuncio ARP come risposta per il probe ARP, l'utente può definire _*_NX_ARP_DEFEND_BY_REPLY_**per inviare la risposta ARP come ulteriore supporto.

### <a name="arp-statistics-and-errors"></a>Statistiche ed errori ARP

Se abilitato, il software NetX ARP tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione ARP di ogni IP:

- Totale richieste ARP inviate
- Totale richieste ARP ricevute
- Totale risposte ARP inviate
- Totale risposte ARP ricevute
- Totale voci dinamiche ARP
- Totale voci statiche ARP
- Total ARP Aged Entries
- Totale messaggi ARP non validi

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con ***il nx_arp_info_get*** servizio.

## <a name="reverse-address-resolution-protocol-rarp-in-ip"></a>RaRP (Reverse Address Resolution Protocol) in IP

Il protocollo RARP (Reverse Address Resolution Protocol) è il protocollo per richiedere l'assegnazione di rete degli indirizzi IP a 32 bit dell'host (RFC 903). Questa operazione viene eseguita tramite una richiesta RARP e continua periodicamente fino a quando un membro della rete non assegna un indirizzo IP all'interfaccia di rete host in una risposta RARP. L'applicazione crea un'istanza IP dal servizio ***nx_ip_create*** con un indirizzo IP pari a zero. Se RARP è abilitato dall'applicazione, può usare il protocollo RARP per richiedere un indirizzo IP dal server di rete accessibile tramite l'interfaccia con un indirizzo IP pari a zero.

### <a name="rarp-enable"></a>RARP Enable

Per usare RARP, l'applicazione deve creare l'istanza IP con un indirizzo IP pari a zero, quindi abilitare RARP usando il servizio ***nx_rarp_enable***. Per i sistemi multihome, almeno un dispositivo di rete associato all'istanza IP deve avere un indirizzo IP pari a zero. L'elaborazione RARP invia periodicamente messaggi di richiesta RARP per il sistema NetX che richiedono un indirizzo IP fino a quando non viene ricevuta una risposta RARP valida con l'indirizzo IP designato di rete. A questo punto, l'elaborazione RARP è stata completata.

Dopo che è stato abilitato, RARP viene disabilitato automaticamente dopo la risoluzione di tutti gli indirizzi di interfaccia. L'applicazione può forzare il rarp a terminare usando il servizio ***nx_rarp_disable***.

###  <a name="rarp-request"></a>Richiesta RARP

Il formato di un pacchetto di richiesta RARP è quasi identico al pacchetto ARP illustrato nella figura 6 nell'argomento [Messaggi ARP](#arp-messages). L'unica differenza è che il campo del tipo di frame 0x8035 il campo *Codice* operazione è 3, che designa una richiesta RARP. Come accennato in precedenza, le richieste RARP verranno inviate periodicamente (ogni NX_RARP_UPDATE_RATE secondi) fino ***a*** quando non viene ricevuta una risposta RARP con l'indirizzo IP assegnato alla rete.

> [!IMPORTANT]
> *È previsto che tutti i messaggi RARP nell'implementazione TCP/IP siano in big endian formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso.*

### <a name="rarp-reply"></a>RISPOSTA RARP

I messaggi di risposta RARP vengono ricevuti dalla rete e contengono l'indirizzo IP assegnato alla rete per questo host. Il formato di un pacchetto di risposta RARP è quasi identico al pacchetto ARP illustrato nella figura 6. L'unica differenza è che il campo del tipo di frame 0x8035 il campo *Codice* operazione è 4, che definisce una risposta RARP. Dopo la ricezione, l'indirizzo IP viene specificato nell'istanza IP, la richiesta RARP periodica è disabilitata e l'istanza IP è ora pronta per il normale funzionamento della rete.

Per gli host multihome, l'indirizzo IP viene applicato all'interfaccia di rete richiedente. Se sono presenti altre interfacce di rete che richiedono ancora un'assegnazione di indirizzo IP, il servizio RARP periodico continua fino a quando non vengono risolte tutte le richieste di indirizzi IP di interfaccia.

> [!IMPORTANT]
> *L'applicazione non deve usare l'istanza IP fino al completamento dell'elaborazione RARP. Il **nx_ip_status_check** può essere usato dalle applicazioni per attendere il completamento di RARP. Per i sistemi multihome, l'applicazione non deve usare l'interfaccia richiedente fino al completamento dell'elaborazione RARP su tale interfaccia. Lo stato dell'indirizzo IP nel dispositivo secondario può essere controllato con **il nx_ip_interface_status_check** servizio.*

### <a name="rarp-statistics-and-errors"></a>Statistiche ed errori RARP

Se abilitato, il software RARP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione RARP di ogni IP:

- Totale richieste RARP inviate
- Totale risposte RARP ricevute
- Totale messaggi RARP non validi

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con ***il nx_rarp_info_get*** servizio.

## <a name="internet-control-message-protocol-icmp"></a>Internet Control Message Protocol (ICMP)

Internet Control Message Protocol ip (ICMP) è limitato al passaggio di informazioni di errore e controllo tra i membri della rete IP.

Come la maggior parte degli altri messaggi a livello di applicazione (ad esempio TCP/IP), i messaggi ICMP vengono incapsulati da un'intestazione IP con la designazione del protocollo ICMP.

### <a name="icmp-statistics-and-errors"></a>Statistiche ed errori ICMP

Se abilitata, NetX tiene traccia di diverse statistiche ed errori ICMP che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione ICMP di ogni IP:

- Totale ping ICMP inviati
- Timeout ping ICMP totali
- Totale thread ping ICMP sospesi
- Totale risposte ping ICMP ricevute
- Totale errori di checksum ICMP
- Totale messaggi ICMP non gestiti

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con ***il nx_icmp_info_get*** servizio.

### <a name="icmp-enable"></a>Abilitazione di ICMP
Prima che i messaggi ICMP possano essere elaborati da NetX, l'applicazione deve chiamare il ***nx_icmp_enable*** per abilitare l'elaborazione ICMP. Al termine, l'applicazione può inviare richieste ping e campi pacchetti ping in ingresso.

### <a name="icmp-echo-request"></a>Richiesta echo ICMP
Una richiesta echo è un tipo di messaggio ICMP che viene in genere usato per verificare l'esistenza di un nodo specifico nella rete, come identificato dal relativo indirizzo IP host. Il comando ping comune viene implementato usando messaggi di richiesta echo/risposta echo ICMP. Se l'host specifico è presente, il relativo stack di rete elabora la richiesta ping e le risposte con una risposta ping. La figura 7 illustra in dettaglio il formato del messaggio ping ICMP.

![Messaggio ping ICMP](./media/user-guide/icmp-ping-message.png)

**FIGURA 7. Messaggio ping ICMP**

> [!IMPORTANT]
> *Tutti i messaggi ICMP nell'implementazione TCP/IP devono essere in big endian predefinito. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso.*

La tabella seguente descrive il formato dell'intestazione ICMP:

| Campo intestazione    | Scopo |
|-----------------|---------------------------------------------------|
| Tipo            | Questo campo specifica il messaggio ICMP (bit 31- 24). I più comuni sono: 0 Echo Reply 8 Echo Request |
| Codice            | Questo campo è specifico del contesto nel campo del tipo (bit 23-16). Per una richiesta echo o una risposta, il codice è impostato su zero. |
| Checksum        | Questo campo contiene il checksum a 16 bit della somma complementare del messaggio ICMP, inclusa l'intera intestazione ICMP che inizia con il campo Tipo. Prima di generare il checksum, il campo checksum viene cancellato.                 |
| Identificazione  | Questo campo contiene un valore ID che identifica l'host. un host deve usare l'ID estratto da una richiesta ECHO in ECHO REPLY (bit 31-16). |
| Numero di sequenza | Questo campo contiene un valore ID. un host deve usare l'ID estratto da una richiesta ECHO in ECHO REPLY (bit 31-16). A differenza del campo dell'identificatore, questo valore cambierà in una successiva richiesta Echo dallo stesso host (bit 15-0). |


### <a name="icmp-echo-response"></a>Risposta echo ICMP
Una risposta ping è un altro tipo di messaggio ICMP generato internamente dal componente ICMP in risposta a una richiesta ping esterna. Oltre all'acknowledgement, la risposta ping contiene anche una copia dei dati utente forniti nella richiesta ping.

## <a name="internet-group-management-protocol-igmp"></a>IGMP (Internet Group Management Protocol)

Il Internet Group Management Protocol (IGMP) fornisce un dispositivo per comunicare con i router adiacenti che intende ricevere o aggiungere a un gruppo multicast IP (RFC 1112 e RFC 2236). Un gruppo multicast è fondamentalmente una raccolta dinamica di membri di rete ed è rappresentato da un indirizzo IP di classe D. I membri del gruppo multicast possono uscire in qualsiasi momento e i nuovi membri possono essere uniti in qualsiasi momento. Il coordinamento necessario per l'aggiunta e l'uscita dal gruppo è responsabilità del gruppo IGMP.

### <a name="igmp-enable"></a>Abilitazione IGMP

Prima di poter eseguire qualsiasi attività multicast in NetX, l'applicazione deve chiamare il ***nx_igmp_enable*** servizio. Questo servizio esegue l'inizializzazione IGMP di base in preparazione per le richieste multicast.

### <a name="multicast-ip-addressing"></a>Indirizzamento IP multicast

Come accennato in precedenza, gli indirizzi multicast sono in realtà indirizzi IP di classe D, come illustrato nella figura 4 a pagina 58. I 28 bit inferiori dell'indirizzo di classe D corrispondono all'ID del gruppo multicast. È presente una serie di indirizzi multicast predefiniti. Tuttavia, *l'indirizzo di tutti* gli host (244.0.0.1) è particolarmente importante per l'elaborazione IGMP. *L'indirizzo di tutti gli* host viene usato dai router per eseguire query su tutti i membri multicast per segnalare a quali gruppi multicast appartengono.

### <a name="physical-address-mapping-in-ip"></a>Mapping degli indirizzi fisici in IP

Gli indirizzi multicast di classe D vengono mappati direttamente agli indirizzi Ethernet fisici compresi tra 01.00.5e.00.00.00 e 01.00.5e.7f.ff.ff. I 23 bit inferiori dell'indirizzo IP multicast vengono mappati direttamente ai 23 bit inferiori dell'indirizzo Ethernet.

### <a name="multicast-group-join"></a>Join a gruppi multicast

Le applicazioni che devono essere unite a un determinato gruppo multicast possono eseguire questa operazione chiamando il ***nx_igmp_multicast_join*** servizio. Questo servizio tiene traccia del numero di richieste per l'aggiunta a questo gruppo multicast. Se questa è la prima richiesta dell'applicazione a partecipare al gruppo multicast, nella rete primaria viene inviato un report IGMP che indica l'intenzione dell'host di partecipare al gruppo. Viene quindi chiamato il driver di rete per configurare l'ascolto dei pacchetti con l'indirizzo Ethernet per questo gruppo multicast.

In un sistema multihome, se il gruppo multicast è accessibile tramite un'interfaccia specifica, l'applicazione deve usare il ***nx_igmp_multicast_interface_join*** del servizio anziché ***nx_igmp_multicast_join**,* che è limitato ai gruppi multicast nella rete primaria.

### <a name="multicast-group-leave"></a>Multicast Group Leave

Le applicazioni che devono lasciare un gruppo multicast aggiunto in precedenza possono eseguire questa operazione chiamando ***il nx_igmp_multicast_leave*** servizio. Questo servizio riduce il conteggio interno associato al numero di volte in cui il gruppo è stato aggiunto. Se non sono presenti richieste di join in sospeso per un gruppo, viene chiamato il driver di rete per disabilitare l'ascolto dei pacchetti con l'indirizzo Ethernet di questo gruppo multicast

### <a name="multicast-loopback"></a>Multicast Loopback

Un'applicazione potrebbe voler ricevere traffico multicast proveniente da una delle origini nello stesso nodo. A tale scopo, è necessario che il componente multicast IP abbia abilitato il loopback usando il ***nx_igmp_loopback_enable***.

### <a name="igmp-report-message"></a>Messaggio del report IGMP

Quando l'applicazione viene aggiunta a un gruppo multicast, viene inviato un messaggio di report IGMP tramite la rete per indicare l'intenzione dell'host di partecipare a un gruppo multicast specifico. Il formato del messaggio del report IGMP è illustrato nella figura 8. L'indirizzo del gruppo multicast viene utilizzato sia per il messaggio di gruppo nel messaggio di report IGMP che per l'indirizzo IP di destinazione.

![Messaggio del report IGMP](./media/user-guide/igmp-report-message.png)

**FIGURA 8. Messaggio del report IGMP**

Nella figura precedente (Figura 8) l'intestazione IGMP contiene un campo versione/tipo, il tempo di risposta massimo, un campo di checksum e un campo indirizzo del gruppo multicast. Per i messaggi IGMPv1, il campo Tempo di risposta massimo è sempre impostato su zero, perché non fa parte del protocollo IGMPv1. Il campo Tempo di risposta massimo viene impostato quando l'host riceve un messaggio IGMP di tipo query e viene cancellato quando un host riceve il messaggio di tipo Report di un altro host, come definito dal protocollo IGMPv2.

Di seguito viene descritto il formato di intestazione IGMP:

| **Campo intestazione**          | **Scopo** |
|-----------------------|--------------------------------------------------------------------|
| Versione               | Questo campo specifica la versione IGMP (bit 31- 28).                                                                               |
| Tipo                  | Questo campo specifica il tipo di messaggio IGMP (bit 27 -24).                                                                       |
| Tempo di risposta massimo | Non usato in IGMPv1. In IGMPv2 questo campo funge da tempo di risposta massimo.                                                      |
| Checksum              | Questo campo contiene il checksum a 16 bit della somma complementare del messaggio IGMP a partire dalla versione IGMP (bit 0-15) |
| Indirizzo gruppo         | Indirizzo IP del gruppo D di classe D a 32 bit |


I messaggi di report IGMP vengono inviati anche in risposta ai messaggi di query IGMP inviati da un router multicast. I router multicast inviano periodicamente messaggi di query per vedere quali host richiedono ancora l'appartenenza al gruppo. I messaggi di query hanno lo stesso formato del messaggio del report IGMP illustrato nella figura 8. Le uniche differenze sono il tipo IGMP è uguale a 1 e il campo dell'indirizzo del gruppo è impostato su 0. I messaggi di query IGMP vengono inviati *all'indirizzo* IP di tutti gli host dal router multicast. Un host che vuole comunque mantenere l'appartenenza al gruppo risponde inviando un altro messaggio di report IGMP.

> [!IMPORTANT]
> *È previsto che tutti i messaggi nell'implementazione TCP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso.*

### <a name="igmp-statistics-and-errors"></a>Statistiche ed errori IGMP

Se abilitato, il software NetX IGMP tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione IGMP di ogni IP:

- Totale report IGMP inviati
- Totale query IGMP ricevute
- Totale errori di checksum IGMP
- Totale gruppi correnti IGMP aggiunti

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con ***il nx_igmp_info_get*** servizio.

## <a name="user-datagram-protocol-udp"></a>User Datagram Protocol (UDP)

Il protocollo UDP (User Datagram Protocol) fornisce la forma più semplice di trasferimento dei dati tra membri di rete (RFC 768). I pacchetti di dati UDP vengono inviati da un membro di rete a un altro nel modo più adatto; ad esempio non esiste un meccanismo predefinito per l'acknowledgement da parte del destinatario del pacchetto. Inoltre, l'invio di un pacchetto UDP non richiede alcuna connessione da stabilire in anticipo. Per questo, la trasmissione di pacchetti UDP è molto efficiente.

### <a name="udp-header"></a>Intestazione UDP
UDP inserisce una semplice intestazione di pacchetto davanti ai dati dell'applicazione durante la trasmissione e rimuove un'intestazione UDP simile dal pacchetto alla ricezione prima di recapitare un pacchetto UDP ricevuto all'applicazione. UDP usa il protocollo IP per l'invio e la ricezione di pacchetti, il che significa che è presente un'intestazione IP davanti all'intestazione UDP quando il pacchetto è in rete. La figura 9 mostra il formato dell'intestazione UDP.

![Intestazione UDP](./media/user-guide/udp-header.png)

**FIGURA 9. Intestazione UDP**

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione UDP/IP siano big endian formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso.*

Di seguito viene descritto il formato dell'intestazione UDP:

| Campo intestazione                   | Scopo |
|--------------------------------|---------------------------------------------|
| Numero di porta di origine a 16 bit      | Questo campo contiene la porta da cui viene inviato il pacchetto UDP. Le porte UDP valide sono da 1 a 0xFFFF. |
| Numero di porta di destinazione a 16 bit | Questo campo contiene la porta UDP a cui viene inviato il pacchetto. Le porte UDP valide sono da 1 a 0xFFFF.   |
| Lunghezza UDP a 16 bit   | Questo campo contiene il numero di byte nel pacchetto UDP, inclusa la dimensione dell'intestazione UDP.                                  |
| Checksum UDP a 16 bit | Questo campo contiene il checksum a 16 bit per il pacchetto, incluse l'intestazione UDP, l'area dei dati del pacchetto e la pseudo-intestazione IP. |

### <a name="udp-enable"></a>UDP Enable

Prima che sia possibile la trasmissione di pacchetti UDP, l'applicazione deve prima abilitare UDP chiamando ***il nx_udp_enable*** servizio. Dopo l'a attivazione, l'applicazione può inviare e ricevere pacchetti UDP.

### <a name="udp-socket-create"></a>Creazione di socket UDP

I socket UDP vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Il tipo iniziale di servizio, la tempo di attesa e la profondità della coda di ricezione sono definiti dal ***nx_udp_socket_create*** servizio. Non sono previsti limiti al numero di socket UDP in un'applicazione.

### <a name="udp-checksum"></a>UDP Checksum

UDP specifica un checksum a 16 bit complementare che copre la pseudo-intestazione IP (costituita dall'indirizzo IP di origine, dall'indirizzo IP di destinazione e dalla parola IP del protocollo/lunghezza), dall'intestazione UDP e dai dati del pacchetto UDP. Se il checksum UDP calcolato è 0, viene archiviato come tutti i valori (0xFFFF). Se nel socket di invio la logica di checksum UDP è disabilitata, viene inserito uno zero nel campo checksum UDP per indicare che il checksum non è stato calcolato. Se il checksum UDP non corrisponde al checksum calcolato dal ricevitore, il pacchetto UDP viene semplicemente eliminato.

Nella rete IP il checksum UDP è facoltativo. NetX consente a un'applicazione di abilitare o disabilitare il calcolo del checksum UDP per ogni socket. Per impostazione predefinita, la logica di checksum del socket UDP è abilitata. L'applicazione può disabilitare la logica di checksum per un particolare socket UDP chiamando ***nx_udp_socket_checksum_disable*** servizio.

Alcuni controller Ethernet sono in grado di generare il checksum UDP in tempo reale. Se il sistema è in grado di usare la funzionalità di calcolo dei checksum hardware, la libreria NetX può essere compilata senza la logica di checksum. Per ***disabilitare*** il checksum software UDP, la libreria NetX deve essere compilata con i simboli seguenti definiti: NX_DISABLE_UDP_TX_CHECKSUM ***e NX_DISABLE_UDP_RX_CHECKSUM* _ (descritti nel capitolo *[2).](chapter2.md) Le opzioni**** di configurazione rimuovono completamente la logica di checksum UDP da NetX, mentre la chiamata al servizio _ nx_udp_socket_checksum_disable consente all'applicazione di disabilitare l'elaborazione del checksum UDP IP per ogni socket.

### <a name="udp-ports-and-binding"></a>Porte UDP e binding

Una porta UDP è un end point logico nel protocollo UDP. Nel componente UDP di NetX sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. Per inviare o ricevere dati UDP, l'applicazione deve prima creare un socket UDP, quindi associarlo a una porta desiderata. Dopo l'associazione di un socket UDP a una porta, l'applicazione può inviare e ricevere dati su tale socket.

### <a name="udp-fast-pathtrade"></a>Percorso rapido UDP&trade;

Il percorso rapido UDP &trade; è il nome di un percorso con sovraccarico di pacchetti basso tramite l'implementazione UDP di NetX. L'invio di un pacchetto UDP richiede solo alcune chiamate di funzione: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ e l'eventuale chiamata al driver di rete. _*_nx_udp_socket_send_*_ è disponibile in NetX per le applicazioni NetX esistenti ed è applicabile solo per i pacchetti IP. Il metodo preferito, tuttavia, è l'uso di _ *_nx_udp_socket_send_** servizio illustrato di seguito. Nella ricezione di pacchetti UDP, il pacchetto UDP viene inserito nella coda di ricezione socket UDP appropriata o recapitato a un thread dell'applicazione sospeso in una singola chiamata di funzione dall'elaborazione dell'interrupt di ricezione del driver di rete. Questa logica altamente ottimizzata per l'invio e la ricezione di pacchetti UDP è l'essenziale della tecnologia Fast Path UDP.

### <a name="udp-packet-send"></a>Invio di pacchetti UDP

L'invio di dati UDP su reti IP viene facilmente ottenuto chiamando la funzione ***nx_udp_socket_send** _. Il chiamante deve impostare la versione IP nel campo _IP address*. NetX determinerà l'indirizzo di origine migliore per i pacchetti UDP trasmessi in base all'indirizzo IP di destinazione. Questo servizio inserisce un'intestazione UDP davanti ai dati del pacchetto e la invia alla rete usando una routine di invio IP interna. Non è presente alcuna sospensione del thread durante l'invio di pacchetti UDP perché tutte le trasmissioni di pacchetti UDP vengono elaborate immediatamente.

Per le destinazioni multicast o broadcast, l'applicazione deve specificare l'indirizzo IP di origine da usare se il dispositivo NetX ha più indirizzi IP tra cui scegliere. Questa operazione può essere eseguita con i servizi ***nx_udp_socket_interface_send.***

> [!IMPORTANT]
> *Se **nx_udp_socket_send** viene usato per la trasmissione di pacchetti multicast o broadcast, l'indirizzo IP della prima interfaccia viene usato come indirizzo di origine.*

> [!IMPORTANT]
> *Se per questo socket è abilitata la logica di checksum UDP, l'operazione di checksum viene eseguita nel contesto del thread chiamante, senza bloccare l'accesso alle strutture di dati UDP o IP.*

> [!NOTE]
> *I dati del payload UDP che risiedono nella **struttura NX_PACKET** devono risiedere su un confine lungo. L'applicazione deve lasciare spazio sufficiente tra il puntatore anteposto e il puntatore di avvio dei dati per NetX per inserire le intestazioni udp, IP e fisiche dei supporti.*

### <a name="udp-packet-receive"></a>Ricezione pacchetti UDP

I thread dell'applicazione possono ricevere pacchetti UDP da un particolare socket ***chiamando nx_udp_socket_receive***. La funzione di ricezione socket recapita il pacchetto meno recente nella coda di ricezione del socket. Se non sono presenti pacchetti nella coda di ricezione, il thread chiamante può sospendere (con un timeout facoltativo) fino all'arrivo di un pacchetto.

L'elaborazione dei pacchetti di ricezione UDP (in genere chiamata dal gestore di interrupt di ricezione del driver di rete) è responsabile dell'inserimento del pacchetto nella coda di ricezione del socket UDP o del recapito al primo thread sospeso in attesa di un pacchetto. Se il pacchetto viene accodato, l'elaborazione di ricezione controlla anche la profondità massima della coda di ricezione associata al socket. Se il pacchetto appena accodato supera la profondità della coda, il pacchetto meno recente nella coda viene eliminato.

### <a name="udp-receive-notify"></a>Notifica di ricezione UDP

Se il thread dell'applicazione deve elaborare i dati ricevuti da più socket, ***nx_udp_socket_receive_notify*** usare la funzione . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.

Il contenuto della funzione di callback è specifico dell'applicazione. Tuttavia, probabilmente conterrà la logica per informare il thread di elaborazione che un pacchetto è ora disponibile nel socket corrispondente.

### <a name="peer-address-and-port"></a>Indirizzo e porta peer

Alla ricezione di un pacchetto UDP, l'applicazione può trovare l'indirizzo IP e il numero di porta del mittente usando il servizio ***nx_udp_packet_info_extract***. In caso di esito positivo, questo servizio fornisce informazioni sull'indirizzo IP del mittente, sul numero di porta del mittente e sull'interfaccia locale tramite cui è stato ricevuto il pacchetto.

### <a name="thread-suspension"></a>Sospensione dei thread

Come accennato in precedenza, i thread dell'applicazione possono essere sospesi durante il tentativo di ricevere un pacchetto UDP su una determinata porta UDP. Dopo che un pacchetto è stato ricevuto su tale porta, viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione UDP, una funzionalità disponibile per la maggior parte dei servizi NetX.

### <a name="udp-socket-statistics-and-errors"></a>Statistiche ed errori dei socket UDP

Se abilitato, il software socket UDP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per ogni istanza IP/UDP:

- Totale pacchetti UDP inviati
- Totale byte UDP inviati
- Totale pacchetti UDP ricevuti
- Totale byte UDP ricevuti
- Totale pacchetti UDP non validi
- Totale pacchetti di ricezione UDP eliminati
- Totale errori checksum ricezione UDP
- Pacchetti socket UDP inviati
- Byte socket UDP inviati
- Pacchetti socket UDP ricevuti
- Byte socket UDP ricevuti
- Pacchetti socket UDP in coda
- Pacchetti di ricezione socket UDP eliminati
- Errori di checksum del socket UDP

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con il servizio ***nx_udp_info_get*** per le statistiche UDP su tutti i socket UDP e il servizio ***nx_udp_socket_info_get*** per le statistiche UDP sul socket UDP specificato.

### <a name="udp-socket-control-block-nx_udp_socket"></a>Blocco di controllo socket UDP NX_UDP_SOCKET

Le caratteristiche di ogni socket UDP si trovano nel blocco di **controllo NX_UDP_SOCKET** associato. Contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di rete per i percorsi di invio e ricezione, la porta associata e la coda di pacchetti di ricezione. Questa struttura è definita nel file **_nx_api.h._**

## <a name="transmission-control-protocol-tcp"></a>TCP (Transmission Control Protocol)

Il Transmission Control Protocol (TCP) fornisce un trasferimento affidabile dei dati di flusso tra due membri di rete (RFC 793). Tutti i dati inviati da un membro di rete vengono verificati e riconosciuti dal membro ricevente. Inoltre, i due membri devono aver stabilito una connessione prima di qualsiasi trasferimento di dati. Tutto questo comporta un trasferimento affidabile dei dati; tuttavia, richiede un sovraccarico sostanzialmente maggiore rispetto al trasferimento dei dati UDP descritto in precedenza.

### <a name="tcp-header"></a>Intestazione TCP

Durante la trasmissione, l'intestazione TCP viene posizionata davanti ai dati dell'utente. Durante la ricezione, l'intestazione TCP viene rimossa dal pacchetto in ingresso, lasciando solo i dati utente disponibili per l'applicazione. TCP usa il protocollo IP per inviare e ricevere pacchetti, il che significa che è presente un'intestazione IP davanti all'intestazione TCP quando il pacchetto si trova in rete. La figura 10 mostra il formato dell'intestazione TCP.

![Intestazione TCP](./media/user-guide/tcp-header.png)

**FIGURA 10. Intestazione TCP**

Di seguito viene descritto il formato dell'intestazione TCP:

| Campo intestazione | Scopo |
|---|---|
| Numero di porta di origine a 16 bit | Questo campo contiene la porta su cui viene inviato il pacchetto TCP. Le porte TCP valide sono da 1 a 0xFFFF. |
| Numero di porta di destinazione a 16 bit | Questo campo contiene la porta TCP a cui viene inviato il pacchetto. Le porte TCP valide sono da 1 a 0xFFFF. |
| Numero di sequenza a 32 bit | Questo campo contiene il numero di sequenza per i dati inviati da questa fine della connessione. La sequenza originale viene stabilita durante la sequenza di connessione iniziale tra due nodi TCP. Ogni trasferimento di dati da quel punto comporta un incremento del numero di sequenza in base alla quantità di byte inviati. |
| Numero di acknowledgement a 32 bit | Questo campo contiene il numero di sequenza corrispondente all'ultimo byte ricevuto da questo lato della connessione. Viene usato per determinare se i dati inviati in precedenza sono stati ricevuti correttamente dall'altra estremità della connessione. |
| Lunghezza intestazione a 4 bit           | Questo campo contiene il numero di parole a 32 bit nell'intestazione TCP. Se nell'intestazione TCP non sono presenti opzioni, questo campo è 5. |
| Bit di codice a 6 bit               | Questo campo contiene i sei diversi bit di codice usati per indicare varie informazioni di controllo associate alla connessione. I bit di controllo sono definiti come segue: |



| Nome | bit | Significato                                                     |
|------|-----|-------------------------------------------------------------|
| URG  | 21  | Dati urgenti presenti                                         |
| ACK  | 20  | Il numero di acknowledgement è valido                             |
| PSH  | 19  | Gestire immediatamente questi dati                                |
| Rst  | 18  | Reimpostare la connessione                                        |
| Syn  | 17  | Sincronizzare i numeri di sequenza (usati per stabilire la connessione) |
| FIN  | 16  | Il mittente ha completato la trasmissione (usata per chiudere la connessione) |

**Finestra a 16 bit**

Questo campo viene usato per il controllo di flusso. Contiene la quantità di byte che il socket può attualmente ricevere. Questo viene usato essenzialmente per il controllo di flusso. Il mittente è responsabile di assicurarsi che i dati da inviare si adattino alla finestra annunciata del ricevitore.

| **Campo intestazione**          | **Scopo** |
| ------------------------- | --- |
| **Checksum TCP a 16 bit**   | Questo campo contiene il checksum a 16 bit per il pacchetto, tra cui l'intestazione TCP, l'area dati del pacchetto e la pseudo intestazione IP.                |
| **Puntatore urgente a 16 bit** | Questo campo contiene l'offset positivo dell'ultimo byte dei dati urgenti. Questo campo è valido solo se il bit di codice URG è impostato nell'intestazione. |

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in big endian formato. In questo formato, il byte più significativo della parola si trova all'indirizzo di byte più basso.*

### <a name="tcp-enable"></a>TCP Enable

Prima che siano possibili connessioni TCP e trasmissioni di pacchetti, è necessario che l'applicazione abiliti TCP chiamando il nx_tcp_enable servizio. Dopo aver abilitato, l'applicazione può accedere a tutti i servizi TCP.

### <a name="tcp-socket-create"></a>Creazione di socket TCP

I socket TCP vengono creati durante l'inizializzazione o durante il runtime dai thread dell'applicazione. Il tipo iniziale di servizio, il tempo di vita e le dimensioni della finestra sono definiti dal nx_tcp_socket_create ***locale.*** Non sono previsti limiti al numero di socket TCP in un'applicazione.

### <a name="tcp-checksum"></a>TCP Checksum

TCP specifica un checksum complementare a 16 bit che copre la pseudo-intestazione IP, costituita dall'indirizzo IP di origine, dall'indirizzo IP di destinazione e dalla parola IP protocollo/lunghezza, dall'intestazione TCP e dai dati del pacchetto TCP.

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum TCP nell'hardware. Per questi sistemi, le applicazioni potrebbero voler usare il più possibile la logica di checksum hardware per ridurre il sovraccarico di runtime. Le applicazioni possono disabilitare completamente la logica di calcolo del checksum TCP dalla libreria NetX in fase di compilazione definendo NX_DISABLE_TCP_TX_CHECKSUM **e** **NX_DISABLE_TCP_RX_CHECKSUM**. In questo modo, il codice di checksum TCP non viene compilato in .

### <a name="tcp-port"></a>Porta TCP

Una porta TCP è un punto di connessione logico nel protocollo TCP. Nel componente TCP di NetX sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. A differenza di UDP in cui i dati da una porta possono essere inviati a qualsiasi altra porta di destinazione, una porta TCP è connessa a un'altra porta TCP specifica e solo quando viene stabilita questa connessione può essere possibile eseguire qualsiasi trasferimento dei dati e solo tra le due porte che la connettono.

> [!IMPORTANT]
> *Le porte TCP sono completamente separate dalle porte UDP. Ad esempio, il numero di porta UDP 1 non ha alcuna relazione con la porta TCP numero 1.*

## <a name="client-server-model"></a>Client-Server modello

Per usare TCP per il trasferimento dei dati, è prima necessario stabilire una connessione tra i due socket TCP. La creazione della connessione viene eseguita in modalità client-server. Il lato client della connessione è il lato che avvia la connessione, mentre il lato server attende semplicemente le richieste di connessione client prima che venga eseguita qualsiasi elaborazione.

> [!IMPORTANT]
> *Per i dispositivi multihome, NetX determina automaticamente l'indirizzo di origine da usare per la connessione e l'indirizzo hop successivo in base all'indirizzo IP di destinazione della connessione.*

### <a name="tcp-socket-state-machine"></a>Computer a stati del socket TCP

La connessione tra due socket TCP (un client e un server) è complessa e viene gestita in modo macchina a stati. Ogni socket TCP viene avviato in uno stato CLOSED. Tramite gli eventi di connessione, la macchina a stati di ogni socket esegue la migrazione allo stato ESTABLISHED, che è il punto in cui viene eseguita la maggior parte del trasferimento dei dati in TCP. Quando un lato della connessione non vuole più inviare dati, si disconnette. Dopo la disconnessione dell'altro lato, alla fine il socket TCP torna allo stato CLOSED. Questo processo si ripete ogni volta che un client e un server TCP stabiliscono e chiudono una connessione. La figura 11 mostra i vari stati della macchina a stati TCP.

![Stati della macchina a stati TCP](./media/user-guide/states-tcp-state-machine.png)

### <a name="figure-11-states-of-the-tcp-state-machine"></a>FIGURA 11. Stati della macchina a stati TCP

### <a name="tcp-client-connection"></a>Connessione client TCP

Come accennato in precedenza, il lato client della connessione TCP avvia una richiesta di connessione a un server TCP. Prima di poter eseguire una richiesta di connessione, è necessario che TCP sia abilitato nell'istanza IP del client. Inoltre, il socket TCP client deve essere successivamente creato con il servizio ***nx_tcp_socket_create** _ e associato a una porta tramite il _*_nx_tcp_client_socket_bind_*_ servizio. Dopo aver associato il socket client, il servizio _ *_nx_tcp_client_socket_connect_** viene usato per stabilire una connessione con un server TCP. Si noti che il socket deve essere in stato CLOSED per avviare un tentativo di connessione. La connessione viene avviata con NetX che emette un pacchetto SYN e quindi attende un pacchetto SYN ACK dal server, che indica l'accettazione della richiesta di connessione. Dopo la ricezione di SYN ACK, NetX risponde con un pacchetto ACK e alza di livello il socket client allo stato ESTABLISHED.

### <a name="tcp-client-disconnection"></a>Disconnessione client TCP

La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket client invia un pacchetto RST al socket del server e inserisce il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito:

- Se il server ha avviato in precedenza una richiesta di disconnessione (il socket client ha già ricevuto un pacchetto FIN, ha risposto con un ACK e si trova nello stato CLOSE WAIT), NetX alza di livello lo stato del socket TCP client allo stato LAST ACK e invia un pacchetto FIN. Attende quindi un ACK dal server prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se d'altra parte, il client è il primo ad avviare una richiesta di disconnessione (il server non si è disconnesso e il socket è ancora nello stato ESTABLISHED), NetX invia un pacchetto FIN per avviare la disconnessione e attende di ricevere una FIN e un ACK dal server prima di completare la disconnessione e posizionare il socket in uno stato CLOSED.

Se sono ancora presenti pacchetti nella coda di trasmissione socket, NetX viene sospeso per il timeout specificato per consentire il riconoscimento dei pacchetti. Se il timeout scade, NetX svuota la coda di trasmissione del socket client.

Per annullare l'associazione della porta dal socket client, l'applicazione chiama ***nx_tcp_client_socket_unbind***. Il socket deve essere in uno stato CLOSED o in corso di disconnessione (ad esempio, lo stato TIMED WAIT) prima del rilascio della porta. In caso contrario, viene restituito un errore.

Infine, se l'applicazione non richiede più il socket client, chiama ***nx_tcp_socket_delete*** per eliminare il socket.

### <a name="tcp-server-connection"></a>Connessione al server TCP

Il lato server di una connessione TCP è passivo. Ad esempio, il server attende che un client avvii la richiesta di connessione. Per accettare una connessione client, è prima necessario che TCP sia abilitato nell'istanza IP chiamando il servizio ***nx_tcp_enable** _. Successivamente, l'applicazione deve creare un socket TCP usando il servizio _ *_nx_tcp_socket_create_**.

Il socket del server deve essere configurato anche per l'ascolto delle richieste di connessione. Questa operazione viene ottenuta usando il ***nx_tcp_server_socket_listen*** servizio. Questo servizio posiziona il socket del server nello stato LISTEN e associa la porta del server specificata al socket.

> [!IMPORTANT]
> *Per impostare una routine di callback di ascolto socket, l'applicazione specifica la funzione di callback appropriata per l'argomento tcp_listen_callback del **servizio nx_tcp_server_socket_listen** socket. Questa funzione di callback dell'applicazione viene quindi eseguita da NetX ogni volta che viene richiesta una nuova connessione sulla porta del server. L'elaborazione nel callback è sotto il controllo dell'applicazione.*

Per accettare richieste di connessione client, l'applicazione chiama il **nx_tcp_server_socket_accept** _service. Il socket del server deve essere in uno stato LISTEN o SYN RECEIVED (ad esempio, il server è nello stato LISTEN e ha ricevuto un pacchetto SYN da un client che richiede una connessione) per chiamare il servizio accept. Uno stato restituito correttamente da _ *_nx_tcp_server_socket_accept_** indica che la connessione è stata impostata e il socket del server è nello stato ESTABLISHED.

Dopo che il socket del server ha una connessione valida, le richieste di connessione client aggiuntive vengono accodati fino alla profondità specificata dal *parametro listen_queue_size*, passato nel ***nx_tcp_server_socket_listen** _service. Per elaborare le connessioni successive su una porta del server, l'applicazione deve chiamare _ *_nx_tcp_server_socket_relisten_** con un socket disponibile(ad esempio, un socket in stato CLOSED). Si noti che è possibile usare lo stesso socket del server se la connessione precedente associata al socket è stata completata e il socket è nello stato CLOSED.

### <a name="tcp-server-disconnection"></a>Disconnessione del server TCP

La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket del server invia un pacchetto RST al socket client e inserisce il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito: |

- Se il client ha avviato in precedenza una richiesta di disconnessione (il socket del server ha già ricevuto un pacchetto FIN, ha risposto con un ACK e si trova nello stato CLOSE WAIT), NetX alza di livello lo stato del socket TCP allo stato LAST ACK e invia un pacchetto FIN. Attende quindi un ACK dal client prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se invece il server è il primo ad avviare una richiesta di disconnessione (il client non si è disconnesso e il socket è ancora nello stato ESTABLISHED), NetX invia un pacchetto FIN per avviare la disconnessione e attende di ricevere una FIN e un ACK dal client prima di completare la disconnessione e posizionare il socket in uno stato CLOSED.

Se nella coda di trasmissione socket sono ancora presenti pacchetti, NetX viene sospeso per il timeout specificato per consentire il riconoscimento di tali pacchetti. Se il timeout scade, NetX scarica la coda di trasmissione del socket del server.

Al termine dell'elaborazione della disconnessione e dopo che il socket del server è nello stato CLOSED, l'applicazione deve chiamare il servizio ***nx_tcp_server_socket_unaccept*** per terminare l'associazione di questo socket alla porta del server. Si noti che questo servizio deve essere chiamato dall'applicazione ***anche se*** nx_tcp_socket_disconnect o ***nx_tcp_server_socket_accept** _ restituiscono uno stato di errore. Dopo il ritorno di _ *_nx_tcp_server_socket_unaccept_** , il socket può essere usato come socket client o server o anche eliminato se non è più necessario. Se si desidera accettare un'altra connessione client sulla stessa porta del server, ***il nx_tcp_server_socket_relisten*** deve essere chiamato su questo socket.

Il segmento di codice seguente illustra la sequenza di chiamate utilizzate da un tipico server TCP:

```c
/* Set up a previously created TCP socket to listen on port 12 */

nx_tcp_server_socket_listen()

/* Loop to make a (another) connection. */
while(1) {

    /* Wait for a client socket connection request for 100 ticks. */
    nx_tcp_server_socket_accept();

    /* (Send and receive TCP messages with the TCP client) */

    /* Disconnect the server socket. */
    nx_tcp_socket_disconnect();

    /* Remove this server socket from listening on the port. */

    nx_tcp_server_socket_unaccept(&server_socket);

    /* Set up server socket to relisten on the same port for the next
    client. */
    nx_tcp_server_socket_relisten();
}
```

### <a name="mss-validation"></a>Convalida MSS

Dimensioni massime segmento (MSS) è la quantità massima di byte che un host TCP può ricevere senza essere frammentata dal livello IP sottostante. Durante la fase di creazione della connessione TCP, entrambe le estremità scambiano il proprio valore MSS TCP, in modo che il mittente non invii un segmento di dati TCP maggiore di MSS del ricevitore. Il modulo TCP NetX convalida facoltativamente il valore MSS annunciato del peer prima di stabilire una connessione. Per impostazione predefinita, NetX non abilita tale controllo. Le applicazioni che vogliono eseguire la convalida MSS devono definire ***NX_ENABLE_TCP_MSS_CHECKING** _ durante la compilazione della libreria NetX e il valore minimo deve essere definito in _*_NX_TCP_MSS_MINIMUM_*_. Le connessioni TCP in ingresso con valori MSS inferiori a _ *_NX_TCP_MSS_MINIMUM_** vengono eliminate.

### <a name="stop-listening-on-a-server-port"></a>Arrestare l'ascolto su una porta del server

Se l'applicazione non vuole più restare in ascolto delle richieste di connessione client su una porta del server specificata in precedenza da una chiamata al servizio ***nx_tcp_server_socket_listen** _, l'applicazione chiama semplicemente il servizio _ *_nx_tcp_server_socket_unlisten_**. Questo servizio inserisce qualsiasi socket in attesa di una connessione nello stato CLOSED e rilascia tutti i pacchetti di richiesta di connessione client in coda.

### <a name="tcp-window-size"></a>Dimensioni finestra TCP

Durante le fasi di configurazione e trasferimento dei dati della connessione, ogni porta segnala la quantità di dati che può gestire, denominata dimensione della finestra. Quando i dati vengono ricevuti ed elaborati, le dimensioni della finestra vengono modificate dinamicamente. In TCP, un mittente può inviare solo una quantità di dati che rientra nella finestra del ricevitore. In pratica, le dimensioni della finestra forniscono il controllo di flusso per il trasferimento dei dati in ogni direzione della connessione.

### <a name="tcp-packet-send"></a>Invio di pacchetti TCP

L'invio di dati TCP è facilmente possibile chiamando la ***nx_tcp_socket_send*** funzione . Se le dimensioni dei dati trasmessi sono maggiori del valore MSS del socket o della finestra di ricezione peer corrente, a seconda di quale sia la dimensione più piccola, la logica interna TCP consente di eliminare i dati che si adattano a min (MSS, peer receive Window) per la trasmissione. Questo servizio crea quindi un'intestazione TCP davanti al pacchetto (incluso il calcolo del checksum). Se le dimensioni della finestra del ricevitore non sono pari a zero, il chiamante invierà il maggior numero di dati possibile per riempire le dimensioni della finestra del ricevitore. Se la finestra di ricezione diventa zero, il chiamante può sospendere e attendere che le dimensioni della finestra del ricevitore aumentino sufficientemente per l'invio del pacchetto. In qualsiasi momento, più thread possono essere sospesi durante il tentativo di inviare dati tramite lo stesso socket.

> [!IMPORTANT]
> *I dati TCP che risiedono nella struttura NX_PACKET devono risiedere su un limite di parola lunga. Inoltre, deve esserci spazio sufficiente tra il puntatore anteposto e il puntatore iniziale dei dati per posizionare le intestazioni TCP, IP e dei supporti fisici.*

### <a name="tcp-packet-retransmit"></a>Ritrasmissione pacchetti TCP

Pacchetti TCP trasmessi in precedenza inviati effettivamente archiviati internamente fino a quando non viene restituito un ACK dall'altro lato della connessione. Se i dati trasmessi non vengono riconosciuti entro il periodo di timeout, il pacchetto archiviato viene inviato nuovamente e viene impostato il periodo di timeout successivo. Quando viene ricevuto un ACK, tutti i pacchetti coperti dal numero di acknowledgement nella coda di trasmissione interna vengono infine rilasciati.

> [!IMPORTANT]
> *L'applicazione non deve riutilizzare il pacchetto o modificare il contenuto del pacchetto dopo che la funzione ***nx_tcp_socket_send** _ restituisce con NX_SUCCESS. Il pacchetto trasmesso viene infine rilasciato dall'elaborazione interna di NetX dopo che i dati sono stati riconosciuti dall'altro end._

### <a name="tcp-keepalive"></a>TCP Keepalive

La funzionalità Keepalive TCP consente a un socket di rilevare se il peer si disconnette senza la terminazione corretta (ad esempio, il peer si è interrotto in modo anomalo) o di impedire a determinate funzionalità di monitoraggio della rete di terminare una connessione per lunghi periodi di inattività. Tcp Keepalive funziona inviando periodicamente un frame TCP senza dati e il numero di sequenza impostato su uno minore del numero di sequenza corrente. Alla ricezione di tale frame Keepalive TCP, il destinatario, se ancora attivo, risponde con un ACK per il numero di sequenza corrente. Questa operazione completa la transazione keepalive.

Per impostazione predefinita, la funzionalità keepalive non è abilitata. Per usare questa funzionalità, la libreria NetX deve essere compilata con ***NX_ENABLE_TCP_KEEPALIVE** _ definito. Il simbolo _ *_NX_TCP_KEEPALIVE_INITIAL_** specifica il numero di secondi di inattività prima dell'avvio del frame keepalive.

### <a name="tcp-packet-receive"></a>Ricezione pacchetti TCP

L'elaborazione dei pacchetti di ricezione TCP (chiamata dal thread helper IP) è responsabile della gestione di varie azioni di connessione e disconnessione, nonché dell'elaborazione di acknowledge di trasmissione. Inoltre, l'elaborazione dei pacchetti di ricezione TCP è responsabile dell'inserimento di pacchetti con dati di ricezione nella coda di ricezione del socket TCP appropriato o del recapito del pacchetto al primo thread sospeso in attesa di un pacchetto.

### <a name="tcp-receive-notify"></a>Notifica di ricezione TCP

Se il thread dell'applicazione deve elaborare i dati ricevuti da più socket, nx_tcp_socket_receive_notify ***usare*** la funzione . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che un pacchetto viene ricevuto nel socket, viene eseguita la funzione di callback.

Il contenuto della funzione di callback è specifico dell'applicazione. Tuttavia, la funzione conterrà molto probabilmente la logica per informare il thread di elaborazione che un pacchetto è disponibile nel socket corrispondente.

### <a name="thread-suspension"></a>Sospensione dei thread

Come accennato in precedenza, i thread dell'applicazione possono essere sospesi durante il tentativo di ricevere dati da una determinata porta TCP. Dopo aver ricevuto un pacchetto su tale porta, viene assegnato al primo thread sospeso e tale thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione TCP, una funzionalità disponibile per la maggior parte dei servizi NetX.

La sospensione dei thread è disponibile anche per i servizi di connessione (client e server), associazione client e disconnessione.

### <a name="tcp-socket-statistics-and-errors"></a>Statistiche ed errori del socket TCP

Se abilitato, il software socket TCP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per ogni istanza IP/TCP:

- Totale pacchetti TCP inviati
- Totale byte TCP inviati
- Totale pacchetti TCP ricevuti
- Totale byte TCP ricevuti
- Totale pacchetti TCP non validi
- Totale pacchetti di ricezione TCP eliminati
- Totale errori checksum ricezione TCP
- Totale connessioni TCP
- Totale disconnessioni TCP
- Totale connessioni TCP eliminate
- Totale ritrasmissioni pacchetti TCP
- Pacchetti socket TCP inviati
- Byte socket TCP inviati
- Pacchetti socket TCP ricevuti
- Byte socket TCP ricevuti
- Ritrasmissioni di pacchetti socket TCP
- Pacchetti socket TCP in coda
- Errori di checksum del socket TCP
- Stato socket TCP
- Profondità coda trasmissione socket TCP
- Dimensioni della finestra di trasmissione del socket TCP
- Dimensioni della finestra di ricezione del socket TCP

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con il servizio ***nx_tcp_info_get** _ per le statistiche TCP totali e il servizio _ *_nx_tcp_socket_info_get_** per le statistiche TCP per ogni socket.

## <a name="tcp-socket-control-block-nx_tcp_socket"></a>Blocco di controllo socket TCP NX_TCP_SOCKET

Le caratteristiche di ogni socket TCP si trovano nel blocco di controllo *NX_TCP_SOCKET* associato, che contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di connessione di rete, la porta associata e la coda di pacchetti di ricezione. Questa struttura è definita nel file ***nx_api.h.***
