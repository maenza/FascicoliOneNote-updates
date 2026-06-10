# FascicoliOneNote

**FascicoliOneNote** converte automaticamente i documenti di un fascicolo (email, PDF, Word, allegati PEC, archivi ZIP/RAR e altro) e li inserisce direttamente nelle pagine di **Microsoft OneNote**, una per ciascun documento.

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

## Scarica il programma

- **Windows x64** (la maggior parte dei PC): [FascicoliOneNote_Setup.exe](https://github.com/maenza/FascicoliOneNote-updates/releases/latest/download/FascicoliOneNote_Setup.exe)
- **Windows on ARM** (es. Surface con Snapdragon): [FascicoliOneNote_Setup_ARM64.exe](https://github.com/maenza/FascicoliOneNote-updates/releases/latest/download/FascicoliOneNote_Setup_ARM64.exe)

Tutte le versioni e le note di rilascio: [pagina delle release](https://github.com/maenza/FascicoliOneNote-updates/releases).

---
## Cosa fa, in breve

1. Apre una finestra grafica dove scegli i file da elaborare, da qualsiasi cartella del computer — **non serve copiarli a mano** nella cartella `input`, e gli originali non vengono toccati
2. Converte tutto in PDF (o lascia i PDF così come sono)
3. Apre una finestra dove scegli in quale blocco appunti e sezione di OneNote inserire i documenti
4. Inserisce ogni documento come pagina separata in OneNote
5. Sposta automaticamente nel Cestino di Windows tutti i file elaborati
6. Il programma è già pronto per il prossimo fascicolo

Tutto avviene **da un solo avvio**: fai le due scelte iniziali (file + destinazione OneNote), poi il programma procede da solo fino alla fine.

---

## Requisiti prima di iniziare

- **Windows 10 o 11**
- **Microsoft OneNote** installato (non la versione web — quella da Microsoft 365 o inclusa con Office). Se non è aperto, viene avviato automaticamente.
- Il programma installato tramite il file `FascicoliOneNote_Setup.exe`

---

## Come si usa

### Avvio

Fai doppio clic su **`fascicolo.bat`** (icona sul desktop o nel menu Start).

Si apre una finestra nera — non chiuderla — e subito dopo la finestra di selezione file.

---

### Scelta 1 — Seleziona i file

Si apre una finestra grafica con l'elenco dei file da elaborare.

- Pulsante **Aggiungi file…** per scegliere uno o più file
- Pulsante **Aggiungi cartella…** per aggiungere tutti i file di una cartella
- **Trascinamento** (drag & drop): puoi trascinare i file direttamente nella finestra
- Pulsante **Rimuovi selezionati** per togliere i file selezionati dall'elenco
- Pulsante **Avvia elaborazione** (in blu, in basso a destra) per procedere
- Pulsante **Annulla** per uscire senza fare nulla

Nell'elenco, ogni riga mostra il nome del file e tra parentesi quadre la cartella di origine — utile per riconoscere file con lo stesso nome provenienti da cartelle diverse.

> **I tuoi file originali NON vengono toccati:** il programma ne fa una copia di lavoro nella cartella `input` e a fine operazione cancella solo quelle copie.

In alternativa puoi copiare i file manualmente nella cartella `input` (vengono pre-caricati nell'elenco).

---

### Scelta 2 — Scegli la destinazione in OneNote

Subito dopo si apre una piccola finestra:

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

- **Blocco appunti** — seleziona il blocco appunti OneNote dove vuoi salvare i documenti
- **Sezione esistente** — se vuoi aggiungere i documenti a una sezione che esiste già, selezionala qui
- **Oppure crea nuova sezione** — scrivi il nome di una nuova sezione (es. il nome del fascicolo)

Clicca **Conferma**.

> Se OneNote non era aperto, il programma lo ha già avviato automaticamente in background durante la selezione file.

---

### Il programma procede da solo

Dopo la conferma, nella finestra nera scorrono i progressi di conversione e caricamento:

```
Fase 3: Conversione file in PDF...

Trovati 12 file. Inizio elaborazione...
Elaborazione file: 100%|████████████| 12/12 [00:45]
  OK: Lettera_avvocato
  OK: Contratto_2024
  OK (PDF diretto): Perizia_tecnica
  ...

Fase 4: Caricamento in OneNote...
  -> [1/12] Lettera_avvocato — OK (4 pagine)
  -> [2/12] Contratto_2024  — OK (12 pagine)
  ...

Fase 5: Spostamento file nel Cestino...
File spostati nel Cestino.
```

Al termine la finestra si chiude automaticamente dopo qualche secondo.

I file elaborati sono stati spostati nel **Cestino di Windows** — non sono ancora cancellati definitivamente. Quando sei sicuro che tutto è andato a buon fine, svuota il Cestino per liberare spazio.

> **Riepilogo finale:** al termine, nella cartella del programma viene aggiornato il file **`riepilogo_ultima_operazione.txt`** con il dettaglio di tutti i file caricati e gli eventuali errori.

---

## Ripresa di un caricamento interrotto

Se la finestra viene chiusa a metà del caricamento (es. per un crash o un riavvio), i file già caricati sono in OneNote e quelli non ancora caricati restano nella cartella `output`. Al prossimo avvio il programma lo rileva e chiede:

> **"Trovati N file non caricati da un'operazione interrotta. Riprendere?"**

- **Sì** — carica solo i file mancanti (nessun doppione in OneNote)
- **No** — i file rimasti vengono spostati nel Cestino e si ricomincia da capo

---

## Formati supportati

- **Email:** `.eml`, `.msg` (inclusi allegati — vengono estratti automaticamente)
- **Documenti firmati digitalmente:** `.p7m` (firma CAdES/CMS tipica delle PEC — il documento interno viene estratto automaticamente)
- **Documenti:** `.pdf`, `.docx`, `.doc`, `.rtf`, `.txt`
- **Fogli di calcolo:** `.xlsx`, `.xls`, `.xlsm` (richiede Microsoft Excel installato; se non disponibile, il file viene inserito come allegato)
- **Immagini:** `.jpg`, `.jpeg`, `.gif`, `.tiff`, `.bmp`, `.png`
- **Immagini mediche:** `.dcm` (DICOM)
- **Archivi:** `.zip`, `.rar`, `.arj` (il contenuto viene estratto e convertito; supporta compressione Deflate64 e archivi annidati fino a 8 livelli)
- **Pagine web:** `.htm`, `.html`, `.xml`
- **Video:** `.mp4`, `.avi`, `.mov`, `.wmv` e altri (inseriti come allegati in OneNote)
- **Audio:** `.mp3`, `.wav`, `.flac` e altri (inseriti come allegati)
- **Qualsiasi altro formato** — inserito in OneNote come allegato diretto (cliccabile), senza conversione

---

## Domande frequenti

**I file che metto in `input` vengono cancellati?**
Sì. Al termine dell'operazione i file in `input` e in `output` vengono spostati nel Cestino di Windows. Puoi recuperarli dal Cestino finché non lo svuoti, ma per sicurezza **usa sempre copie** dei file originali, non gli originali stessi.

**Ho un'email con molti allegati. Come viene trattata?**
Lo script apre l'email, estrae il testo del corpo e tutti gli allegati, e li converte. Il risultato è un unico PDF per ogni email, che contiene il testo e tutti gli allegati leggibili uno dopo l'altro.

**Ho un file `.p7m` (allegato PEC con firma digitale). Viene elaborato?**
Sì. I file `.p7m` contengono un documento con firma CAdES/CMS (tipica delle PEC italiane): il programma estrae automaticamente il documento interno (PDF, Word, ecc.) e lo converte normalmente. I file `.p7s` e `.p7b`, che contengono solo la firma senza documento, vengono invece saltati.

**Ho un file ZIP o RAR con dentro tanti documenti. Come funziona?**
L'archivio viene estratto automaticamente. Ogni documento trovato viene convertito separatamente. Sono supportati anche gli ZIP con compressione Deflate64 (il formato usato da «Cartella compressa» di Windows e da 7-Zip) e gli archivi annidati (zip-in-zip), fino a 8 livelli di profondità.

**Ho un foglio Excel. Viene convertito?**
Sì, se Microsoft Excel è installato sul computer. In caso contrario il file viene inserito in OneNote come allegato cliccabile.

**Cosa succede con i video e gli audio?**
Non vengono convertiti in PDF. Vengono inseriti in OneNote come file allegati cliccabili dalla pagina.

**OneNote dice "chiamata respinta" o vedo messaggi di errore con tentativi?**
OneNote a volte è occupato mentre elabora la pagina precedente. Lo script lo gestisce automaticamente e riprova più volte aspettando qualche secondo tra un tentativo e l'altro. Di solito si risolve da solo.

**Il programma si blocca o non trova Python?**
Prova a riavviare il computer dopo l'installazione. L'installer aggiunge Python al percorso di sistema e a volte serve un riavvio perché la modifica sia attiva.

---

## Struttura delle cartelle

```
Documenti\
└── FascicoliOneNote\
    ├── input\                           ← file del fascicolo (o scelti via GUI)
    ├── output\                          ← PDF convertiti (temporanei)
    ├── fascicolo.bat                    ← AVVIA QUESTO per elaborare un fascicolo
    ├── fascicolo.py                     ← script Python (non aprire direttamente)
    ├── inserisci_onenote.ps1            ← script PowerShell (non aprire direttamente)
    └── riepilogo_ultima_operazione.txt  ← log dell'ultima operazione
```

---

## Versione

**1.2** — Windows **x64** + **ARM64**

Novità della 1.2 (aggiornamento di sicurezza e stabilità — installazione consigliata):
- **Finestra nitida sugli schermi ad alta risoluzione:** la finestra di selezione file ora si adatta alla scala del monitor (125%, 150%, …). Prima, passando tra monitor con risoluzioni diverse, appariva piccola e sfocata.
- **Librerie sempre aggiornate:** l'installer aggiorna le librerie Python anche sulle installazioni esistenti, così le correzioni di sicurezza arrivano a tutti a ogni aggiornamento.
- **Estrazione archivi più sicura:** il limite anti «zip-bomb» è ora applicato ai byte realmente estratti, anche con archivi che dichiarano dimensioni false.
- **Riconoscimento file più preciso:** corretto il riconoscimento dei documenti RTF e dei file XML con BOM.
- **Robustezza:** limite di lettura sul manifest degli aggiornamenti; estrazione di sistema abbandonata dopo 30 s se improduttiva; in caso di errore grave nella conversione gli originali NON vengono più spostati nel Cestino.

Novità della 1.1 (aggiornamento di sicurezza — installazione consigliata):
- **Macro disattivate all'apertura dei documenti Office:** Word ed Excel vengono ora avviati con la sicurezza macro forzata al massimo, così le macro di un `.doc`/`.docx`/`.xls`/`.xlsm` **non** vengono eseguite durante la conversione. Poiché i documenti elaborati arrivano spesso da terzi (allegati PEC, `.p7m`, archivi), un file con macro malevole non può più eseguire codice sul computer.
- **Controllo aggiornamenti più sicuro:** il link di download proposto viene aperto solo se è un indirizzo `https://`.

Novità della 1.0:
- **Allegati `.p7m` (PEC) estratti correttamente:** un bug silenzioso causava la perdita del PDF estratto da un `.p7m`; ora compaiono in OneNote come previsto.
- **Fogli Excel (`.xlsx`/`.xls`/`.xlsm`):** convertiti in PDF se Excel è installato.
- **Email con solo corpo HTML:** le `.eml`/`.msg` senza testo semplice ora vengono convertite in PDF invece di finire come allegato originale.
- **ZIP con compressione Deflate64:** gli ZIP creati da «Cartella compressa» di Windows o da 7-Zip ora vengono sempre aperti.
- **Archivi dentro archivi:** un `.zip`/`.rar` dentro un altro archivio viene ora estratto e convertito anch'esso (fino a 8 livelli).
- **File `.rar` più affidabile:** individuazione automatica di UnRAR, con estrattore alternativo di riserva.
- **File temporaneamente bloccati:** se un file è occupato da antivirus o indicizzazione, l'elaborazione riprova automaticamente invece di scartarlo.
- **Avvio di OneNote più rapido:** OneNote si scalda in background durante la selezione file; il ritardo alla finestra di destinazione è quasi azzerato.
- **ARM64 distribuita pubblicamente:** la versione per Windows on ARM ha superato tutti i test su hardware reale ed è ora disponibile.
- **Python 3.13.12** (serie in manutenzione attiva con installer Windows ufficiale per x64 e ARM64).

Novità della beta7:
- Flusso scorrevole (scelte all'inizio, nessun "Premi Invio", chiusura automatica), riepilogo finale con log degli errori, avvio automatico di OneNote, ripresa dei caricamenti interrotti.

Novità della beta6:
- Stabilità file `.msg` con `.eml` allegata; limite di profondità per email annidate (anti-crash).

Novità della beta5:
- Controllo aggiornamenti integrato; punto di ripristino con feedback visivo durante l'installazione.

Novità della beta4:
- Robustezza percorsi con apostrofo; sicurezza archivi `.arj` di grandi dimensioni.

Novità della beta3:
- Python aggiornato a serie 3.13; avviso se la libreria `defusedxml` non è installata.

Novità della beta2:
- I file dentro un archivio non convertibili vengono inseriti come allegato invece di essere ignorati.

Novità della beta1:
- PDF con testo selezionabile; Word avviato una sola volta per tutto il fascicolo; allegati per i formati non supportati.

Riepilogo versioni alpha (storico sintetico):
- **alpha16:** installazione Python robusta (rilevamento via registro, diagnostica).
- **alpha13-15:** conversione `.doc` via Microsoft Word; correzioni avvio.
- **alpha11-12:** interfaccia grafica con drag & drop, punto di ripristino, hardening sicurezza (anti-XXE, anti zip-slip/zip-bomb, escape XML), allegati per formati non convertibili.
