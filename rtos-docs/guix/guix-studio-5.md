---
title: GUIX Studio Screen Designer
description: La progettazione di schermate dell'applicazione è lo scopo principale di GUIX Studio.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d7a4ffca7d49a82b75ed756fc360a2f543faa8a9fe9d31e5a5ace39087c96568
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785782"
---
# <a name="chapter-5-guix-studio-screen-designer"></a>Capitolo 5: GuiX Studio Screen Designer

La progettazione di schermate dell'applicazione è lo scopo principale di GUIX Studio. La progettazione dello schermo viene eseguita tramite tutte le diverse visualizzazioni descritte in precedenza nel capitolo 3. Tuttavia, l'elemento principale della progettazione dello schermo in GUIX Studio è la visualizzazione di ***destinazione,*** in cui tutti gli elementi dello schermo vengono visualizzati visivamente e esattamente nello stesso modo in cui verranno visualizzati sullo schermo di destinazione incorporato. Questi elementi dello schermo possono essere selezionati, spostati, ridimensionati e così via tramite semplici operazioni con mouse e pulsanti. Inoltre, le operazioni sui pulsanti di allineamento e ordine Z sono disponibili negli oggetti selezionati. Le sottose sezioni seguenti descrivono diverse funzionalità della progettazione dello schermo di GUIX Studio. 

## <a name="creatingconfiguring-projects"></a>Creazione/configurazione di progetti

La creazione di progetti in GUIX Studio è semplice: è sufficiente selezionare il pulsante * Nuovo **Project** _ o la selezione del menu _*_Project,_*_ Nuovo Project . GuiX Studio visualizza quindi la finestra di dialogo _ *_Configura Project_** . In questa finestra di dialogo vengono specificate le impostazioni di visualizzazione di base, nonché le informazioni sul percorso in cui individuare il codice generato da GUIX Studio.

Quando viene creato un nuovo progetto, viene visualizzata la finestra di dialogo Configura progetto. Qui lo sviluppatore specifica il numero di schermi hardware disponibili nella destinazione e le proprietà di ogni visualizzazione. Le proprietà includono il nome logico della visualizzazione, la risoluzione x/y, la profondità e il formato dei colori e altre proprietà di visualizzazione. GUIX Studio supporta più schermi nello stesso progetto. Se sono necessari altri schermi, il campo ***Number of Displays** _ (Numero di schermi ) deve essere modificato in modo che corrisponda al numero di schermi nel dispositivo incorporato. Il numero massimo di schermi in un progetto è 4. _ *_La figura 21_** mostra la finestra di Project configurazione.

La modifica del progetto e/o delle impostazioni di visualizzazione viene eseguita tramite l'opzione di menu ***Configura, Project/Visualizza** _ oppure selezionando il progetto o la visualizzazione, facendo clic con il pulsante destro del mouse e scegliendo _*_Configura, Project/Visualizza_*_. In entrambi i casi, viene *_visualizzata la finestra_* di dialogo _ Configura Project * per facilitare le modifiche alle impostazioni del progetto e/o alla visualizzazione.

![Screenshot della finestra di dialogo Project configurazione.](./media/guix-studio/config_project.png)

**Figura 21**

Nel gruppo Directory è possibile specificare le directory di output predefinite per i file di origine e di intestazione C prodotti da Studio. Queste directory vengono in genere salvate in relazione al percorso del progetto per semplificare lo spostamento dei progetti da un computer a un altro o da un file system a un altro.

Nel campo Intestazioni aggiuntive è possibile specificare file di intestazione personalizzati. Se sono necessari più file di intestazione, usare il punto e virgola per delimitare l'elenco.

Quando si richiamano i comandi "Genera applicazione" o "Genera risorse" di Studio, si tratta delle directory predefinite in cui verranno scritti i file di origine. Naturalmente è possibile eseguire l'override di questi percorsi di directory in qualsiasi momento immettendo nuovi percorsi nella finestra di dialogo Directory di output.

