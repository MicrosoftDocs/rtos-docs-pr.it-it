---
title: Capitolo 4 - Descrizione dei Azure RTOS ThreadX SMP
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS ThreadX SMP in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 71b964963968b0ec6fa3c8cc70cc46576e8ff33e2cfad0315182afe1f1afcc5b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802159"
---
# <a name="chapter-4---description-of-azure-rtos-threadx-smp-services"></a>Capitolo 4 - Descrizione dei Azure RTOS ThreadX SMP

Questo capitolo contiene una descrizione di tutti i Azure RTOS ThreadX SMP in ordine alfabetico. I nomi sono progettati in modo da raggruppare tutti i servizi simili. Nella sezione "Valori restituiti" delle descrizioni seguenti, i  valori in **GRASSETTO** non sono interessati dalla definizione TX_DISABLE_ERROR_CHECKING usata per disabilitare il controllo degli errori dell'API; mentre i valori visualizzati in nonbold sono completamente disabilitati. Inoltre, un **"Sì"** elencato sotto l'intestazione "**Preemption Possible**" indica che la chiamata al servizio può riprendere un thread con priorità più alta, eliminando così il thread chiamante.

- **tx_block_allocate**: *Allocare un blocco di memoria a dimensione fissa* 
- **tx_block_pool_create:** Creare *un pool di blocchi di memoria a dimensione fissa* 
- **tx_block_pool_delete:** Eliminare *il pool di blocchi di memoria* 
- **tx_block_pool_info_get:** Recuperare *informazioni sul pool di blocchi* 
- **tx_block_pool_performance_info_get:** Ottenere *informazioni sulle prestazioni del pool di blocchi* 
- **tx_block_pool_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema del pool di blocchi* 
- **tx_block_pool_prioritize:** Classificare in *ordine di priorità l'elenco di sospensione del pool di blocchi* 
- **tx_block_release:** *Rilasciare un blocco di memoria a dimensione fissa*
- **tx_byte_allocate**: *Allocare byte di memoria* 
- **tx_byte_pool_create:** Creare *un pool di memoria di byte* 
- **tx_byte_pool_delete:** Elimina *pool di byte di memoria* 
- **tx_byte_pool_info_get:** Recuperare *informazioni sul pool di byte* 
- **tx_byte_pool_performance_info_get:** Ottenere *informazioni sulle prestazioni del pool di byte* 
- **tx_byte_pool_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema del pool di byte* 
- **tx_byte_pool_prioritize:** Classificare in *ordine di priorità l'elenco di sospensione del pool di byte* 
- **tx_byte_release:** *Rilasciare i byte nel pool di memoria* 
- **tx_event_flags_create:** Creare *un gruppo di flag di eventi* 
- **tx_event_flags_delete:** Eliminare *il gruppo di flag di evento* 
- **tx_event_flags_get:** Ottenere *i flag di evento dal gruppo di flag di evento* 
- **tx_event_flags_info_get:** recuperare *informazioni sul gruppo di flag di eventi* 
- **tx_event_flags_performance_info_get:** Ottenere *informazioni sulle prestazioni del gruppo di flag di eventi* 
- **tx_event_flags_performance_system_info_get:** Recuperare *le informazioni sul sistema di prestazioni* 
- **tx_event_flags_set:** impostare *i flag di evento in un gruppo di flag di eventi* 
- **tx_event_flags_set_notify:** *Notificare all'applicazione quando sono impostati i flag di evento*
- **tx_interrupt_control:** Abilitare *e disabilitare gli interrupt* 
- **tx_mutex_create:** Creare *mutex di esclusione reciproca* 
- **tx_mutex_delete:** Elimina *mutex di esclusione reciproca* 
- **tx_mutex_get:** Ottenere *la proprietà del mutex* 
- **tx_mutex_info_get:** *recuperare informazioni sul mutex* 
- **tx_mutex_performance_info_get:** Ottenere *informazioni sulle prestazioni del mutex* 
- **tx_mutex_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema mutex* 
- **tx_mutex_prioritize:** Classificare *in ordine di priorità l'elenco delle sospensioni mutex* 
- **tx_mutex_put:** Rilascio *della proprietà del mutex* 
- **tx_queue_create:** Creare *una coda di messaggi* 
- **tx_queue_delete:** Eliminare *la coda di messaggi* 
- **tx_queue_flush:** Messaggi *vuoti nella coda di messaggi* 
- **tx_queue_front_send:** *Inviare un messaggio all'inizio della coda* 
- **tx_queue_info_get:** Recuperare *informazioni sulla coda* 
- **tx_queue_performance_info_get:** Ottenere *informazioni sulle prestazioni della coda* 
- **tx_queue_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema di accodamento*
- **tx_queue_prioritize:** Classificare *in ordine di priorità l'elenco di sospensione della coda* 
- **tx_queue_receive:** Ottenere *un messaggio dalla coda di messaggi* 
- **tx_queue_send:** *Inviare un messaggio alla coda di messaggi* 
- **tx_queue_send_notify:** Notifica *all'applicazione quando il messaggio viene inviato alla coda* 
- **tx_semaphore_ceiling_put:** *inserire un'istanza nel semaforo di conteggio con il limite massimo* 
- **tx_semaphore_create:** Creare *un semaforo di conteggio* 
- **tx_semaphore_delete:** Eliminare *il semaforo di conteggio* 
- **tx_semaphore_get:** *Ottenere l'istanza dal semaforo di conteggio* 
- **tx_semaphore_info_get:** Recuperare *informazioni sul semaforo* 
- **tx_semaphore_performance_info_get:** Ottenere *informazioni sulle prestazioni del semaforo* 
- **tx_semaphore_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema semaforo* 
- **tx_semaphore_prioritize:** Classificare *in ordine di priorità l'elenco di sospensione del semaforo* 
- **tx_semaphore_put:** Inserire *un'istanza nel semaforo di conteggio* 
- **tx_semaphore_put_notify:** *Notificare all'applicazione quando viene inserito il semaforo* 
- **tx_thread_create:** Creare *un thread dell'applicazione* 
- **tx_thread_delete:** Eliminare *il thread dell'applicazione*
- **tx_thread_entry_exit_notify:** Notificare *all'applicazione l'ingresso e l'uscita del thread* 
- **tx_thread_identify**: *recupera il puntatore al thread attualmente in esecuzione* 
- **tx_thread_info_get:** recuperare *informazioni sul thread* 
- **tx_thread_performance_info_get:** Ottenere *informazioni sulle prestazioni dei thread* 
- **tx_thread_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema di thread* 
- **tx_thread_preemption_change:** modificare *la soglia di preemption del thread dell'applicazione* 
- **tx_thread_priority_change**: modifica *della priorità del thread dell'applicazione* 
- **tx_thread_relinquish:** *cesciare il controllo ad altri thread dell'applicazione* 
- **tx_thread_reset:** Reimpostare *il thread* 
- **tx_thread_resume:** Riprendere *il thread dell'applicazione sospeso* 
- **tx_thread_sleep:** *sospende il thread corrente per l'ora specificata* 
- **tx_thread_smp_core_exclude:** *Escludere l'esecuzione di thread in un set di core* 
- **tx_thread_smp_core_exclude_get**: *ottiene l'esclusione principale corrente del thread* 
- **tx_thread_smp_core_get:** recupera *il core del chiamante attualmente in esecuzione* 
- **tx_thread_stack_error_notify:** *Registrare il callback di notifica degli errori dello stack di thread* 
- **tx_thread_suspend:** Sospendere *il thread dell'applicazione*
- **tx_thread_terminate**: *termina il thread dell'applicazione* 
- **tx_thread_time_slice_change**: modifica *la sezione temporale del thread dell'applicazione* 
- **tx_thread_wait_abort:** *interrompi sospensione del thread specificato* 
- **tx_time_get**: *recupera l'ora corrente* 
- **tx_time_set**: *imposta l'ora corrente* 
- **tx_timer_activate:** Attivare *il timer dell'applicazione* 
- **tx_timer_change:** Modificare *il timer dell'applicazione* 
- **tx_timer_create:** Creare *un timer dell'applicazione* 
- **tx_timer_deactivate:** *Disattivare il timer dell'applicazione* 
- **tx_timer_delete:** Eliminare *il timer dell'applicazione* 
- **tx_timer_info_get:** Recuperare *informazioni su un timer dell'applicazione* 
- **tx_timer_performance_info_get:** Ottenere *informazioni sulle prestazioni del timer* 
- **tx_timer_performance_system_info_get:** Ottenere *informazioni sulle prestazioni del sistema timer* 
- **tx_timer_smp_core_exclude:** Escludere *l'esecuzione del timer in un set di core* 
- **tx_timer_smp_core_exclude_get**: ottiene *l'esclusione principale corrente del timer*

## <a name="tx_block_allocate"></a>tx_block_allocate
Allocare un blocco di memoria a dimensione fissa

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_allocate(TX_BLOCK_POOL *pool_ptr, VOID **block_ptr,
                          ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio alloca un blocco di memoria a dimensione fissa dal pool di memoria specificato. Le dimensioni effettive del blocco di memoria vengono determinate durante la creazione del pool di memoria.

> [!WARNING]
> È importante assicurarsi che il codice dell'applicazione non scrivo all'esterno del blocco di memoria allocato. In questo caso, si verifica un danneggiamento in un blocco di memoria adiacente (in genere successivo). I risultati sono imprevedibili e sono spesso fatali.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore a un pool di blocchi di memoria creato in precedenza.
- **block_ptr:** puntatore a un puntatore a blocco di destinazione. Al termine dell'allocazione, l'indirizzo del blocco di memoria allocato viene inserito in cui punta questo parametro.
- **wait_option**: definisce il comportamento del servizio se non sono disponibili blocchi di memoria. Le opzioni di attesa sono definite nel modo seguente:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (da 0x00000001 a 0xFFFFFFFE)  
    
    La TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che l'operazione sia riuscita o meno. Questa è l'unica opzione valida se il servizio viene chiamato da un non thread; ad esempio inizializzazione, timer o ISR.

    Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso per un periodo indefinito fino a quando non è disponibile un blocco di memoria.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa di un blocco di memoria.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Allocazione del blocco di memoria riuscita.
- **TX_DELETED:**(0x01) Il pool di blocchi di memoria è stato eliminato durante la sospensione del thread.
- **TX_NO_MEMORY:** il servizio (0x10) non è stato in grado di allocare un blocco di memoria entro il tempo di attesa specificato.
- **TX_WAIT_ABORTED:**(0x1A) Sospensione interrotta da un altro thread, timer o ISR.
- TX_POOL_ERROR: (0x02) Puntatore del pool a blocchi di memoria non valido.
- TX_PTR_ERROR: (0x03) Puntatore non valido al puntatore di destinazione.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un thread non thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```c
TX_BLOCK_POOL   my_pool;
unsigned char*memory_ptr;
UINT         status;

/* Allocate a memory block from my_pool. Assume that the
   pool has already been created with a call to
   tx_block_pool_create. */
status = tx_block_allocate(&my_pool, (VOID **) &memory_ptr,
                               TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
   address of the allocated block of memory. */
```

### <a name="see-also"></a>Vedere anche

- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_create"></a>tx_block_pool_create
Creare un pool di blocchi di memoria a dimensione fissa

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_pool_create(TX_BLOCK_POOL *pool_ptr,
                          CHAR *name_ptr, ULONG block_size,
                          VOID *pool_start, ULONG pool_size);
```
### <a name="description"></a>Descrizione

Questo servizio crea un pool di blocchi di memoria di dimensioni fisse. L'area di memoria specificata è suddivisa in quanti più blocchi di memoria a dimensione fissa possibile usando la formula :    
**total blocks** = (**total bytes**) / (**block size** + sizeof(void *))

> [!IMPORTANT]
> Ogni blocco di memoria contiene un puntatore di overhead invisibile all'utente ed è rappresentato da "sizeof(void *)" nella formula precedente.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore a un blocco di controllo del pool di blocchi di memoria.
- **name_ptr:** puntatore al nome del pool di blocchi di memoria.
- **block_size**: numero di byte in ogni blocco di memoria.
- **pool_start:** indirizzo iniziale del pool di blocchi di memoria. L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.
- **pool_size**: numero totale di byte disponibili per il pool di blocchi di memoria.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Creazione del pool a blocchi di memoria completata.
- TX_POOL_ERROR: (0x02) Puntatore del pool a blocchi di memoria non valido. Il puntatore è NULL o il pool è già stato creato.
- TX_PTR_ERROR: (0x03) Indirizzo iniziale del pool non valido.
- TX_SIZE_ERROR: (0x05) Dimensioni del pool non valide.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_BLOCK_POOL  my_pool;
UINT           status;

/* Create a memory pool whose total size is 1000 bytes
   starting at address 0x100000. Each block in this
   pool is defined to be 50 bytes long. */
status = tx_block_pool_create(&my_pool, "my_pool_name",
               50, (VOID *) 0x100000, 1000);

/* If status equals TX_SUCCESS, my_pool contains 18
   memory blocks of 50 bytes each. The reason
   there are not 20 blocks in the pool is
   because of the one overhead pointer associated with each
   block. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_delete"></a>tx_block_pool_delete

Eliminare il pool di blocchi di memoria

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il pool di memoria a blocchi specificato. Tutti i thread sospesi in attesa di un blocco di memoria da questo pool vengono ripresi e vengono TX_DELETED stato restituito.

> [!IMPORTANT]
> È responsabilità dell'applicazione gestire l'area di memoria associata al pool, disponibile al termine del servizio. Inoltre, l'applicazione deve impedire l'uso di un pool eliminato o dei blocchi di memoria precedenti.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore a un pool di blocchi di memoria creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Eliminazione del pool a blocchi di memoria completata.
- TX_POOL_ERROR: (0x02) Puntatore del pool a blocchi di memoria non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_BLOCK_POOLmy_pool;
UINT           status;

    /* Delete entire memory block pool. Assume that the pool
      has already been created with a call to
      tx_block_pool_create. */
    status =  tx_block_pool_delete(&my_pool);

    /* If status equals TX_SUCCESS, the memory block pool is
       deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_info_get"></a>tx_block_pool_info_get

Recuperare informazioni sul pool a blocchi

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_pool_info_get(TX_BLOCK_POOL *pool_ptr, CHAR **name,
                          ULONG *available, ULONG *total_blocks,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_BLOCK_POOL **next_pool);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul pool di memoria a blocchi specificato.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore al pool di blocchi di memoria creato in precedenza.
- **name:** puntatore alla destinazione per il puntatore al nome del pool di blocchi.
- **available**: puntatore alla destinazione per il numero di blocchi disponibili nel pool di blocchi.
- **total_blocks:** puntatore alla destinazione per il numero totale di blocchi nel pool di blocchi.
- **first_suspended:** puntatore alla destinazione per il puntatore al thread che si trova per primo nell'elenco di sospensione di questo pool di blocchi.
- **suspended_count:** puntatore alla destinazione per il numero di thread attualmente sospesi in questo pool di blocchi.
- **next_pool:** puntatore alla destinazione per il puntatore del successivo pool di blocchi creato.

> [!IMPORTANT]
> Se si specifica un TX_NULL per qualsiasi parametro, il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Recupero delle informazioni sul pool a blocchi riuscito.
- TX_POOL_ERROR: (0x02) Puntatore del pool a blocchi di memoria non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_BLOCK_POOL    my_pool;
CHAR             *name;
ULONG            available;
ULONG            total_blocks;
TX_THREAD        *first_suspended;
ULONG            suspended_count;
TX_BLOCK_POOL    *next_pool;
UINT             status;

/* Retrieve information about the previously created
   block pool "my_pool." */
status = tx_block_pool_info_get(&my_pool, &name,
                &available,&total_blocks,
                &first_suspended, &suspended_count,
                &next_pool);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_performance_info_get"></a>tx_block_pool_performance_info_get

Ottenere informazioni sulle prestazioni del pool di blocchi

### <a name="prototype"></a>Prototipo

```c
UINT tx_block_pool_performance_info_get(TX_BLOCK_POOL *pool_ptr,
       ULONG *allocates, ULONG *releases,
       ULONG *suspensions, ULONG *timeouts));
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al pool di blocchi di memoria specificato.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX SMP devono essere compilate con TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO **per** questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore al pool di blocchi di memoria creato in precedenza.
- **allocates:** puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.
- **releases:** puntatore alla destinazione per il numero di richieste di versione eseguite in questo pool.
- **suspensions:** puntatore alla destinazione per il numero di sospensioni di allocazione di thread in questo pool.
- **timeouts:** puntatore alla destinazione per il numero di timeout di sospensione di allocazione in questo pool.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere prestazioni del pool a blocchi riuscite.
- **TX_PTR_ERROR**: (0x03) Puntatore del pool di blocchi non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_BLOCK_POOL     my_pool;
ULONG             allocates;
ULONG             releases;
ULONG             suspensions;
ULONG             timeouts;

/* Retrieve performance information on the previously created block
   pool. */
