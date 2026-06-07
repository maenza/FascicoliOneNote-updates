# FascicoliOneNote

**FascicoliOneNote** è uno strumento che converte automaticamente i documenti di un fascicolo (email, PDF, Word, immagini, archivi ZIP/RAR e altro) e li inserisce direttamente nelle pagine di **Microsoft OneNote**, una per ciascun documento.

È pensato per chi deve digitalizzare fascicoli cartacei o elettronici e vuole ritrovarli organizzati in OneNote senza dover fare copia-incolla a mano.

---

> ## ⚠️ Software artigianale — uso a proprio rischio
>
> FascicoliOneNote è un programma realizzato in maniera **artigianale**, da un singolo autore e senza una struttura di sviluppo professionale alle spalle. Viene fornito **"così com'è" (*as is*), senza garanzie di alcun tipo**, esplicite o implicite.
>
> **L'utente lo utilizza sotto la propria esclusiva responsabilità.** In particolare è tenuto a:
> - **verificare sempre i risultati** dell'elaborazione prima di considerare un fascicolo completo;
> - **conservare copie di sicurezza** dei file originali (il programma lavora su copie, ma la prudenza resta a carico dell'utente);
> - valutare l'idoneità del software al proprio caso d'uso.
>
> L'autore **non risponde** di eventuali perdite di dati, malfunzionamenti o danni diretti o indiretti derivanti dall'uso del programma.

---

## Cosa fa, in breve

1. Apre una finestra grafica dove scegli i file da elaborare, da qualsiasi cartella del computer (con i pulsanti **Aggiungi file/cartella** o trascinandoli) — **non serve copiarli a mano** nella cartella `input`, e gli originali non vengono toccati
2. Converte tutto in PDF (o lascia i PDF così come sono)
3. Apre una finestra dove scegli in quale blocco appunti e sezione di OneNote inserire i documenti
4. Inserisce ogni documento come pagina separata in OneNote
5. Sposta automaticamente nel Cestino di Windows tutti i file elaborati (sia da `input` che da `output`)
6. Il programma è già pronto per il prossimo fascicolo

---

## Requisiti prima di iniziare

- **Windows 10 o 11**
- **Microsoft OneNote** installato e aperto (non la versione web — quella da Microsoft 365 o quella inclusa con Office)
- Il programma installato tramite il file `FascicoliOneNote_Setup.exe`

> **Importante:** OneNote deve essere già aperto e il blocco appunti dove vuoi inserire i documenti deve essere visibile prima di avviare lo script. Se OneNote è chiuso, lo script non trova nulla.

---

## Dove si trova il programma dopo l'installazione

L'installer crea la cartella:

```
Documenti\FascicoliOneNote\
```

All'interno trovi:

| Cartella / File | A cosa serve |
|---|---|
| `input\` | **Qui metti i file da elaborare** |
| `output\` | Qui vengono salvati i PDF convertiti (temporaneamente) |
| `fascicolo.bat` | **Questo avvii per la prima fase** — converte i file |
| `fascicolo.py` | Lo script Python (non aprire direttamente) |
| `inserisci_onenote.ps1` | **Questo avvii per la seconda fase** — inserisce in OneNote |

---

## Come si usa — passo per passo

### Passo 1 — Prepara i file

A partire dalla versione **1.0-alpha11** non serve più copiare i file a mano nella cartella `input`: all'avvio si apre una **finestra grafica** dove scegliere i file da qualsiasi cartella del computer.

- Pulsante **Aggiungi file…** per scegliere uno o più file
- Pulsante **Aggiungi cartella…** per aggiungere tutti i file di una cartella
- **Trascinamento** (drag & drop): puoi trascinare i file direttamente nella finestra
- Pulsante **Rimuovi selezionati** per togliere i file selezionati dall'elenco
- Pulsante **Avvia elaborazione** per procedere (in blu, in basso a destra)
- Pulsante **Annulla** per uscire senza fare nulla

Nell'elenco, ogni riga mostra il nome del file e tra parentesi quadre la cartella di origine — utile per riconoscere file con lo stesso nome provenienti da cartelle diverse.

Se premi **Avvia elaborazione** senza aver aggiunto nessun file, appare un avviso e puoi continuare ad aggiungere file.

> **I tuoi file originali NON vengono toccati:** il programma ne fa una copia di lavoro nella cartella `input` e a fine operazione cancella solo quelle copie. Gli originali restano dove sono.

In alternativa puoi ancora copiare i file manualmente nella cartella `input` (vengono pre-caricati nell'elenco):

```
Documenti\FascicoliOneNote\input\
```

Puoi aggiungere quanti file vuoi. I formati supportati sono:

- **Email:** `.eml`, `.msg` (inclusi allegati — vengono estratti automaticamente)
- **Documenti firmati digitalmente:** `.p7m` (firma CAdES/CMS tipica delle PEC — il documento interno viene estratto automaticamente)
- **Documenti:** `.pdf`, `.docx`, `.doc`, `.rtf`, `.txt`
- **Immagini:** `.jpg`, `.jpeg`, `.gif`, `.tiff`, `.bmp`, `.png`
- **Immagini mediche:** `.dcm` (DICOM)
- **Archivi:** `.zip`, `.rar`, `.arj` (il contenuto viene estratto e convertito)
- **Pagine web:** `.htm`, `.html`, `.xml`
- **Video:** `.mp4`, `.avi`, `.mov`, `.wmv` e altri (vengono inseriti come allegati in OneNote)
- **Audio:** `.mp3`, `.wav`, `.flac` e altri (inseriti come allegati)
- **Qualsiasi altro formato** — file con estensioni non riconosciute vengono inseriti in OneNote come allegati diretti (cliccabili), senza conversione

---

### Passo 2 — Avvia la conversione

Fai doppio clic su **`fascicolo.bat`** oppure usa l'icona sul desktop o nel menu Start.

Si apre una finestra nera (il terminale). Lo script inizia ad elaborare i file uno per uno e mostra una barra di avanzamento:

```
Trovati 12 file. Inizio elaborazione...

Elaborazione file: 100%|████████████| 12/12 [00:45]
  OK: Lettera_avvocato
  OK: Contratto_2024
  OK (PDF diretto): Perizia_tecnica
  ...

Completato. 12 PDF pronti in: C:\Users\...\output

Premi Invio per continuare...
```

Quando compare **"Premi Invio per continuare..."**, l'elaborazione è finita. Premi Invio per chiudere la finestra.

> Se vedi messaggi del tipo `ATTENZIONE: formato non supportato`, significa che alcuni file non possono essere convertiti e verranno saltati. Non è un errore bloccante — gli altri file vengono elaborati normalmente.

---

### Passo 3 — Apri OneNote

Prima di procedere:

1. Apri **Microsoft OneNote** (non la versione web)
2. Assicurati che il blocco appunti dove vuoi inserire i documenti sia aperto e visibile

Se OneNote non è aperto, lo script del passo successivo non trova nessun blocco appunti e non può procedere.

---

### Passo 4 — Inserisci in OneNote e cancella i file

Questo passo viene avviato **automaticamente** dal `.bat` subito dopo la conversione. Non devi fare nulla di aggiuntivo.

Si apre una piccola finestra con tre campi:

```
┌─────────────────────────────────────────┐
│  Blocco appunti:  [ Studio Legale    ▼] │
│                                         │
│  Sezione esistente: [ Fascicoli      ▼] │
│                                         │
│  Oppure crea nuova sezione:             │
│  [________________________________]     │
│                                         │
│      [Conferma]      [Annulla]          │
└─────────────────────────────────────────┘
```

**Come compilare la finestra:**

- **Blocco appunti** — seleziona dall'elenco il blocco appunti OneNote dove vuoi salvare i documenti
- **Sezione esistente** — se vuoi aggiungere i documenti a una sezione che esiste già, selezionala qui
- **Oppure crea nuova sezione** — se vuoi creare una sezione nuova (es. il nome del fascicolo), scrivi il nome qui e lascia il campo "Sezione esistente" come sta

Clicca **Conferma**. Lo script inizia a inserire i PDF in OneNote, uno per pagina, mostrando il progresso nella finestra PowerShell:

```
Inserisco 12 PDF in OneNote...
  -> [1/12] Lettera_avvocato
     OK (4 pagine)
  -> [2/12] Contratto_2024
     OK (12 pagine)
  ...

Completato! Tutti i file sono stati inseriti in OneNote.
Premi Invio per chiudere
```

Quando compare **"Premi Invio per chiudere"**, l'operazione è terminata. Apri OneNote e troverai tutti i documenti inseriti come pagine nella sezione scelta.

---

### Passo 5 — I file vengono spostati nel Cestino

Dopo che hai premuto Invio per chiudere la finestra di OneNote, il programma sposta automaticamente nel **Cestino di Windows** tutti i file nelle cartelle `input` e `output`. La finestra avvisa con un messaggio:

```
*** ATTENZIONE ***
I file elaborati sono stati spostati nel Cestino di Windows.
Se non ti servono piu', ricordati di svuotare il Cestino
per liberare spazio su disco.
```

I file non sono ancora cancellati definitivamente — sono nel Cestino e puoi recuperarli se necessario. Quando sei sicuro che tutto è andato a buon fine, svuota il Cestino per liberare spazio.

Il programma è già pronto per il prossimo fascicolo.

---

## Domande frequenti

**I file che metto in `input` vengono cancellati?**
Sì. Al termine dell'operazione, dopo che hai premuto Invio, i file in `input` e in `output` vengono spostati nel Cestino di Windows. Puoi recuperarli dal Cestino finché non lo svuoti, ma per sicurezza **usa sempre copie** dei file originali, non gli originali stessi.

**Ho un'email con molti allegati. Come viene trattata?**
Lo script apre l'email, estrae il testo del corpo e tutti gli allegati, e li converte. Il risultato è un unico PDF per ogni email, che contiene il testo e tutti gli allegati leggibili uno dopo l'altro.

**Ho un file ZIP o RAR con dentro tanti documenti. Come funziona?**
L'archivio viene estratto automaticamente. Ogni documento trovato dentro viene convertito separatamente. Il risultato è un PDF con tutti i documenti dell'archivio uniti in sequenza.

**Cosa succede con i video e gli audio?**
Non vengono convertiti in PDF. Vengono copiati nella cartella `output` con un prefisso `_video_` o `_audio_` e inseriti in OneNote come file allegati (cliccabili dalla pagina).

**OneNote dice "chiamata respinta" o vedo messaggi di errore con tentativi?**
OneNote a volte è occupato mentre elabora la pagina precedente. Lo script lo gestisce automaticamente e riprova fino a 5 volte aspettando qualche secondo tra un tentativo e l'altro. Di solito si risolve da solo.

**Il programma si blocca o non trova Python?**
Prova a riavviare il computer dopo l'installazione. L'installer aggiunge Python al percorso di sistema e a volte serve un riavvio perché la modifica sia attiva.

**Ho un file `.p7m` (firma digitale PEC). Viene elaborato?**
Sì. I file `.p7m` sono documenti con firma digitale CMS (tipici delle PEC italiane): il programma estrae automaticamente il documento originale contenuto al loro interno (PDF, Word, ecc.) e lo converte normalmente. I file `.p7s` e `.p7b`, che contengono solo la firma senza documento, vengono invece saltati.

---

## Struttura delle cartelle

```
Documenti\
└── FascicoliOneNote\
    ├── input\          ← metti qui i file del fascicolo
    ├── output\         ← PDF convertiti (temporanei)
    ├── fascicolo.bat   ← PASSO 1: converti
    ├── fascicolo.py    ← script Python (non aprire)
    └── inserisci_onenote.ps1  ← PASSO 2: inserisci in OneNote
```

---

## Versione

**1.0-beta6** — Windows **x64** (beta pubblica)

> La beta pubblica è disponibile **solo per Windows x64**. La versione **ARM64** è un progetto separato, **ancora in fase di test e non distribuita**: i test su hardware ARM non hanno dato esito positivo, quindi non viene pubblicata finché non è pronta.

Novità della beta6:
- **Stabilità file .msg con .eml allegata:** una PEC inoltrata come `.msg` con la mail originale in allegato `.eml` ora viene elaborata correttamente. Prima causava un errore e l'intero file veniva saltato.
- **Sicurezza email annidate:** aggiunto un limite di profondità (50 livelli) per i messaggi `message/rfc822` annidati. Un file con annidamento eccessivo non causa più un crash; il messaggio più profondo viene allegato come `.eml` originale senza perdita di dati.

Novità della beta5:
- **Controllo aggiornamenti integrato:** all'avvio il programma verifica (in modo silenzioso e non bloccante) se è disponibile una versione più recente e, in tal caso, mostra un avviso con il link per scaricarla.
- **Punto di ripristino con feedback:** durante l'installazione la creazione del punto di ripristino mostra ora una finestra visibile con lo stato di avanzamento (prima girava nascosta e l'installer sembrava bloccato).

Novità della beta4:
- **Robustezza percorsi:** lo spostamento dei file nel Cestino ora funziona anche se il percorso utente contiene un apostrofo (es. `Dell'Aquila`).
- **Sicurezza archivi:** gli archivi `.arj` sorgente troppo grandi (oltre 500 MB) vengono rifiutati prima dell'estrazione, evitando che un archivio molto compresso riempia il disco.

Novità della beta3:
- **Sicurezza:** Python aggiornato alla 3.12.10 (ultima patch ufficiale con installer Windows). All'avvio della conversione, se la libreria `defusedxml` non è presente, viene mostrato un avviso (il parsing XML userebbe altrimenti un fallback meno sicuro).

Novità della beta2:
- **Stabilità archivi:** anche i file dentro uno ZIP/RAR/ARJ che non si riescono a convertire (es. un `.doc` senza Word) vengono ora inseriti in OneNote come allegato, invece di essere ignorati.

Novità della beta1:
- **Più veloce:** i documenti vengono uniti in un unico PDF mantenendo il testo (niente più doppia conversione in immagini). L'inserimento in OneNote usa un'attesa intelligente al posto delle pause fisse.
- **Testo ricercabile:** i PDF prodotti mantengono il testo selezionabile dove possibile.
- **Più stabile:** Microsoft Word viene avviato una sola volta per tutto il fascicolo; gli allegati delle email non convertibili vengono comunque inseriti in OneNote come allegato (con il nome del file) invece di essere scartati.

Riepilogo delle versioni alpha precedenti:
- **alpha16:** installazione di Python robusta (installa se mancante, rilevamento via registro, diagnostica).
- **alpha13-15:** conversione `.doc` via Microsoft Word; correzioni avvio e installazione Python.
- **alpha11-12:** interfaccia grafica con drag & drop, punto di ripristino, hardening sicurezza (anti-XXE, anti zip-slip/zip-bomb, escape XML), allegati per i formati non convertibili.