## <a name="selecting-widgets"></a>Selezione dei widget

La selezione dei widget viene eseguita facendo clic sul widget nell'albero ***Project View** _ widget (* Project Visualizza _ widget) oppure facendo clic sul widget visibile nell'area Target View _*_(Visualizzazione di_*_ destinazione). Quando viene selezionato un singolo widget, le relative proprietà vengono visualizzate nell'area _*_Visualizzazione_*_ proprietà. _*_La figura 22_*_ mostra il widget "_*_button_**" selezionato.

![Screenshot del widget selezionato.](./media/guix-studio/select_button.png)

**Figura 22**

## <a name="using-properties"></a>Utilizzo delle proprietà

Come accennato in precedenza, le proprietà per un widget selezionato vengono presentate nella ***Visualizzazione Proprietà** _. Tutti i widget hanno un set comune di proprietà, oltre ad alcune proprietà specifiche per il tipo di widget specifico. Ad esempio, un widget pulsante ha una proprietà _ *_Pushed_** mentre un widget finestra no. Di seguito è riportato il set comune di proprietà del widget:

| Proprietà         | Significato                                                                               |
| ---------------- | ------------------------------------------------------------------------------------- |
| Tipo di widget    | Tipo di widget, come riferimento                                                                               |
| Nome widget      | Nome del widget, passato alla funzione di creazione del widget e usato per la denominazione delle variabili nei file di origine generati.               |
| Widget ID        | ID del widget. Questo valore ID viene usato per generare segnali dai widget figlio alle schermate padre.                            |
| Sinistra             | Coordinata più a sinistra del widget                                                                                                 |
| Inizio              | Coordinata superiore del widget                                                                                                  |
| Larghezza            | Larghezza del widget in pixel                                                                                                      |
| Altezza           | Altezza del widget in pixel                                                                                                     |
| Bordo           | Tipo di bordo del widget                                                                                                          |
| Modalità trasparente      | Deve essere controllato se il widget è parzialmente trasparente                                                                       |
| Disegna selezionati    | Deve essere selezionato se il widget deve inizialmente disegnare se stesso nello stato selezionato.                                            |
| Abilita           | Deve essere controllato se l'utente finale può selezionare o fare clic sul widget.                                                    |
| Accetta lo stato attivo    | Deve essere selezionato se il widget accetta lo stato attivo.                                                                                 |
| Alloca in fase di esecuzione | Deve essere controllato se il blocco di controllo widget deve essere allocato in modo dinamico.                                                 |
| Riempimento normale      | ID risorsa colore di riempimento normale                                                                                                  |
| Riempimento selezionato    | ID risorsa colore di riempimento selezionato                                                                                                |
| Funzione Draw    | Nome della funzione di disegno personalizzata definita dall'utente. Se questo campo è vuoto, viene usata la funzione di disegno standard per il tipo di widget. |
| Funzione Event   | Nome della funzione di gestione degli eventi personalizzata definita dall'utente. Se vuoto, viene usata la gestione degli eventi standard per questo tipo di widget.          |

***La figura 23*** mostra le proprietà di un widget finestra semplice.

![Screenshot delle proprietà di un widget finestra semplice.](./media/guix-studio/image57.jpg)

**Figura 23**

Molti tipi di widget hanno proprietà aggiuntive specifiche per ogni tipo di widget.

Ad esempio, nella figura 23 precedente il tipo di widget Finestra supporta un ID mappa pixel sfondo e un'impostazione di stile che indica se lo sfondo deve essere centrato o affiancato.

I widget di testo supportano un campo ID stringa, insieme agli stili di allineamento del testo e a una specifica del tipo di carattere. Le proprietà aggiuntive del widget sono in genere molto intuitive dopo aver letto la descrizione di ogni tipo di widget e gli stili disponibili e Create function parameters for that widget type (Crea parametri di funzione per tale tipo di widget).

