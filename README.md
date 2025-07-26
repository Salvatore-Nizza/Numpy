# File Organizer - NumPy

Questo progetto Python è un **organizzatore di file** e uno **strumento di analisi delle immagini**, progettato per gestire e categorizzare file di diversi tipi e per estrarre informazioni dettagliate dalle immagini. Include una funzionalità di reportistica CSV e un'interfaccia a riga di comando per l'aggiunta di singoli file.

## Contenuto del Progetto

Il progetto è composto da:

*   Un **notebook Jupyter** (o script Python equivalente) che esegue l'organizzazione dei file (Step 1) e l'analisi delle immagini (Step 3).
*   Uno script Python `addfile.py` che fornisce un'interfaccia a riga di comando per lo spostamento di singoli file (Step 2).
*   Una cartella `files/` contenente i file di esempio da organizzare.

## Funzionalità

### Step 1: Organizzazione e Catalogazione dei File

Lo script principale nel notebook itera sui file presenti nella cartella `files/` e li sposta in sottocartelle dedicate in base al loro tipo.

*   **Organizzazione Automatica**: I file vengono spostati nelle sottocartelle `audio/`, `docs/`, e `images/`.
    *   File con estensioni `.jpg`, `.jpeg`, `.png` vengono classificati come "image".
    *   File con estensioni `.txt`, `.odt` vengono classificati come "doc".
    *   File con estensione `.mp3` vengono classificati come "audio".
*   **Creazione Sottocartelle**: Se una sottocartella non esiste, viene creata automaticamente.
*   **Informazioni in Tempo Reale**: Durante il processo, lo script stampa a schermo il nome, il tipo e la dimensione in byte di ciascun file spostato. Un esempio di output è: `nome_file type: tipo_file size: dimensioneB`.
*   **File di Recap**: Viene creato o aggiornato un file `recap.csv` con le stesse informazioni (nome, tipo, dimensione in byte) per tutti i file elaborati. Il file `recap.csv` è gestito in modalità "append" (`'a'`) per aggiungere nuove informazioni senza sovrascrivere quelle esistenti, e include un'intestazione per le colonne.

### Step 2: Aggiunta Singola di File tramite CLI

Lo script `addfile.py` è un eseguibile da linea di comando che permette di spostare un singolo file nella sua sottocartella appropriata e di aggiornare il `recap.csv`.

*   **Interfaccia CLI**: Accetta un unico argomento obbligatorio: il nome del file da spostare (incluso il formato, es. `'trump.jpeg'`).
*   **Gestione Errori**: Se il file specificato non esiste nella cartella `files/`, l'interfaccia comunica all'utente che il file non è stato trovato.

### Step 3: Analisi Dettagliata delle Immagini

Questo script, integrato nel notebook dello Step 1, itera sulla sottocartella `images/` per analizzare le caratteristiche di ciascuna immagine e costruire una tabella riassuntiva.

*   **Rilevamento Tipo Immagine**: Lo script determina se un'immagine è in scala di grigio (un solo livello di colore), RGB (3 livelli) o RGBA (4 livelli, l'ultimo è il canale alpha).
*   **Caricamento e Trasformazione**: Le immagini vengono caricate usando la libreria PIL e trasformate in array NumPy per l'analisi.
*   **Tabella Riassuntiva**: Viene generata una tabella dettagliata che include:
    *   Nome del file.
    *   Altezza e larghezza dell'immagine in pixel.
    *   Se l'immagine è in scala di grigio: la colonna `grayscale` indica la media dei valori dell'unico livello di colore.
    *   Se l'immagine è a colori (RGB/RGBA): le colonne `R`, `G`, `B` e `ALPHA` indicano la media dei valori di ciascun livello di colore.
*   **Formattazione Output**: La tabella è formattata professionalmente usando la libreria `tabulate`.

## Struttura della Cartella

La struttura finale attesa della cartella `files/` dopo l'esecuzione dello script di Step 1 è la seguente:

```
- files/
    - audio/
        - song1.mp3
        - song2.mp3
    - docs/
        - ciao.txt
        - pippo.odt
    - images/
        - bw.png
        - daffodil.jpg
        - eclipse.png
        - trump.jpeg
    - recap.csv
```

## Requisiti

Il progetto richiede le seguenti librerie Python, installabili tramite `pip`:

*   `os` (standard library, non necessita installazione)
*   `shutil` (standard library, non necessita installazione)
*   `csv` (standard library, non necessita installazione)
*   `sys` (standard library, non necessita installazione)
*   `argparse` (standard library, non necessita installazione)
*   `numpy` (`pip install numpy`)
*   `Pillow` (`pip install Pillow`) - per il modulo `PIL.Image`
*   `tabulate` (`pip install tabulate`)

## Come Utilizzare

1.  **Clona il Repository**: Clona questo repository sul tuo sistema locale.
2.  **Organizza i File**: Assicurati che il notebook principale e lo script `addfile.py` siano nella stessa cartella, e che la cartella `files/` sia allo stesso livello.
3.  **Installa le Dipendenze**: Esegui `pip install numpy Pillow tabulate` nel tuo ambiente Python.

### Esecuzione dello Step 1 (Organizzazione) e Step 3 (Analisi Immagini)

Apri il notebook Jupyter fornito (es. `nome_del_tuo_notebook.ipynb`) e esegui le celle in ordine. Lo script:

*   Importerà le librerie necessarie (`os`, `shutil`, `csv`, `numpy`, `PIL.Image`, `tabulate`).
*   Eseguirà l'organizzazione dei file nella cartella `files/`, spostandoli nelle rispettive sottocartelle e stampando le informazioni.
*   Aggiornerà o creerà il file `recap.csv`.
*   Successivamente, eseguirà l'analisi delle immagini presenti nella sottocartella `images/`, stampando la tabella riassuntiva.

### Esecuzione dello Step 2 (Aggiunta Singola File)

Dalla riga di comando, naviga nella directory del progetto ed esegui lo script `addfile.py` specificando il nome del file da spostare:

```bash
python addfile.py nome_file.estensione
```

Ad esempio:

```bash
python addfile.py esempio.txt
```

Se il file non esiste, riceverai un messaggio di errore.
