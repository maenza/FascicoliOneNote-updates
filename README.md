# FascicoliOneNote — Distribuzione e aggiornamenti

Questo repository è il **canale pubblico di distribuzione** di
[FascicoliOneNote](https://github.com/maenza/FascicoliOneNote). Contiene **solo le
release** dell'installer (`FascicoliOneNote_Setup.exe`) — **nessun codice sorgente**.

## Scaricare l'ultima versione

L'installer più recente è sempre disponibile a questo link permanente:

**[⬇️ Scarica FascicoliOneNote_Setup.exe](https://github.com/maenza/FascicoliOneNote-updates/releases/latest/download/FascicoliOneNote_Setup.exe)**

Tutte le versioni: vedi la pagina [Releases](https://github.com/maenza/FascicoliOneNote-updates/releases).

## A cosa serve

Il programma controlla automaticamente se esiste una versione più recente leggendo un
piccolo manifest pubblico (`latest.json`). Quando ne trova una, mostra un avviso con il
link di download qui sopra. Questo permette di tenere il **codice sorgente privato** e,
allo stesso tempo, offrire un download pubblico senza richiedere alcun login.

## Per il manutentore — pubblicare una nuova versione

1. Compila l'installer dal repo privato (`build.ps1`).
2. Crea una nuova release qui e carica `FascicoliOneNote_Setup.exe` come asset
   (mantieni **esattamente** questo nome: il link permanente dipende da esso).
   Per le build ARM64 usa un nome distinto (es. `FascicoliOneNote_Setup_arm64.exe`).
3. Aggiorna il manifest `latest.json` (Gist) con il nuovo `build`, la nuova `version`
   e una `note`:
   `gh gist edit e8b7e2994a680e0f23774ac7298358e3 latest.json`

Entro 24 ore i PC con una versione precedente vedranno l'avviso di aggiornamento.