## <a name="manipulating-widgets"></a>Modifica dei widget

Per modificare un widget, è innanzitutto necessario selezionare . A tale scopo, fare clic direttamente sul widget nella ***Visualizzazione** di destinazione _ o selezionarlo nell'albero del widget _ *_Project Visualizza_**. Una volta selezionato, il widget avrà un contorno tratteggiato. In questo stato può essere spostato semplicemente facendo clic sul widget e trascinandolo nella posizione desiderata sul relativo elemento padre. Se il widget è un widget di primo livello, il trascinamento del widget imposta in modo efficace la posizione iniziale del widget sulla visualizzazione di destinazione. Naturalmente è sempre possibile spostare o ridimensionare qualsiasi widget in qualsiasi momento usando l'API GUIX.

Per ridimensionare l'altezza del widget, posizionare il mouse sul bordo superiore del widget e attendere che il puntatore del mouse cambi in una freccia verso l'alto. A questo punto l'altezza del widget può essere modificata semplicemente spostando il mouse mentre il pulsante destro del mouse è premuto. La larghezza del mouse può essere ridimensionata in modo simile posizionando il puntatore del mouse sul bordo sinistro del widget. ***Figura 24** _ mostra il widget "_*_button_**" ridimensionato e spostato nell'area sinistra/superiore della finestra padre.

![Screenshot del widget del pulsante.](./media/guix-studio/resize_button.png)

**Figura 24**

## <a name="manipulating-multiple-widgets"></a>Modifica di più widget

Per selezionare più widget, fare clic su più widget nella visualizzazione di destinazione tenendo premuto ***CTRL.*** In questo modo verranno visualizzati tutti i widget selezionati con un contorno tratteggiato intorno. Si noti che quando si selezionano più widget, ogni widget nel gruppo di selezione deve essere un elemento figlio dello stesso elemento padre.

Dopo aver selezionato più widget, questi possono essere spostati contemporaneamente facendo clic all'interno di uno dei widget selezionati e spostando il mouse con il pulsante destro del mouse premuto. È anche possibile usare i pulsanti di allineamento sulla barra **degli** strumenti * per allineare il gruppo di widget selezionati. _*_La figura 25_*_ mostra i widget "_*_button_*_" e "_*_new button_*_" selezionati e la figura _*_26_*_ mostra il risultato della selezione del pulsante _ *_Align-Left_** mentre questi widget sono selezionati.

![Screenshot dei widget del pulsante e del nuovo pulsante selezionati](./media/guix-studio/multiple_select.png)

**Figura 25**

![Screenshot del risultato della selezione del Align-Left pulsante.](./media/guix-studio/align_left.png)

**Figura 26**

## <a name="cutcopypaste-operations"></a>Operazioni Taglia/Copia/Incolla

Un widget selezionato in ***Visualizzazione di destinazione** _ può essere tagliato, copiato e incollato in modo standard. I widget e le schermate possono essere copiati all'interno di un progetto o copiati da un progetto e incollati in un altro. La _*_barra degli strumenti_*_ include pulsanti per le operazioni taglia, copia e incolla. Nell'opzione di menu Modifica sono disponibili anche le stesse opzioni. Si noti che quando si incolla un widget, il widget padre deve essere selezionato prima di incollare il nuovo widget. _*_La figura 27_*_ mostra il risultato della selezione del widget "_*_button_**", della copia e del incollamento della copia nella stessa finestra.

![Screenshot delle operazioni taglia/copia/incolla.](./media/guix-studio/copy_paste_button.png)

**Figura 27**

Copiare e incollare all'interno di un progetto è in genere semplice perché le risorse che potrebbero essere richieste dai widget copiati sono sempre presenti quando si lavora all'interno di un progetto. Tuttavia, se si copia un widget dal progetto A e lo si incolla nel progetto B, possono verificarsi alcuni problemi con le dipendenze delle risorse.

