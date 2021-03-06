---
title: Capitolo 4 - Descrizione dei Azure RTOS NetX Secure
description: Questo capitolo contiene una descrizione di tutti i servizi NetX Secure (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b10260778f7f5e1a5bd0a38aded2339008b066cca77f2439a5881d28a0489524
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797756"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a>Capitolo 4 - Descrizione dei Azure RTOS NetX Secure

Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX Secure (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla macro **NX_SECURE_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- [nx_secure_crypto_table_self_test](#nx_secure_crypto_table_self_test)
  - Eseguire self_test sui metodi di crittografia
- [nx_secure_module_hash_compute](#nx_secure_module_hash_compute)
  - Calcola il valore hash usando user_supplied funzione hash
- [nx_secure_tls_active_certificate_set](#nx_secure_tls_active_certificate_set)
  - Impostare il certificato di identità attivo per una sessione TLS protetta di NetX
- [nx_secure_tls_client_psk_set](#nx_secure_tls_client_psk_set)
  - Impostare una chiave Pre_Shared per una sessione client TLS protetta di NetX
- [nx_secure_tls_initialize](#nx_secure_tls_initialize)
  - Inizializza il modulo NetX Secure TLS]
- [nx_secure_tls_local_certificate_add](#nx_secure_tls_local_certificate_add)
  - Aggiungere un certificato locale alla sessione TLS protetta di NetX
- [nx_secure_tls_local_certificate_find](#nx_secure_tls_local_certificate_find)
  - Trovare un certificato locale in una sessione TLS sicura NetX in base al nome comune
- [nx_secure_tls_local_certificate_remove](#nx_secure_tls_local_certificate_remove)
  - Rimuovere il certificato locale dalla sessione TLS protetta di NetX
- [nx_secure_tls_metadata_size_calculate](#nx_secure_tls_metadata_size_calculate)
  - Calcolare le dimensioni dei metadati crittografici per una sessione TLS sicura di NetX
- [nx_secure_tls_packet_allocate](#nx_secure_tls_packet_allocate)
  - Allocare un pacchetto per una sessione TLS protetta NetX
- [nx_secure_tls_psk_add](#nx_secure_tls_psk_add)
  - Aggiungere una Pre_Shared chiave a una sessione TLS protetta di NetX
- [nx_secure_tls_remote_certificate_allocate](#nx_secure_tls_remote_certificate_allocate)
  - Allocare spazio per il certificato fornito da un host TLS remoto
- [nx_secure_tls_remote_certificate_buffer_allocate](#nx_secure_tls_remote_certificate_buffer_allocate)
  - Allocare spazio per tutti i certificati forniti da un host TLS remoto
- [nx_secure_tls_remote_certificate_free_all](#nx_secure_tls_remote_certificate_free_all)
  - Spazio disponibile allocato per i certificati in ingresso
- [nx_secure_tls_server_certificate_add](#nx_secure_tls_server_certificate_add)
  - Aggiungere un certificato specifico per i server TLS usando un identificatore numerico
- [nx_secure_tls_server_certificate_find](#nx_secure_tls_server_certificate_find)
  - Trovare un certificato usando un identificatore numerico
- [nx_secure_tls_server_certificate_remove](#nx_secure_tls_server_certificate_remove)
  - Rimuovere un certificato del server locale usando un identificatore numerico
- [nx_secure_tls_session_certificate_callback_set](#nx_secure_tls_session_certificate_callback_set)
  - Configurare un callback per TLS da usare per la convalida aggiuntiva del certificato
- [nx_secure_tls_session_client_callback_set](#nx_secure_tls_session_client_callback_set)
  - Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS
- [nx_secure_tls_session_x509_client_verify_configure](#nx_secure_tls_session_x509_client_verify_configure)
  - Abilitare la verifica X.509 del client e allocare spazio per i certificati client
- [nx_secure_tls_session_client_verify_disable](#nx_secure_tls_session_client_verify_disable)
  - Disabilitare l'autenticazione del certificato client per una sessione TLS protetta NetX
- [nx_secure_tls_session_client_verify_enable](#nx_secure_tls_session_client_verify_enable)
  - Abilitare l'autenticazione del certificato client per una sessione TLS protetta NetX
- [nx_secure_tls_session_create](#nx_secure_tls_session_create)
  - Creare una sessione TLS sicura NetX per le comunicazioni protette
- [nx_secure_tls_session_delete](#nx_secure_tls_session_delete)
  - Eliminare una sessione TLS protetta di NetX
- [nx_secure_tls_session_end](#nx_secure_tls_session_end)
  - Terminare una sessione TLS protetta di NetX attiva
- [nx_secure_tls_session_packet_buffer_set](#nx_secure_tls_session_packet_buffer_set)
  - Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS protetta di NetX
- [nx_secure_tls_session_protocol_version_override](#nx_secure_tls_session_protocol_version_override)
  - Eseguire l'override della versione predefinita del protocollo TLS per una sessione TLS protetta di NetX
- [nx_secure_tls_session_receive](#nx_secure_tls_session_receive)
  - Ricevere dati da una sessione TLS protetta di NetX
- [nx_secure_tls_session_renegotiate_callback_set](#nx_secure_tls_session_renegotiate_callback_set)
  - Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione
- [nx_secure_tls_session_renegotiate](#nx_secure_tls_session_renegotiate)
  - Avviare un handshake di rinegoziazione della sessione con l'host remoto
- [nx_secure_tls_session_reset](#nx_secure_tls_session_reset)
  - Cancellare e reimpostare una sessione TLS protetta di NetX
- [nx_secure_tls_session_send](#nx_secure_tls_session_send)
  - Inviare dati tramite una sessione TLS protetta di NetX
- [nx_secure_tls_session_server_callback_set](#nx_secure_tls_session_server_callback_set)
  - Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS
- [nx_secure_tls_session_sni_extension_parse](#nx_secure_tls_session_sni_extension_parse)
  - Analizzare un'Indicazione nome server (SNI) ricevuta da un client TLS
- [nx_secure_tls_session_sni_extension_set](#nx_secure_tls_session_sni_extension_set)
  - Impostare un Indicazione nome server DNS dell'estensione SNI da inviare a un server remoto
- [nx_secure_tls_session_start](#nx_secure_tls_session_start)
  - Avviare una sessione TLS protetta di NetX
- [nx_secure_tls_session_time_function_set](#nx_secure_tls_session_time_function_set)
  - Assegnare una funzione timestamp a una sessione TLS sicura netx
- [nx_secure_tls_trusted_certificate_add](#nx_secure_tls_trusted_certificate_add)
  - Aggiungere un certificato attendibile alla sessione TLS protetta di NetX
- [nx_secure_tls_trusted_certificate_remove](#nx_secure_tls_trusted_certificate_remove)
  - Rimuovere un certificato attendibile dalla sessione TLS protetta di NetX
- [nx_secure_x509_certificate_initialize](#nx_secure_x509_certificate_initialize)
  - Inizializzare il certificato X.509 per NetX Secure TLS
- [nx_secure_x509_common_name_dns_check](#nx_secure_x509_common_name_dns_check)
  - Controllare il nome DNS rispetto al certificato X.509
- [nx_secure_x509_crl_revocation_check](#nx_secure_x509_crl_revocation_check)
  - Controllare il certificato X.509 rispetto a un elenco di revoche di certificati (CRL) fornito]
- [nx_secure_x509_dns_name_initialize](#nx_secure_x509_dns_name_initialize)
  - Inizializzare una struttura dei nomi DNS X.509
- [nx_secure_x509_extended_key_usage_extension_parse](#nx_secure_x509_extended_key_usage_extension_parse)
  - Trovare e analizzare un'estensione X.509 estesa per l'utilizzo delle chiavi in un certificato X.509
- [nx_secure_x509_extension_find](#nx_secure_x509_extension_find)
  - Trovare e restituire un'estensione X.509 in un certificato X.509
- [nx_secure_x509_key_usage_extension_parse](#nx_secure_x509_key_usage_extension_parse)
  - Trovare e analizzare un'estensione X.509 Key Usage in un certificato X.509

## <a name="nx_secure_crypto_table_self_test"></a>nx_secure_crypto_table_self_test

Eseguire il test self-test sui metodi di crittografia

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a>Descrizione

Questo servizio viene eseguito tramite i test self-test del metodo di crittografia per la convalida. Il test self-service è disponibile solo se la libreria NetX Secure viene compilata con il simbolo NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK definito.

Per ogni metodo di crittografia supportato, il test self-service fornisce dati di input predefiniti e verifica che l'output corrisponda al valore previsto predefinito.

NetX Secure Crypto Self Test supporta gli algoritmi e le dimensioni delle chiavi seguenti:

- DES: crittografia e decrittografia
- Triple DES (3DES): crittografia e decrittografia
- AES: 128, 192, dimensioni della chiave a 256 bit, crittografia e decrittografia, in modalità CBC e modalità contatore.
- HMAC-MD5: autenticazione e calcolo hash
- HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, autenticazione e calcolo hash
- MD5: autenticazione
- Funzione pseudo-casuale (PRF): PRF_HMAC_SHA1 e PRF_HMAC_SHA2-256
- RSA: operazione di power-modulus RSA a 1024, 2048 e 4096 bit
- SHA: autenticazione SHA1 (96 e 160 bit), SHA2 (256 bit, 384 bit, 512 bit)

Questa funzione include i vettori predefiniti per gli algoritmi di crittografia elencati in precedenza. Tuttavia, verifica solo quelli elencati nella *cipher_table* passati a questa funzione. Ad esempio, per una sessione TLS usa solo il TLS_RSA_WITH_AES_128_CBC_SHA ciphersuite, questa funzione eseguirà test self-service su RSA (1024, 2048, 4096 bit), AES-CBC (128 bit) e SHA1.

### <a name="parameters"></a>Parametri

- **crypto_table** Puntatore alla tabella di crittografia usata dalla sessione TLS. Si tratta dello stesso crypto_table passato alla **_chiamata nx_secure_tls_session_create()._**
- **metadati** Puntatore allo spazio per l'area dei metadati di crittografia. .
- **metadata_size** Dimensioni del buffer dei metadati.

### <a name="return-values"></a>Valori restituiti

- **NX_SECURE_TLS_SUCCESS** (0x00) Sono stati testati correttamente i metodi di crittografia forniti.
- **NX_PTR_ERROR** (0x07) Struttura del metodo di crittografia non valida
- **NX_NOT_SUCCESSFUL** (0x43) Il test self-test della crittografia ha esito negativo.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* crypto_tls_ciphers is the cipher table for the TLS session. */
/* metadata_buffer is the memory area used by the cipher functions. */

/* The following function verifies the supplied ciphersuties using the built-in
   self test. */

if (nx_secure_crypto_table_self_test(&crypto_tls_ciphers, metadata_buffer,
    sizeof(metadata_buffer)))
{
    printf("Crypto self test failed!\r\n");
    exit(0);
}
else
{
    printf("Crypto self test succeed!\r\n");
}

/* Now the ciphersuites are successfully test, it can be used in
   nx_secure_tls_session_create() */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_module_hash_compute"></a>nx_secure_module_hash_compute

Calcola il valore hash usando la funzione hash fornita dall'utente

### <a name="prototype"></a>Prototipo

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a>Descrizione

Questa funzione calcola il valore hash del flusso di dati nell'area di memoria specificata, usando il metodo di crittografia HMAC fornito e la stringa di chiave. La funzione di calcolo hash del modulo è disponibile solo se la libreria NetX Secure viene compilata con il simbolo seguente definito: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK

### <a name="parameters"></a>Parametri

- **hmac_ptr** Puntatore al metodo di crittografia HMAC usato per il calcolo del valore hash.
- **start_address** Indirizzo iniziale del buffer di dati
- **end_address** Indirizzo finale del buffer di dati. Si noti che il calcolo hash non copre i dati in questa end_address.
- **chiave** Stringa chiave usata nel calcolo HMAC.
- **key_length** Dimensioni della stringa di chiave, in byte
- **metadati** Puntatore allo spazio utilizzato dall'algoritmo HMAC.
- **metadata_size** Dimensioni del buffer dei metadati.
- **output_buffer** Posizione di memoria in cui viene archiviato l'output hash.
- **output_buffer_size** Spazio disponibile del buffer di output, in byte
- **actual_size** Restituito dalla funzione che indica il numero effettivo di byte scritti nel output_buffer.

### <a name="return-values"></a>Valori restituiti

- **0 Il** valore hash è stato calcolato correttamente.
- **1 Il** calcolo dell'hash non è riuscito.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Define the HMAC SHA256 method */
NX_CRYPTO_METHOD hmac_sha256 =
{
    NX_CRYPTO_AUTHENTICATION_HMAC_SHA2_256,    /* HMAC SHA256 algorithm  */
    0,                                         /* Key size, not used     */
    0,                                         /* IV size, not used      */
    NX_CRYPTO_HMAC_SHA256_ICV_FULL_LEN_IN_BITS,/* Transmitted ICV size   */
    NX_CRYPTO_SHA2_BLOCK_SIZE_IN_BYTES,        /* Block size in bytes    */
    sizeof(NX_CRYPTO_SHA256_HMAC),             /* Metadata size in bytes */
    _nx_crypto_method_hmac_sha256_init,        /* HMAC SHA256 init       */
    _nx_crypto_method_hmac_sha256_cleanup,     /* HMAC SHA256 cleanup    */
    _nx_crypto_method_hmac_sha256_operation    /* HMAC SHA256 operation  */
};

/* Define the hash key being used. */
const CHAR hash_key = “my hash key”;

/* Define starting address. */
UINT starting_address = 0x10000;

/* Define the ending address.
   Note that the hash computation covers the memory location
   before the ending address. */
UINT ending_address = 0x11000;

/* Declare the output buffer. */
#define OUTPUT_BUFFER_SIZE
UCHAR output_buffer[OUTPUT_BUFFER_SIZE];

UINT actual_size;

/* Declare 1K bytes of metadata buffer area. */
UCHAR metadata_buffer[1024];

/* Compute the hash value of the data between 0x10000 – 0x10FFF */
nx_secure_module_hash_compute(&hmac_sha256,
                              starting_address, ending_address,
                              hash_key, strlen(hash_key),
                              metadata_buffer, sizeof(metadata_buffer),
                              output_buffer, OUTPUT_BUFFER_SIZE, &actual_size);

/* If this function returns “0”, the hash value has been computed and is stored
   in output_buffer. */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_crypto_method_self_test

## <a name="nx_secure_tls_active_certificate_set"></a>nx_secure_tls_active_certificate_set

Impostare il certificato di identità attivo per una sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a>Descrizione

Questo servizio deve essere chiamato dall'interno di un callback di sessione (vedere nx_secure_tls_session_client_callback_set e nx_secure_tls_session_server_callback_set). Quando viene chiamato con una struttura NX_SECURE_X509_CERT inizializzata in precedenza, tale certificato verrà usato al posto del certificato di identità predefinito. Nella maggior parte dei casi, il certificato deve essere stato aggiunto all'archivio locale (vedere nx_secure_tls_local_certificate_add) o l'handshake TLS potrebbe non riuscire.

Questo servizio è progettato per consentire a TLS di supportare più certificati di identità. Ciò è utile per un server TLS che fornisce più indirizzi di rete in modo che il server possa scegliere un certificato appropriato da fornire al client remoto a seconda del punto di ingresso del client. Per un client TLS, questa routine può essere usata per modificare il certificato inviato a un server remoto in fase di esecuzione dopo che il server si è identificato nell'handshake TLS (questo caso è più raro del caso d'uso del server TLS).

Nel caso in cui più certificati possano condividere lo stesso nome distinto X.509, i certificati dovranno essere aggiunti usando nx_secure_tls_server_certificate_add, che introduce un identificatore numerico separato dal certificato.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS passata nel callback di sessione.
- **certificato** Puntatore a un certificato X.509 inizializzato che deve essere usato per la sessione corrente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Assegnazione del certificato alla sessione completata.
- **NX_PTR_ERROR** (0x07) Puntatore di certificato o sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define TLS_SNI_SERVER_NAME “www.example.com”
#define TLS_DEFAULT_SERVER_CERT_ID 2
#define TLS_EXAMPLE_CERT_ID 3


/* Callback for ClientHello extensions processing. */
static ULONG tls_server_callback(NX_SECURE_TLS_SESSION *tls_session,
                                 NX_SECURE_TLS_HELLO_EXTENSION *extensions,
                                 UINT num_extensions)
{
NX_SECURE_X509_DNS_NAME dns_name;
INT compare_value;
UINT status;
NX_SECURE_X509_CERT *cert_ptr;

    /* Grab a pointer to our default certificate in case the SNI extension is not
       available or the specified server name is unknown. */
    nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                     TLS_DEFAULT_SERVER_CERT_ID);


    /* Process Server Name Indication extension. */
    status = _nx_secure_tls_session_sni_extension_parse(tls_session, extensions,
                                                    num_extensions, &dns_name);

    /* If no extension found, that is OK. Use default certificate. */
    if(status == NX_SUCCESS)
    {
          /* SNI extension found, select an active certificate based on the server
             name. */

          /* Make sure our SNI name matches. */
          compare_value = memcmp(dns_name.nx_secure_x509_dns_name,
                                TLS_SNI_SERVER_NAME, strlen(TLS_SNI_SERVER_NAME));

          if(compare_value == 0 && dns_name.nx_secure_x509_dns_name_length !=
             strlen(TLS_SNI_SERVER_NAME))
          {
             /* Found a match, find the certificate we want to use. */
             _nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                                      TLS_EXAMPLE_CERT_ID);
          }
          else
          {
             /* No matching server name found. The application may choose to simply
                provide the default certificate (and probably resulting in an error
                in the remote client) or returning an error here to end the
                handshake. A user-defined non-zero error code will be sufficient –
                the error code will abort the TLS handshake and be returned to the
                caller that started the server. */
                return(0x500);
          }
      }
      else
      {
      }
      /* Set the certificate we want to use. */
      nx_secure_tls_active_certificate_set(tls_session, cert_ptr);

      /* Return success to continue TLS handshake. */
      return(NX_SUCCESS);
}

/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_TLS_SESSION server_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&server_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_tls_session_create: 0x%x\n", status);
    }

    /* Setup our packet reassembly buffer. See
       nx_secure_tls_session_packet_buffer_set for more information. */
    nx_secure_tls_session_packet_buffer_set(&server_tls_session,
                                      server_packet_buffer,
                                      sizeof(server_packet_buffer));


    /* Set callback for server TLS extension handling. */
    _nx_secure_tls_session_server_callback_set(&server_tls_session,
                                              tls_server_callback);

    /* Initialize our certificates – certificate data defined elsewhere. See
       section “Importing X.509 Certificates into NetX Secure” for more
       information. */
    nx_secure_x509_certificate_initialize(&default_certificate,
                                      default_cert_der,
                                      default _cert_der_len, NX_NULL, 0,
                                      default_cert_key_der,
                                      default_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &default_certificate,
                                         TLS_DEFAULT_SERVER_CERT_ID);

    /* Alternative identity certificate, needs to have a private key! */
    nx_secure_x509_certificate_initialize(&example_certificate,
                                      example_cert_der,
                                      example cert_der_len, NX_NULL, 0,
                                      example_cert_key_der,
                                      example_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &example_certificate,
                                         TLS_EXAMPLE_CERT_ID);

    /* Now we can start the TLS session as normal. */
       …
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_session_server_callback_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find
- nx_secure_tls_server_certificate_remove

## <a name="nx_secure_tls_client_psk_set"></a>nx_secure_tls_client_psk_set

Impostare una chiave precondi shared per una sessione client TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una chiave precondi shared (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo sessione TLS e imposta tale chiave PSK da usare nelle connessioni client TLS successive. La chiave PSK viene usata al posto di un certificato digitale quando le ciphersuit PSK sono abilitate e usate.

In questo caso, la chiave PSK è associata a un server TLS remoto specifico con cui il client TLS vuole comunicare. La chiave PSK impostata tramite questa API verrà fornita all'host del server TLS remoto durante il successivo handshake TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **pre_shared_key** Valore PSK effettivo.
- **psk_length** Lunghezza del valore PSK.
- **psk_identity** Stringa usata per identificare questo valore PSK.
- **identity_length** Lunghezza dell'identità PSK.
- **hint** Stringa usata per indicare il gruppo di psk tra cui scegliere in un server TLS.
- **hint_length** Lunghezza della stringa di hint.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta corretta di PSK.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Impossibile aggiungere un'altra chiave PSK.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_psk_add
- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_initialize"></a>nx_secure_tls_initialize

Inizializza il modulo NetX Secure TLS

### <a name="prototype"></a>Prototipo

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza il modulo NetX Secure TLS. Deve essere chiamato prima che sia possibile accedere ad altri servizi NetX Secure.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

Nessuno

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_tls_local_certificate_add"></a>nx_secure_tls_local_certificate_add

Aggiungere un certificato locale alla sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza della NX_SECURE_X509_CERT inizializzata all'archivio locale di una sessione TLS. Questo certificato può essere usato dallo stack TLS per identificare il dispositivo durante l'handshake TLS (se è stato contrassegnato come certificato di identità durante l'inizializzazione della struttura del certificato usando nx_secure_x509_certificate_initialize) o come autorità di certificazione come parte di una catena di certificati fornita all'host remoto durante l'handshake TLS.

Se sono necessari più certificati locali con lo stesso nome comune, è possibile aggiungere certificati usando il *servizio nx_secure_tls_server_certificate_add* (vedere l'avviso seguente).

Per la modalità server TLS **è** necessario un certificato.

Un certificato è *facoltativo* per la modalità client TLS.

> [!IMPORTANT]
> *Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API del certificato server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add indici basati sul nome comune X.509. I servizi certificati locali offrono un'alternativa pratica all'identificatore numerico per le applicazioni che usano un solo certificato di identità. Usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificate_ptr** Puntatore a un'istanza del certificato TLS inizializzata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato completata.
- **NX_INVALID_PARAMETERS** (0x4D) Tentativo di aggiunta di un certificato non valido o duplicato.
- **NX_PTR_ERROR** (0x07) Puntatore di certificato o sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_local_certificate_find

## <a name="nx_secure_tls_local_certificate_find"></a>nx_secure_tls_local_certificate_find

Trovare un certificato locale in una sessione TLS sicura NetX in base al nome comune

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a>Descrizione

Questo servizio trova un certificato nell'archivio certificati del dispositivo locale di una sessione TLS e restituisce un puntatore alla struttura NX_SECURE_X509_CERT nell'archivio. Il common_name e la lunghezza (name_length) vengono usati per identificare il certificato nell'archivio abbinando il campo Nome comune soggetto X.509 del certificato.

Se sono presenti più certificati con lo stesso nome comune, verrà restituito solo il primo. Usare *nx_secure_tls_server_certificate_find.*

> [!IMPORTANT]
> *Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API del certificato server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add indici basati sul nome comune X.509. I servizi certificati locali offrono un'alternativa pratica all'identificatore numerico per le applicazioni che usano un solo certificato di identità. Usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificato** Restituisce Puntatore al certificato corrispondente.
- **common_name** Stringa del nome comune di cui trovare la corrispondenza (nome DNS).
- **name_length** Lunghezza dei common_name stringa.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** certificato (0x00) trovato e puntatore restituito nel parametro "certificate".
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Non è stato trovato alcun certificato con il nome comune specificato.
- **NX_PTR_ERROR** (0x07) Sessione TLS, puntatore al certificato o stringa di nome comune non valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_SECURE_X509_CERT *certificate_ptr;

/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */

status = nx_secure_tls_local_certificate_find(&tls_session, &certificate_ptr,
                                      “common name”, strlen(“common name”));

/* If status is NX_SUCCESS the variable “certificate_ptr” points to a certificate
   structure containing a certificate with the Common Name “common name”. */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_local_certificate_remove"></a>nx_secure_tls_local_certificate_remove

Rimuovere il certificato locale dalla sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un'istanza del certificato locale da una sessione TLS, con chiave nel campo Nome comune nel certificato.

> [!IMPORTANT]
> *Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API del certificato server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add indici basati sul nome comune X.509. I servizi certificati locali offrono un'alternativa pratica all'identificatore numerico per le applicazioni che usano un solo certificato di identità. Usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **common_name** Valore common name del certificato da rimuovere.
- **common_name_length** Lunghezza della stringa Common Name.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato completata.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Il certificato non è stato trovato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_metadata_size_calculate"></a>nx_secure_tls_metadata_size_calculate

Calcolare le dimensioni dei metadati crittografici per una sessione TLS sicura di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a>Descrizione

Questo servizio calcola e restituisce le dimensioni dei metadati crittografici necessari per una particolare sessione TLS e una tabella di crittografia TLS (vedere la sezione "Inizializzazione di TLS con metodi di crittografia" per altre informazioni sulla tabella di crittografia).

Questo servizio deve essere chiamato con la tabella crittografica desiderata per calcolare le dimensioni del buffer dei metadati passato nx_secure_tls_session_create.

### <a name="parameters"></a>Parametri

- **crypto_table** Puntatore a una tabella di crittografia NetX Secure TLS completa.
- **metadata_size** Output del calcolo delle dimensioni in byte.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Calcolo delle dimensioni dei metadati riuscito.
- **NX_PTR_ERROR** (0x07) Tabella di crittografia non valida o puntatore alle dimensioni restituite.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Return variable for metadata size. */
ULONG crypto_metadata_size;

/* Calculate metadata size.  */
status =  nx_secure_tls_metadata_size_calculate(&nx_crypto_tls_ciphers,
                                                &crypto_metadata_size);


/* If status is NX_SUCCESS then crypto_metadata_size contains the size of the
   metadata buffer for the table nx_crypto_tls_ciphers.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create

## <a name="nx_secure_tls_packet_allocate"></a>nx_secure_tls_packet_allocate

Allocare un pacchetto per una sessione TLS protetta NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio alloca un NX_PACKET per la sessione TLS attiva specificata dal NX_PACKET_POOL. Questo servizio deve essere chiamato dall'applicazione per allocare pacchetti di dati da inviare tramite una connessione TLS. La sessione TLS deve essere inizializzata prima di chiamare questo servizio.

Il pacchetto allocato viene inizializzato correttamente in modo che i dati di intestazione e piè di pagina TLS possano essere aggiunti dopo che i dati del pacchetto sono stati popolati. In caso contrario, il comportamento è identico *nx_packet_allocate*.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **pool_ptr** Puntatore a un NX_PACKET_POOL da cui allocare il pacchetto.
- **packet_ptr** Puntatore di output al pacchetto appena allocato.
- **wait_option** Opzione di sospensione per l'allocazione di pacchetti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'allocazione dei pacchetti è riuscita.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) L'allocazione dei pacchetti sottostante non è riuscita.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_psk_add"></a>nx_secure_tls_psk_add

Aggiungere una chiave precondicondita a una sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una chiave precondi shared (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo sessione TLS. La chiave PSK viene usata al posto di un certificato digitale quando le ciphersuit PSK sono abilitate e usate.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **pre_shared_key** Valore PSK effettivo.
- **psk_length** Lunghezza del valore PSK.
- **psk_identity** Stringa usata per identificare questo valore PSK.
- **identity_length** Lunghezza dell'identità PSK.
- **hint** Stringa usata per indicare il gruppo di psk tra cui scegliere in un server TLS.
- **hint_length** Lunghezza della stringa di hint.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta corretta di PSK.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Impossibile aggiungere un'altra chiave PSK.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_client_psk_set
- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_local_certificate_add

## <a name="nx_secure_tls_remote_certificate_allocate"></a>nx_secure_tls_remote_certificate_allocate

Allocare spazio per il certificato fornito da un host TLS remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza della NX_SECURE_X509_CERT non inizializzata a una sessione TLS allo scopo di allocare spazio per i certificati forniti da un host remoto durante una sessione TLS. I dati del certificato remoto vengono analizzati da NetX Secure TLS e tali informazioni vengono usate per popolare l'istanza della struttura di certificati fornita a questa funzione. I certificati aggiunti in questo modo vengono inseriti in un elenco collegato.

Se si prevede che l'host remoto fornirà più certificati, questa funzione deve essere chiamata ripetutamente per allocare spazio per tutti i certificati. I certificati aggiuntivi vengono aggiunti alla fine dell'elenco di certificati collegati.

Se non si alloca un certificato remoto, la modalità client TLS avrà esito negativo durante l'handshake TLS, a meno che non sia in uso una crittografia PSK (Pre-Shared Key).

Il *raw_certificate_buffer* punta allo spazio allocato per archiviare il certificato remoto in ingresso. I certificati tipici con chiavi RSA a 2048 bit che usano SHA-256 per le firme sono nell'intervallo tra 1000 e 2000 byte. Il buffer deve essere sufficientemente grande da contenere almeno tale dimensione, ma a seconda dei certificati host remoti può essere notevolmente più piccolo o più grande. Si noti che se il buffer è troppo piccolo per contenere il certificato in ingresso, l'handshake TLS terminerà con un errore.

Per la modalità server TLS, è necessaria un'allocazione remota del certificato solo se è abilitata l'autenticazione del certificato client.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificate_ptr** Puntatore a un'istanza del certificato X.509 non inizializzata.
- **raw_certificate_buffer** Puntatore a un buffer per contenere il certificato non analizzato ricevuto dall'host remoto.
- **raw_buffer_size** Dimensione del buffer del certificato non elaborato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione del certificato.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Il buffer fornito era troppo piccolo.
- **NX_INVALID_PARAMETERS** (0x4D) Tentativo di aggiungere un certificato non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize,
- nx_secure_tls_session_create

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a>nx_secure_tls_remote_certificate_buffer_allocate

Allocare spazio per tutti i certificati forniti da un host TLS remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio alloca spazio per elaborare le catene di certificati in ingresso dagli host server remoti per eseguire l'autenticazione e la verifica X.509 in un'istanza del client TLS. Per la modalità server TLS, l'allocazione remota dei certificati è necessaria solo se  è abilitata l'autenticazione del certificato X.509 client. Per le istanze del server TLS è necessario usare nx_secure_tls_session_x509_client_verify_configure servizio.

Se non si allocano certificati remoti, la modalità client TLS avrà esito negativo durante l'handshake TLS, a meno che non sia in uso una crittografia PSK (Pre-Shared Key).

Il *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati. Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale a ogni certificato. Il *buffer_size*  parametro indica le dimensioni del buffer. Lo spazio necessario è disponibile con la formula seguente:

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

I certificati tipici con chiavi RSA a 2048 bit che usano SHA-256 per le firme sono nell'intervallo tra 1000 e 2000 byte. Il buffer deve essere sufficientemente grande da contenere almeno le dimensioni per ogni certificato, ma a seconda dei certificati host remoti può essere notevolmente più piccolo o più grande. Si noti che se il buffer è troppo piccolo per contenere il certificato in ingresso, l'handshake TLS terminerà con un errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certs_number** Numero di certificati da allocare dal buffer fornito.
- **certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.
- **buffer_size** Dimensioni del buffer del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione del certificato.
- **NX_PTR_ERROR** (0x07) Puntatore di buffer o sessione TLS non valido.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Il buffer fornito era troppo piccolo.
- **NX_INVALID_PARAMETERS** (0x4D) Il buffer era troppo piccolo per contenere il numero desiderato di certificati.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE           (CERTIFICATE_NUMBER * \
                              (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_buffer_allocate(&tls_session,
                                                      CERTIFICATE_NUMBER,
                                                      certificate_buffer,
                                                      BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create

## <a name="nx_secure_tls_remote_certificate_free_all"></a>nx_secure_tls_remote_certificate_free_all

Spazio disponibile allocato per i certificati in ingresso

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per liberare tutti i buffer del certificato allocati a una sessione TLS specifica nx_secure_tls_remote_certificate_allocated tramite la restituzione nello spazio del certificato disponibile della sessione. Questa operazione può essere necessaria se un'applicazione riutilizza un oggetto sessione TLS senza eliminarlo e ricrearlo con nx_secure_tls_session_delete e nx_secure_tls_session_create.

Si noti che lo spazio del certificato remoto viene recuperato automaticamente quando la sessione TLS viene reimpostata come accade nx_secure_tls_session_end quindi la maggior parte delle applicazioni non deve chiamare questo servizio.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_INVALID_PARAMETERS** (0x4D) Errore interno: è probabile che l'archivio certificati sia danneggiato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */

/* … TLS session setup, TCP connection, etc… */

/* End TLS session. */
nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

/* Free up certificate buffers for next connection. */
nx_secure_tls_remote_certificate_free_all(&tls_session);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_end

## <a name="nx_secure_tls_server_certificate_add"></a>nx_secure_tls_server_certificate_add

Aggiungere un certificato specifico per i server TLS usando un identificatore numerico

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per aggiungere un certificato all'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X.509 (nome comune) all'interno del certificato. L'identificatore numerico è separato dal certificato e consente di aggiungere più certificati come certificati di identità a un server TLS, nonché di aggiungere più certificati con lo stesso nome comune allo stesso archivio locale della sessione TLS. Questo stesso servizio può essere usato per i certificati client, ma è raro che un client TLS abbia più certificati di identità.

Il cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione. Il valore effettivo non è importante (diverso da zero), ma deve essere univoco nell'archivio per la sessione TLS fornita. Il cert_id può essere usato per trovare e rimuovere certificati dall'archivio locale usando nx_secure_tls_server_certificate_find e nx_secure_tls_server_certificate_remove, rispettivamente.

> [!IMPORTANT]
> *Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L nx_secure_tls_server_certificate_add API usa un identificatore numerico univoco per ogni certificato e l'indice dei servizi certificati locali in base al nome comune X.509. I servizi certificati server consentono l'esistenza di più certificati con dati condivisi (in particolare nome comune) nello stesso archivio locale. Ciò è utile per un server con più identità.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificato** Puntatore a un'istanza del certificato X.509 inizializzata in precedenza.
- **cert_id** Numero DI ID certificato positivo, diverso da zero e relativamente univoco.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00)Operazione riuscita.
- **NX_PTR_ERROR** (0x07) Sessione TLS o puntatore del certificato non valido.
- **NX_SECURE_TLS_CERT_ID_INVALID** (0x138) L'ID certificato specificato ha un valore non valido (probabilmente 0).
- **NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) L'ID certificato specificato era già presente nell'archivio locale.
- **NX_INVALID_PARAMETERS(0x4D)** Errore interno: è probabile che l'archivio certificati sia danneggiato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_find
- nx_secure_tls_server_certificate_remove

## <a name="nx_secure_tls_server_certificate_find"></a>nx_secure_tls_server_certificate_find

Trovare un certificato usando un identificatore numerico

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per trovare un certificato nell'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico invece di indicizzare l'archivio usando il soggetto X.509 (nome comune) all'interno del certificato.

Il cert_id è un intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS usando nx_secure_tls_server_certificate_add.

> [!IMPORTANT]
> *Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L nx_secure_tls_server_certificate_add API usa un identificatore numerico univoco per ogni certificato e l'indice dei servizi certificati locali in base al nome comune X.509. I servizi certificati server consentono l'esistenza di più certificati con dati condivisi (in particolare nome comune) nello stesso archivio locale. Ciò è utile per un server con più identità.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificato** Puntatore a un puntatore al certificato X.509 per restituire un riferimento al certificato trovato.
- **cert_id** Valore ID certificato positivo diverso da zero.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00)Operazione riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore di certificato o sessione TLS non valido.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) L'ID certificato specificato non corrisponde ad alcuno nell'archivio locale della sessione TLS fornita.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_remove

##  <a name="nx_secure_tls_server_certificate_remove"></a>nx_secure_tls_server_certificate_remove

Rimuovere un certificato del server locale usando un identificatore numerico

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per rimuovere un certificato dall'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X.509 (nome comune) all'interno del certificato.

Il cert_id è un intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS usando nx_secure_tls_server_certificate_add.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **cert_id** Valore ID certificato positivo diverso da zero.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00)Operazione riuscita.
- **NX_PTR_ERROR** (0x07) Sessione TLS non valida.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) L'ID certificato specificato non corrisponde ad alcuno nell'archivio locale della sessione TLS fornita.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);
/* Use certificate in TLS session, etc… */

/* Remove certificate from TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_remove(&tls_session, 0x12);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_active_certificate_set
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find

## <a name="nx_secure_tls_session_alert_value_get"></a>nx_secure_tls_session_alert_value_get

Ottenere il valore e il livello di avviso TLS inviati dall'host remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato per recuperare il livello e il valore di avviso TLS quando l'host remoto invia un avviso in risposta a un problema o a un errore.

I valori dei parametri alert_level e alert_value sono validi solo se questa funzione viene chiamata immediatamente dopo una chiamata API TLS che ha restituito lo stato NX_SECURE_TLS_ALERT_RECEIVED (0x114) che indica che è stato ricevuto un avviso dall'host remoto.

Si noti che se l'host locale TLS invia un avviso, i codici di errore restituiti sono molto più descrittivi dell'errore effettivo rispetto all'avviso TLS stesso perché i valori di avviso TLS vengono intenzionalmente lasciati ambigui per impedire determinati tipi di attacco (ad esempio un attacco "oracolo di riempimento" o simili).

Il livello di avviso accetta solo uno dei due valori seguenti: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) o NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2). In generale, solo l'avviso CloseNotify (usato per indicare un esito positivo di una sessione TLS) riceverà un livello di "Avviso", anche se alcune situazioni di configurazione dell'estensione possono anche essere considerate avvisi. La maggior parte degli avvisi sarà "Fatal" che indica un potenziale errore di sicurezza e determina la chiusura immediata della connessione TLS (handshake o sessione).

I valori degli avvisi TLS sono definiti nelle RFC TLS, di seguito è riportato l'elenco di RFC 5246 (TLSv1.2) per riferimento:

| Nome avviso                     | Valore | Descrizione                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| close_notify                  | 0     | Nessun errore, indica l'esito positivo della sessione                                                                                                                   |
| unexpected_message            | 10    | TLS ha ricevuto un messaggio imprevisto o non in ordine                                                                                                           |
| bad_record_mac               | 20    | Decrittografia e/o verifica MAC non riuscita                                                                                                                    |
| decryption_failed_RESERVED   | 21    | **DEPRECATO** Decrittografia non riuscita (deprecata a causa di attacchi oracle di riempimento)                                                                                      |
| record_overflow               | 22    | È stato ricevuto un record maggiore delle dimensioni massime del record TLS                                                                                        |
| decompression_failure         | 30    | Si è verificato un problema durante la compressione/decompressione di un record TLS                                                                                       |
| handshake_failure             | 40    | Si è verificato un errore di handshake non specificato che non è coperto da un avviso diverso                                                                            |
| no_certificate_RESERVED      | 41    | **DEPRECATO** in TLS (solo SSL)                                                                                                                                 |
| bad_certificate               | 42    | Un certificato ricevuto conteneva una formattazione o firme non valide                                                                                   |
| unsupported_certificate       | 43    | È stato ricevuto un certificato di tipo non valido,ad esempio un certificato di sola firma usato per l'autenticazione del server TLS                                    |
| certificate_revoked           | 44    | Lo stato del certificato (fornito da un CRL o OCSP) è stato indicato come "revocato"                                                                       |
| certificate_expired           | 45    | Il certificato ricevuto non è compreso nell'intervallo di date valido (non ancora valido o scaduto)                                                                 |
| certificate_unknown           | 46    | È stato rilevato un problema di certificato sconosciuto non coperto da altri avvisi                                                                          |
| illegal_parameter             | 47    | Una configurazione o un valore negoziato nell'handshake TLS non è valido o non è compreso nell'intervallo                                                                      |
| unknown_ca                    | 48    | Non è stato possibile tracciare il certificato di identità ricevuto tramite una catena di certificati in un certificato ca radice attendibile.                                              |
| access_denied                 | 49    | Indica che è stato ricevuto un certificato valido, ma il controllo di accesso dell'applicazione ha indicato che il certificato non era valido per le risorse richieste.            |
| decode_error                  | 50    | Un campo o un valore in un'intestazione TLS o un messaggio di handshake non è compreso nell'intervallo o non è valido, causando un errore nella decodifica di un record TLS.                      |
| decrypt_error                 | 51    | Impossibile verificare la firma o l'hash del messaggio completato durante l'handshake TLS.                                                                         |
| export_restriction_RESERVED  | 60    | DEPRECATO in TLSv1.2                                                                                                                                        |
| protocol_version              | 70    | La versione del protocollo TLS negoziata durante l'handshake è riconosciuta ma non supportata (ad esempio TLSv1.0 è stata presentata ma non abilitata).                       |
| insufficient_security         | 71    | Inviato ogni volta che un handshake ha esito negativo a causa della mancanza di crittografia sicura (ad esempio, le dimensioni della chiave sono troppo piccole per i requisiti dell'applicazione)                                |
| internal_error                | 80    | Si è verificato un errore non TLS (ad esempio problemi di allocazione della memoria, problemi dell'applicazione) che ha generato una sessione TLS interrotta.                                         |
| user_canceled                 | 90    | Restituito se la sessione TLS viene annullata da un utente o un'applicazione prima del completamento dell'handshake (simile a CloseNotify).                                 |
| no_renegotiation              | 100   | Indica che l'host remoto non è disposto a eseguire handshake di rinegoziazione TLS in risposta a una richiesta di rinegoziazione.                                 |
| unsupported_extension         | 110   | Inviato se un client TLS riceve un serverHello contenente estensioni non richieste in modo esplicito nel ClientHello iniziale (a indicare che il server presenta un problema). |

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **alert_level** Restituisce il livello dell'avviso ricevuto (avviso o irreversibile).
- **alert_value** Restituisce il valore dell'avviso ricevuto (vedere la tabella).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione riuscita.
- **NX_PTR_ERROR** (0x07) Sessione TLS non valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Return values. */
UINT status, alert_level, alert_value;


/* Start a TLS session.  */
status =  nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Check for “alert received” error. */
if(status == NX_SECURE_TLS_ALERT_RECEIVED)
{

        /* Get the alert level and value. */
        status =  nx_secure_tls_session_alert_value_get(&tls_session,
                                             &alert_level, &alert_value);

        /* Print out the received alert level and value. */
        printf("Alert recieved. Value: %d, Level: %d\n", alert_value,
                alert_level);
}
else if(status != NX_SUCCESS)
{
    /* Additional error handling. */
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_start
- nx_secure_tls_session_send
- nx_secure_tls_session_receive

## <a name="nx_secure_tls_session_certificate_callback_set"></a>nx_secure_tls_session_certificate_callback_set

Configurare un callback per TLS da usare per la convalida aggiuntiva del certificato

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un puntatore a funzione a una sessione TLS che TLS richiama quando un certificato viene ricevuto da un host remoto, consentendo all'applicazione di eseguire controlli di convalida, ad esempio la convalida DNS, la revoca del certificato e l'imposizione dei criteri dei certificati.

NetX Secure TLS eseguirà la convalida del percorso X.509 di base sul certificato prima di richiamare il callback per assicurarsi che il certificato possa essere tracciato in un certificato nell'archivio certificati attendibili TLS, ma tutte le altre convalide verranno gestite da questo callback.

Il callback fornisce il puntatore di sessione TLS e un puntatore al certificato di identità dell'host remoto (foglia nella catena di certificati). Il callback deve restituire NX_SUCCESS se la convalida ha esito positivo, in caso contrario deve restituire un codice di errore che indica l'errore di convalida. Qualsiasi valore diverso da NX_SUCCESS causerà l'interruzione immediata dell'handshake TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **func_ptr** Puntatore alla funzione di callback di convalida del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione del puntatore a funzione.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
    /* Certificate validation checking goes here. */
    return(NX_SUCCESS);
}

/* In TLS setup routine. */
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                            certificate_callback);

        /* If status is NX_SUCCESS the certificate callback was added.  */
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_crl_revocation_check

## <a name="nx_secure_tls_session_client_callback_set"></a>nx_secure_tls_session_client_callback_set

Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un puntatore a funzione a una sessione TLS che TLS richiama quando un handshake client TLS ha ricevuto un messaggio ServerHelloDone. La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ServerHello ricevuto che richiedono input o decisioni.

Il callback viene eseguito con il blocco di controllo sessione TLS richiamato e una matrice di NX_SECURE_TLS_HELLO_EXTENSION oggetti . La matrice di oggetti estensione deve essere passata a una funzione helper che troverà e an parserà un'estensione specifica. Attualmente non sono supportate estensioni specifiche in NetX Secure che richiedono l'input del client TLS, ma il callback è disponibile per i progettisti di applicazioni per gestire estensioni personalizzate o nuove che potrebbero diventare disponibili. Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi hello, vedere *nx_secure_tls_session_sni_extension_parse*.

Il callback client può essere usato anche per selezionare il certificato di identità attivo usando *nx_secure_tls_active_certificate_set* per il client TLS nel caso in cui il server remoto abbia richiesto un certificato e fornito informazioni per consentire al client TLS di selezionare un certificato specifico. Per altre informazioni, vedere le informazioni nx_secure_tls_active_certificate_set riferimento.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **func_ptr** Puntatore alla funzione di callback client TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione del puntatore a funzione.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Callback routine used to process ServerHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the server). */

ULONG tls_client_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{

    /* Extension parsing would go here. */

    /* Set an active identity certificate – the certificate should have been added
       to the local store at application start with
       nx_secure_tls_local_certificate_add. */
    nx_secure_tls_active_certificate_set(session, &global_identity_certificate);

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
    /* Add callback to TLS session.  */
    status =  nx_secure_tls_session_client_callback_set(tls_session,
                                                        client_callback);

    /* If status is NX_SUCCESS the callback was added and will be invoked once
       a ServerHelloDone message is received. */

    return(status);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_server_callback_set
- nx_secure_tls_active_certificate_set

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a>nx_secure_tls_session_x509_client_verify_configure

Abilitare la verifica X.509 del client e allocare spazio per i certificati client

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio abilita l'autenticazione client X.509 facoltativa per un'istanza del server TLS. Alloca anche lo spazio necessario per elaborare le catene di certificati in ingresso dall'host client remoto. I certificati forniti dal client remoto verranno verificati rispetto ai certificati attendibili dell'istanza del server TLS, assegnati al servizio *nx_secure_tls_trusted_certificate_add.*

Per la modalità client TLS, è necessaria l'allocazione remota dei certificati nx_secure_tls_remote_certificate_buffer_allocate *deve* essere usata. L'abilitazione dell'autenticazione client X.509 in un'istanza del client TLS non avrà alcun effetto.

Il *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati. Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale a ogni certificato. Il *buffer_size* parametro indica le dimensioni del buffer. Lo spazio necessario è disponibile con la formula seguente:

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

I certificati tipici con chiavi RSA a 2048 bit che usano SHA-256 per le firme sono nell'intervallo tra 1000 e 2000 byte. Il buffer deve essere sufficientemente grande da contenere almeno tale dimensione per ogni certificato, ma a seconda dei certificati host remoti può essere notevolmente più piccolo o più grande. Si noti che se il buffer è troppo piccolo per contenere il certificato in ingresso, l'handshake TLS terminerà con un errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certs_number** Numero di certificati da allocare dal buffer specificato.
- **certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.
- **buffer_size** Dimensioni del buffer del certificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00)Allocazione del certificato completata.
- **NX_PTR_ERROR** (0x07) Sessione TLS o puntatore al buffer non valido.
- **NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Il buffer fornito era troppo piccolo.
- **NX_INVALID_PARAMETERS** (0x4D) Il buffer era troppo piccolo per contenere il numero desiderato di certificati.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE          (CERTIFICATE_NUMBER * \
                                (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Enable X.509 Client verification and allocate certificate space in our TLS
   Server session.  */
status =  nx_secure_tls_session_x509_client_verify_configure(&tls_session,
                                                    CERTIFICATE_NUMBER,
                                                    certificate_buffer,
                                                    BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_buffer_allocate

## <a name="nx_secure_tls_session_client_verify_disable"></a>nx_secure_tls_session_client_verify_disable

Disabilitare l'autenticazione del certificato client per una sessione TLS sicura netx

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita l'autenticazione del certificato client per una sessione TLS specifica. Vedere nx_secure_tls_session_client_verify_enable per altre informazioni.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Modifica dello stato riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_client_verify_enable
- nx_secure_tls_session_start
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_client_verify_enable"></a>nx_secure_tls_session_client_verify_enable

Abilitare l'autenticazione del certificato client per una sessione TLS sicura netx

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita l'autenticazione del certificato client per una sessione TLS specifica. Se si abilita l'autenticazione del certificato client per un'istanza del server TLS, il server TLS richiederà un certificato da qualsiasi client TLS remoto durante l'handshake TLS iniziale. Il certificato ricevuto dal client TLS remoto è accompagnato da un messaggio CertificateVerify, che il server TLS usa per verificare che il client sia proprietario del certificato (ha accesso alla chiave privata associata a tale certificato).

Se il certificato fornito può essere verificato e tracciato di nuovo in un certificato nell'archivio certificati attendibili del server TLS tramite una catena di certificati X.509, il client TLS remoto viene autenticato e l'handshake continua. In caso di errori durante l'elaborazione del certificato o del messaggio CertificateVerify, l'handshake TLS termina con un errore.

> [!NOTE]
> *Il server TLS deve avere almeno un certificato nell'archivio attendibile aggiunto con nx_secure_tls_trusted_certificate_add l'autenticazione avrà sempre esito negativo.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Modifica dello stato riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_client_verify_enable
- nx_secure_tls_session_start
- nx_secure_tls_session_create
- nx_secure_tls_trusted_certificate_add

## <a name="nx_secure_tls_session_create"></a>nx_secure_tls_session_create

Creare una sessione TLS sicura netx per le comunicazioni sicure

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza un'istanza della NX_SECURE_TLS_SESSION da usare per stabilire comunicazioni TLS sicure su una connessione di rete.

Il metodo accetta un NX_SECURE_TLS_CRYPTO oggetto popolato con i metodi di crittografia disponibili da usare per TLS. Il *encryption_metadata_area* punta a un buffer allocato per l'uso da parte di TLS per i "metadati" usati dai metodi di crittografia nella tabella NX_SECURE_TLS_CRYPTO per i calcoli. Le dimensioni della tabella possono essere determinate usando il nx_secure_tls_metadata_size_calculate dati. Per altri dettagli, vedere la sezione "Crittografia in NetX Secure TLS" nel capitolo 3.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **cipher_table** Puntatore ai metodi di crittografia TLS.
- **encryption_metadata_area** Puntatore allo spazio per i metadati di crittografia.
- **encryption_metadata_size** Dimensioni del buffer dei metadati.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00)Inizializzazione della sessione TLS riuscita.
- **NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.
- **NX_INVALID_PARAMETERS** (0x4D) Il buffer dei metadati è troppo piccolo per i metodi specificati.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Un metodo di crittografia obbligatorio per la versione abilitata di TLS non è stato fornito nella tabella di crittografia.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Reference the platform-specific TLS cryptographic method table. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Declare a buffer for the cryptographic metadata. The size should be calculated
   using nx_secure_tls_metadata_size_calculate. */
UCHAR crypto_metadata[4500];

/* Initialize TLS session.  */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* If status is NX_SUCCESS the TLS Session was successfully initialized.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_metadata_size_calculate
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_end
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_delete
- Crittografia in NetX Secure TLS nel capitolo 3

## <a name="nx_secure_tls_session_delete"></a>nx_secure_tls_session_delete

Eliminare una sessione TLS sicura di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina una sessione TLS rappresentata da un'istanza NX_SECURE_TLS_SESSION e rilascia tutte le risorse di sistema di proprietà di tale istanza di sessione.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_end
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_end"></a>nx_secure_tls_session_end

Terminare una sessione TLS protetta di NetX attiva

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio termina una sessione TLS rappresentata da un'NX_SECURE_TLS_SESSION di struttura inviando il messaggio TLS CloseNotify all'host remoto. Il servizio attende quindi che l'host remoto risponda con il proprio messaggio CloseNotify.

Se l'host remoto non invia un messaggio CloseNotify, TLS considera questo errore e una possibile violazione della sicurezza, quindi controllare il valore restituito è importante per una connessione sicura. Il **wait_option** può essere usato per controllare per quanto tempo il servizio deve attendere la risposta prima di restituire il controllo al thread chiamante.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **wait_option** Indica per quanto tempo il servizio deve attendere la risposta dall'host remoto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Non ha ricevuto una risposta dall'host remoto prima del timeout.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Impossibile allocare un pacchetto per inviare il messaggio CloseNotify.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Impossibile inviare il messaggio CloseNotify sul socket TCP.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_packet_buffer_set"></a>nx_secure_tls_session_packet_buffer_set

Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio associa un buffer di riassemblaggio di pacchetti a una sessione TLS. Per decrittografare e analizzare i record TLS in ingresso, i dati in ogni record devono essere assemblati dai pacchetti TCP sottostanti. I record TLS possono avere dimensioni massime di 16 KB (anche se in genere sono molto più piccoli), quindi potrebbero non essere adatti a un singolo pacchetto TCP.

Se si sa che le dimensioni dei messaggi in ingresso saranno inferiori al limite di record TLS di 16 KB, le dimensioni del buffer possono essere ridotte, ma per gestire i dati in ingresso sconosciuti il buffer deve essere reso il più grande possibile. Se un record in ingresso è maggiore del buffer fornito, la sessione TLS terminerà con un errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **buffer_ptr** Puntatore al buffer per TLS da usare per il riassemblaggio dei pacchetti.
- **buffer_size** Dimensione in byte del buffer fornito.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_INVALID_PARAMETERS** (0x4D) Buffer o puntatore di sessione TLS non valido.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_protocol_version_override"></a>nx_secure_tls_session_protocol_version_override

Eseguire l'override della versione predefinita del protocollo TLS per una sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a>Descrizione

Questo servizio esegue l'override della versione predefinita (più recente) del protocollo TLS usata da una sessione specifica. Ciò consente a NetX Secure TLS di usare una versione precedente di TLS per una sessione TLS specifica senza disabilitare le versioni più recenti di TLS in fase di compilazione. Questo può essere utile nelle applicazioni che potrebbero dover comunicare con un host meno recente che non supporta la versione più recente di TLS.

> [!IMPORTANT]
> *A causa della versione 5.11SP3, NetX Secure TLS supporta RFC 7507 (vedere la nota seguente) e qualsiasi override di una versione precedente con questa API comporta l'invio di un scsv di fallback in ClientHello. Se il server supporta una versione più recente di TLS e il fallback SCSV è incluso in ClientHello, tale server interromperà l'handshake TLS con un avviso di fallback non appropriato. ScSV viene inviato solo quando l'override della versione è una versione precedente di TLS di quella abilitata (ad esempio, se si esegue l'override della versione a TLS 1.2, non verrà inviato alcun SCSV).*

I valori validi per il protocol_version sono le macro seguenti: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 e NX_SECURE_TLS_VERSION_TLS_1_2.

Le macro NX_SECURE_TLS_DISABLE_TLS_1_1 e NX_SECURE_TLS_ENABLE_TLS_1_0 possono essere usate per controllare le versioni di TLS compilate nell'applicazione. TLS versione 1.2 è sempre abilitato.

Si noti che se l'host remoto non supporta la versione fornita, la connessione avrà esito negativo. Solo la versione di sostituzione fornita verrà negoziata da NetX Secure TLS.

> [!IMPORTANT]
> RFC 7507: SCSV di fallback TLS. Questa RFC è stata introdotta per attenuare un problema di sicurezza causato originariamente da server che gestivano in modo non corretto la negoziazione di downgrade del protocollo e rifiutavano invece messaggi ClientHello altrimenti validi. Nel tentativo di mantenere la compatibilità con questi server precedenti, alcune applicazioni client TLS hanno iniziato a ripetere gli handshake non riusciti con e la versione precedente di TLS (ad esempio TLS 1.2 non è riuscito, quindi provare TLS 1.1). Questa soluzione alternativa ha tuttavia introdotto un nuovo problema: un utente malintenzionato potrebbe forzare il downgrade di un client introducendo artificialmente un errore di rete o di pacchetto che causa l'esito negativo della connessione al server, anche quando il server supporta la versione tls più recente. Effettuando il downgrade a una versione precedente, l'utente malintenzionato potrebbe sfruttare i punti deboli di tale versione (SSLv3<sup>21</sup> in particolare è debole per l'attacco POODLE). Per evitare questa situazione, RFC 7507 ha presentato il "fallback SCSV", uno pseudo-ciphersuite<sup>22</sup> inviato in ClientHello che invia una notifica a un server TLS quando un client TLS usa una versione TLS che non è la versione più recente supportata. In questo modo, un server che supporta una versione più recente può rifiutare un ClientHello contenente il fallback SCSV e impedire il successo dell'attacco di downgrade.

21. NetX Secure non implementa SSLv3 a causa dell'esistenza di gravi punti deboli noti, ad esempio POODLE.

22. Una pseudo-ciphersuite, o SCSV (Signaling Cipher Suite Value), è un numero di crittografia riservato usato per segnalare le implementazioni TLS abilitate sulle funzionalità non disponibili nelle versioni precedenti di TLS. Il fallback SCSV e il TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) sono esempi.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **protocol_version** Macro della versione TLS per la versione specifica di TLS da usare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Modifica dello stato riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Versione TLS nota ma non supportata.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Versione del protocollo non valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_start
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_receive"></a>nx_secure_tls_session_receive

Ricevere dati da una sessione TLS sicura di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve i dati dalla sessione TLS attiva specificata, gestendo la decrittografia dei dati prima di fornirla al chiamante nel parametro NX_PACKET. Se nella sessione specificata non viene accodato alcun dato, la chiamata viene sospesa in base all'opzione di attesa fornita.

> [!IMPORTANT]
> *Se NX_SUCCESS viene restituito , l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **packet_ptr** Puntatore a un puntatore a pacchetti TLS allocato.
- **wait_option** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione riuscita della sessione TLS.
- **NX_NO_PACKET** (0x01) Nessun dato ricevuto.
- **NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio ricevuto non ha superato un controllo hash di autenticazione.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio ricevuto contiene una versione del protocollo sconosciuta nell'intestazione.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Ha ricevuto un avviso TLS dall'host remoto.
- **NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a>nx_secure_tls_session_renegotiate_callback_set

Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un callback a una sessione TLS che verrà richiamata ogni volta che l'host remoto riceve il primo messaggio di un handshake di rinegoziazione della sessione.

La funzione di callback è concepita come notifica all'applicazione dell'inizio di un handshake di rinegoziazione. L'applicazione può scegliere di terminare la sessione TLS restituisce qualsiasi valore diverso da zero dal callback che causerà la chiusura della sessione TLS da parte di TLS con un errore. Se l'applicazione vuole procedere con la rinegoziazione, il callback deve restituire NX_SUCCESS.

> [!NOTE]
> *A causa della semantica di rinegoziazione TLS, il callback verrà richiamato per i client TLS sicuri NetX ogni volta che viene ricevuto un HelloRequest dal server remoto, ma non quando il client avvia la rinegoziazione. Nei server NETX Secure TLS, il callback verrà richiamato ogni volta che viene ricevuto un ClientHello di rinegoziazione (qualsiasi ClientHello ricevuto nel contesto di una sessione TLS attiva). Ciò significa che il callback verrà richiamato se l'host remoto o l'applicazione locale ha avviato la rinegoziazione perché il server TLS invierà un HelloRequest a cui risponderà il client remoto.*

NetX Secure TLS implementa l'estensione Secure Renegotiation Inidication da RFC 5746 per garantire che gli handshake di rinegoziazione non siano soggetti ad attacchi man-in-the-middle.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore all'istanza di sessione TLS.
- **func_ptr** Puntatore alla funzione di callback.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Assegnazione del callback riuscita.
- **NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido per la funzione di callback o la sessione TLS.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Simple callback notifying the user that a renegotiation is starting. */
ULONG tls_renegotiation_callback(NX_SECURE_TLS_SESSION *session)
{
    printf("Renegotiation initiated by remote host\n");

    return(NX_SUCCESS);
}

/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Set callback for renegotiation notification. */
status = nx_secure_tls_session_renegotiate_callback_set(&tls_session,
                                                tls_renegotiation_callback);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_start
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_renegotiate

## <a name="nx_secure_tls_session_renegotiate"></a>nx_secure_tls_session_renegotiate

Avviare un handshake di rinegoziazione della sessione con l'host remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un handshake di *rinegoziazione* della sessione con un host TLS remoto connesso. Una rinegoziazione è costituita da un secondo handshake TLS nel contesto di una sessione TLS stabilita in precedenza. Ognuno dei nuovi messaggi di handshake viene crittografato usando la sessione TLS fino a quando non vengono generate nuove chiavi di sessione e non vengono s scambiati i messaggi ChangeCipherSpec, in cui le nuove chiavi vengono usate per crittografare tutti i messaggi.

Una rinegoziazione può essere avviata in qualsiasi momento dopo aver stabilito una sessione TLS. Se si tenta una rinegoziazione durante un handshake TLS o prima che venga stabilita una sessione TLS, non verrà eseguita alcuna azione.

> [!NOTE]
> *Quando questo servizio viene richiamato, verrà eseguito un intero handshake TLS, quindi il tempo di completamento e lo stato restituito variano a seconda delle impostazioni TLS correnti e dei parametri della sessione.*

NetX Secure TLS implementa l'estensione Secure Renegotiation Inidication da RFC 5746 per garantire che gli handshake di rinegoziazione non siano soggetti ad attacchi man-in-the-middle.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore all'istanza di sessione TLS.
- **wait_option** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione. Viene passato a tutti i servizi NetX all'interno di TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La rinegoziazione è riuscita.
- **NX_NO_PACKET** (0x01) Nessun dato ricevuto.
- **NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio ricevuto non ha superato un controllo hash di autenticazione.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio ricevuto contiene una versione del protocollo sconosciuta nell'intestazione.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Ha ricevuto un avviso TLS dall'host remoto.
- **NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) La sessione TLS locale o remota è inattiva, rendendo impossibile la rinegoziazione.
- **NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13A) L'host remoto non ha fornito l'estensione SCSV o Secure Renegotiation e pertanto non è possibile eseguire la rinegoziazione.
- **NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED(0x111)** Allocazione pacchetti sottostante non riuscita.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Setup a client socket connection.  */
status = nx_tcp_client_socket_connect(&tcp_socket, server_ipv4_address,
REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

/* Start the TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Send some data in the first TLS session. (Check “status” for errors…)*/
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Hello there!\r\n", 14, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);

/* Now renegotiate the session. */
status  = nx_secure_tls_session_renegotiate(&tls_session, NX_WAIT_FOREVER);

/* If status == NX_SUCCESS, new TLS session keys have been generated. */

/* Send some data in the new TLS session. This will be encrypted using the new
   keys. */
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Another message…\r\n", 18, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_start
- nx_secure_tls_session_receive
- nx_secure_tls_session_send
- nx_secure_tls_session_renegotiation_callback_set

## <a name="nx_secure_tls_session_reset"></a>nx_secure_tls_session_reset

Cancellare e reimpostare una sessione TLS sicura di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella una sessione TLS e reimposta lo stato come se la sessione fosse stata appena creata in modo che un oggetto sessione TLS esistente possa essere usato nuovamente per una nuova sessione.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_INVALID_PARAMETERS** (0x4D) Puntatore di sessione TLS non valido.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_send
- nx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_send"></a>nx_secure_tls_session_send

Inviare dati tramite una sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia i dati nel NX_PACKET fornito, usando la sessione TLS attiva specificata e gestendo la crittografia di tali dati prima di inviarli all'host remoto. Se le dimensioni dell'ultima finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio viene sospeso facoltativamente in base alle opzioni di attesa specificate.

> [!IMPORTANT]
> *A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **packet_ptr** Puntatore a un pacchetto TLS contenente i dati da inviare.
- **wait_option** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del ricevitore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_NO_PACKET** (0x01) Nessun dato ricevuto.
- **NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) L'invio del socket TCP sottostante non è riuscito.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.
- **NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_packet_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_session_end
- nx_secure_tls_session_create

## <a name="nx_secure_tls_session_server_callback_set"></a>nx_secure_tls_session_server_callback_set

Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un puntatore a funzione a una sessione TLS che TLS richiama quando un handshake del server TLS ha ricevuto un messaggio ClientHello. La funzione di callback consente a un'applicazione di elaborare le estensioni TLS dal messaggio ClientHello ricevuto che richiedono input o decisioni.

Il callback viene eseguito con il blocco di controllo sessione TLS richiamato e una matrice di NX_SECURE_TLS_HELLO_EXTENSION oggetti . La matrice di oggetti estensione deve essere passata a una funzione helper che troverà e an parserà un'estensione specifica. Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi hello, vedere *nx_secure_tls_session_sni_extension_parse*.

Il callback del server può essere usato anche per selezionare il certificato di identità attivo *usando* nx_secure_tls_active_certificate_set per il server TLS. Ciò si verifica più spesso in risposta a un'estensione Indicazione nome server (SNI) che consente a un client TLS di indicare il server che sta tentando di contattare. Per altre *informazioni, vedere nx_secure_tls_session_sni_extension_parse* *e nx_secure_tls_active_certificate_set* riferimento.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **func_ptr** Puntatore alla funzione di callback del server TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione del puntatore a funzione.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Application-supplied function to map server DNS name to a specific certificate
   ID. The certificate ID is supplied by the application when the certificate is
   added with nx_secure_tls_server_certificate_add. */
UINT application_find_id_by_dns_name(NX_SECURE_X509_DNS_NAME *dns_name)
{
    if(strncmp(dns_name->nx_secure_x509_dns_name, “server_name”,
               dns_name->nx_secure_x509_dns_name_length) == 0)
    {
        /* DNS name matches one we know, return it’s ID. */
        return(0x12);
    }

    /* Unknown DNS name, return 0 to indicate no matching ID found. */
    return(0);
}

/* Callback routine used to process ClientHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the client). */
ULONG tls_server_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;
UINT cert_id;
NX_SECURE_X509_CERT *certificate;


    /* Find and parse a Server Name Indication (SNI) extension. */
    status = nx_secure_tls_session_sni_extension_parse(session, extensions,
                                                       num_extensions, &dns_name);

    if(status != NX_SUCCESS && status != NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
        /* Parsed an invalid extension, return the error. */
        return(status);
    }

    if(status == NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
            /* SNI extension not found, just return success to use the default
               certificate. */
            return(NX_SUCCESS);
    }

    /* Find the application-supplied numeric identifier for the specified DNS
       name provided by the remote client. */
    cert_id = application_find_id_by_dns_name(&dns_name);

    /* If cert_id is 0, just use the default identity certificate added with
       nx_secure_tls_local_certificate_add. */
    if(cert_id != 0)
    {
        /* Application found a matching name, find the certificate in our
           store. */
        status = nx_secure_tls_server_certificate_find(tls_session, &certificate,
                                                       cert_id);

        if(status != NX_SUCCESS)
        {
            /* Didn’t find a valid certificate with the supplied ID. Return an
               error so TLS can shut down the handshake. */
            return(NX_SECURE_TLS_CERTIFICATE_NOT_FOUND);
        }

        /* Set the active identity certificate – the certificate should have been
           added to the local store at application start with
           nx_secure_tls_local_certificate_add. */
        nx_secure_tls_active_certificate_set(session, certificate);
    }

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_server_callback_set(tls_session,
                                                            server_callback);

        /* If status is NX_SUCCESS the callback was added and will be invoked
           immediately after a ClientHello message is received. */

        return(status);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_active_certificate_set
- nx_secure_tls_session_sni_extension_parse
- nx_secure_tls_server_certificate_add
- nx_secure_tls_server_certificate_find

## <a name="nx_secure_tls_session_sni_extension_parse"></a>nx_secure_tls_session_sni_extension_parse

Analizzare un'Indicazione nome server (SNI) ricevuta da un client TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a>Descrizione

Questo servizio deve essere chiamato dall'interno di un callback di sessione del server TLS, aggiunto a una sessione TLS usando nx_secure_tls_session_server_callback_set. Il callback viene richiamato dopo la ricezione di un messaggio ClientHello da un client TLS remoto e viene fornita una matrice di estensioni disponibili (e il numero di estensioni nella matrice). Tale matrice e la relativa lunghezza possono essere passate direttamente a questa routine per determinare se è presente un'estensione SNI. In caso contrario, viene restituito NX_SECURE_TLS_EXTENSION_NOT_FOUND che indica semplicemente che il client ha scelto di non determinare l'estensione SNI (non si tratta di un errore).

Se viene trovata l'estensione SNI, il nome DNS X.509 fornito dal client TLS viene restituito nella dns_name struttura. Attualmente, l'estensione SNI fornisce solo una singola voce di nome DNS, che può essere usata dal server TLS per determinare quale certificato di identità inviare al client remoto.**

La NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo nx_secure_x509_dns_name e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*.  La macro NX_SECURE_X509_DNS_NAME_MAX le dimensioni del buffer nx_secure_x509_dns_name dati.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **estensioni** Puntatore a una matrice di estensioni Hello TLS (dal callback di sessione).
- **num_extensions** Numero di estensioni nella matrice (dal callback di sessione).
- **dns_name** Restituisce il nome DNS fornito nell'estensione SNI.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Analisi dell'estensione completata.
- **NX_PTR_ERROR** (0x07) Matrice di estensioni non valida o puntatore di sessione TLS.
- **NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) estensione SNI non trovata.
- **NX_SECURE_TLS_SNI_EXTENSION_INVALID** formato dell'estensione SNI (0x137) non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_server_callback_set
- nx_secure_tls_session_client_callback_set
- nx_secure_tls_server_callback_set
- nx_secure_tls_active_certificate_set

## <a name="nx_secure_tls_session_sni_extension_set"></a>nx_secure_tls_session_sni_extension_set

Impostare un Indicazione nome server DNS dell'estensione SNI da inviare a un server remoto

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione client TLS di fornire un nome DNS del server preferito a un server TLS remoto usando l'estensione TLS Indicazione nome server (SNI). L'estensione SNI consente al server di selezionare il certificato di identità e i parametri corretti in base alle preferenze del server indicate dal client. L'estensione SNI attualmente supporta solo un singolo nome DNS da inviare, quindi il parametro del nome singolare. Il dns_name deve essere inizializzato con nx_secure_x509_dns_name_initialize *e* conterrà il server preferito del client. Per annullare l'impostazione del nome dell'estensione, è sufficiente chiamare questo servizio con un valore di parametro "dns_name" di NX_NULL.

La NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo nx_secure_x509_dns_name e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*.  La macro NX_SECURE_X509_DNS_NAME_MAX le dimensioni del buffer nx_secure_x509_dns_name dati.

> [!NOTE]
> *Questa routine deve essere chiamata prima nx_secure_tls_session_start richiamata o ClientHello non conterrà l'estensione SNI.*

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **dns_name** Nome DNS fornito dall'applicazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta riuscita del nome del server DNS.
- **NX_PTR_ERROR** (0x07) Nome DNS o puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
#define TLS_SNI_SERVER_NAME “www.example.com”

NX_SECURE_X509_DNS_NAME dns_name;
NX_SECURE_TLS_SESSION client_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&client_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));


    /* Initialize the DNS server name we want to send in the SNI extension. */
    nx_secure_x509_dns_name_initialize(&dns_name, TLS_SNI_SERVER_NAME,
                                    strlen(TLS_SNI_SERVER_NAME));

    /* The SNI server name needs to be set prior to starting the TLS session. */
    nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);

   /* Start TLS session as normal. */
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_start
- nx_secure_x509_dns_name_initialize

## <a name="nx_secure_tls_session_start"></a>nx_secure_tls_session_start

Avviare una sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione TLS usando il blocco di controllo della sessione TLS fornito e un socket TCP connesso. La connessione TCP deve essere già completata dopo una chiamata riuscita a nx_tcp_client_socket_connect o nx_tcp_server_socket_accept.

Questo servizio determinerà il tipo di sessione TLS (client o server) dal socket TCP.

L'opzione wait definisce il comportamento del servizio mentre è in corso l'handshake TLS.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **tcp_socket_ptr** Puntatore a un socket TCP connesso.
- **wait_option** Definisce il comportamento del servizio mentre è in corso l'handshake TLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Un tipo di messaggio TLS ricevuto non è corretto.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Una crittografia fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) L'elaborazione del messaggio durante l'handshake TLS non è riuscita.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio in arrivo non ha superato un controllo MAC hash.
- **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) L'invio di un socket TCP sottostante non è riuscito.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Un messaggio in arrivo ha un campo di lunghezza non valido.
- **NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) Un messaggio ChangeCipherSpec in ingresso non è corretto.
- **NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) Un certificato TLS in ingresso non è utilizzabile per identificare il server TLS remoto.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) La crittografia a chiave pubblica fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) L'host remoto non ha indicato ciphersuit supportati dallo stack NETX Secure TLS.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio TLS ricevuto ha una versione TLS sconosciuta nell'intestazione.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Un messaggio TLS ricevuto aveva una versione TLS nota ma non supportata nell'intestazione.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Un'allocazione interna di pacchetti TLS non è riuscita.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) L'host remoto ha fornito un certificato non valido.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) L'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.
- **NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) Una voce nella tabella ciphersuite ha un puntatore a funzione NULL.
- **NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) Un client TLS remotoHello includeva il fallback SCSV e tentava un fallback della versione.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Initialize the TLS session structure. */
nx_secure_tls_session_create(&tls_session,
                              &nx_crypto_tls_ciphers,
                              crypto_metadata,
                              sizeof(crypto_metadata));

/* Setup the TLS packet reassembly buffer. */
status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                 sizeof(tls_packet_buffer));

/* Initialize a certificate for the TLS server. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data, 500,
NX_NULL, 0, private_key, 64);

/* If status is NX_SUCCESS, certificate is initialized. */

/* Add the certificate a local certificate to identify this TLS server. */
status = nx_secure_tls_add_local_certificate(&tls_session, &certificate);

/* If status is NX_SUCCESS, certificate was added successfully. */

/* Create and start a TCP socket as a server. */
/* NOTE: This assumes an IP instance called “ip_0” has already been created. */

/* Create a TCP server socket on the previously created IP instance, with normal
   delivery, IP fragmentation enabled, default time to live, a 8192-byte receive
   window, no urgent callback routine, and the "client_disconnect" routine to
   handle disconnection initiated from the other end of the connection.  */
status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Server Socket", NX_IP_NORMAL,
                               NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192, NX_NULL,
                               NX_NULL);

/* If status is NX_SUCCESS, the TCP socket was created successfully. */

/* Start up a TCP server socket by listening on port 443 with a listen queue of
   size 5. */
status =  nx_tcp_server_socket_listen(&ip_0, 443, &tcp_socket, 5, NX_NULL);

/* Application main loop. */
while(1)
{
        /* Accept incoming requests on the TCP socket. */
        status =  nx_tcp_server_socket_accept(&tcp_socket, NX_WAIT_FOREVER);

        /* At this point, the TCP socket should be established (but not the TLS
        session yet). */

        /* Start the TLS session on our active TCP socket. */
        status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                             NX_WAIT_FOREVER);

        /* At this point, if status is NX_SUCCESS, the TLS session has been
           established.  Application may now send/receive data through this
           channel. */

        /* Send and receive data using the TLS session. */
        /* Allocate TLS packets using nx_secure_tls_packet_allocate, write data with
           nx_packet_data_append, read data with nx_packet_data_extract_offset. */

        /* Send TLS data. */
        nx_secure_tls_session_send(&tls_session, &send_packet, NX_WAIT_FOREVER);

        nx_secure_tls_session_receive(&tls_session, &receive_packet_ptr,
        NX_WAIT_FOREVER);


        /* Once all application data is sent/received, end the TLS session. */
        status = nx_secure_tls_session_end(&tls_session);

        /* If status is NX_SUCCESS, the TLS session has been closed properly. */

        /* Now disconnect the TCP server socket from the client.  */
        nx_tcp_socket_disconnect(&tcp_socket, 200);

        /* Unaccept the TCP server socket.  Note that unaccept is called even if
           disconnect or accept fails.  */
        nx_tcp_server_socket_unaccept(&tcp_socket);

        /* Setup server socket for listening with this socket again.  */
        nx_tcp_server_socket_relisten(&ip_0, 443, &tcp_socket);
}

/* When the server application is shut down, clean up the TLS session. */
nx_secure_tls_session_delete(&tls_session);

/* Finally, clean up the TCP socket as well. */
nx_tcp_socket_delete(&tcp_socket);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_socket_receive
- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_send
- nx_secure_tls_session_delete
- nx_secure_tls_session_receive
- nx_secure_tls_packet_allocate
- nx_secure_tls_session_end
- nx_secure_tls_session_create
- nx_tcp_socket_accept
- nx_tcp_socket_listen
- nx_tcp_socket_disconnect
- nx_tcp_socket_unaccept
- nx_tcp_socket_relisten
- nx_tcp_socket_delete
- nx_packet_allocate
- nx_packet_data_append
- nx_packet_data_extract_offset

## <a name="nx_secure_tls_session_time_function_set"></a>nx_secure_tls_session_time_function_set

Assegnare una funzione timestamp a una sessione TLS sicura netx

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a>Descrizione

Questa funzione configura un puntatore a funzione che TLS richiama quando deve ottenere l'ora corrente, usata in vari messaggi di handshake TLS e per la verifica dei certificati.

È previsto che la funzione restituisca il GMT corrente in formato UNIX 32 bit (secondi a partire dalla mezzanotte a partire dal 1° gennaio 1970, UTC, ignorando i secondi intercalare), in base ai requisiti ClientHello nella RFC 5246 TLS.

Se non viene assegnata alcuna funzione timestamp, verrà usato il valore 0 per il timestamp nell'handshake TLS e il controllo della scadenza del certificato non funzionerà.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS.
- **time_func_ptr** Puntatore a una funzione che restituisce l'ora corrente (GMT) in UNIX formato a 32 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_INVALID_PARAMETERS** (0x4D) Puntatore di sessione TLS non valido.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* This function returns a 32-bit UNIX-style representation of the current GMT
   time. */
ULONG get_gmt_time(void)
{
ULONG time_value;

   /* Platform-specific time calculation goes here… */

   return(time_value);
}

/* Reset a TLS session.  */
status =  nx_secure_tls_timestamp_function_set(&tls_session, get_gmt_time);


/* If status is NX_SUCCESS the function was successfully added.*/
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_session_start
- nx_secure_tls_session_delete
- nx_secure_tls_session_sendnx_secure_tls_session_receive
- nx_secure_tls_session_create

## <a name="nx_secure_tls_trusted_certificate_add"></a>nx_secure_tls_trusted_certificate_add

Aggiungere un certificato attendibile alla sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza inizializzata NX_SECURE_X509_CERT struttura a una sessione TLS. Questo certificato viene usato dallo stack TLS per verificare i certificati forniti dall'host remoto durante l'handshake TLS.

I certificati attendibili sono necessari per la modalità client TLS.

I certificati attendibili sono necessari solo per la modalità server TLS se è abilitata l'autenticazione del certificato client.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **certificate_ptr** Puntatore a un'istanza del certificato TLS inizializzata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato completata.
- **NX_INVALID_PARAMETERS** (0x4D) Tentativo di aggiungere un certificato non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Initialize certificate structure. */
status = nx_secure_x509_certificate_initialize(&certificate, certificate_data,
                                               certificate_buffer,
                                               sizeof(certificate_buffer), 500,
                                               private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_trusted_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_remove

## <a name="nx_secure_tls_trusted_certificate_remove"></a>nx_secure_tls_trusted_certificate_remove

Rimuovere un certificato attendibile dalla sessione TLS protetta di NetX

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un certificato attendibile da una sessione TLS, con chiave nel campo Nome comune nel certificato.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.
- **common_name** Valore common name del certificato da rimuovere.
- **common_name_length** Lunghezza della stringa Common Name.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato completata.
- **NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Il certificato non è stato trovato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_x509_certificate_initialize
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_add

## <a name="nx_secure_x509_certificate_initialize"></a>nx_secure_x509_certificate_initialize

Inizializzare il certificato X.509 per NetX Secure TLS

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_certificate_initialize(
                  NX_SECURE_X509_CERT *certificate_ptr,
                  const UCHAR *certificate_data,
                  USHORT certificate_data_length,
                  UCHAR *raw_data_buffer,
                  USHORT buffer_size,
                  const UCHAR *private_key_data,
                  USHORT private_key_data_length,
                  UINT private_key_type);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza una struttura NX_SECURE_X509_CERT da un certificato digitale X.509 con codifica binaria da usare in una sessione TLS.

I dati del **certificato devono** essere un certificato digitale X.509 valido in formato binario con codifica DER. I dati possono essere da qualsiasi origine (ad esempio file system, buffer costante compilato e così via) purché sia fornito un puntatore UCHAR a tale dati.

Il *raw_data_buffer* e le relative dimensioni sono parametri facoltativi che specificano un buffer dedicato in cui vengono copiati i dati del certificato prima dell'analisi. Se raw_data_buffer viene passato come NX_NULL, la struttura NX_SECURE_X509_CERT farà riferimento direttamente alla matrice certificate_data (buffer_size viene ignorata in questo caso). Se raw_data_buffer viene passato come ***NX_NULL,*** non modificare i dati a cui punta il puntatore certificate_data o l'elaborazione del certificato avrà probabilmente esito negativo.

Il parametro della chiave privata è per i certificati di identità locali: la chiave privata viene usata dai server per decrittografare i dati della chiave in ingresso da un client (crittografati usando la chiave pubblica del server) e dai client per verificare la propria identità a un server quando il server richiede un certificato client. L'aggiunta di una chiave privata con questa API contrassegnerà automaticamente il certificato associato come certificato di identità per un'applicazione TLS. Quando si inizializzano i certificati per altri scopi ,ad esempio l'archivio attendibile, il parametro *private_key_data* deve essere passato come NULL, il *private_key_data_length* come 0 e il *private_key_type* deve essere passato come NX_SECURE_X509_KEY_TYPE_NONE.

Il *private_key_type* parametro indica la formattazione della chiave privata. Ad esempio, se la chiave privata è una chiave privata RSA in formato PKCS#1 con codifica DER, il private_key_type deve essere passato come NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, un tipo noto a NetX Secure che verrà analizzato immediatamente e salvato per un uso successivo.

Il private_key_type supporta anche i tipi di chiave definiti dall'utente<sup>23</sup> per piattaforme e applicazioni con formati di chiave specifici o altre esigenze. Ad esempio, un motore di crittografia basato su hardware può usare un formato specifico non riconosciuto dal software NetX Secure oppure una chiave privata può essere crittografata o rappresentata da un token di crittografia, come nel caso di un hardware crittografico Trusted Platform Module (TPM) o PKCS#11. Quando si usa un tipo di chiave definito dall'utente, i dati della chiave vengono passati verbatim alla routine crittografica appropriata, ad esempio una chiave privata RSA verrebbe passata, senza alcuna analisi o elaborazione, direttamente alla routine crittografica RSA fornita a TLS nella tabella ciphersuite. Il tipo di chiave definito dall'utente viene passato anche alla routine crittografica (nel caso di RSA, questo è il parametro "op").

L'intervallo di chiavi definite dall'utente copre la metà superiore di un intero senza segno a 32 bit, 0x0001 0000-0xFFFF FFFF. I valori inferiori 0x0001 0000 sono riservati per l'uso di NetX Secure.

I tipi di chiave definiti dall'utente sono una funzionalità avanzata che richiede routine crittografiche personalizzate per gestire i dati della chiave privata non elaborati. Se si ha bisogno di questa funzionalità, contattare il rappresentante di Express Logic.

### <a name="parameters"></a>Parametri

- **certificate_ptr** Puntatore a un'istanza del certificato X.509 non inizializzata.
- **certificate_data** Puntatore ai dati binari X.509 con codifica DER.
- **raw_data_buffer** Puntatore al buffer dei dati del certificato dedicato facoltativo.
- **buffer_size** Dimensioni del buffer dei dati del certificato dedicato facoltativo.
- **certificate_data_length** Lunghezza in byte dei dati binari del certificato.
- **private_key_data** Puntatore ai dati facoltativi della chiave privata.
- **private_key_data_length** Lunghezza dei dati della chiave privata.
- **private_key_type** Identificatore del tipo di chiave.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta del certificato completata.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) I dati del certificato non contengono un certificato X.509 con codifica DER.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** certificato (0x10D) non dispone di una crittografia a chiave pubblica supportata da NetX Secure.
- **NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) La chiave privata o il certificato non contiene una sequenza ASN.1 valida.
- **NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18A) La chiave privata specificata non è una chiave RSA PKCS#1 valida.
- **NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19D) Il tipo di chiave privata fornito non è definito dall'utente e non corrisponde ad alcun tipo noto.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a>Vedere anche

- nx_secure_local_certificate_add
- nx_secure_tls_session_create
- nx_secure_tls_remote_certificate_allocate
- Importazione di certificati X.509 in NetX Secure nel capitolo 3.

## <a name="nx_secure_x509_common_name_dns_check"></a>nx_secure_x509_common_name_dns_check

Controllare il nome DNS rispetto al certificato X.509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a>Descrizione

Questo servizio controlla il nome comune di un certificato rispetto a un nome di dominio principale (TLD) fornito dal chiamante ai fini della convalida DNS di un host remoto. Questa funzione di utilità deve essere chiamata dall'interno di una routine di callback di convalida del certificato fornita dall'applicazione. Il nome TLD deve essere la parte superiore dell'URL usato per accedere all'host remoto ("." -separated string before the first slash). Se il nome comune contiene un carattere jolly,ad esempio .example.com, il carattere jolly corrisponderà a qualsiasi con *lo stesso suffisso. Si* noti che solo il primo carattere jolly (" ") rilevato (lettura da destra a sinistra) verrà considerato  per la corrispondenza con caratteri jolly, ad esempio abc.*.example.com corrisponderà a qualsiasi nome che termina con ".example.com".

Se il nome comune non corrisponde alla stringa specificata, viene analizzata l'estensione "subjectAltName" (se presente nel certificato) e vengono confrontate anche le voci DNSName. Se nessuna di queste voci corrisponde, viene restituito un errore.

È importante comprendere il formato del nome comune (e delle voci subjectAltName) nei certificati previsti. Ad esempio, alcuni certificati possono usare un indirizzo IP non elaborato o un carattere jolly. La stringa DNS TLD deve essere formattata in modo che corrisponda ai valori previsti nei certificati ricevuti.

### <a name="parameters"></a>Parametri

- **certificate_ptr** Puntatore a un'istanza del certificato X.509.
- **dns_tld** Top-Level nome di dominio con cui eseguire il confronto.
- **dns_tld_length** Lunghezza della stringa TLD.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Confronto riuscito con nome comune o subjectAltName.
- **NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) Nessun nome corrispondente trovato.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
UCHAR *tld = “www.example.com”;

    /* Check our DNS TLD against the certificate provided by the
       remote TLS host. */
    status = nx_secure_x509_common_name_dns_check(certificate, tld, strlen(tld));

        if(status != NX_SUCCESS)
        {
            /* TLD did not match any names in the certificate. */
            return(status);
        }

        /* DNS validation and any other checks were successful. */
        return(NX_SUCCESS);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_crl_revocation_check

## <a name="nx_secure_x509_crl_revocation_check"></a>nx_secure_x509_crl_revocation_check

Controllare il certificato X.509 rispetto a un elenco di revoche di certificati (CRL) fornito

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a>Descrizione

Questo servizio accetta un elenco di revoche di certificati con codifica DER e cerca un certificato specifico in tale elenco. L'autorità di certificazione del CRL viene convalidata rispetto a un archivio certificati fornito, l'autorità di certificazione CRL viene convalidata in modo che sia uguale a quella per il certificato controllato e il numero di serie del certificato in questione viene usato per cercare l'elenco di certificati revocati. Se le autorità di certificazione corrispondono, la firma viene verificata e il certificato non è **presente** nell'elenco, la chiamata ha esito positivo. In tutti gli altri casi viene restituito un errore.

### <a name="parameters"></a>Parametri

- **crl_data** Puntatore a un CRL con codifica DER.
- **crl_length** Lunghezza in byte dei dati CRL.
- **store** Puntatore a un archivio certificati X.509.
- **certificate_ptr** Puntatore a un'istanza del certificato X.509.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Convalida riuscita che il certificato non è stato revocato.
- **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** certificato dell'autorità di certificazione CRL (0x119) non trovato.
- **NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) Certificato autorità di certificazione non trovato.
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) L'ASN.1 CRL conteneva un campo di lunghezza non valido.
- **NX_SECURE_X509_UNEXPECTED_ASN1_TAG(0x189)** Il CRL conteneva asn.1 non valido.
- **NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) Una verifica della catena di certificati non è riuscita.
- **NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL e autorità di certificazione non corrispondono.
- **NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) La firma CRL non è valida.
- **NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) Il certificato controllato è stato trovato nell'elenco CRL e viene quindi revocato.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* CRL obtained for the expected certificate issuer through some means (downloaded
   from server manually, obtained from CRL endpoint, etc…) */
const UCHAR *crl_data;
UINT crl_length = 300;

/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
NX_SECURE_X509_CERTIFICATE_STORE *store;

    /* Obtain a certificate store to check against. In the certificate callback,
       it usually makes the most sense to use the store associated with the TLS
       session. */
    store = &session -> nx_secure_tls_credentials.nx_secure_tls_certificate_store;

    /* Check our certificate against the CRL and TLS certificate store. */
    status = nx_secure_x509_crl_revocation_check(crl, crl_length, store,
                                                 certificate);

        if(status != NX_SUCCESS)
        {
            if(status == NX_SECURE_X509_CRL_CERTIFICATE_REVOKED)
            {
                /* Certificate was revoked. */
               return(status);
            }
            else
            {
               /* CRL was invalid or some other issue. In this case the certificate
                  may still be valid since the CRL itself was a problem. At this
                  point it is up to the application to decide whether to continue
                  with the TLS handshake. For this example, assume certificate is
                  valid (faulty CRL is a possible Denial-of-Service attack).*/
               status = NX_SUCCESS;
        }

    /* Other certificate checking can go here. */

    /* Return status of certificate checks. */
    return(status);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_common_name_dns_check

## <a name="nx_secure_x509_dns_name_initialize"></a>nx_secure_x509_dns_name_initialize

Inizializzare una struttura dei nomi DNS X.509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza un nome DNS X.509 da usare con determinati servizi API che richiedono un formato di nome specifico. Ad esempio, il *servizio nx_secure_tls_sni_extension_parse* prevede che un oggetto NX_SECURE_X509_DNS_NAME corrisponda al nome fornito da un host remoto nell'estensione Indicazione nome server durante l'handshake TLS. Un nome DNS è semplicemente una stringa di caratteri con una lunghezza: la lunghezza massima consentita di un nome DNS (e le dimensioni del buffer interno in NX_SECURE_X509_DNS_NAME) è controllata dalla macro NX_SECURE_X509_DNS_NAME_MAX (100 byte predefiniti).

### <a name="parameters"></a>Parametri

- **dns_name** Struttura dei nomi DNS da inizializzare.
- **name_string** Dati di stringa del nome DNS.
- **lunghezza** Lunghezza della stringa del nome.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione riuscita.
- **NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) La stringa del nome specificata ha superato NX_SECURE_X509_DNS_NAME_MAX.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_create
- nx_secure_tls_session_sni_extension_parse
- nx_secure_tls_session_sni_extension_set

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a>nx_secure_x509_extended_key_usage_extension_parse

Trovare e analizzare un'estensione X.509 estesa per l'utilizzo delle chiavi in un certificato X.509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a>Descrizione

Questo servizio deve essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)*. Cerca un OID di utilizzo della chiave estesa specifico all'interno di un certificato X.509 e restituisce se l'OID è presente. Il key_usage è un mapping integer degli OID usato internamente da NetX Secure X.509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.

Gli OID pertinenti per l'estensione per l'utilizzo della chiave estesa sono indicati nella tabella seguente. Un'implementazione tipica del client TLS che vuole controllare l'utilizzo della chiave estesa in un certificato del server TLS ricevuto verificherebbe l'esistenza del NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH OID: se l'estensione è presente ma tale OID non lo è, il certificato verrebbe considerato non valido per l'identificazione dell'host come server TLS e il callback di verifica del certificato dovrebbe restituire un errore. Se l'estensione stessa non è presente, l'applicazione deve decidere se procedere o meno con l'handshake TLS.

Nel callback di verifica del certificato, il codice restituito dell'errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato all'uso dell'applicazione. Se si verifica un errore nel controllo dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare il motivo dell'errore.

| Identificatore di sicurezza NetX                                | Valore OID         | Descrizione                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH   | 1.3.6.1.5.5.7.3.1 | Il certificato può essere usato per identificare un server TLS |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH   | 1.3.6.1.5.5.7.3.2 | Il certificato può essere usato per identificare un client TLS |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING  | 1.3.6.1.5.5.7.3.3 | Il certificato può essere usato per firmare il codice             |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT | 1.3.6.1.5.5.7.3.4 | Il certificato può essere usato per firmare i messaggi di posta elettronica           |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING | 1.3.6.1.5.5.7.3.8 | Il certificato può essere usato per firmare i timestamp       |
| NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING  | 1.3.6.1.5.5.7.3.9 | Il certificato può essere usato per firmare le risposte OCSP   |

OID e mapping per l'estensione X.509 Extended Key Usage

### <a name="parameters"></a>Parametri

- **certificato** Puntatore al certificato da verificare.
- **key_usage** Mapping di interi OID dalla tabella precedente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) OID utilizzo chiave specificato trovato.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) rilevato tag multi byte ASN.1 (certificato non supportato).
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Rilevato campo ASN.1 invaild (certificato non valido).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Classe di tag ASN.1 non valida (certificato non valido).
- **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) È stata rilevata un'estensione non valida (certificato non valido).
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) L'estensione Utilizzo chiavi esteso non è stata trovata nel certificato fornito.
- **NX_PTR_ERROR** (0x07) Puntatore di certificato non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT* certificate)
{
UINT status;

    /* Extended key usage - look for specific OIDs. */
    status = nx_secure_x509_extended_key_usage_extension_parse(certificate,
                        NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH);

    if(status != NX_SUCCESS)
    {
        if(NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND)
        {
            printf("Extended key usage extension not found or specified key usage OID not
                    provided in extension.\n");
            /* The certificate was valid but the specified OID was not found. The
               application can decide whether to continue or abort the TLS handshake. */
            return(NX_SECURE_X509_KEY_USAGE_ERROR);
        }
        else
        {
            /* The extension or certificate was invalid. */
            return(status);
        }
    }

    /* The specified OID was found, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extension_find

## <a name="nx_secure_x509_extension_find"></a>nx_secure_x509_extension_find

Trovare e restituire un'estensione X.509 in un certificato X.509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a>Descrizione

Questo servizio deve essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)* ed è un servizio X.509 avanzato.

La funzione cerca un'estensione specifica all'interno di un certificato X.509 in base a un OID e restituisce se l'OID è presente, insieme a una struttura contenente riferimenti ai dati dell'estensione non elaborati pertinenti. Il extension_id è un mapping di interi degli OID usato internamente da NetX Secure X.509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.

Le funzioni helper fornite per estensioni specifiche (ad esempio *nx_secure_x509_key_usage_extension_parse*) chiamano nx_secure_x509_extension_find internamente per ottenere i dati dell'estensione.

Gli OID pertinenti per le estensioni X.509 note sono indicati nella tabella seguente.

La NX_SECURE_X509_EXTENSION contiene puntatori al certificato X.509 che consentono alle funzioni helper come *nx_secure_x509_key_usage_extension_parse* di decodificare rapidamente i dati ASN.1 con codifica DER dell'estensione non elaborata.

Per informazioni su estensioni specifiche, vedere RFC 5280 (specifica X.509) o il riferimento per le funzioni helper appropriate, se disponibili.

La versione corrente di NetX Secure X.509 ha un supporto limitato per le estensioni X.509. In futuro verranno aggiunte altre funzioni helper.

> [!IMPORTANT]
> *Questo servizio è una funzionalità avanzata per gli utenti che hanno familiarità con le estensioni X.509 e con codifica DER ASN.1. Viene fornito per consentire agli utenti di accedere alle estensioni per le quali NetX Secure X.509 attualmente non fornisce funzioni helper. Per tali estensioni senza funzioni helper, sarà necessario analizzare manualmente l'ASN.1 con codifica DER non elaborato.*

| NetX Secure Identifier                              | Valore OID | Descrizione                                                                    | Funzione helper? |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES  | 2.5.29.9  | Attributi della directory: attributi di informazioni di base sul soggetto del certificato  | No               |
| NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID       | 2.5.29.14 | Usato per identificare una chiave pubblica specifica                                         | No               |
| NX_SECURE_TLS_X509_TYPE_KEY_USAGE             | 2.5.29.15 | Fornisce informazioni sugli utilizzi validi per la chiave pubblica del certificato              | Sì              |
| NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME     | 2.5.29.17 | Fornisce nomi DNS alternativi per identificare il certificato                     | Sì<sup>24</sup>        |
| NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME      | 2.5.29.18 | Fornisce nomi DNS alternativi per identificare l'autorità emittente del certificato            | No               |
| NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS     | 2.5.29.19 | Fornisce informazioni di base sui vincoli di utilizzo dei certificati                        | No               |
| NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS      | 2.5.29.30 | Usato per vincolare i nomi dei certificati a domini specifici                        | No               |
| NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION      | 2.5.29.31 | Fornisce gli URI per la distribuzione CRL                                             | No               |
| NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES  | 2.5.29.32 | Elenco di criteri certificato per sistemi PKI di grandi dimensioni                             | No               |
| NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS | 2.5.29.33 | Elenco dei criteri dei certificati della CA                                                | No               |
| NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID     | 2.5.29.35 | Usato per identificare una chiave pubblica specifica associata a una firma del certificato | No               |
| NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS    | 2.5.29.36 | Vincoli dei criteri dell'autorità di certificazione                                                          | No               |
| NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE   | 2.5.29.37 | Informazioni aggiuntive sull'utilizzo delle chiavi basate su OID                                     | Sì              |
| NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL          | 2.5.29.46 | Fornisce informazioni per ottenere i delta CRL                                  | No               |
| NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY     | 2.5.29.54 | Campo del certificato della CA che indica che non è possibile usare AnyPolicy                  | No               |

OID e mapping per le estensioni X.509

24. L'estensione SubjectAltName viene analizzata come parte del controllo del nome DNS nel nx_secure_x509_common_name_dns_check.

### <a name="parameters"></a>Parametri

- **certificato** Puntatore al certificato da verificare.
- **estensione** Restituisce la struttura contenente il puntatore ai dati di estensione e la lunghezza.
- **extension_id** Mapping di interi OID dalla tabella precedente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) OID estensione specificato trovato e dati restituiti.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) rilevato tag multi byte ASN.1 (certificato non supportato).
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Rilevato campo ASN.1 invaild (certificato non valido).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Classe di tag ASN.1 non valida (certificato non valido).
- **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) È stata rilevata un'estensione non valida
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) L'OID dell'estensione specificato non è stato trovato nel certificato fornito.
- **NX_PTR_ERROR** (0x07) Puntatore di estensione o certificato non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Function to parse a Basic Constraints X.509 extension. */
UINT _basic_constraints_extension_parse(NX_SECURE_X509_CERT *certificate)
{
const UCHAR             *current_buffer;
ULONG                    length;
UINT                     status;
NX_SECURE_X509_EXTENSION extension_data;

    /* Find the Basic Constraints extension in the certificate. */
    status = _nx_secure_x509_extension_find(certificate, &extension_data,
                              NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS);

    /* See if extension present - it might be OK if not present! */
    if (status != NX_SUCCESS)
    {
        return(status);
    }

    /* The extension_data structure now points to the raw extension ASN.1
      (DER-encoded). */
    current_buffer = extension_data.nx_secure_x509_extension_data;
    length = extension_data.nx_secure_x509_extension_data_length;

   /* Extension ASN.1 parsing… */

   return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extended_key_usage_extension_parse

## <a name="nx_secure_x509_key_usage_extension_parse"></a>nx_secure_x509_key_usage_extension_parse

Trovare e analizzare un'estensione Utilizzo chiavi X.509 in un certificato X.509

### <a name="prototype"></a>Prototipo

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a>Descrizione

Questo servizio deve essere chiamato dall'interno di un callback di verifica del certificato *(vedere nx_secure_tls_session_certificate_callback_set).* Verrà cercata l'estensione Utilizzo chiavi e, se trovata, restituirà il campo di bit Utilizzo chiavi nel parametro "bitfield".

I bit, come definito dalla specifica X.509 (RFC 5280), sono indicati nella tabella seguente. Un'operazione AND bit per bit con la maschera di bit appropriata (e il controllo della presenza di valori non zero) offrirà il valore di ogni bit.

Si noti che la codifica DER del campo di bit elimina gli zeri aggiuntivi, quindi la posizione effettiva dei bit nei dati del certificato non elaborati sarà probabilmente diversa dalle relative posizioni nel campo di bit decodificato. Le maschera di bit fornite devono essere usate solo nel campo di bit decodificato restituito da *nx_secure_x509_key_usage_extension_parse* e non con i dati non elaborati del certificato con codifica DER.

Nel callback di verifica del certificato, il codice restituito di errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'uso da parte dell'applicazione. Se si verifica un errore durante la verifica dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare il motivo dell'errore.

| NetX Secure Identifier                            | Posizione del bit | Descrizione                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE  | 0            | Il certificato può essere usato per le firme digitali                                                                                                               |
| NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION    | 1            | Il certificato può essere usato per verificare firme digitali diverse da quelle per certificati e CRL                                                              |
| NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT   | 2            | Il certificato può essere usato per crittografare le chiavi simmetriche (trasporto delle chiavi)                                                                                            |
| NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT  | 3            | Il certificato può essere usato per crittografare direttamente i dati utente non elaborati (non comune)                                                                                         |
| NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT      | 4            | Il certificato può essere usato per il contratto di chiave (come con Diffie-Hellman)                                                                                           |
| NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN     | 5            | Il certificato può essere usato per firmare e verificare altri certificati (il certificato è un certificato CA o ICA).                                                  |
| NX_SECURE_X509_KEY_USAGE_CRL_SIGN           | 6            | La chiave pubblica del certificato viene usata per verificare le firme nei CRL                                                                                                  |
| NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY      | 7            | Usato con il bit dell'accordo di chiave (bit 4): se impostato, la chiave del certificato può essere usata solo per crittografare durante il contratto di chiave. Non definito se il bit dell'accordo di chiave non è impostato. |
| NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY      | 8            | Usato con il bit dell'accordo di chiave (bit 4): se impostato, la chiave del certificato può essere usata solo per decrittografare durante l'accordo di chiave. Non definito se il bit dell'accordo di chiave non è impostato. |

Maschera di bit e valori per l'estensione utilizzo chiavi X.509

### <a name="parameters"></a>Parametri

- **certificato** Puntatore al certificato da verificare.
- **bitfield** Restituisce l'intero campo di bit dall'estensione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS(0x00)** Estensione utilizzo chiave trovata e campo di bit restituito.
- **NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) rilevato tag multi byte ASN.1 (certificato non supportato).
- **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Rilevato campo ASN.1 invaild (certificato non valido).
- **NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Classe di tag ASN.1 non valida (certificato non valido).
- **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) È stata rilevata un'estensione non valida (certificato non valido).
- **NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)L'estensione Utilizzo chiavi non è stata trovata nel certificato fornito.
- **NX_PTR_ERROR** (0x07) Certificato o puntatore di campo di bit non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session,
  NX_SECURE_X509_CERT* certificate)
{
UINT status;
USHORT key_usage_bitfield;

    /* Key usage – extract key usage bitfield. */
    status = nx_secure_x509_key_usage_extension_parse(certificate, &key_usage_bitfield);

   /* Check certificate for a few specific key usage bits. */
   if((key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE) == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION)   == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT)  == 0)
    {
        printf("Expected key usage bitfield bits not set!\n");
        return(NX_SECURE_X509_KEY_USAGE_ERROR);
    }

    /* The specified bits were set, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a>Vedere anche

- nx_secure_tls_session_certificate_callback_set
- nx_secure_x509_extended_key_usage_extension_parse
- nx_secure_x509_crl_revocation_check
- nx_secure_x509_common_name_dns_check
- nx_secure_x509_extension_find