status = tx_block_pool_performance_info_get(&my_pool, &allocates,
                                            &releases,
                &suspensions,
                &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_release

## <a name="tx_block_pool_performance_system_info_get"></a>tx_block_pool_performance_system_info_get

Ottenere informazioni sulle prestazioni del sistema del pool di blocchi

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_pool_performance_system_info_get(ULONG *allocates,
       ULONG *releases, ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative a tutti i pool di blocchi di memoria nell'applicazione.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX SMP devono essere compilate con TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO **per** questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **allocates:** puntatore alla destinazione per il numero totale di richieste di allocazione eseguite in tutti i pool di blocchi.
- **releases:** puntatore alla destinazione per il numero totale di richieste di versione eseguite in tutti i pool di blocchi.
- **suspensions:** puntatore alla destinazione per il numero totale di sospensioni di allocazione di thread in tutti i pool di blocchi.
- **timeouts:** puntatore alla destinazione per il numero totale di timeout di sospensione di allocazione in tutti i pool di blocchi.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere prestazioni del sistema del pool a blocchi riuscite.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
ULONG         allocates;
ULONG         releases;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all the block pools in
   the system. */
status = tx_block_pool_performance_system_info_get(&allocates,
                     &releases,&suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_prioritize
- tx_block_release

## <a name="tx_block_pool_prioritize"></a>tx_block_pool_prioritize

Classificare in ordine di priorità l'elenco di sospensioni del pool a blocchi

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il thread con priorità più alta sospeso per un blocco di memoria in questo pool all'inizio dell'elenco di sospensione. Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.

### <a name="parameters"></a>Parametri 

- **pool_ptr:** puntatore a un blocco di controllo del pool di blocchi di memoria.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Priorità del pool a blocchi riuscita.
- TX_POOL_ERROR: (0x02) Puntatore del pool a blocchi di memoria non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_BLOCK_POOL my_pool;
UINT          status;

/* Ensure that the highest priority thread will receive
   the next free block in this pool. */
status = tx_block_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_block_release call will wake up this thread. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_release

## <a name="tx_block_release"></a>tx_block_release

Rilasciare un blocco di memoria a dimensione fissa

### <a name="prototype"></a>Prototipo

```C
UINT tx_block_release(VOID *block_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rilascia un blocco allocato in precedenza al pool di memoria associato. Se sono presenti uno o più thread sospesi in attesa di blocchi di memoria da questo pool, al primo thread sospeso viene assegnato questo blocco di memoria e ripreso.

> [!IMPORTANT]
> L'applicazione deve impedire l'uso di un'area del blocco di memoria dopo il rilascio nel pool.

### <a name="parameters"></a>Parametri

- **block_ptr:** puntatore al blocco di memoria allocato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Rilascio del blocco di memoria riuscito.
- TX_PTR_ERROR: (0x03) Puntatore non valido al blocco di memoria.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_BLOCK_POOLmy_pool;
unsigned char*memory_ptr;
UINT         status;

/* Release a memory block back to my_pool. Assume that the
   pool has been created and the memory block has been
   allocated. */
status = tx_block_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the block of memory pointed
   to by memory_ptr has been returned to the pool. */
```
### <a name="see-also"></a>Vedere anche

- tx_block_allocate
- tx_block_pool_create
- tx_block_pool_delete
- tx_block_pool_info_get
- tx_block_pool_performance_info_get
- tx_block_pool_performance_system_info_get
- tx_block_pool_prioritize

## <a name="tx_byte_allocate"></a>tx_byte_allocate

Allocare byte di memoria

### <a name="prototype"></a>Prototipo

```C
UINT tx_byte_allocate(TX_BYTE_POOL *pool_ptr,
                          VOID **memory_ptr, ULONG memory_size,
                          ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio alloca il numero specificato di byte dal pool di byte di memoria specificato.

> [!WARNING]
> È importante assicurarsi che il codice dell'applicazione non scrivo all'esterno del blocco di memoria allocato. In questo caso, si verifica un danneggiamento in un blocco di memoria adiacente (in genere successivo). I risultati sono imprevedibili e sono spesso fatali.

> [!IMPORTANT]
> Le prestazioni di questo servizio sono una funzione delle dimensioni del blocco e della quantità di frammentazione nel pool. Di conseguenza, questo servizio non deve essere usato durante i thread di esecuzione critici per il tempo.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore a un pool di memoria creato in precedenza.
- **memory_ptr:** puntatore a un puntatore di memoria di destinazione. Al termine dell'allocazione, viene inserito l'indirizzo dell'area di memoria allocata a cui punta questo parametro.
- **memory_size**: numero di byte richiesti.
- **wait_option:** definisce il comportamento del servizio se la memoria disponibile non è sufficiente. Le opzioni di attesa sono definite nel modo seguente:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (da 0x00000001 a 0xFFFFFFFE)

    La TX_NO_WAIT comporta un ritorno immediato da questo servizio indipendentemente dal fatto che l'operazione sia riuscita o meno. *Questa è l'unica opzione valida se il servizio viene chiamato dall'inizializzazione.*

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando non è disponibile memoria sufficiente.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della memoria.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Allocazione di memoria riuscita.
- **TX_DELETED:** il pool di memoria (0x01) è stato eliminato durante la sospensione del thread.
- **TX_NO_MEMORY:** il servizio (0x10) non è stato in grado di allocare la memoria entro il tempo di attesa specificato.
- **TX_WAIT_ABORTED:**(0x1A) Sospensione interrotta da un altro thread, timer o ISR.
- TX_POOL_ERROR: (0x02) Puntatore del pool di memoria non valido.
- TX_PTR_ERROR: (0x03) Puntatore non valido al puntatore di destinazione.
- TX_SIZE_ERROR: (0X05) Le dimensioni richieste sono pari a zero o maggiori del pool.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un thread non thread.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_BYTE_POOL my_pool;
unsigned char*memory_ptr;
UINT         status;

/* Allocate a 112 byte memory area from my_pool. Assume
   that the pool has already been created with a call to
   tx_byte_pool_create. */
status =  tx_byte_allocate(&my_pool, (VOID **) &memory_ptr,
                       112, TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
   address of the allocated memory area. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_create"></a>tx_byte_pool_create

Creare un pool di memoria di byte

### <a name="prototype"></a>Prototipo

```C
UINT tx_byte_pool_create(TX_BYTE_POOL *pool_ptr,
                          CHAR *name_ptr, VOID *pool_start,
                          ULONG pool_size);
```
### <a name="description"></a>Descrizione

Questo servizio crea un pool di byte di memoria nell'area specificata. Inizialmente il pool è costituito fondamentalmente da un blocco gratuito molto grande. Tuttavia, il pool viene suddiviso in blocchi più piccoli quando vengono effettuate le allocazioni.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore a un blocco di controllo del pool di memoria.
- **name_ptr:** puntatore al nome del pool di memoria.
- **pool_start**: indirizzo iniziale del pool di memoria. L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.
- **pool_size**: numero totale di byte disponibili per il pool di memoria.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Creazione del pool di memoria completata.
- TX_POOL_ERROR: (0x02) Puntatore del pool di memoria non valido. Il puntatore è NULL o il pool è già stato creato.
- TX_PTR_ERROR: (0x03) Indirizzo iniziale del pool non valido.
- TX_SIZE_ERROR: (0x05) Dimensioni del pool non valide.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_BYTE_POOL my_pool;
UINT         status;

/* Create a memory pool whose total size is 2000 bytes
   starting at address 0x500000. */
status =  tx_byte_pool_create(&my_pool, "my_pool_name",
             (VOID *) 0x500000, 2000);

/* If status equals TX_SUCCESS, my_pool is available for
   allocating memory. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_delete"></a>tx_byte_pool_delete

Eliminare il pool di byte di memoria

### <a name="prototype"></a>Prototipo

```C
UINT tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il pool di byte di memoria specificato. Tutti i thread sospesi in attesa di memoria da questo pool vengono ripresi e vengono TX_DELETED stato restituito.

> [!IMPORTANT]
> È responsabilità dell'applicazione gestire l'area di memoria associata al pool, disponibile al termine del servizio. Inoltre, l'applicazione deve impedire l'uso di un pool eliminato o di una memoria allocata in precedenza da esso.

### <a name="parameters"></a>Parametri 

- **pool_ptr:** puntatore a un pool di memoria creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Eliminazione del pool di memoria completata.
- TX_POOL_ERROR: (0x02) Puntatore del pool di memoria non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_BYTE_POOL my_pool;
UINT         status;

/* Delete entire memory pool. Assume that the pool has already
   been created with a call to tx_byte_pool_create. */
status =   tx_byte_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, memory pool is deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

Recuperare informazioni sul pool di byte

### <a name="prototype"></a>Prototipo

```C
UINT tx_byte_pool_info_get(TX_BYTE_POOL *pool_ptr, CHAR **name,
                          ULONG *available, ULONG *fragments,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_BYTE_POOL **next_pool);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul pool di byte di memoria specificato.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore al pool di memoria creato in precedenza.
- **name:** puntatore alla destinazione per il puntatore al nome del pool di byte.
- **available**: puntatore alla destinazione per il numero di byte disponibili nel pool.
- **fragments:** puntatore alla destinazione per il numero totale di frammenti di memoria nel pool di byte.
- **first_suspended:** puntatore alla destinazione per il puntatore al thread che si trova per primo nell'elenco di sospensione di questo pool di byte.
- **suspended_count:** puntatore alla destinazione per il numero di thread attualmente sospesi in questo pool di byte.
- **next_pool:** puntatore alla destinazione per il puntatore del successivo pool di byte creato.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Recupero delle informazioni sul pool riuscito.
- TX_POOL_ERROR: (0x02) Puntatore del pool di memoria non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_BYTE_POOL my_pool;
CHAR         *name;
ULONG        available;
ULONG        fragments;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_BYTE_POOL *next_pool;
UINT         status;

/* Retrieve information about the previously created
   block pool "my_pool." */
status =  tx_byte_pool_info_get(&my_pool, &name,
             &available, &fragments,
             &first_suspended, &suspended_count,
             &next_pool);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_performance_info_get"></a>tx_byte_pool_performance_info_get

Ottenere informazioni sulle prestazioni del pool di byte

### <a name="prototype"></a>Prototipo

```C
UINT tx_byte_pool_performance_info_get(TX_BYTE_POOL *pool_ptr,
        ULONG *allocates, ULONG *releases,
        ULONG *fragments_searched, ULONG *merges, ULONG *splits,
        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al pool di byte di memoria specificato.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **pool_ptr:** puntatore al pool di byte di memoria creato in precedenza.
- **allocates:** puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.
- **releases:** puntatore alla destinazione per il numero di richieste di versione eseguite in questo pool.
- **fragments_searched:** puntatore alla destinazione per il numero di frammenti di memoria interni cercati durante le richieste di allocazione nel pool.
- **merges:** puntatore alla destinazione per il numero di blocchi di memoria interni uniti durante le richieste di allocazione in questo pool.
- **splits:** puntatore alla destinazione per il numero di blocchi di memoria interni suddivisi (frammenti) creati durante le richieste di allocazione nel pool.
- **suspensions:** puntatore alla destinazione per il numero di sospensioni di allocazione di thread nel pool.
- **timeouts:** puntatore alla destinazione per il numero di timeout di sospensione di allocazione in questo pool.

> [!IMPORTANT]
> Se si specifica un TX_NULL per qualsiasi parametro, il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- TX_SUCCESS: (0x00) Ottenere le prestazioni del pool di byte con esito positivo.
- **TX_PTR_ERROR**: (0x03) Puntatore del pool di byte non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_BYTE_POOL     my_pool;
ULONG            fragments_searched;
ULONG            merges;
ULONG            splits;
ULONG            allocates;
ULONG            releases;
ULONG            suspensions;
ULONG            timeouts;

/* Retrieve performance information on the previously created byte
   pool.  */
status =  tx_byte_pool_performance_info_get(&my_pool,
                &fragments_searched,
                &merges, &splits,
                &allocates, &releases,
                      &suspensions,&timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_performance_system_info_get"></a>tx_byte_pool_performance_system_info_get

Ottenere informazioni sulle prestazioni del sistema del pool di byte

### <a name="prototype"></a>Prototipo

```C
UINT  tx_byte_pool_performance_system_info_get(ULONG *allocates,
        ULONG *releases, ULONG *fragments_searched, ULONG *merges,
        ULONG *splits, ULONG *suspensions, ULONG *timeouts);;
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni su tutti i pool di byte di memoria nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **allocates:** puntatore alla destinazione per il numero di richieste di allocazione eseguite in questo pool.
- **releases:** puntatore alla destinazione per il numero di richieste di versione eseguite in questo pool.
- **fragments_searched:** puntatore alla destinazione per il numero totale di frammenti di memoria interni cercati durante le richieste di allocazione in tutti i pool di byte.
- **merges:** puntatore alla destinazione per il numero totale di blocchi di memoria interni uniti durante le richieste di allocazione in tutti i pool di byte.
- **splits:** puntatore alla destinazione per il numero totale di blocchi di memoria interni suddivisi (frammenti) creati durante le richieste di allocazione in tutti i pool di byte.
- **suspensions:** puntatore alla destinazione per il numero totale di sospensioni di allocazione di thread in tutti i pool di byte.
- **timeouts:** puntatore alla destinazione per il numero totale di timeout di sospensione di allocazione in tutti i pool di byte.

> [!IMPORTANT]
> Se si specifica un TX_NULL per qualsiasi parametro, il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere le prestazioni del pool di byte con esito positivo.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
ULONG         fragments_searched;
ULONG         merges;
ULONG         splits;
ULONG         allocates;
ULONG         releases;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all byte pools in the
   system. */
status =
tx_byte_pool_performance_system_info_get(&fragments_searched,
                &merges, &splits, &allocates, &releases,
                &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_prioritize
- tx_byte_release

## <a name="tx_byte_pool_prioritize"></a>tx_byte_pool_prioritize

Classificare in ordine di priorità l'elenco di sospensioni del pool di byte

### <a name="prototype"></a>Prototipo

```c
UINT tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il thread con priorità più alta sospeso per la memoria in questo pool all'inizio dell'elenco di sospensione. Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.

### <a name="parameters"></a>Parametri 

- **pool_ptr:** puntatore a un blocco di controllo del pool di memoria.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Priorità del pool di memoria riuscita.
- TX_POOL_ERROR: (0x02) Puntatore del pool di memoria non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
TX_BYTE_POOL my_pool;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next free memory from this pool. */
status = tx_byte_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_byte_release call will wake up this thread,
   if there is enough memory to satisfy its request. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_release

## <a name="tx_byte_release"></a>tx_byte_release

Rilasciare i byte nel pool di memoria

### <a name="prototype"></a>Prototipo

```C
UINT tx_byte_release(VOID *memory_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rilascia un'area di memoria allocata in precedenza al pool associato. Se sono presenti uno o più thread sospesi in attesa di memoria da questo pool, a ogni thread sospeso viene data memoria e ripresa fino a quando la memoria non è esaurita o finché non sono presenti altri thread sospesi. Questo processo di allocazione della memoria ai thread sospesi inizia sempre con il primo thread sospeso.

> [!IMPORTANT]
> L'applicazione deve impedire l'uso dell'area di memoria dopo il rilascio.

### <a name="parameters"></a>Parametri

- **memory_ptr:** puntatore all'area di memoria allocata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Rilascio della memoria riuscito.
- TX_PTR_ERROR: (0x03) Puntatore all'area di memoria non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
unsigned char    *memory_ptr;
UINT             status;

/* Release a memory back to my_pool. Assume that the memory
   area was previously allocated from my_pool. */
status =  tx_byte_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the memory pointed to by
   memory_ptr has been returned to the pool. */
```
### <a name="see-also"></a>Vedere anche

- tx_byte_allocate
- tx_byte_pool_create
- tx_byte_pool_delete
- tx_byte_pool_info_get
- tx_byte_pool_performance_info_get
- tx_byte_pool_performance_system_info_get
- tx_byte_pool_prioritize

## <a name="tx_event_flags_create"></a>tx_event_flags_create

Creare un gruppo di flag di evento

### <a name="prototype"></a>Prototipo

```c
UINT tx_event_flags_create(TX_EVENT_FLAGS_GROUP *group_ptr,
                          CHAR *name_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio crea un gruppo di 32 flag di evento. Tutti i 32 flag di evento nel gruppo vengono inizializzati su zero. Ogni flag di evento è rappresentato da un singolo bit.

### <a name="parameters"></a>Parametri

- **group_ptr:** puntatore a un blocco di controllo del gruppo di flag di evento. 
- **name_ptr:** puntatore al nome del gruppo di flag di evento.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Creazione del gruppo di eventi completata.
- TX_GROUP_ERROR: (0x06) Puntatore del gruppo di eventi non valido. Il puntatore è NULL o il gruppo di eventi è già stato creato.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_EVENT_FLAGS_GROUP my_event_group;
UINT         status;

/* Create an event flags group. */
status = tx_event_flags_create(&my_event_group,
            "my_event_group_name");

/* If status equals TX_SUCCESS, my_event_group is ready
   for get and set services. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_delete"></a>tx_event_flags_delete

Eliminare il gruppo di flag di evento

### <a name="prototype"></a>Prototipo

```c
UINT tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il gruppo di flag di evento specificato. Tutti i thread sospesi in attesa di eventi da questo gruppo vengono ripresi e vengono TX_DELETED stato restituito.

> [!IMPORTANT]
> L'applicazione deve assicurarsi che un callback di notifica impostato per questo gruppo di flag di evento venga completato (o disabilitato) prima di eliminare il gruppo di flag di evento. Inoltre, l'applicazione deve impedire l'uso futuro di un gruppo di flag di eventi eliminati.

### <a name="parameters"></a>Parametri 

- **group_ptr:** puntatore a un gruppo di flag di eventi creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Eliminazione del gruppo di flag di evento riuscita.
- TX_GROUP_ERROR: (0x06) Puntatore di gruppo flag di evento non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT                 status;

/* Delete event flags group. Assume that the group has
   already been created with a call to
   tx_event_flags_create. */
status = tx_event_flags_delete(&my_event_flags_group);

/* If status equals TX_SUCCESS, the event flags group is
   deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_get"></a>tx_event_flags_get

Ottenere i flag di evento dal gruppo di flag di evento

### <a name="prototype"></a>Prototipo

```C
UINT tx_event_flags_get(TX_EVENT_FLAGS_GROUP *group_ptr,
                          ULONG requested_flags, UINT get_option,
                          ULONG *actual_flags_ptr, ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio recupera i flag di evento dal gruppo di flag di evento specificato. Ogni gruppo di flag di evento contiene 32 flag di evento. Ogni flag è rappresentato da un singolo bit. Questo servizio può recuperare un'ampia gamma di combinazioni di flag di eventi, come selezionato dai parametri di input.

### <a name="parameters"></a>Parametri

- **group_ptr:** puntatore a un gruppo di flag di eventi creato in precedenza.
- **requested_flags**: variabile senza segno a 32 bit che rappresenta i flag di evento richiesti.
- **get_option**: specifica se sono necessari tutti o uno dei flag di evento richiesti. Di seguito sono riportate le selezioni valide:
    - **TX_AND**: (0x02)
    - **TX_AND_CLEAR**: (0x03)
    - **TX_OR**: (0x00)
    - **TX_OR_CLEAR**: (0x01)

    La TX_AND o TX_AND_CLEAR specifica che tutti i flag di evento devono essere presenti nel gruppo. La TX_OR o TX_OR_CLEAR specifica che qualsiasi flag di evento è soddisfacente. I flag di evento che soddisfano la richiesta vengono cancellati (impostati su zero) se TX_AND_CLEAR o TX_OR_CLEAR specificati.

- **actual_flags_ptr:** puntatore alla destinazione in cui vengono inseriti i flag di evento recuperati. Si noti che i flag effettivi ottenuti possono contenere flag che non sono stati richiesti.
- **wait_option**: definisce il comportamento del servizio se i flag di evento selezionati non sono impostati. Le opzioni di attesa sono definite nel modo seguente:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (da 0x00000001 a 0xFFFFFFFE)

    La TX_NO_WAIT comporta un ritorno immediato da questo servizio indipendentemente dal fatto che l'operazione sia riuscita o meno. Questa è l'unica opzione valida se il servizio viene chiamato da un non thread; ad esempio inizializzazione, timer o ISR.

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso a tempo indeterminato fino a quando non sono disponibili i flag di evento.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa dei flag di evento.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Ottenere i flag di evento successful.
- **TX_DELETED:**(0x01) Il gruppo Flag di evento è stato eliminato durante la sospensione del thread.
- **TX_NO_EVENTS:** il servizio (0x07) non è riuscito a ottenere gli eventi specificati entro il tempo di attesa specificato.
- **TX_WAIT_ABORTED:**(0x1A) Sospensione interrotta da un altro thread, timer o ISR.
- TX_GROUP_ERROR: (0x06) Puntatore di gruppo flag di evento non valido.
- TX_PTR_ERROR: (0x03) Puntatore non valido per i flag di evento effettivi.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un thread non thread.
- TX_OPTION_ERROR: (0x08) È stata specificata l'opzione get non valida.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_EVENT_FLAGS_GROUP my_event_flags_group;
ULONG         actual_events;
UINT          status;

/* Request that event flags 0, 4, and 8 are all set. Also,
   if they are set they should be cleared. If the event
   flags are not set, this service suspends for a maximum of
   20 timer-ticks. */
status = tx_event_flags_get(&my_event_flags_group, 0x111,
                      TX_AND_CLEAR, &actual_events, 20);

/* If status equals TX_SUCCESS, actual_events contains the
   actual events obtained. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_info_get"></a>tx_event_flags_info_get

Recuperare informazioni sul gruppo di flag di evento

### <a name="prototype"></a>Prototipo

```C
UINT tx_event_flags_info_get(TX_EVENT_FLAGS_GROUP *group_ptr,
                         CHAR **name, ULONG *current_flags,
                         TX_THREAD **first_suspended,
                         ULONG *suspended_count,
                         TX_EVENT_FLAGS_GROUP **next_group);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul gruppo di flag di evento specificato.

### <a name="parameters"></a>Parametri

- **group_ptr:** puntatore a un blocco di controllo del gruppo di flag di evento.
- **name:** puntatore alla destinazione per il puntatore al nome del gruppo di flag di evento.
- **current_flags:** puntatore alla destinazione per i flag del set corrente nel gruppo di flag di evento.
- **first_suspended:** puntatore alla destinazione per il puntatore al thread che si trova per primo nell'elenco di sospensione di questo gruppo di flag di evento.
- **suspended_count:** puntatore alla destinazione per il numero di thread attualmente sospesi in questo gruppo di flag di evento.
- **next_group:** puntatore alla destinazione per il puntatore del gruppo di flag di evento creato successivo.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Recupero delle informazioni sul gruppo di eventi riuscito.
- TX_GROUP_ERROR: (0x06) Puntatore al gruppo di eventi non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
TX_EVENT_FLAGS_GROUPmy_event_group;
CHAR          *name;
ULONG         current_flags;
TX_THREAD     *first_suspended;
ULONG         suspended_count;
TX_EVENT_FLAGS_GROUP*next_group;
UINT          status;

/* Retrieve information about the previously created
   event flags group "my_event_group." */
status =  tx_event_flags_info_get(&my_event_group, &name,
             &current_flags,
             &first_suspended, &suspended_count,
             &next_group);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_performance-info_get"></a>tx_event_flags_performance info_get

Ottenere informazioni sulle prestazioni del gruppo di flag di eventi

### <a name="prototype"></a>Prototipo

```C
UINT tx_event_flags_performance_info_get(TX_EVENT_FLAGS_GROUP
                        *group_ptr, ULONG *sets, ULONG *gets,
                        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al gruppo di flag di eventi specificato.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX SMP devono essere compilate **con TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **group_ptr:** puntatore al gruppo di flag di eventi creato in precedenza.
- **sets:** puntatore alla destinazione per il numero di flag di evento che impostano le richieste eseguite su questo gruppo.
- **gets:** puntatore alla destinazione per il numero di richieste get di flag di evento eseguite su questo gruppo.
- **suspensions:** puntatore alla destinazione per il numero di flag di evento del thread che ottengono le sospensioni in questo gruppo.
- **timeouts:** puntatore alla destinazione per il numero di flag di evento che ottengono timeout di sospensione in questo gruppo.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere le prestazioni del gruppo di flag di evento riuscito.
- **TX_PTR_ERROR:**(0x03) Puntatore di gruppo flag di evento non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_EVENT_FLAGS_GROUPmy_event_flag_group;
ULONG           sets;
ULONG           gets;
ULONG           suspensions;
ULONG           timeouts;

/* Retrieve performance information on the previously created event
   flag group. */
status =  tx_event_flags_performance_info_get(&my_event_flag_group,
   &sets, &gets, &suspensions,
   &timeouts);

/* If status is TX_SUCCESS the performance information was successfully
   retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_performance_system_info_get"></a>tx_event_flags_performance_system_info_get

Recuperare informazioni sul sistema di prestazioni

### <a name="prototype"></a>Prototipo

```c
UINT  tx_event_flags_performance_system_info_get(ULONG *sets,
        ULONG *gets,ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni di tutti i gruppi di flag di eventi nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX SMP devono essere compilate **con TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **sets:** puntatore alla destinazione per il numero totale di flag di evento che impostano le richieste eseguite su tutti i gruppi.
- **gets:** puntatore alla destinazione per il numero totale di richieste get di flag di evento eseguite su tutti i gruppi.
- **suspensions:** puntatore alla destinazione per il numero totale di flag di evento del thread che ottengono sospensioni in tutti i gruppi.
- **timeouts:** puntatore alla destinazione per il numero totale di flag di eventi che ottengono timeout di sospensione in tutti i gruppi.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Riuscito flag di evento prestazioni del sistema.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```c
ULONG         sets;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all previously created event
   flag groups. */
status = tx_event_flags_performance_system_info_get(&sets, &gets,
                &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_set
- tx_event_flags_set_notify

## <a name="tx_event_flags_set"></a>tx_event_flags_set

Impostare i flag di evento in un gruppo di flag di evento

### <a name="prototype"></a>Prototipo

```C
UINT tx_event_flags_set(TX_EVENT_FLAGS_GROUP *group_ptr,
                          ULONG  flags_to_set,UINT set_option);
```
### <a name="description"></a>Descrizione

Questo servizio imposta o cancella i flag di evento in un gruppo di flag di eventi, a seconda dell'opzione set specificata. Tutti i thread sospesi la cui richiesta di flag di evento è ora soddisfatta vengono ripresi.

### <a name="parameters"></a>Parametri

- **group_ptr:** puntatore al blocco di controllo del gruppo di flag di eventi creato in precedenza.
- **flags_to_set**: specifica i flag di evento da impostare o cancellare in base all'opzione impostata selezionata.
- **set_option**: specifica se i flag di evento specificati sono ANDed o ORed nei flag di evento correnti del gruppo. Di seguito sono riportate le selezioni valide:
    - **TX_AND**: (0x02)
    - **TX_OR**: (0x00) La selezione TX_AND specifica che i flag di evento specificati sono **E** nei flag di evento correnti nel gruppo. Questa opzione viene spesso usata per cancellare i flag di evento in un gruppo. In caso contrario, TX_OR viene specificato , i flag di evento specificati sono **OR** ed con l'evento corrente nel gruppo.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Flag di evento Successful impostati.
- TX_GROUP_ERROR: (0x06) Puntatore non valido al gruppo di flag di evento.
- TX_OPTION_ERROR: (0x08) È stata specificata un'opzione set non valida.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_EVENT_FLAGS_GROUPmy_event_flags_group;
UINT         status;

/* Set event flags 0, 4, and 8. */
status =  tx_event_flags_set(&my_event_flags_group,
                           0x111, TX_OR);

/* If status equals TX_SUCCESS, the event flags have been
   set and any suspended thread whose request was satisfied
   has been resumed. */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set_notify

## <a name="tx_event_flags_set_notify"></a>tx_event_flags_set_notify

Notificare all'applicazione quando sono impostati i flag di evento

### <a name="prototype"></a>Prototipo

```C
UINT tx_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr,
       VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback di notifica che viene chiamata ogni volta che uno o più flag di evento vengono impostati nel gruppo di flag di evento specificato. L'elaborazione del callback di notifica è definita dall'applicazione.

> [!NOTE]
> I flag di evento dell'applicazione impostano il callback di notifica non è autorizzato a chiamare alcuna API SMP ThreadX con un'opzione di sospensione.

### <a name="parameters"></a>Parametri 
- **group_ptr:** puntatore al gruppo di flag di evento creato in precedenza.
- **events_set_notify:** puntatore alla funzione di notifica impostata dei flag di evento dell'applicazione. Se questo valore è TX_NULL, la notifica è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Registrazione riuscita della notifica di impostazione dei flag di evento.
- TX_GROUP_ERROR: (0x06) Puntatore di gruppo flag di evento non valido.
- TX_FEATURE_NOT_ENABLED: (0xFF) Il sistema è stato compilato con funzionalità di notifica disabilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_EVENT_FLAGS_GROUPmy_group;

/* Register the "my_event_flags_set_notify" function for monitoring
   event flags set in the event flags group "my_group." */
status =  tx_event_flags_set_notify(&my_group,
                my_event_flags_set_notify);

/* If status is TX_SUCCESS the event flags set notification function
   was successfully registered. */

void my_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr)
   /* One or more event flags was set in this group! */
```
### <a name="see-also"></a>Vedere anche

- tx_event_flags_create
- tx_event_flags_delete
- tx_event_flags_get
- tx_event_flags_info_get
- tx_event_flags_performance_info_get
- tx_event_flags_performance_system_info_get
- tx_event_flags_set

## <a name="tx_interrupt_control"></a>tx_interrupt_control

Abilitare e disabilitare gli interrupt

### <a name="prototype"></a>Prototipo

```C
UINT tx_interrupt_control(UINT new_posture);
```
### <a name="description"></a>Descrizione

Questo servizio abilita o disabilita gli interrupt come specificato dal parametro di input **new_posture**.

> [!IMPORTANT]
> Se questo servizio viene chiamato da un thread dell'applicazione, la posizione di interruzione rimane parte del contesto del thread. Ad esempio, se il thread chiama questa routine per disabilitare gli interrupt e quindi sospende, quando viene ripreso, gli interrupt vengono nuovamente disabilitati.

> [!WARNING]
> Questo servizio non deve essere usato per abilitare gli interrupt durante l'inizializzazione. Questa operazione potrebbe causare risultati imprevedibili.

### <a name="parameters"></a>Parametri

- **new_posture:** questo parametro specifica se gli interrupt sono disabilitati o abilitati. I valori validi **includono TX_INT_DISABLE e TX_INT_ENABLE.** I valori effettivi per questi parametri sono specifici della porta. Inoltre, alcune architetture di elaborazione potrebbero supportare posture di disabilitazione di interrupt aggiuntive. Per altre **_informazioni,readme_threadx.txt_** informazioni dettagliate sul disco di distribuzione.

### <a name="return-values"></a>Valori restituiti

- postura precedente: questo servizio restituisce la posizione di interruzione precedente al chiamante. In questo modo, gli utenti del servizio possono ripristinare la posizione precedente dopo che gli interrupt sono stati disabilitati.

### <a name="allowed-from"></a>Consentito da

Thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
UINT my_old_posture;

/* Lockout interrupts */
my_old_posture =  tx_interrupt_control(TX_INT_DISABLE);

/* Perform critical operations that need interrupts
   locked-out.... */

/* Restore previous interrupt lockout posture. */
tx_interrupt_control(my_old_posture);
```
### <a name="see-also"></a>Vedere anche

Nessuno

## <a name="tx_mutex_create"></a>tx_mutex_create

Creare mutex di esclusione reciproca

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_create(TX_MUTEX *mutex_ptr,
                          CHAR *name_ptr, UINT priority_inherit);
```
### <a name="description"></a>Descrizione
    
Questo servizio crea un mutex per l'esclusione reciproca tra thread per la protezione delle risorse.

### <a name="parameters"></a>Parametri

- **mutex_ptr:** puntatore a un blocco di controllo mutex.
- **name_ptr:** puntatore al nome del mutex.
- **priority_inherit**: specifica se questo mutex supporta o meno l'ereditarietà delle priorità. Se questo valore è TX_INHERIT, l'ereditarietà della priorità è supportata. Tuttavia, se TX_NO_INHERIT, l'ereditarietà della priorità non è supportata da questo mutex.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Creazione del mutex completata.
- TX_MUTEX_ERROR: (0x1C) Puntatore mutex non valido. Il puntatore è NULL o il mutex è già stato creato.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.
- TX_INHERIT_ERROR: (0x1F) Parametro inherit di priorità non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Create a mutex to provide protection over a
   common resource. */
status =  tx_mutex_create(&my_mutex,"my_mutex_name",
                           TX_NO_INHERIT);

/* If status equals TX_SUCCESS, my_mutex is ready for
   use. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_delete"></a>tx_mutex_delete

Eliminare il mutex di esclusione reciproca

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_delete(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il mutex specificato. Tutti i thread sospesi in attesa del mutex vengono ripresi e vengono TX_DELETED stato restituito.

> [!IMPORTANT]
> È responsabilità dell'applicazione impedire l'uso di un mutex eliminato.

### <a name="parameters"></a>Parametri

- **mutex_ptr:** puntatore a un mutex creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Eliminazione del mutex completata.
- TX_MUTEX_ERROR: (0x1C) Puntatore mutex non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Delete a mutex. Assume that the mutex
   has already been created. */
status =  tx_mutex_delete(&my_mutex);

/* If status equals TX_SUCCESS, the mutex is
   deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_get"></a>tx_mutex_get

Ottenere la proprietà del mutex

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_get(TX_MUTEX *mutex_ptr, ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio tenta di ottenere la proprietà esclusiva del mutex specificato. Se il thread chiamante è già proprietario del mutex, viene incrementato un contatore interno e viene restituito uno stato di esito positivo.

Se il mutex è di proprietà di un altro thread e questo thread ha una priorità più alta ed è stata specificata l'ereditarietà della priorità al momento della creazione del mutex, la priorità del thread con priorità inferiore verrà temporaneamente elevata a quella del thread chiamante.

> [!IMPORTANT]
> La priorità del thread con priorità inferiore che possiede un mutex con prioritàinheritance non deve mai essere modificata da un thread esterno durante la proprietà del mutex.

### <a name="parameters"></a>Parametri

- **mutex_ptr:** puntatore a un mutex creato in precedenza.
- **wait_option**: definisce il comportamento del servizio se il mutex è già di proprietà di un altro thread. Le opzioni di attesa sono definite come segue:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (0x00000001 tramite 0xFFFFFFFE)

    La TX_NO_WAIT determina un ritorno immediato da questo servizio indipendentemente dal fatto che sia stato eseguito correttamente o meno. *Questa è l'unica opzione valida se il servizio viene chiamato dall'inizializzazione.*

    Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso per un periodo illimitato fino a quando il mutex non è disponibile.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa del mutex.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Operazione get mutex riuscita.
- **TX_DELETED:** il mutex (0x01) è stato eliminato durante la sospensione del thread.
- **TX_NOT_AVAILABLE:** il servizio (0x1D) non è stato in grado di ottenere la proprietà del mutex entro il tempo di attesa specificato.
- **TX_WAIT_ABORTED:** la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.
- TX_MUTEX_ERROR: (0x1C) Puntatore mutex non valido.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa TX_NO_WAIT in una chiamata da un nonthread.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread e timer

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Obtain exclusive ownership of the mutex "my_mutex".
   If the mutex "my_mutex" is not available, suspend until it
   becomes available. */
status =  tx_mutex_get(&my_mutex, TX_WAIT_FOREVER);
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_info_get"></a>tx_mutex_info_get

Recuperare informazioni sul mutex

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_info_get(TX_MUTEX *mutex_ptr, CHAR **name,
                          ULONG *count, TX_THREAD **owner,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count, TX_MUTEX **next_mutex);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni dal mutex specificato.

### <a name="parameters"></a>Parametri

- **mutex_ptr:** puntatore al blocco di controllo mutex.
- **name:** puntatore alla destinazione per il puntatore al nome del mutex.
- **count:** puntatore alla destinazione per il numero di proprietà del mutex.
- **owner:** puntatore alla destinazione per il puntatore del thread proprietario.
- **first_suspended**: puntatore alla destinazione per il puntatore al thread che si trova per primo nell'elenco di sospensione di questo mutex.
- **suspended_count:** puntatore alla destinazione per il numero di thread attualmente sospesi in questo mutex.
- **next_mutex:** puntatore alla destinazione per il puntatore del mutex creato successivo.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Recupero delle informazioni mutex riuscito.
- TX_MUTEX_ERROR: (0x1C) Puntatore mutex non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_MUTEX     my_mutex;
CHAR         *name;
ULONG        count;
TX_THREAD    *owner;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_MUTEX     *next_mutex;
UINT         status;

/* Retrieve information about the previously created
   mutex "my_mutex." */
status =  tx_mutex_info_get(&my_mutex, &name,
                          &count, &owner,
                          &first_suspended, &suspended_count,
                          &next_mutex);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_performance_info_get"></a>tx_mutex_performance_info_get

Ottenere informazioni sulle prestazioni del mutex

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_performance_info_get(TX_MUTEX *mutex_ptr, ULONG *puts,
       ULONG *gets, ULONG *suspensions, ULONG *timeouts,
       ULONG *inversions, ULONG *inheritances);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al mutex specificato.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_MUTEX_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **mutex_ptr:** puntatore al mutex creato in precedenza.
- **puts:** puntatore alla destinazione per il numero di richieste put eseguite su questo mutex.
- **gets:** puntatore alla destinazione per il numero di richieste get eseguite su questo mutex.
- **suspensions:** puntatore alla destinazione per il numero di sospensioni get mutex di thread in questo mutex.
- **timeouts:** puntatore alla destinazione per il numero di timeout di sospensione get mutex in questo mutex.
- **inversions:** puntatore alla destinazione per il numero di inversioni di priorità dei thread in questo mutex.
- **inheritances:** puntatore alla destinazione per il numero di operazioni di ereditarietà della priorità dei thread in questo mutex.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere prestazioni mutex riuscite. 
- **TX_PTR_ERROR:**(0x03) Puntatore mutex non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_MUTEX     my_mutex;
ULONG        puts;
ULONG        gets;
ULONG        suspensions;
ULONG        timeouts;
ULONG        inversions;
ULONG        inheritances;

/* Retrieve performance information on the previously created
   mutex. */
status =  tx_mutex_performance_info_get(&my_mutex_ptr, &puts, &gets,
                &suspensions, &timeouts, &inversions,
                &inheritances);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_performance_system_info_get"></a>tx_mutex_performance_system_info_get

Ottenere informazioni sulle prestazioni del sistema mutex

### <a name="prototype"></a>Prototipo

```C
UINT  tx_mutex_performance_system_info_get(ULONG *puts, ULONG *gets,
        ULONG *suspensions, ULONG *timeouts,
        ULONG *inversions, ULONG *inheritances);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni su tutti i mutex nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_MUTEX_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **puts:** puntatore alla destinazione per il numero totale di richieste put eseguite in tutti i mutex.
- **gets**: puntatore alla destinazione per il numero totale di richieste get eseguite su tutti i mutex.
- **suspensions:** puntatore alla destinazione per il numero totale di sospensioni di mutex di thread in tutti i mutex.
- **timeouts:** puntatore alla destinazione per il numero totale di timeout di sospensione di mutex get su tutti i mutex.
- **inversions**: puntatore alla destinazione per il numero totale di inversioni di priorità dei thread in tutti i mutex.
- **inheritances:** puntatore alla destinazione per il numero totale di operazioni di ereditarietà della priorità dei thread in tutti i mutex.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere prestazioni del sistema mutex riuscite.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
ULONG         puts;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;
ULONG         inversions;
ULONG         inheritances;

/* Retrieve performance information on all previously created
   mutexes. */
status = tx_mutex_performance_system_info_get(&puts, &gets,
                &suspensions, &timeouts,
                &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_prioritize
- tx_mutex_put

## <a name="tx_mutex_prioritize"></a>tx_mutex_prioritize

Assegnare la priorità all'elenco di sospensioni mutex

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il thread con priorità più alta sospeso per la proprietà del mutex all'inizio dell'elenco di sospensione. Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.

### <a name="parameters"></a>Parametri 

- **mutex_ptr:** puntatore al mutex creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Priorità del mutex riuscito.
- TX_MUTEX_ERROR: (0x1C) Puntatore mutex non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Ensure that the highest priority thread will receive
   ownership of the mutex when it becomes available. */
status = tx_mutex_prioritize(&my_mutex);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_mutex_put call that releases ownership of the
   mutex will give ownership to this thread and wake it
   up. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_put

## <a name="tx_mutex_put"></a>tx_mutex_put

Rilasciare la proprietà del mutex

### <a name="prototype"></a>Prototipo

```C
UINT tx_mutex_put(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio decrementa il numero di proprietà del mutex specificato. Se il numero di proprietà è zero, il mutex viene reso disponibile.

> [!IMPORTANT]
> Se è stata selezionata l'ereditarietà della priorità durante la creazione del mutex, la priorità del thread di rilascio verrà ripristinata alla priorità che aveva quando ha ottenuto originariamente la proprietà del mutex. Eventuali altre modifiche di priorità apportate al thread di rilascio durante la proprietà del mutex possono essere annullate.

### <a name="parameters"></a>Parametri

- **mutex_ptr:** puntatore al mutex creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Rilascio mutex riuscito.
- **TX_NOT_OWNED:**(0x1E) Mutex non è di proprietà del chiamante.
- TX_MUTEX_ERROR: (0x1C) Puntatore non valido al mutex.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread e timer

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_MUTEX         my_mutex;
UINT             status;
/* Release ownership of "my_mutex." */
status =  tx_mutex_put(&my_mutex);

/* If status equals TX_SUCCESS, the mutex ownership
   count has been decremented and if zero, released. */
```
### <a name="see-also"></a>Vedere anche

- tx_mutex_create
- tx_mutex_delete
- tx_mutex_get
- tx_mutex_info_get
- tx_mutex_performance_info_get
- tx_mutex_performance_system_info_get
- tx_mutex_prioritize

## <a name="tx_queue_create"></a>tx_queue_create

Creare una coda di messaggi

### <a name="prototype"></a>Prototipo

```c
UINT tx_queue_create(TX_QUEUE *queue_ptr, CHAR *name_ptr,
                          UINT message_size,
                          VOID *queue_start, ULONG queue_size);
```
### <a name="description"></a>Descrizione

Questo servizio crea una coda di messaggi che viene in genere usata per la comunicazione interthreading. Il numero totale di messaggi viene calcolato in base alla dimensione del messaggio specificata e al numero totale di byte nella coda.

> [!IMPORTANT]
> Se il numero totale di byte specificati nell'area di memoria della coda non è divisibile in modo uniforme in base alla dimensione del messaggio specificata, i byte rimanenti nell'area di memoria non vengono utilizzati.

### <a name="parameters"></a>Parametri

- **queue_ptr:** puntatore a un blocco di controllo della coda di messaggi.
- **name_ptr:** puntatore al nome della coda di messaggi.
- **message_size**: specifica le dimensioni di ogni messaggio nella coda. Le dimensioni dei messaggi vanno da 1 parola a 32 bit a 16 parole a 32 bit. Le opzioni valide per le dimensioni dei messaggi sono valori numerici compresi tra 1 e 16 inclusi.
- **queue_start**: indirizzo iniziale della coda di messaggi. L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.
- **queue_size**: numero totale di byte disponibili per la coda di messaggi.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Creazione coda messaggi riuscita.
- TX_QUEUE_ERROR: (0x09) Puntatore alla coda di messaggi non valido. Il puntatore è NULL o la coda è già stata creata.
- TX_PTR_ERROR: (0x03) Indirizzo iniziale della coda di messaggi non valido.
- TX_SIZE_ERROR: (0x05) Dimensioni della coda di messaggi non valide.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
UINT         status;

/* Create a message queue whose total size is 2000 bytes
   starting at address 0x300000. Each message in this
   queue is defined to be 4 32-bit words long. */
status = tx_queue_create(&my_queue, "my_queue_name",
            4, (VOID *) 0x300000, 2000);

/* If status equals TX_SUCCESS, my_queue contains room
   for storing 125 messages (2000 bytes/ 16 bytes per
   message). */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_delete"></a>tx_queue_delete

Eliminare una coda di messaggi

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_delete(TX_QUEUE *queue_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina la coda di messaggi specificata. Tutti i thread sospesi in attesa di un messaggio da questa coda vengono ripresi e vengono TX_DELETED stato restituito.

> [!IMPORTANT]
> L'applicazione deve assicurarsi che qualsiasi callback di notifica di invio per questa coda venga completato (o disabilitato) prima di eliminare la coda. Inoltre, l'applicazione deve impedire qualsiasi uso futuro di una coda eliminata.

*È anche responsabilità dell'applicazione gestire l'area di memoria associata alla coda, disponibile al termine del servizio.*

### <a name="parameters"></a>Parametri 

- **queue_ptr:** puntatore a una coda di messaggi creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Eliminazione della coda di messaggi completata.
- TX_QUEUE_ERROR: (0x09) Puntatore alla coda di messaggi non valido.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
UINT         status;

/* Delete entire message queue. Assume that the queue
   has already been created with a call to
   tx_queue_create. */
status = tx_queue_delete(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
   deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_flush"></a>tx_queue_flush

Messaggi vuoti nella coda di messaggi

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_flush(TX_QUEUE *queue_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina tutti i messaggi archiviati nella coda di messaggi specificata. Se la coda è piena, i messaggi di tutti i thread sospesi vengono eliminati. Ogni thread sospeso viene quindi ripreso con uno stato restituito che indica che l'invio del messaggio è riuscito. Se la coda è vuota, questo servizio non esegue alcuna operazione.

### <a name="parameters"></a>Parametri 

- **queue_ptr:** puntatore a una coda di messaggi creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Scaricamento coda messaggi riuscito.
- TX_QUEUE_ERROR: (0x09) Puntatore alla coda di messaggi non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```c
TX_QUEUE     my_queue;
UINT         status;

/* Flush out all pending messages in the specified message
   queue. Assume that the queue has already been created
   with a call to tx_queue_create. */
status =  tx_queue_flush(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
    empty. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_front_send"></a>tx_queue_front_send

Inviare un messaggio all'inizio della coda

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_front_send(TX_QUEUE *queue_ptr,
                           VOID *source_ptr, ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio invia un messaggio alla posizione anteriore della coda di messaggi specificata. Il messaggio viene **copiato all'inizio** della coda dall'area di memoria specificata dal puntatore di origine.

### <a name="parameters"></a>Parametri

- **queue_ptr:** puntatore a un blocco di controllo della coda di messaggi.
- **source_ptr**: puntatore al messaggio.
- **wait_option**: definisce il comportamento del servizio se la coda di messaggi è piena. Le opzioni di attesa sono definite come segue:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (0x00000001 tramite 0xFFFFFFFE)

    La TX_NO_WAIT determina un ritorno immediato da questo servizio indipendentemente dal fatto che sia stato eseguito correttamente o meno. *Questa è l'unica opzione valida se il servizio viene chiamato da un non thread; ad esempio inizializzazione, timer o ISR.*

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando non c'è spazio nella coda.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa dello spazio nella coda.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Invio del messaggio riuscito.
- **TX_DELETED:**(0x01) La coda di messaggi è stata eliminata mentre il thread è stato sospeso.
- **TX_QUEUE_FULL:** il servizio (0x0B) non è riuscito a inviare il messaggio perché la coda era piena per la durata del tempo di attesa specificato.
- **TX_WAIT_ABORTED:** la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.
- TX_QUEUE_ERROR: (0x09) Puntatore alla coda di messaggi non valido.
- TX_PTR_ERROR: (0x03) Puntatore di origine non valido per il messaggio.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa TX_NO_WAIT in una chiamata da un nonthread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
UINT         status;
ULONG        my_message[4];

/* Send a message to the front of "my_queue." Return
   immediately, regardless of success. This wait
   option is used for calls from initialization, timers,
   and ISRs. */
status = tx_queue_front_send(&my_queue, my_message,
            TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is at the front
   of the specified queue. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_info_get"></a>tx_queue_info_get

Recuperare informazioni sulla coda

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_info_get(TX_QUEUE *queue_ptr, CHAR **name,
        ULONG *enqueued, ULONG *available_storage
        TX_THREAD **first_suspended, ULONG *suspended_count,
        TX_QUEUE **next_queue);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulla coda di messaggi specificata.

### <a name="parameters"></a>Parametri

- **queue_ptr:** puntatore a una coda di messaggi creata in precedenza.
- **name:** puntatore alla destinazione per il puntatore al nome della coda.
- **enqueued:** puntatore alla destinazione per il numero di messaggi attualmente presenti nella coda.
- **available_storage:** puntatore alla destinazione per il numero di messaggi per cui la coda dispone attualmente di spazio.
- **first_suspended**: puntatore alla destinazione per il puntatore al thread che si trova per primo nell'elenco di sospensione di questa coda.
- **suspended_count:** puntatore alla destinazione per il numero di thread attualmente sospesi in questa coda.
- **next_queue**: puntatore alla destinazione per il puntatore della coda creata successiva.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere informazioni sulla coda con esito positivo.
- TX_QUEUE_ERROR: (0x09) Puntatore alla coda di messaggi non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
CHAR         *name;
ULONG        enqueued;
ULONG        available_storage;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_QUEUE     *next_queue;
UINT         status;

/* Retrieve information about the previously created
   message queue "my_queue." */
status = tx_queue_info_get(&my_queue, &name,
            &enqueued, &available_storage,
            &first_suspended, &suspended_count,
            &next_queue);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_performance_info_get"></a>tx_queue_performance_info_get

Ottenere informazioni sulle prestazioni della coda

### <a name="prototype"></a>Prototipo

```C
UINT  tx_queue_performance_info_get(TX_QUEUE *queue_ptr,
        ULONG *messages_sent, ULONG *messages_received,
        ULONG *empty_suspensions, ULONG *full_suspensions,
        ULONG *full_errors, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative alla coda specificata.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_QUEUE_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **queue_ptr:** puntatore alla coda creata in precedenza.
- **messages_sent:** puntatore alla destinazione per il numero di richieste di invio eseguite su questa coda.
- **messages_received**: puntatore alla destinazione per il numero di richieste di ricezione eseguite su questa coda.
- **empty_suspensions:** puntatore alla destinazione per il numero di sospensioni vuote della coda in questa coda.
- **full_suspensions:** puntatore alla destinazione per il numero di sospensioni complete della coda in questa coda.
- **full_errors**: puntatore alla destinazione per il numero di errori completi della coda in questa coda.
- **timeouts:** puntatore alla destinazione per il numero di timeout di sospensione del thread in questa coda.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Prestazioni coda riuscite.
- **TX_PTR_ERROR:**(0x03) Puntatore a coda non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
ULONG        messages_sent;
ULONG        messages_received;
ULONG        empty_suspensions;
ULONG        full_suspensions;
ULONG        full_errors;
ULONG        timeouts;

/* Retrieve performance information on the previously created
   queue. */
status = tx_queue_performance_info_get(&my_queue, &messages_sent,
            &messages_received, &empty_suspensions,
            &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_performance_system_info_get"></a>tx_queue_performance_system_info_get

Ottenere informazioni sulle prestazioni del sistema di accodamento

### <a name="prototype"></a>Prototipo

```C
UINT  tx_queue_performance_system_info_get(ULONG *messages_sent,
        ULONG *messages_received, ULONG *empty_suspensions,
        ULONG *full_suspensions, ULONG *full_errors,
        ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative a tutte le code nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_QUEUE_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **messages_sent:** puntatore alla destinazione per il numero totale di richieste di invio eseguite su tutte le code.
- **messages_received:** puntatore alla destinazione per il numero totale di richieste di ricezione eseguite su tutte le code.
- **empty_suspensions:** puntatore alla destinazione per il numero totale di sospensioni vuote della coda in tutte le code.
- **full_suspensions:** puntatore alla destinazione per il numero totale di sospensioni complete della coda in tutte le code.
- **full_errors:** puntatore alla destinazione per il numero totale di errori completi della coda in tutte le code.
- **timeouts**: puntatore alla destinazione per il numero totale di timeout di sospensione dei thread in tutte le code.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere prestazioni del sistema di accodamento riuscite.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```c
ULONG         messages_sent;
ULONG         messages_received;
ULONG         empty_suspensions;
ULONG         full_suspensions;
ULONG         full_errors;
ULONG         timeouts;

/* Retrieve performance information on all previously created
   queues. */
status = tx_queue_performance_system_info_get(&messages_sent,
            &messages_received, &empty_suspensions,
            &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_prioritize"></a>tx_queue_prioritize

Classificare l'elenco di sospensioni code in ordine di priorità

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio posiziona il thread con priorità più alta sospeso per un messaggio (o per inserire un messaggio) in questa coda all'inizio dell'elenco di sospensione. Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.

### <a name="parameters"></a>Parametri 

- **queue_ptr:** puntatore a una coda di messaggi creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Priorità coda riuscita.
- TX_QUEUE_ERROR: (0x09) Puntatore della coda di messaggi non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next message placed on this queue. */
status = tx_queue_prioritize(&my_queue);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_queue_send or tx_queue_front_send call made
   to this queue will wake up this thread. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_receive
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_receive"></a>tx_queue_receive

Ottenere un messaggio dalla coda di messaggi

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_receive(TX_QUEUE *queue_ptr,
                          VOID *destination_ptr, ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio recupera un messaggio dalla coda di messaggi specificata. Il messaggio recuperato viene **copiato** dalla coda nell'area di memoria specificata dal puntatore di destinazione. Il messaggio viene quindi rimosso dalla coda.

> [!WARNING]
> L'area di memoria di destinazione specificata deve essere sufficientemente grande da contenere il messaggio. Ad esempio, la destinazione del messaggio a cui punta **destination_ptr** deve essere grande almeno quanto la dimensione del messaggio per questa coda. In caso contrario, se la destinazione non è sufficientemente grande, si verifica un danneggiamento della memoria nell'area di memoria seguente.

### <a name="parameters"></a>Parametri

- **queue_ptr:** puntatore a una coda di messaggi creata in precedenza.
- **destination_ptr**: posizione in cui copiare il messaggio.
- **wait_option**: definisce il comportamento del servizio se la coda di messaggi è vuota. Le opzioni di attesa sono definite nel modo seguente:
    - **TX_NO_WAIT**: (0x00000000) 
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) 
    - valore di timeout: (da 0x00000001 a 0xFFFFFFFE)

    La TX_NO_WAIT comporta un ritorno immediato da questo servizio indipendentemente dal fatto che l'operazione sia riuscita o meno. Questa è l'unica opzione valida se il servizio viene chiamato da un non thread; ad esempio inizializzazione, timer o ISR.

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso a tempo indeterminato fino a quando non è disponibile un messaggio.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa di un messaggio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Recupero del messaggio riuscito.
- **TX_DELETED**: (0x01) La coda di messaggi è stata eliminata durante la sospensione del thread.
- **TX_QUEUE_EMPTY:** il servizio (0x0A) non è stato in grado di recuperare un messaggio perché la coda era vuota per la durata del tempo di attesa specificato.
- **TX_WAIT_ABORTED:**(0x1A) Sospensione interrotta da un altro thread, timer o ISR.
- TX_QUEUE_ERROR: (0x09) Puntatore della coda di messaggi non valido.
- TX_PTR_ERROR: (0x03) Puntatore di destinazione non valido per il messaggio.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un thread non thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_QUEUE     my_queue;
UINT         status;
ULONG my_message[4];

/* Retrieve a message from "my_queue." If the queue is
   empty, suspend until a message is present. Note that
   this suspension is only possible from application
   threads. */
status =  tx_queue_receive(&my_queue, my_message,
                          TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the message is in
   "my_message." */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_send
- tx_queue_send_notify

## <a name="tx_queue_send"></a>tx_queue_send

Inviare un messaggio alla coda di messaggi

### <a name="prototype"></a>Prototipo

```C
UINT tx_queue_send(TX_QUEUE *queue_ptr,
                          VOID *source_ptr, ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio invia un messaggio alla coda di messaggi specificata. Il messaggio inviato viene **copiato** nella coda dall'area di memoria specificata dal puntatore di origine.

### <a name="parameters"></a>Parametri

- **queue_ptr:** puntatore a una coda di messaggi creata in precedenza.
- **source_ptr**: puntatore al messaggio.
- **wait_option**: definisce il comportamento del servizio se la coda di messaggi è piena. Le opzioni di attesa sono definite come segue:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (0x00000001 tramite 0xFFFFFFFE)

    La TX_NO_WAIT determina un ritorno immediato da questo servizio indipendentemente dal fatto che sia stato eseguito correttamente o meno. *Questa è l'unica opzione valida se il servizio viene chiamato da un non thread; ad esempio inizializzazione, timer o ISR.*

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando non c'è spazio nella coda.

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa dello spazio nella coda.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Invio del messaggio riuscito.
- **TX_DELETED:**(0x01) La coda di messaggi è stata eliminata mentre il thread è stato sospeso.
- **TX_QUEUE_FULL:** il servizio (0x0B) non è riuscito a inviare il messaggio perché la coda era piena per la durata del tempo di attesa specificato.
- **TX_WAIT_ABORTED:** la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.
- TX_QUEUE_ERROR: (0x09) Puntatore alla coda di messaggi non valido.
- TX_PTR_ERROR: (0x03) Puntatore di origine non valido per il messaggio.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa TX_NO_WAIT in una chiamata da un nonthread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to "my_queue." Return immediately,
   regardless of success. This wait option is used for
   calls from initialization, timers, and ISRs. */
status =  tx_queue_send(&my_queue, my_message, TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is in the
   queue. */
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send_notify

## <a name="tx_queue_send_notify"></a>tx_queue_send_notify 

Notificare all'applicazione quando il messaggio viene inviato alla coda

### <a name="prototype"></a>Prototipo

```C
UINT  tx_queue_send_notify(TX_QUEUE *queue_ptr,
        VOID (*queue_send_notify)(TX_QUEUE *));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback di notifica che viene chiamata ogni volta che un messaggio viene inviato alla coda specificata. L'elaborazione del callback di notifica è definita dall'applicazione.

> [!NOTE]
> Il callback di notifica dell'invio in coda dell'applicazione non può chiamare alcuna API SMP ThreadX con un'opzione di sospensione.

### <a name="parameters"></a>Parametri 

- **queue_ptr:** puntatore alla coda creata in precedenza.
- **queue_send_notify:** puntatore alla funzione di notifica di invio in coda dell'applicazione. Se questo valore è TX_NULL, la notifica è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Registrazione riuscita della notifica di invio della coda.
- TX_QUEUE_ERROR: (0x09) Puntatore a coda non valido.
- TX_FEATURE_NOT_ENABLED: (0xFF) Il sistema è stato compilato con funzionalità di notifica disabilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_QUEUE         my_queue;

/* Register the "my_queue_send_notify" function for monitoring
   messages sent to the queue "my_queue." */
status = tx_queue_send_notify(&my_queue, my_queue_send_notify);

/* If status is TX_SUCCESS the queue send notification function was
   successfully registered. */
void my_queue_send_notify(TX_QUEUE *queue_ptr)
{
/* A message was just sent to this queue! */
}
```
### <a name="see-also"></a>Vedere anche

- tx_queue_create
- tx_queue_delete
- tx_queue_flush
- tx_queue_front_send
- tx_queue_info_get
- tx_queue_performance_info_get
- tx_queue_performance_system_info_get
- tx_queue_prioritize
- tx_queue_receive
- tx_queue_send

## <a name="tx_semaphore_ceiling_put"></a>tx_semaphore_ceiling_put 

Inserire un'istanza nel semaforo di conteggio con il limite massimo

### <a name="prototype"></a>Prototipo

```C
UINT  tx_semaphore_ceiling_put(TX_SEMAPHORE *semaphore_ptr,
        ULONG ceiling);
```
### <a name="description"></a>Descrizione

Questo servizio inserisce un'istanza nel semaforo di conteggio specificato, che in realtà incrementa di uno il semaforo di conteggio. Se il valore corrente del semaforo di conteggio è maggiore o uguale al limite massimo specificato, l'istanza non verrà inserita e verrà restituito un TX_CEILING_EXCEEDED errore.

### <a name="parameters"></a>Parametri 

- **semaphore_ptr:** puntatore al semaforo creato in precedenza.
- **ceiling:** limite massimo consentito per il semaforo (i valori validi sono da 1 a 0xFFFFFFFF).

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Operazione completata.
- **TX_CEILING_EXCEEDED**: (0x21) La richiesta Put supera il limite massimo.
- TX_INVALID_CEILING: (0x22) È stato specificato un valore non valido pari a zero per il limite massimo.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore semaforo non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```c
TX_SEMAPHORE     my_semaphore;

/* Increment the counting semaphore "my_semaphore" but make sure
   that it never exceeds 7 as specified in the call. */
status = tx_semaphore_ceiling_put(&my_semaphore, 7);

/* If status is TX_SUCCESS the semaphore count has been
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_create"></a>tx_semaphore_create

Creare un semaforo di conteggio

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_create(TX_SEMAPHORE *semaphore_ptr,
                           CHAR *name_ptr, ULONG initial_count);
```
### <a name="description"></a>Descrizione

Questo servizio crea un semaforo di conteggio per la sincronizzazione tra thread. Il conteggio iniziale del semaforo viene specificato come parametro di input.

### <a name="parameters"></a>Parametri 

- **semaphore_ptr:** puntatore a un blocco di controllo semaforo. 
- **name_ptr:** puntatore al nome del semaforo.
- **initial_count**: specifica il conteggio iniziale per questo semaforo. I valori validi vanno da 0x00000000 a 0xFFFFFFFF.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Creazione del semaforo completata.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore semaforo non valido. Il puntatore è NULL o il semaforo è già stato creato.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Create a counting semaphore whose initial value is 1.
   This is typically the technique used to make a binary
   semaphore. Binary semaphores are used to provide
   protection over a common resource. */
status = tx_semaphore_create(&my_semaphore,
            "my_semaphore_name", 1);

/* If status equals TX_SUCCESS, my_semaphore is ready for
   use. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_delete"></a>tx_semaphore_delete

Eliminare il semaforo di conteggio

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il semaforo di conteggio specificato. Tutti i thread sospesi in attesa di un'istanza del semaforo vengono ripresi e vengono TX_DELETED stato restituito.

> [!IMPORTANT]
> L'applicazione deve assicurarsi che un callback di notifica put per questo semaforo venga completato (o disabilitato) prima di eliminare il semaforo. Inoltre, l'applicazione deve impedire qualsiasi uso futuro di un semaforo eliminato.

### <a name="parameters"></a>Parametri 

- **semaphore_ptr:** puntatore a un semaforo creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Eliminazione del semaforo completata.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore al semaforo di conteggio non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Delete counting semaphore. Assume that the counting
   semaphore has already been created. */
status = tx_semaphore_delete(&my_semaphore);

/* If status equals TX_SUCCESS, the counting semaphore is
   deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_get"></a>tx_semaphore_get

Ottenere l'istanza dal semaforo di conteggio

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_get(TX_SEMAPHORE *semaphore_ptr,
                          ULONG wait_option)
```
### <a name="description"></a>Descrizione

Questo servizio recupera un'istanza (un singolo conteggio) dal semaforo di conteggio specificato. Di conseguenza, il conteggio del semaforo specificato viene ridotto di uno.

### <a name="parameters"></a>Parametri

- **semaphore_ptr:** puntatore a un semaforo di conteggio creato in precedenza.
- **wait_option**: definisce il comportamento del servizio se non sono disponibili istanze del semaforo. ad esempio, il conteggio dei semafori è zero. Le opzioni di attesa sono definite nel modo seguente:
    - **TX_NO_WAIT**: (0x00000000)
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF)
    - valore di timeout: (da 0x00000001 a 0xFFFFFFFE)

    La TX_NO_WAIT comporta un ritorno immediato da questo servizio indipendentemente dal fatto che l'operazione sia riuscita o meno. *Questa è l'unica opzione valida se il servizio viene chiamato da un non thread; ad esempio inizializzazione, timer o ISR.*

    Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando non è disponibile un'istanza del semaforo. 

    La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa di un'istanza del semaforo.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Recupero riuscito di un'istanza del semaforo.
- **TX_DELETED:**(0x01) Il semaforo di conteggio è stato eliminato durante la sospensione del thread.
- **TX_NO_INSTANCE**: il servizio (0x0D) non è stato in grado di recuperare un'istanza del semaforo di conteggio (il numero di semafori è zero entro il tempo di attesa specificato).
- **TX_WAIT_ABORTED:**(0x1A) Sospensione interrotta da un altro thread, timer o ISR.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore al semaforo di conteggio non valido.
- TX_WAIT_ERROR: (0x04) È stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un thread non.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```c
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Get a semaphore instance from the semaphore
   "my_semaphore." If the semaphore count is zero,
   suspend until an instance becomes available.
   Note that this suspension is only possible from
   application threads. */
status =  tx_semaphore_get(&my_semaphore, TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the thread has obtained
   an instance of the semaphore. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semahore_delete
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_info_get"></a>tx_semaphore_info_get

Recuperare informazioni sul semaforo

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_info_get(TX_SEMAPHORE *semaphore_ptr,
                          CHAR **name, ULONG *current_value,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_SEMAPHORE **next_semaphore)
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul semaforo specificato.

### <a name="parameters"></a>Parametri

- **semaphore_ptr:** puntatore al blocco di controllo semaforo.
- **name:** puntatore alla destinazione per il puntatore al nome del semaforo.
- **current_value:** puntatore alla destinazione per il conteggio del semaforo corrente.
- **first_suspended**: puntatore alla destinazione per il puntatore al thread che si trova per primo nell'elenco di sospensione di questo semaforo.
- **suspended_count:** puntatore alla destinazione per il numero di thread attualmente sospesi in questo semaforo.
- **next_semaphore:** puntatore alla destinazione per il puntatore del semaforo creato successivo.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Recupero delle informazioni sul semaforo riuscito.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore semaforo non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
TX_SEMAPHORE my_semaphore;
CHAR         *name;
ULONG        current_value;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_SEMAPHORE *next_semaphore;
UINT         status;

/* Retrieve information about the previously created
   semaphore "my_semaphore." */
status =  tx_semaphore_info_get(&my_semaphore, &name,
                      &current_value,
                      &first_suspended, &suspended_count,
                      &next_semaphore);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_performance_info_get"></a>tx_semaphore_performance_info_get 

Ottenere informazioni sulle prestazioni del semaforo

### <a name="prototype"></a>Prototipo

```C
UINT  tx_semaphore_performance_info_get(TX_SEMAPHORE *semaphore_ptr,
        ULONG *puts, ULONG *gets,
        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al semaforo specificato.

> [!NOTE]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **semaphore_ptr:** puntatore al semaforo creato in precedenza.
- **puts:** puntatore alla destinazione per il numero di richieste put eseguite su questo semaforo.
- **gets:** puntatore alla destinazione per il numero di richieste get eseguite su questo semaforo.
- **suspensions:** puntatore alla destinazione per il numero di sospensioni di thread in questo semaforo.
- **timeouts:** puntatore alla destinazione per il numero di timeout di sospensione del thread in questo semaforo.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Le prestazioni del semaforo sono riuscite.
- **TX_PTR_ERROR:**(0x03) Puntatore semaforo non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_SEMAPHORE     my_semaphore;
ULONG            puts;
ULONG            gets;
ULONG            suspensions;
ULONG            timeouts;

/* Retrieve performance information on the previously created
   semaphore. */
status =  tx_semaphore_performance_info_get(&my_semaphore, &puts,
               &gets, &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_performance_system_info_get"></a>tx_semaphore_performance_system_info_get 

Ottenere informazioni sulle prestazioni del sistema semaforo

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_performance_system_info_get(ULONG *puts,
       ULONG *gets, ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni di tutti i semafori nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **puts:** puntatore alla destinazione per il numero totale di richieste put eseguite su tutti i semafori.
- **gets:** puntatore alla destinazione per il numero totale di richieste get eseguite su tutti i semafori.
- **suspensions:** puntatore alla destinazione per il numero totale di sospensioni di thread in tutti i semafori.
- **timeouts:** puntatore alla destinazione per il numero totale di timeout di sospensione dei thread in tutti i semafori.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- TX_SUCCESS: (0x00) Prestazioni del sistema semaforo riuscite.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
ULONG         puts;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all previously created
   semaphores. */
status = tx_semaphore_performance_system_info_get(&puts, &gets,
               &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_prioritize
- tx_semaphore_put
- tx_semaphore_put_notify

## <a name="tx_semaphore_prioritize"></a>tx_semaphore_prioritize

Classificare in ordine di priorità l'elenco delle sospensioni del semaforo

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio posiziona il thread con priorità più alta sospeso per un'istanza del semaforo all'inizio dell'elenco di sospensione. Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.

### <a name="parameters"></a>Parametri 

- **semaphore_ptr:** puntatore a un semaforo creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Priorità del semaforo riuscito.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore al semaforo di conteggio non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next instance of this semaphore. */
status =  tx_semaphore_prioritize(&my_semaphore);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_semaphore_put call made to this semaphore will
   wake up this thread. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_put

## <a name="tx_semaphore_put"></a>tx_semaphore_put

Inserire un'istanza nel semaforo di conteggio

### <a name="prototype"></a>Prototipo

```C
UINT tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio inserisce un'istanza nel semaforo di conteggio specificato, che in realtà incrementa di uno il semaforo di conteggio.

> [!IMPORTANT]
> Se questo servizio viene chiamato quando il semaforo è tutto uno (OxFFFFFFFF), la nuova operazione put causerà la reimpostazione del semaforo su zero.

### <a name="parameters"></a>Parametri

- **semaphore_ptr:** puntatore al blocco di controllo del semaforo di conteggio creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Put semaforo riuscito.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore non valido al semaforo di conteggio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_SEMAPHORE     my_semaphore;
UINT             status;

/* Increment the counting semaphore "my_semaphore." */
status =  tx_semaphore_put(&my_semaphore);

/* If status equals TX_SUCCESS, the semaphore count has
   been incremented. Of course, if a thread was waiting,
   it was given the semaphore instance and resumed. */
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_get
- tx_semaphore_put_notify

## <a name="tx_semaphore_put_notify"></a>tx_semaphore_put_notify

Notificare all'applicazione quando viene inserito il semaforo

### <a name="prototype"></a>Prototipo

```C
UINT  tx_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr,
        VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback di notifica che viene chiamata ogni volta che viene inserito il semaforo specificato. L'elaborazione del callback di notifica è definita dall'applicazione.

> [!NOTE]
> Il callback di notifica del semaforo dell'applicazione non può chiamare alcuna API SMP ThreadX con un'opzione di sospensione.

### <a name="parameters"></a>Parametri 

- **semaphore_ptr:** puntatore al semaforo creato in precedenza.
- **semaphore_put_notify:** puntatore alla funzione di notifica put del semaforo dell'applicazione. Se questo valore è TX_NULL, la notifica è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Registrazione riuscita della notifica put del semaforo.
- TX_SEMAPHORE_ERROR: (0x0C) Puntatore semaforo non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema è stato compilato con funzionalità di notifica disabilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_SEMAPHORE     my_semaphore;

/* Register the "my_semaphore_put_notify" function for monitoring
   the put operations on the semaphore "my_semaphore." */
status =  tx_semaphore_put_notify(&my_semaphore,
                my_semaphore_put_notify);

/* If status is TX_SUCCESS the semaphore put notification function
   was successfully registered. */

void my_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr)
{
   /* The semaphore was just put! */
}
```
### <a name="see-also"></a>Vedere anche

- tx_semaphore_ceiling_put
- tx_semaphore_create
- tx_semaphore_delete
- tx_semaphore_get
- tx_semaphore_info_get
- tx_semaphore_performance_info_get
- tx_semaphore_performance_system_info_get
- tx_semaphore_prioritize
- tx_semaphore_put

## <a name="tx_thread_create"></a>tx_thread_create

Creare un thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_create(TX_THREAD *thread_ptr,
                          CHAR *name_ptr, VOID (*entry_function)(ULONG),
                          ULONG entry_input, VOID *stack_start,
                          ULONG stack_size, UINT priority,
                          UINT preempt_threshold, ULONG time_slice,
                          UINT auto_start);
```
### <a name="description"></a>Descrizione

Questo servizio crea un thread dell'applicazione che avvia l'esecuzione in corrispondenza della funzione di immissione dell'attività specificata. Lo stack, la priorità, la soglia di precedenza e la sezione temporale sono tra gli attributi specificati dai parametri di input. Inoltre, viene specificato anche lo stato di esecuzione iniziale del thread.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore a un blocco di controllo del thread.
- **name_ptr:** puntatore al nome del thread.
- **entry_function**: specifica la funzione C iniziale per l'esecuzione del thread. Quando un thread viene restituito da questa funzione di ingresso, viene inserito in uno stato completato e sospeso a tempo indeterminato.
- **entry_input:** valore a 32 bit passato alla funzione di immissione del thread quando viene eseguito per la prima volta. L'uso di questo input è determinato esclusivamente dall'applicazione.
- **stack_start**: indirizzo iniziale dell'area di memoria dello stack. 
- **stack_size**: numero di byte nell'area di memoria dello stack. L'area dello stack del thread deve essere sufficientemente grande da gestire l'annidamento delle chiamate di funzione nel peggiore dei casi e l'utilizzo delle variabili locali.
- **priority:** priorità numerica del thread. I valori validi sono da 0 a (TX_MAX_PRIORITES-1), dove il valore 0 rappresenta la priorità più alta.
- **preempt_threshold:** livello di priorità più alto (da 0 a (TX_MAX_PRIORITIES-1)) di preemption disabilitato. Solo le priorità superiori a questo livello sono autorizzate a eseguire il pre-accesso a questo thread. Questo valore deve essere minore o uguale alla priorità specificata. Un valore uguale alla priorità del thread disabilita preemption-threshold.
- **time_slice:** numero di tick timer che questo thread può eseguire prima che altri thread pronti con la stessa priorità hanno la possibilità di essere eseguiti. Si noti che l'uso di preemption-threshold disabilita la sezione temporale. I valori di intervallo temporale validi sono compresi tra 1 e 0xFFFFFFFF (inclusi). Il valore **TX_NO_TIME_SLICE** (valore 0) disabilita la sezione temporale di questo thread.

    > [!IMPORTANT]
    > L'uso della sezione temporale comporta un leggero sovraccarico del sistema. Poiché la sezione temporale è utile solo nei casi in cui più thread condividono la stessa priorità, ai thread con una priorità univoca non deve essere assegnato un intervallo di tempo.

- **auto_start**: specifica se il thread viene avviato immediatamente o viene inserito in uno stato sospeso. Le opzioni legali **sono TX_AUTO_START** (0x01) **e TX_DONT_START** (0x00). Se TX_DONT_START specificato, l'applicazione deve chiamare in un secondo momento tx_thread_resume per consentire l'esecuzione del thread.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Creazione del thread riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore di controllo thread non valido. Il puntatore è NULL o il thread è già stato creato.
- TX_PTR_ERROR: (0x03) Indirizzo iniziale non valido del punto di ingresso o dell'area dello stack non valido, in genere NULL.
- TX_SIZE_ERROR: (0x05) Le dimensioni dell'area dello stack non sono valide. I thread devono avere almeno **TX_MINIMUM_STACK** byte da eseguire.
- TX_PRIORITY_ERROR: (0x0F) Priorità del thread non valida, ovvero un valore non compreso nell'intervallo compreso tra (da 0 a (TX_MAX_PRIORITIES-1)).
- TX_THRESH_ERROR: (0x18) Specificato valore preemptionthreshold non valido. Questo valore deve essere una priorità valida minore o uguale alla priorità iniziale del thread.
- TX_START_ERROR: (0x10) Selezione avvio automatico non valida.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          status;

/* Create a thread of priority 15 whose entry point is
   "my_thread_entry". This thread’s stack area is 1000
   bytes in size, starting at address 0x400000. The
   preemption-threshold is setup to allow preemption of threads
   with priorities ranging from 0 through 14. Time-slicing is
   disabled. This thread is automatically put into a ready
   condition. */
status =  tx_thread_create(&my_thread, "my_thread_name",
                my_thread_entry, 0x1234,
                (VOID *) 0x400000, 1000,
                15, 15, TX_NO_TIME_SLICE,
                TX_AUTO_START);

/* If status equals TX_SUCCESS, my_thread is ready
   for execution! */
...

/* Thread’s entry function. When "my_thread" actually
   begins execution, control is transferred to this
   function. */
VOID my_thread_entry (ULONG initial_input)
{

    /* When we get here, the value of initial_input is
    0x1234. See how this was specified during
    creation. */

    /* The real work of the thread, including calls to
    other function should be called from here! */

    /* When this function returns, the corresponding
    thread is placed into a "completed" state. */
}
```
### <a name="see-also"></a>Vedere anche

- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_delete"></a>tx_thread_delete

Eliminare il thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_delete(TX_THREAD *thread_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il thread dell'applicazione specificato. Poiché il thread specificato deve essere in uno stato terminato o completato, questo servizio non può essere chiamato da un thread che tenta di eliminare se stesso.

> [!IMPORTANT]
> È responsabilità dell'applicazione gestire l'area di memoria associata allo stack del thread, disponibile al termine del servizio. Inoltre, l'applicazione deve impedire l'uso di un thread eliminato.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore a un thread dell'applicazione creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Eliminazione del thread riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- **TX_DELETE_ERROR:**(0x11) Il thread specificato non si trova in uno stato terminato o completato.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread e timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          status;

/* Delete an application thread whose control block is
   "my_thread". Assume that the thread has already been
   created with a call to tx_thread_create. */
status =  tx_thread_delete(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_entry_exit_notify"></a>tx_thread_entry_exit_notify

Notificare all'applicazione l'ingresso e l'uscita del thread

### <a name="prototype"></a>Prototipo

```C
UINT  tx_thread_entry_exit_notify(TX_THREAD *thread_ptr,
        VOID (*entry_exit_notify)(TX_THREAD *, UINT));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback di notifica che viene chiamata ogni volta che il thread specificato viene immesso o chiuso. L'elaborazione del callback di notifica è definita dall'applicazione.

> [!NOTE]
> Il callback di notifica di ingresso/uscita del thread dell'applicazione non può chiamare alcuna API SMP ThreadX con un'opzione di sospensione.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore al thread creato in precedenza.
- **entry_exit_notify:** puntatore alla funzione di notifica di ingresso/uscita del thread dell'applicazione. Il secondo parametro della funzione di notifica di ingresso/uscita indica se è presente una voce o un'uscita. Il valore TX_THREAD_ENTRY (0x00) indica che il thread è stato immesso, mentre il valore TX_THREAD_EXIT (0x01) indica che il thread è stato chiuso. Se questo valore è TX_NULL, la notifica è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Registrazione riuscita della funzione di notifica di ingresso/uscita del thread.
- TX_THREAD_ERROR: (0x0E) Puntatore di thread non valido.
- **TX_FEATURE_NOT_ENABLED(0xFF)** Il sistema è stato compilato con funzionalità di notifica disabilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_THREAD         my_thread;

/* Register the "my_entry_exit_notify" function for monitoring
   the entry/exit of the thread "my_thread." */
status =  tx_thread_entry_exit_notify(&my_thread,
                my_entry_exit_notify);

/* If status is TX_SUCCESS the entry/exit notification function was
   successfully registered. */
void my_entry_exit_notify(TX_THREAD *thread_ptr, UINT condition)
{

    /* Determine if the thread was entered or exited. */
    if (condition == TX_THREAD_ENTRY)
                 /* Thread entry! */
    else if (condition == TX_THREAD_EXIT)
         /* Thread exit! */
}
```

### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_identify"></a>tx_thread_identify

Recupera il puntatore al thread attualmente in esecuzione

### <a name="prototype"></a>Prototipo

```C
TX_THREAD* tx_thread_identify(VOID);
```
### <a name="description"></a>Descrizione

Questo servizio restituisce un puntatore al thread attualmente in esecuzione. Se non è in esecuzione alcun thread, questo servizio restituisce un puntatore Null.

> [!IMPORTANT]
> Se questo servizio viene chiamato da un ISR, il valore restituito rappresenta il thread in esecuzione prima del gestore di interrupt in esecuzione.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

- puntatore thread: puntatore al thread attualmente in esecuzione. Se non è in esecuzione alcun thread, il valore restituito viene TX_NULL.

### <a name="allowed-from"></a>Consentito da

Thread e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_THREAD     *my_thread_ptr;

/* Find out who we are! */
my_thread_ptr =  tx_thread_identify();

/* If my_thread_ptr is non-null, we are currently executing
   from that thread or an ISR that interrupted that thread.
   Otherwise, this service was called
   from an ISR when no thread was running when the
   interrupt occurred.  */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_info_get"></a>tx_thread_info_get

Recuperare informazioni sul thread

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_info_get(TX_THREAD *thread_ptr, CHAR **name,
                          UINT *state, ULONG *run_count,
                          UINT *priority,
                          UINT *preemption_threshold,
                          ULONG *time_slice,
                          TX_THREAD **next_thread,
                          TX_THREAD **suspended_thread);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul thread specificato.

### <a name="parameters"></a>Parametri 

- **thread_ptr:** puntatore al blocco di controllo del thread.
- **name:** puntatore alla destinazione per il puntatore al nome del thread.
- **state:** puntatore alla destinazione per lo stato di esecuzione corrente del thread. I possibili valori sono i seguenti:
    - **TX_READY**: (0x00)
    - **TX_COMPLETED**: (0x01)
    - **TX_TERMINATED**: (0x02)
    - **TX_SUSPENDED**: (0x03)
    - **TX_SLEEP**: (0x04)
    - **TX_QUEUE_SUSP**: (0x05)
    - **TX_SEMAPHORE_SUSP**: (0x06)
    - **TX_EVENT_FLAG**: (0x07)
    - **TX_BLOCK_MEMORY**: (0x08)
    - **TX_BYTE_MEMORY**: (0x09)
    - **TX_MUTEX_SUSP**: (0x0D)

- **run_count:** puntatore alla destinazione per il conteggio di esecuzione del thread. 
- **priority:** puntatore alla destinazione per la priorità del thread.
- **preemption_threshold:** puntatore alla destinazione per la soglia di preemption-threshold del thread.
- **time_slice:** puntatore alla destinazione per l'intervallo di tempo del thread. 
- **next_thread:** puntatore alla destinazione per il puntatore al thread creato successivamente.
- **suspended_thread:** puntatore alla destinazione per puntatore al thread successivo nell'elenco di sospensione.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Recupero delle informazioni sul thread riuscito.
- TX_THREAD_ERROR: (0x0E) Puntatore di controllo thread non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_THREAD my_thread;
CHAR *name;
UINT state;
ULONG run_count;
UINT priority;
UINT preemption_threshold;
UINT time_slice;
TX_THREAD *next_thread;
TX_THREAD *suspended_thread;
UINT status;

/* Retrieve information about the previously created
   thread "my_thread." */
status =  tx_thread_info_get(&my_thread, &name,
                  &state, &run_count,
            &priority, &preemption_threshold,
                  &time_slice, &next_thread,&suspended_thread);
/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_performance_info_get"></a>tx_thread_performance_info_get 

Ottenere informazioni sulle prestazioni dei thread

### <a name="prototype"></a>Prototipo

```C
UINT  tx_thread_performance_info_get(TX_THREAD *thread_ptr,
        ULONG *resumptions, ULONG *suspensions,
        ULONG *solicited_preemptions, ULONG *interrupt_preemptions,
        ULONG *priority_inversions, ULONG *time_slices,
        ULONG *relinquishes, ULONG *timeouts, ULONG *wait_aborts,
        TX_THREAD **last_preempted_by);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al thread specificato.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_THREAD_ENABLE_PERFORMANCE_INFO per consentire al servizio di restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri 

- **thread_ptr:** puntatore al thread creato in precedenza.
- **resumptions:** puntatore alla destinazione per il numero di ripresi di questo thread.
- **suspensions:** puntatore alla destinazione per il numero di sospensioni di questo thread.
- **solicited_preemptions:** puntatore alla destinazione per il numero di preemption come risultato di una chiamata al servizio API ThreadX effettuata da questo thread.
- **interrupt_preemptions**: puntatore alla destinazione per il numero di interruzioni del thread come risultato dell'elaborazione di interrupt.
- **priority_inversions:** puntatore alla destinazione per il numero di inversione di priorità di questo thread.
- **time_slices**: puntatore alla destinazione per il numero di volte in cui il thread è stato spostato.
- **relinquishes:** puntatore alla destinazione per il numero di richieste di thread eseguite da questo thread.
- **timeouts:** puntatore alla destinazione per il numero di timeout di sospensione in questo thread.
- **wait_aborts**: puntatore alla destinazione per il numero di attese interrotte eseguite su questo thread.
- **last_preempted_by:** puntatore alla destinazione per il puntatore del thread che ha preesimpiato questo thread.

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere le prestazioni del thread con esito positivo.
- **TX_PTR_ERROR:**(0x03) Puntatore di thread non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```c
TX_THREAD     my_thread;
ULONG         resumptions;
ULONG         suspensions;
ULONG         solicited_preemptions;
ULONG         interrupt_preemptions;
ULONG         priority_inversions;
ULONG         time_slices;
ULONG         relinquishes;
ULONG         timeouts;
ULONG         wait_aborts;
TX_THREAD     *last_preempted_by;

/* Retrieve performance information on the previously created
   thread. */
status = tx_thread_performance_info_get(&my_thread, &resumptions,
               &suspensions,
               &solicited_preemptions, &interrupt_preemptions,
               &priority_inversions, &time_slices,
               &relinquishes, &timeouts,
               &wait_aborts, &last_preempted_by);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_performance_system_info_get"></a>tx_thread_performance_system_info_get 

Ottenere informazioni sulle prestazioni del sistema di thread

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_performance_system_info_get(ULONG *resumptions,
       ULONG *suspensions, ULONG *solicited_preemptions,
       ULONG *interrupt_preemptions, ULONG *priority_inversions,
       ULONG *time_slices, ULONG *relinquishes, ULONG *timeouts,
       ULONG *wait_aborts, ULONG *non_idle_returns,
       ULONG *idle_returns);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni di tutti i thread nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_THREAD_ENABLE_PERFORMANCE_INFO per consentire al servizio di restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **resumptions:** puntatore alla destinazione per il numero totale di ripresi di thread.
- **suspensions:** puntatore alla destinazione per il numero totale di sospensioni di thread.
- **solicited_preemptions:** puntatore alla destinazione per il numero totale di preemption di thread come risultato della chiamata di un thread a un servizio API ThreadX.
- **interrupt_preemptions**: puntatore alla destinazione per il numero totale di interruzioni del thread in seguito all'elaborazione dell'interrupt.
- **priority_inversions:** puntatore alla destinazione per il numero totale di inversione della priorità dei thread.
- **time_slices**: puntatore alla destinazione per il numero totale di time-slice del thread.
- **relinquishes:** puntatore alla destinazione per il numero totale di richieste di thread.
- **timeouts:** puntatore alla destinazione per il numero totale di timeout di sospensione del thread.
- **wait_aborts:** puntatore alla destinazione per il numero totale di attese di thread interrotte. 
- **non_idle_returns:** puntatore alla destinazione per il numero di volte in cui un thread torna al sistema quando un altro thread è pronto per l'esecuzione. 
- **idle_returns**: puntatore alla destinazione per il numero di volte in cui un thread torna al sistema quando nessun altro thread è pronto per l'esecuzione (sistema inattivo).

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Ottenere prestazioni del sistema di thread riuscite.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
ULONG         resumptions;
ULONG         suspensions;
ULONG         solicited_preemptions;
ULONG         interrupt_preemptions;
ULONG         priority_inversions;
ULONG         time_slices;
ULONG         relinquishes;
ULONG         timeouts;
ULONG         wait_aborts;
ULONG         non_idle_returns;
ULONG         idle_returns;

/* Retrieve performance information on all previously created
   thread. */
status = tx_thread_performance_system_info_get(&resumptions,
                &suspensions,
                &solicited_preemptions, &interrupt_preemptions,
                &priority_inversions, &time_slices, &relinquishes,
                &timeouts, &wait_aborts, &non_idle_returns,
                &idle_returns);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_preemption_change"></a>tx_thread_preemption_change

Modificare la soglia di preemption del thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_preemption_change(TX_THREAD *thread_ptr,
                          UINT new_threshold, UINT *old_threshold);
```
### <a name="description"></a>Descrizione

Questo servizio modifica la soglia di preemption del thread specificato. La soglia di preemption impedisce la preemption del thread specificato da parte di thread uguali o minori del valore preemption-threshold.

> [!IMPORTANT]
> L'uso di preemption-threshold disabilita il selicing temporale per il thread specificato.

### <a name="parameters"></a>Parametri

- **thread_ptr**: puntatore a un thread dell'applicazione creato in precedenza.
- **new_threshold:** nuovo livello di priorità della soglia di precedenza (da 0 a (TX_MAX_PRIORITIES-1)).
- **old_threshold:** puntatore a una posizione per restituire la soglia di precedenza precedente.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Modifica della soglia di preemption riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- **TX_THRESH_ERROR**: (0x18) La nuova soglia di precedenza specificata non è una priorità di thread valida (un valore diverso da (da 0 a (TX_MAX_PRIORITIES-1)) o è maggiore di (priorità inferiore) rispetto alla priorità del thread corrente.
- TX_PTR_ERROR: (0x03) Puntatore non valido alla posizione di archiviazione precedente.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread e timer

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```c
TX_THREAD     my_thread;
UINT          my_old_threshold;
UINT          status;

/* Disable all preemption of the specified thread. The
   current preemption-threshold is returned in
   "my_old_threshold". Assume that "my_thread" has
   already been created. */
status = tx_thread_preemption_change(&my_thread,
                             0, &my_old_threshold);

/* If status equals TX_SUCCESS, the application thread is
   non-preemptable by another thread. Note that ISRs are
   not prevented by preemption disabling. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_priority_change"></a>tx_thread_priority_change

Modificare la priorità del thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_priority_change(TX_THREAD *thread_ptr,
                          UINT new_priority, UINT *old_priority);
```
### <a name="description"></a>Descrizione

Questo servizio modifica la priorità del thread specificato. Le priorità valide sono da 0 a (TX_MAX_PRIORITES-1), dove 0 rappresenta il livello di priorità più alto.

> [!IMPORTANT]
> La soglia di precedenza del thread specificato viene impostata automaticamente sulla nuova priorità. Se si desidera una nuova soglia, **il tx_thread_preemption_change** deve essere usato dopo questa chiamata.

### <a name="parameters"></a>Parametri

- **thread_ptr**: puntatore a un thread dell'applicazione creato in precedenza.
- **new_priority:** nuovo livello di priorità del thread (da 0 a (TX_MAX_PRIORITIES-1).)
- **old_priority:** puntatore a una posizione per restituire la priorità precedente del thread.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Modifica della priorità riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- TX_PRIORITY_ERROR: (0x0F) La nuova priorità specificata non è valida (un valore diverso da (da 0 a (TX_MAX_PRIORITIES-1)).
- TX_PTR_ERROR: (0x03) Puntatore non valido alla posizione di archiviazione con priorità precedente.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread e timer

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          my_old_priority;
UINT          status;

/* Change the thread represented by "my_thread" to priority
   0. */
status = tx_thread_priority_change(&my_thread,
                            0, &my_old_priority);

/* If status equals TX_SUCCESS, the application thread is
   now at the highest priority level in the system. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_relinquish"></a>tx_thread_relinquish

Resciso il controllo ad altri thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
VOID tx_thread_relinquish(VOID);
```
### <a name="description"></a>Descrizione

Questo servizio clinea il controllo del processore ad altri thread pronti per l'esecuzione con la stessa priorità o con priorità più alta.

> [!IMPORTANT]
> Oltre a rinunciare al controllo ai thread con la stessa priorità, questo servizio cede anche il controllo al thread con priorità più alta impedito dall'esecuzione a causa dell'impostazione della soglia di precedenza del thread corrente.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

Nessuno

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
ULONG run_counter_1 =  0;
ULONG run_counter_2 =  0;

/* Example of two threads relinquishing control to
   each other in an infinite loop. Assume that
   both of these threads are ready and have the same
   priority. The run counters will always stay within one
   of each other. */

VOID  my_first_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {

        /* Increment the run counter. */
        run_counter_1++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}

VOID my_second_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_2++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_reset"></a>tx_thread_reset

Reimpostare il thread

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_reset(TX_THREAD *thread_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio reimposta il thread specificato da eseguire nel punto di ingresso definito al momento della creazione del thread. Il thread deve essere in uno **stato TX_COMPLETED** o **TX_TERMINATED** per essere reimpostato

> [!IMPORTANT]
> Il thread deve essere ripreso per poter essere eseguito di nuovo.

### <a name="parameters"></a>Parametri 

- **thread_ptr:** puntatore a un thread creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Reimpostazione del thread riuscita.
- **TX_NOT_DONE:**(0x20) Il thread specificato non è in TX_COMPLETED o TX_TERMINATED stato.
- TX_THREAD_ERROR: (0x0E) Puntatore di thread non valido.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;

/* Reset the previously created thread "my_thread." */
status = tx_thread_reset(&my_thread);

/* If status is TX_SUCCESS the thread is reset. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_resume"></a>tx_thread_resume

Riprendere il thread dell'applicazione sospeso

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_resume(TX_THREAD *thread_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio riprende o prepara l'esecuzione di un thread precedentemente sospeso da una ***tx_thread_suspend*** chiamata. Inoltre, questo servizio riprende i thread creati senza avvio automatico.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore a un thread dell'applicazione sospeso.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Ripresa del thread riuscita.
- **TX_SUSPEND_LIFTED:**(0x19) La sospensione ritardata impostata in precedenza è stata revocata.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- **TX_RESUME_ERROR:**(0x12) Il thread specificato non è sospeso o è stato precedentemente sospeso da un servizio diverso **_da tx_thread_suspend_**.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          status;

/* Resume the thread represented by "my_thread". */
status =  tx_thread_resume(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   now ready to execute. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_sleep"></a>tx_thread_sleep

Sospendi thread corrente per l'ora specificata

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_sleep(ULONG timer_ticks);
```
### <a name="description"></a>Descrizione

Questo servizio causa la sospensione del thread chiamante per il numero specificato di tick del timer. La quantità di tempo fisico associata a un tick timer è specifica dell'applicazione. Questo servizio può essere chiamato solo da un thread dell'applicazione.

### <a name="parameters"></a>Parametri

- **timer_ticks:** numero di tick del timer per sospendere il thread dell'applicazione chiamante, compreso tra 0 e 0xFFFFFFFF. Se viene specificato 0, il servizio viene restituito immediatamente.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Sospensione thread riuscita.
- **TX_WAIT_ABORTED:** la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.
- **TX_CALLER_ERROR:** servizio (0x13) chiamato da un non thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
UINT status;

/* Make the calling thread sleep for 100
   timer-ticks. */
status = tx_thread_sleep(100);

/* If status equals TX_SUCCESS, the currently running
   application thread slept for the specified number of
   timer-ticks. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_smp_core_exclude"></a>tx_thread_smp_core_exclude

Escludere l'esecuzione di thread in un set di core

### <a name="prototype"></a>Prototipo

```C
UINT  tx_thread_smp_core_exclude(TX_THREAD *thread_ptr,
                          ULONG exclusion_map);
```
### <a name="description"></a>Descrizione

Questa funzione esclude l'esecuzione del thread specificato nei core specificati nella mappa di bit denominata "*exclusion_map*". Ogni bit in "*exclusion_map*" rappresenta un core (il bit 0 rappresenta core 0 e così via). Se il bit è impostato, il core corrispondente viene escluso dall'esecuzione del thread specificato.

> [!IMPORTANT]
> L'uso dell'esclusione del processore può causare un'elaborazione aggiuntiva nella logica di mapping tra thread e core per trovare la corrispondenza ottimale. Questa elaborazione è vincolata dal numero di thread pronti.

### <a name="parameters"></a>Parametri 

- **thread_ptr:** puntatore al thread per modificare l'esclusione principale.
- **exclusion_map**: mappa di bit in cui un bit sit indica che tale core è escluso. Se si specifica un valore 0, il thread può essere eseguito su qualsiasi core (impostazione predefinita).

### <a name="return-values"></a>Valori restituiti

- TX_SUCCESS: (0x00) Esclusione core riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore di thread non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, ISR, thread e timer

### <a name="example"></a>Esempio

```C
/* Exclude core 0 for "Thread 0". */
tx_thread_smp_core_exclude(&thread_0, 0x01);
```

### <a name="see-also"></a>Vedere anche

- tx_thread_smp_core_exclude_get
- tx_thread_smp_core_get

## <a name="tx_thread_smp_core_exclude_get"></a>tx_thread_smp_core_exclude_get

Ottiene l'esclusione principale corrente del thread

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr,
                         ULONG *exclusion_map_ptr);
```
### <a name="description"></a>Descrizione

Questa funzione restituisce l'elenco di esclusione principale corrente.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore al thread da cui recuperare l'esclusione principale.
- **exclusion_map_ptr:** destinazione per la mappa di bit di esclusione core corrente.

### <a name="return-values"></a>Valori restituiti

- TX_SUCCESS: (0x00) Recupero riuscito dell'esclusione principale del thread.
- TX_THREAD_ERROR: (0x0E) Puntatore di thread non valido.
- TX_PTR_ERROR: (0x03) Puntatore di destinazione di esclusione non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, ISR, thread e timer

### <a name="example"></a>Esempio

```C
ULONGexcluded_cores;
/* Retrieve the core exclusion for "Thread 0". */
tx_thread_smp_core_exclude_get(&thread_0, &excluded_cores);
```

### <a name="see-also"></a>Vedere anche

- tx_thread_smp_core_exclude
- tx_thread_smp_core_get

## <a name="tx_thread_smp_core_get"></a>tx_thread_smp_core_get

Recuperare il core del chiamante attualmente in esecuzione

### <a name="prototype"></a>Prototipo

```C
UINT  tx_thread_smp_core_get(void);
```
### <a name="description"></a>Descrizione

Questa funzione restituisce l'ID principale del core che esegue questo servizio.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

- core_id: ID del core attualmente in esecuzione, (da 0 a TX_THREAD_SMP_MAX_CORES-1)

### <a name="allowed-from"></a>Consentito da

Inizializzazione, ISR, thread e timer

### <a name="example"></a>Esempio

```C
UINTcore;
/* Pickup the currently executing core. */
core = tx_thread_smp_core_get();

/* At this point, “core” contains the executing core ID. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_smp_core_exclude
- tx_thread_smp_core_exclude_get

## <a name="tx_thread_stack_error_notify"></a>tx_thread_stack_error_notify

Registrare il callback di notifica degli errori dello stack di thread

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_stack_error_notify(VOID (*error_handler)(TX_THREAD *));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback di notifica per la gestione degli errori dello stack di thread. Quando ThreadX SMP rileva un errore dello stack di thread durante l'esecuzione, chiamerà questa funzione di notifica per elaborare l'errore. L'elaborazione dell'errore è completamente definita dall'applicazione. Può essere eseguito qualsiasi tipo di operazione, dalla sospensione del thread che viola alla reimpostazione dell'intero sistema.

> [!IMPORTANT]
> La libreria ThreadX SMP deve essere compilata **con TX_ENABLE_STACK_CHECKING** per consentire al servizio di restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **error_handler:** puntatore alla funzione di gestione degli errori dello stack dell'applicazione. Se questo valore è TX_NULL, la notifica viene disabilitata.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Reimpostazione del thread riuscita.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
void my_stack_error_handler(TX_THREAD *thread_ptr);

/* Register the "my_stack_error_handler" function with ThreadX SMP
   so that thread stack errors can be handled by the application. */
status =  tx_thread_stack_error_notify(my_stack_error_handler);

/* If status is TX_SUCCESS the stack error handler is registered.*/
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_suspend"></a>tx_thread_suspend

Sospendere il thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_suspend(TX_THREAD *thread_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio sospende il thread dell'applicazione specificato. Un thread può chiamare questo servizio per sospendere se stesso.

> [!IMPORTANT]
> Se il thread specificato è già sospeso per un altro motivo, questa sospensione viene mantenuta internamente fino a quando non viene revocata la sospensione precedente. In questo caso, viene eseguita questa sospensione non condizionale del thread specificato. Altre richieste di sospensione non condizionali non hanno alcun effetto.

Dopo essere stato sospeso, il thread deve essere ripreso ***dal*** tx_thread_resume eseguire di nuovo.

## <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore a un thread dell'applicazione.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Sospensione del thread riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- **TX_SUSPEND_ERROR:**(0x14) Il thread specificato si trova in uno stato terminato o completato.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          status;

/* Suspend the thread represented by "my_thread". */
status = tx_thread_suspend(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   unconditionally suspended. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_terminate
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_terminate"></a>tx_thread_terminate

Termina il thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_terminate(TX_THREAD *thread_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio termina il thread dell'applicazione specificato indipendentemente dal fatto che il thread sia sospeso o meno. Un thread può chiamare questo servizio per terminare se stesso.

> [!IMPORTANT]
> Dopo essere stato terminato, il thread deve essere reimpostato per poter essere eseguito nuovamente.

> [!WARNING]
> È responsabilità dell'applicazione assicurarsi che il thread si trova in uno stato adatto per la terminazione. Ad esempio, un thread non deve essere terminato durante l'elaborazione critica dell'applicazione o all'interno di altri componenti middleware in cui potrebbe lasciare tale elaborazione in uno stato sconosciuto.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore al thread dell'applicazione.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Terminazione del thread riuscita.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread e timer

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          status;

/* Terminate the thread represented by "my_thread". */
status =  tx_thread_terminate(&my_thread);

/* If status equals TX_SUCCESS, the thread is terminated
   and cannot execute again until it is reset. */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_time_slice_change
- tx_thread_wait_abort

## <a name="tx_thread_time_slice_change"></a>tx_thread_time_slice_change

Modifica la sezione temporale del thread dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_time_slice_change(TX_THREAD *thread_ptr,
                          ULONG new_time_slice, ULONG *old_time_slice);
```
### <a name="description"></a>Descrizione

Questo servizio modifica l'intervallo di tempo del thread dell'applicazione specificato. La selezione di un intervallo di tempo per un thread assicura che non verrà eseguito più del numero specificato di tick del timer prima che altri thread con la stessa priorità o priorità più alta hanno la possibilità di essere eseguiti.

> [!IMPORTANT]
> L'uso di preemption-threshold disabilita il selicing temporale per il thread specificato.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore al thread dell'applicazione.
- **new_time_slice:** nuovo valore dell'intervallo di tempo. I valori validi includono TX_NO_TIME_SLICE e numerici da 1 a 0xFFFFFFFF.
- **old_time_slice:** puntatore alla posizione per l'archiviazione del valore timeslice precedente del thread specificato.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Successful time-slice chance (Probabilità di intervallo di tempo riuscita).
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- TX_PTR_ERROR: (0x03) Puntatore non valido alla posizione di archiviazione precedente dell'intervallo di tempo.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread e timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
ULONG         my_old_time_slice;
UINT          status;

/* Change the time-slice of the thread associated with
   "my_thread" to 20. This will mean that "my_thread"
   can only run for 20 timer-ticks consecutively before
   other threads of equal or higher priority get a chance
   to run. */
status = tx_thread_time_slice_change(&my_thread, 20,
                             &my_old_time_slice);

/* If status equals TX_SUCCESS, the thread’s time-slice
   has been changed to 20 and the previous time-slice is
   in "my_old_time_slice." */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_wait_abort

## <a name="tx_thread_wait_abort"></a>tx_thread_wait_abort

Interrompere la sospensione del thread specificato

### <a name="prototype"></a>Prototipo

```C
UINT tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe la sospensione o qualsiasi altro oggetto sospeso del thread specificato. Se l'attesa viene interrotta, TX_WAIT_ABORTED valore restituito dal servizio su cui il thread era in attesa.

> [!IMPORTANT]
> Questo servizio non rilascia la sospensione esplicita che viene effettuata dal tx_thread_suspend servizio.

### <a name="parameters"></a>Parametri

- **thread_ptr:** puntatore a un thread dell'applicazione creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Interruzione dell'attesa del thread completata.
- TX_THREAD_ERROR: (0x0E) Puntatore del thread dell'applicazione non valido.
- **TX_WAIT_ABORT_ERROR:**(0x1B) Il thread specificato non è in attesa.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
TX_THREAD     my_thread;
UINT          status;

/* Abort the suspension condition of "my_thread." */
status =  tx_thread_wait_abort(&my_thread);

/* If status equals TX_SUCCESS, the thread is now ready
   again, with a return value showing its suspension
   was aborted (TX_WAIT_ABORTED). */
```
### <a name="see-also"></a>Vedere anche

- tx_thread_create
- tx_thread_delete
- tx_thread_entry_exit_notify
- tx_thread_identify
- tx_thread_info_get
- tx_thread_performance_info_get
- tx_thread_performance_system_info_get
- tx_thread_preemption_change
- tx_thread_priority_change
- tx_thread_relinquish
- tx_thread_reset
- tx_thread_resume
- tx_thread_sleep
- tx_thread_stack_error_notify
- tx_thread_suspend
- tx_thread_terminate
- tx_thread_time_slice_change

## <a name="tx_time_get"></a>tx_time_get

Recupera l'ora corrente

### <a name="prototype"></a>Prototipo

```C
ULONG tx_time_get(VOID);
```
### <a name="description"></a>Descrizione

Questo servizio restituisce il contenuto dell'orologio di sistema interno. Ogni volta che l'orologio di sistema interno aumenta di uno. L'orologio di sistema viene impostato su zero durante l'inizializzazione e può essere modificato in un valore specifico dal servizio ***tx_time_set***.

> [!IMPORTANT]
> L'ora effettiva che ogni timer rappresenta è specifica dell'applicazione.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

- tick dell'orologio di sistema: valore dell'orologio di sistema interno, in esecuzione gratuito.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
ULONG current_time;

/* Pickup the current system time, in timer-ticks. */
current_time =  tx_time_get();

/* Current time now contains a copy of the internal system
   clock. */
```
### <a name="see-also"></a>Vedere anche

- tx_time_set

## <a name="tx_time_set"></a>tx_time_set

Imposta l'ora corrente

### <a name="prototype"></a>Prototipo

```C
VOID tx_time_set(ULONG new_time);
```
### <a name="description"></a>Descrizione

Questo servizio imposta l'orologio di sistema interno sul valore specificato. Ogni timer-tick aumenta di uno il clock di sistema interno.

> [!IMPORTANT]
> L'ora effettiva che ogni timer rappresenta è specifica dell'applicazione.

### <a name="parameters"></a>Parametri

- **new_time:** nuova ora da inserire nell'orologio di sistema, i valori validi sono da 0 a 0xFFFFFFFF.

### <a name="return-values"></a>Valori restituiti

Nessuno

### <a name="allowed-from"></a>Consentito da

Thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Set the internal system time to 0x1234. */
tx_time_set(0x1234);

/* Current time now contains 0x1234 until the next timer
   interrupt. */
```
### <a name="see-also"></a>Vedere anche

- tx_time_get

## <a name="tx_timer_activate"></a>tx_timer_activate

Attivare il timer dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_activate(TX_TIMER *timer_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio attiva il timer dell'applicazione specificato. Le routine di scadenza dei timer che scadono contemporaneamente vengono eseguite nell'ordine in cui sono stati attivati.

> [!NOTE]
> Prima di poter essere attivato di nuovo, è necessario reimpostare **tx_timer_change** timer con un solo tentativo scaduto.

### <a name="parameters"></a>Parametri

- **timer_ptr:** puntatore a un timer dell'applicazione creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Attivazione del timer dell'applicazione completata.
- **TX_TIMER_ERROR**: (0x15) Puntatore del timer dell'applicazione non valido.
- **TX_ACTIVATE_ERROR:**(0x17) Timer era già attivo o è un timer con un solo clic che è già scaduto.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_TIMER     my_timer;
UINT         status;

/* Activate an application timer. Assume that the
   application timer has already been created. */
status = tx_timer_activate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   now active. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_change"></a>tx_timer_change

Modificare il timer dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_change(TX_TIMER *timer_ptr,
                          ULONG initial_ticks, ULONG reschedule_ticks);
```
### <a name="description"></a>Descrizione

Questo servizio modifica le caratteristiche di scadenza del timer applicazione specificato. Il timer deve essere disattivato prima di chiamare questo servizio.

> [!IMPORTANT]
> Una chiamata al servizio **tx_timer_activate** è necessaria dopo questo servizio per avviare di nuovo il timer.

### <a name="parameters"></a>Parametri

- **timer_ptr:** puntatore a un blocco di controllo timer.
- **initial_ticks**: specifica il numero iniziale di tick per la scadenza del timer. I valori validi sono compreso tra 1 e 0xFFFFFFFF.
- **reschedule_ticks**: specifica il numero di tick per tutte le scadenze del timer dopo il primo. Uno zero per questo parametro rende il timer un timer unico. In caso contrario, per i timer periodici, i valori validi sono compreso tra 1 e 0xFFFFFFFF.

   > [!NOTE]
   > È necessario reimpostare un timer unico scaduto tramite tx_timer_change **prima** di poterlo attivare di nuovo.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Modifica del timer dell'applicazione riuscita.
- TX_TIMER_ERROR: (0x15) Puntatore del timer dell'applicazione non valido.
- TX_TICK_ERROR: (0x16) Valore non valido (zero) specificato per i tick iniziali.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_TIMER         my_timer;
UINT             status;

/* Change a previously created and now deactivated timer
   to expire every 50 timer ticks, including the initial
   expiration. */
status =  tx_timer_change(&my_timer,50, 50);

/* If status equals TX_SUCCESS, the specified timer is
   changed to expire every 50 ticks. */

/* Activate the specified timer to get it started again. */
status = tx_timer_activate(&my_timer);
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_create"></a>tx_timer_create

Creare un timer dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_create(TX_TIMER *timer_ptr, CHAR *name_ptr,
                          VOID (*expiration_function)(ULONG),
                          ULONG expiration_input, ULONG initial_ticks,
                          ULONG reschedule_ticks, UINT auto_activate)
```
### <a name="description"></a>Descrizione

Questo servizio crea un timer dell'applicazione con la funzione di scadenza specificata e periodica.

### <a name="parameters"></a>Parametri

- **timer_ptr:** Puntatore a un blocco di controllo timer
- **name_ptr**: puntatore al nome del timer.
- **expiration_function**: funzione dell'applicazione da chiamare alla scadenza del timer.
- **expiration_input:** input da passare alla funzione di scadenza alla scadenza del timer.
- **initial_ticks**: specifica il numero iniziale di tick per la scadenza del timer. I valori validi sono compreso tra 1 e 0xFFFFFFFF.
- **reschedule_ticks**: specifica il numero di tick per tutte le scadenze del timer dopo il primo. Uno zero per questo parametro rende il timer un timer unico. In caso contrario, per i timer periodici, i valori validi sono compreso tra 1 e 0xFFFFFFFF.

   > [!NOTE]
   > Dopo la scadenza di un timer in un solo tentativo, è necessario reimpostarlo tramite tx_timer_change prima di poter essere attivato nuovamente.

- **auto_activate**: determina se il timer viene attivato automaticamente durante la creazione. Se questo valore è **TX_AUTO_ACTIVATE** (0x01) il timer viene reso attivo. In caso contrario, **se TX_NO_ACTIVATE** (0x00) è selezionato, il timer viene creato in uno stato non attivo. In questo caso, è necessaria **_tx_timer_activate_** chiamata al servizio per ottenere il timer effettivamente avviato.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Creazione timer applicazione completata.
- TX_TIMER_ERROR: (0x15) Puntatore del timer dell'applicazione non valido. Il puntatore è NULL o il timer è già stato creato.
- TX_TICK_ERROR: (0x16) Valore non valido (zero) specificato per i tick iniziali.
- TX_ACTIVATE_ERROR: (0x17) Attivazione non valida selezionata.
- TX_CALLER_ERROR: (0x13) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_TIMER     my_timer;
UINT         status;

/* Create an application timer that executes
   "my_timer_function" after 100 ticks initially and then
   after every 25 ticks. This timer is specified to start
   immediately! */
status =  tx_timer_create(&my_timer,"my_timer_name",
                my_timer_function, 0x1234, 100, 25,
                TX_AUTO_ACTIVATE);

/* If status equals TX_SUCCESS, my_timer_function will
   be called 100 timer ticks later and then called every
   25 timer ticks. Note that the value 0x1234 is passed to
   my_timer_function every time it is called. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_change
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_deactivate"></a>tx_timer_deactivate

Disattivare il timer dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_deactivate(TX_TIMER *timer_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disattiva il timer dell'applicazione specificato. Se il timer è già disattivato, questo servizio non ha alcun effetto.

### <a name="parameters"></a>Parametri 

- **timer_ptr:** puntatore a un timer dell'applicazione creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Disattivazione timer applicazione riuscita.
- TX_TIMER_ERROR: (0x15) Puntatore del timer dell'applicazione non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
TX_TIMER     my_timer;
UINT         status;

/* Deactivate an application timer. Assume that the
   application timer has already been created. */
status =  tx_timer_deactivate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   now deactivated. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_delete"></a>tx_timer_delete

Eliminare il timer dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_delete(TX_TIMER *timer_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina il timer dell'applicazione specificato.

> [!IMPORTANT]
> È responsabilità dell'applicazione impedire l'uso di un timer eliminato.

### <a name="parameters"></a>Parametri 

- **timer_ptr:** puntatore a un timer dell'applicazione creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Eliminazione del timer dell'applicazione completata.
- TX_TIMER_ERROR: (0x15) Puntatore del timer dell'applicazione non valido.
- TX_CALLER_ERROR: (0x13) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
TX_TIMER     my_timer;
UINT         status;

/* Delete application timer. Assume that the application
   timer has already been created. */
status =  tx_timer_delete(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   deleted. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_info_get"></a>tx_timer_info_get

Recuperare informazioni su un timer dell'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_info_get(TX_TIMER *timer_ptr, CHAR **name,
                          UINT *active, ULONG *remaining_ticks,
                          ULONG *reschedule_ticks,
                          TX_TIMER **next_timer)
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul timer dell'applicazione specificato.

### <a name="parameters"></a>Parametri

- **timer_ptr:** puntatore a un timer dell'applicazione creato in precedenza.
- **name:** puntatore alla destinazione per il puntatore al nome del timer.
- **active:** puntatore alla destinazione per l'indicazione attiva del timer. Se il timer è inattivo o questo servizio viene chiamato dal timer stesso, viene restituito TX_FALSE valore predefinito. In caso contrario, se il timer è attivo, viene restituito TX_TRUE valore predefinito.
- **remaining_ticks:** puntatore alla destinazione per il numero di tick del timer rimasti prima della scadenza del timer.
- **reschedule_ticks:** puntatore alla destinazione per il numero di tick timer che verranno usati per ripianificare automaticamente il timer. Se il valore è zero, il timer è un'unica esecuzione e non verrà riprogrammato.
- **next_timer:** puntatore alla destinazione per il puntatore del timer dell'applicazione creato successivo.

> [!NOTE]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Recupero delle informazioni del timer riuscito.
- TX_TIMER_ERROR: (0x15) Puntatore del timer dell'applicazione non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
TX_TIMER     my_timer;
CHAR         *name;
UINT         active;
ULONG        remaining_ticks;
ULONG        reschedule_ticks;
TX_TIMER     *next_timer;
UINT         status;

/* Retrieve information about the previously created
   application timer "my_timer." */
status =  tx_timer_info_get(&my_timer, &name,
                          &active,&remaining_ticks,
                &reschedule_ticks,
                         &next_timer);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_performance_info_get"></a>tx_timer_performance_info_get 

Ottenere informazioni sulle prestazioni del timer

### <a name="prototype"></a>Prototipo

```C
UINT  tx_timer_performance_info_get(TX_TIMER *timer_ptr,
        ULONG *activates, ULONG *reactivates,
        ULONG *deactivates, ULONG *expirations,
        ULONG *expiration_adjusts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative al timer dell'applicazione specificato.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_TIMER_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri 

- **timer_ptr:** puntatore al timer creato in precedenza.
- **activates:** puntatore alla destinazione per il numero di richieste di attivazione eseguite su questo timer.
- **riattiva:** puntatore alla destinazione per il numero di riattivazioni automatiche eseguite su questo timer periodico.
- **deactivates:** puntatore alla destinazione per il numero di richieste di disattivazione eseguite su questo timer.
- **expirations:** puntatore alla destinazione per il numero di scadenze del timer.
- **expiration_adjusts:** puntatore alla destinazione per il numero di modifiche alla scadenza interne eseguite su questo timer. Queste modifiche vengono eseguite nell'elaborazione dell'interrupt del timer per i timer che sono maggiori delle dimensioni predefinite dell'elenco timer (per impostazione predefinita i timer con scadenze maggiori di 32 tick).

> [!IMPORTANT]
> Se si specifica un TX_NULL per qualsiasi parametro, il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS**: (0x00) Ottenere le prestazioni del timer con esito positivo.
- **TX_PTR_ERROR**: (0x03) Puntatore timer non valido.
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
TX_TIMER     my_timer;
ULONG        activates;
ULONG        reactivates;
ULONG        deactivates;
ULONG        expirations;
ULONG        expiration_adjusts;

/* Retrieve performance information on the previously created
   timer.  */
status =  tx_timer_performance_info_get(&my_timer, &activates,
                &reactivates,&deactivates, &expirations,
                &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_system_info_get

## <a name="tx_timer_performance_system_info_get"></a>tx_timer_performance_system_info_get 

Ottenere informazioni sulle prestazioni del sistema timer

### <a name="prototype"></a>Prototipo

```C
UINT  tx_timer_performance_system_info_get(ULONG *activates,
        ULONG *reactivates, ULONG *deactivates,
        ULONG *expirations, ULONG *expiration_adjusts);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle prestazioni relative a tutti i timer dell'applicazione nel sistema.

> [!IMPORTANT]
> La libreria e l'applicazione ThreadX  SMP devono essere compilate con TX_TIMER_ENABLE_PERFORMANCE_INFO per questo servizio per restituire informazioni sulle prestazioni.

### <a name="parameters"></a>Parametri

- **activates:** puntatore alla destinazione per il numero totale di richieste di attivazione eseguite su tutti i timer.
- **reactivates:** puntatore alla destinazione per il numero totale di riattivazioni automatiche eseguite su tutti i timer periodici.
- **deactivates:** puntatore alla destinazione per il numero totale di richieste di disattivazione eseguite su tutti i timer.
- **expirations:** puntatore alla destinazione per il numero totale di scadenze in tutti i timer.
- **expiration_adjusts:** puntatore alla destinazione per il numero totale di modifiche di scadenza interne eseguite su tutti i timer. Queste modifiche vengono eseguite nell'elaborazione dell'interrupt del timer per i timer di dimensioni superiori alle dimensioni predefinite dell'elenco dei timer (per impostazione predefinita i timer con scadenze maggiori di 32 tick).

> [!IMPORTANT]
> L'TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS:**(0x00) Successful timer system performance get (Prestazioni del sistema timer riuscite).
- **TX_FEATURE_NOT_ENABLED**: (0xFF) Il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="example"></a>Esempio

```C
ULONG     activates;
ULONG     reactivates;
ULONG     deactivates;
ULONG     expirations;
ULONG     expiration_adjusts;

/* Retrieve performance information on all previously created
   timers.  */
status =  tx_timer_performance_system_info_get(&activates,
                &reactivates, &deactivates, &expirations,
                &expiration_adjusts);
/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- tx_timer_activate
- tx_timer_change
- tx_timer_create
- tx_timer_deactivate
- tx_timer_delete
- tx_timer_info_get
- tx_timer_performance_info_get

## <a name="tx_timer_smp_core_exclude"></a>tx_timer_smp_core_exclude

Escludere l'esecuzione del timer in un set di core

### <a name="prototype"></a>Prototipo

```C
UINT  tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);
```
### <a name="description"></a>Descrizione

Questa funzione esclude l'esecuzione del timer specificato nei core specificati nella mappa di bit denominata "*exclusion_map*". Ogni bit in "*exclusion_map*" rappresenta un core (il bit 0 rappresenta core 0 e così via). Se il bit è impostato, il core corrispondente viene escluso dall'esecuzione del timer specificato.

> [!IMPORTANT]
> L'uso dell'esclusione del processore può causare un'elaborazione aggiuntiva nella logica di mapping tra thread e core per trovare la corrispondenza ottimale. Questa elaborazione è vincolata dal numero di thread pronti.

### <a name="parameters"></a>Parametri

- **timer_ptr:** puntatore al timer per modificare l'esclusione principale.
- **exclusion_map**: mappa di bit in cui un bit sit indica che tale core è escluso. Se si specifica un valore 0, il timer può essere eseguito su qualsiasi core (impostazione predefinita).

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Esclusione core riuscita.
- **TX_TIMER_ERROR** (0x0E) Puntatore timer non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, ISR, thread e timer

### <a name="example"></a>Esempio

```C
/* Exclude core 0 for "Timer 0". */
tx_timer_smp_core_exclude(&timer_0, 0x01);
```

### <a name="see-also"></a>Vedere anche

- tx_timer_smp_core_exclude_get

## <a name="tx_timer_smp_core_exclude_get"></a>tx_timer_smp_core_exclude_get

Ottiene l'esclusione di base corrente del timer

### <a name="prototype"></a>Prototipo

```C
UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr,
                         ULONG *exclusion_map_ptr);
```
### <a name="description"></a>Descrizione

Questa funzione restituisce l'elenco di esclusione principale corrente.

### <a name="parameters"></a>Parametri

- **timer_ptr:** puntatore al timer da cui recuperare l'esclusione principale.
- **exclusion_map_ptr:** destinazione per la mappa di bit di esclusione core corrente.

### <a name="return-values"></a>Valori restituiti

- TX_SUCCESS: (0x00) Recupero riuscito dell'esclusione principale del timer.
- TX_TIMER_ERROR: (0x0E) Puntatore timer non valido.
- TX_PTR_ERROR: (0x03) Puntatore di destinazione di esclusione non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, ISR, thread e timer

### <a name="example"></a>Esempio

```C
ULONGexcluded_cores;

/* Retrieve the core exclusion for "Timer 0". */
tx_timer_smp_core_exclude_get(&timer_0,&excluded_cores);
```
### <a name="see-also"></a>Vedere anche

- tx_timer_smp_core_exclude