Quando si copiano widget all'interno di Studio, l'applicazione Studio crea un elenco delle risorse richieste dai widget copiati e genera una tabella delle dipendenze delle risorse portabile sotto forma di CODICE XML che viene copiata negli Appunti di Windows, insieme alle informazioni effettive del widget copiate. Quando si incollano i widget in un progetto diverso, Studio esamina innanzitutto l'elenco delle dipendenze delle risorse e aggiunge le risorse necessarie al progetto aperto, se non esistono già. Studio identifica le risorse corrispondenti in base ai nomi degli ID risorsa e per le risorse stringa Studio confronta anche il contenuto della stringa. Se vengono trovate risorse corrispondenti, Studio aggiorna gli ID delle risorse dei widget incollati per usare correttamente le risorse nel nuovo progetto. Se le risorse non vengono trovate, vengono aggiunte.

Quando Studio aggiunge una risorsa al progetto come parte di un'operazione incolla del widget, Studio aggiunge effettivamente un collegamento alla risorsa nel caso di risorse di tipo carattere e mappa pixel. Questo collegamento viene generato dal progetto di origine e si riceveranno messaggi di avviso se tali risorse non vengono trovate rispetto al percorso del progetto in cui si incolla. I collegamenti alle risorse verranno aggiunti al progetto indipendentemente, ma potrebbe essere necessario copiare manualmente i tipi di carattere e i file di immagine nei percorsi adeguati sotto il nuovo albero del progetto per eliminare gli errori di caricamento delle risorse. Studio non copia i file con estensione ttf, .png o .jpg da un percorso a un altro.

Il modo più semplice per evitare eventuali problemi in questo senso è mantenere una struttura di directory coerente tra i progetti che si vuole condividere. Se si vuole spostare facilmente elementi da Project A a Project B, mantenere le immagini grafiche e i tipi di carattere usati da entrambi i progetti in una sottodirectory coerente di ogni cartella di progetto.

## <a name="changing-z-order"></a>Modifica dell'ordine Z

I widget possono essere spostati facilmente davanti o dietro altri widget. A tale scopo, selezionare il widget e selezionare i _**_ pulsanti ***Sposta** in primo piano _ o Sposta indietro sulla barra _*_degli strumenti_*_. _ *_Figura 28_** mostra lo spostamento del secondo pulsante in secondo piano.

![Screenshot dell'ordine Z del pulsante.](./media/guix-studio/change_z_order.png)

**Figura 28**

## <a name="assigning-colors-fonts-and-pixelmaps"></a>Assegnazione di colori, tipi di carattere e mappe pixel

Oltre a selezionare colori, tipi di carattere e mappe pixel nella visualizzazione Proprietà per un widget selezionato, è supportato anche un metodo di trascinamento a sintassi abbreviata per l'assegnazione di risorse ai widget. Per usare questa funzionalità, è sufficiente fare clic con il pulsante sinistro del mouse su una risorsa, ad esempio un colore del tipo di carattere nella visualizzazione delle risorse, e trascinare la risorsa sul widget desiderato nella visualizzazione di destinazione. Rilasciare la risorsa rilasciando il pulsante sinistro del mouse sul widget.

Le risorse colore vengono sempre assegnate al colore di sfondo normale del widget quando si usa il metodo di trascinamento della selezione. È necessario assegnare altri colori, ad esempio il colore selezionato o il colore del testo selezionato, usando la visualizzazione Proprietà.

Analogamente, le risorse della mappa pixel vengono assegnate al campo "normale" o "riempimento" della mappa pixel di un widget che supporta la visualizzazione della mappa pixel. Per assegnare altri campi a un widget che supporta più mappe pixel, è necessario usare la visualizzazione Proprietà.

## <a name="using-templates"></a>Uso di modelli

Qualsiasi schermata o raccolta di widget figlio che si progetta in Studio può essere usata come modello per le nuove schermate e i nuovi controlli figlio. È possibile basare un modello su un widget di tipo Finestra, che è il caso d'uso normale, o su qualsiasi altro tipo di widget. L'uso di un modello è simile alla copia e incolla di un widget, ad eccezione del fatto che qualsiasi elemento derivato da un modello viene modificato automaticamente quando viene modificato il modello su cui si basa. Non è consentito modificare le proprietà del widget del modello quando si lavora con una schermata derivata o un'istanza ereditata del modello. Tuttavia, quando si modificano le proprietà del modello in qualsiasi modo, tutte le istanze che fanno riferimento a tale modello vengono aggiornate automaticamente, poiché derivano da tale modello.

Un altro vantaggio dell'uso dei modelli per gli elementi ripetuti è che le dimensioni del file delle specifiche generate da Studio saranno in genere inferiori rispetto alla ricreazione degli elementi ripetuti ogni volta che vengono usati.

Per indicare che una schermata o una raccolta di widget figlio deve essere usata come modello, si attiva la casella di controllo "Modello" nella visualizzazione delle proprietà del widget. Dopo aver selezionato la casella di controllo "Modello", il widget del modello verrà visualizzato in ***Inserisci| Menu a*** discesa modello.

Come esempio di utilizzo di un modello, è possibile definire una finestra che viene usata come barra dei pulsanti. Questa finestra può contenere diversi pulsanti figlio e questa barra dei pulsanti viene usata di frequente su varie schermate. È possibile definire una piccola finestra autonoma all'interno del progetto di Studio che contiene i pulsanti figlio necessari e assegnare a questa finestra il nome "button_bar". Selezionare quindi questa finestra e attivare la proprietà "Modello". Selezionare quindi una schermata in cui si vuole aggiungere questa barra dei pulsanti. Usare l'istruzione Insert| Modello|button_bar comando di menu per inserire un'istanza della button_bar nella schermata. Si noti che è possibile riposizionare la barra dei pulsanti, ma non è consentito modificare la maggior parte delle proprietà. È tuttavia possibile usare il widget button_bar (e tutti gli elementi figlio) esattamente come qualsiasi altro tipo di widget GUIX predefinito. Per modificare il button_bar, è necessario selezionare il modello button_bar per apportare le modifiche.

Un altro esempio di utilizzo tipico del modello è un'applicazione che include molte schermate simili. Ad esempio, l'applicazione potrebbe avere 10 schermate diverse che condividono tutte una barra del titolo comune, il colore di riempimento, le dimensioni e così via. In questo caso, è possibile definire una schermata modello che include i widget figlio della barra del titolo e configura le dimensioni dello schermo, il colore di riempimento e altre proprietà. Dopo aver definito questa schermata del modello, è possibile derivare le 10 schermate diverse da questo modello. Quando si usa l'istruzione Insert| Modello| \<base_screen> comando di menu , la schermata verrà avviata con tutti i widget figlio e le impostazioni della schermata del modello. Si noti che ogni schermata derivata dalla schermata del modello non è una copia del modello, ma è realmente un'istanza derivata della schermata del modello. È quindi possibile personalizzare ogni schermata derivata in modo da contenere il contenuto aggiuntivo necessario.

Si noti che, oltre a salvare le dimensioni del file delle specifiche generate, l'uso di modelli può semplificare la gestione delle modifiche all'aspetto dell'applicazione. Nell'esempio precedente si supponga che sia necessario modificare il colore di sfondo delle 10 schermate simili. Anziché essere necessari per selezionare ogni schermata e modificare le impostazioni del colore di riempimento, è necessario selezionare solo il modello di base e modificarne il colore di riempimento. Questa modifica verrà immediatamente riflessa in tutte le schermate derivate.

Un ulteriore commento relativo ai modelli: è necessario garantire che il flusso di elaborazione degli eventi sia mantenuto, vale a dire che se si fornisce un gestore eventi per una schermata di base (per la gestione degli eventi widget comuni) e per una schermata derivata, il gestore eventi dello schermo derivato deve chiamare il gestore dell'evento base_screen nel caso predefinito. In questo modo il gestore eventi dello schermo di base può elaborare gli eventi generati dai widget comuni a tutte le schermate derivate da questa base di modelli.

## <a name="record-and-playback-macro"></a>Macro di registrazione e riproduzione

Le funzioni di registrazione e riproduzione di macro consentono di registrare e riprodurre sequenze di tasti ed eventi del mouse.

La registrazione in un file macro viene eseguita selezionando il pulsante della barra degli strumenti ***Registra macro** _ o scegliendo _*_Modifica, Registra macro_*_ dal menu. GUIX Studio visualizza la finestra _*_di dialogo Registra macro_*_ che consente di specificare il percorso del file macro. Dopo aver selezionato questa opzione, fare clic sul _*_pulsante Registra_*_ per avviare la registrazione. Al termine della registrazione, selezionare di nuovo il pulsante della barra degli strumenti _*_Registra_*_ macro o usare il menu a discesa selezionando _ *_Modifica, Termina macro_** per terminare la registrazione macro.

La riproduzione di un file di macro viene eseguita selezionando il pulsante della barra degli strumenti ***Macro** di riproduzione _ usando il menu a discesa principale per selezionare il comando _*_Modifica, Macro di_*_ riproduzione. GUIX Studio presenta la finestra di dialogo _ *_Playback Macro_** che consente di specificare il file macro registrato in precedenza da eseguire.

Quando si registrano macro che scelgono file di input o di output, ad esempio l'aggiunta di un tipo di carattere o di un'immagine, è importante usare la tastiera per digitare il nome del file, anziché usare il mouse per selezionare dal browser di file. Poiché il registratore di macro registra gli eventi del mouse e della tastiera e poiché il browser dei file può cambiare nel tempo, è più affidabile digitare il nome del file che selezionare il file graficamente.

## <a name="zooming-target-view"></a>Visualizzazione destinazione zoom

La funzione Zoom avanti consente di ottenere una visualizzazione da vicino della schermata di destinazione.

È possibile scegliere l'impostazione di zoom percentuale desiderata in ***Configura| Visualizzazione di destinazione| Opzione** di menu Zoom _ . La barra *_degli strumenti_** include anche pulsanti per lo zoom avanti/indietro.

## <a name="gridsnap-settings"></a>Griglia/Blocca Impostazioni

La finestra di dialogo * Griglia **e blocca Impostazioni** _ contiene alcune impostazioni e opzioni per griglia e blocca. _*_La figura 29_*_ mostra la _*_finestra di dialogo Impostazione_*_ griglia e blocca quando il menu _ *_Congigure| Visualizzazione di destinazione| L'opzione Griglia/Blocca_** è selezionata.

![Screenshot delle opzioni Griglia e Blocca Impostazioni.](./media/guix-studio/image63.jpg)

**Figura 29**

Attivare **l'opzione*** Mostra griglia _ per visualizzare la griglia nella schermata di destinazione. È possibile specificare l'incremento della griglia (in pixel) nel _*_campo Spaziatura_*_ griglia. L'opzione _ *_Blocca sulla_* griglia * consente di ottenere la posizione corretta di un widget. L'attivazione di questa opzione consente di attivare gli snap.

Quando ***l'opzione Griglia e*** blocca è abilitata:

- Se si trascina un oggetto con il mouse nella visualizzazione di destinazione, l'oggetto si sposterà in base all'incremento della griglia.
- Se si trascina il bordo di un oggetto da ridimensionare, il bordo che si sta trascinando verrà allineato alla posizione della griglia.
- Se si seleziona un oggetto e si utilizzano i tasti su/sinistra/giù/destra, il widget selezionato si  sposta in base all'incremento di allineamento, è possibile specificare l'incremento di allineamento (in pixel) nel campo Spaziatura di allineamento.
