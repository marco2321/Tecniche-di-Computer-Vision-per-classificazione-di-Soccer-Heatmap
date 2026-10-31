# Tecniche di Computer Vision per la classificazione di Soccer Heatmap

## Descrizione del progetto

Il progetto esplora l'applicazione di tecniche di Machine Learning, Deep Learning e Computer Vision all'analisi dei dati calcistici, attraverso la generazione e l'elaborazione di heatmap spaziali.

L'obiettivo è trasformare i dati degli eventi di una partita in rappresentazioni numeriche e visive del campo da gioco, per analizzare la distribuzione delle azioni e sperimentare modelli capaci di riconoscere pattern spaziali.

Il lavoro è stato sviluppato nell'ambito della tesi triennale in Ingegneria Informatica presso l'Università degli Studi Roma Tre.

**Stato del progetto:** sviluppo degli esperimenti completato; tesi in fase di revisione e personalizzazione, con discussione prevista indicativamente a marzo 2027.

## Dataset

Il progetto utilizza gli StatsBomb Open Data, un dataset pubblico contenente dati calcistici strutturati in formato JSON.

I file contengono informazioni sulle partite e sugli eventi di gioco, comprese le coordinate spaziali delle azioni.

I dati vengono elaborati tramite Python per:
- individuare le partite e le squadre di interesse;
- estrarre eventi specifici, come passaggi, tiri e azioni difensive;
- recuperare le coordinate degli eventi sul campo;
- costruire rappresentazioni spaziali utilizzabili dai modelli di Machine Learning e Deep Learning.

## Metodologia e fasi sperimentali

Il progetto segue un percorso sperimentale progressivo, partendo dall'elaborazione dei dati grezzi fino all'applicazione di architetture neurali.

### 1. Preprocessing e generazione delle heatmap

- Lettura e organizzazione dei dati JSON di StatsBomb.
- Utilizzo di Pandas per la normalizzazione e il filtraggio degli eventi.
- Estrazione delle coordinate spaziali X e Y.
- Generazione di heatmap tramite Kernel Density Estimation (KDE), utilizzando Seaborn.
- Visualizzazione della distribuzione degli eventi sul campo da gioco.

### 2. Discretizzazione spaziale e feature extraction

Per rendere le rappresentazioni spaziali utilizzabili dagli algoritmi di Machine Learning, le heatmap vengono trasformate in matrici numeriche.

- Utilizzo di `numpy.histogram2d` per suddividere il campo in una griglia 25 × 25.
- Conversione delle coordinate in matrici di frequenza spaziale, composte da 625 celle.
- Aggregazione e normalizzazione delle heatmap.
- Confronto tra diverse distribuzioni spaziali attraverso la metrica Mean Squared Error (MSE).
- Sperimentazione di una rappresentazione semplificata del campo in nove macro-zone.

### 3. Machine Learning: classificazione con Random Forest

È stato sperimentato l'utilizzo di Random Forest per analizzare la relazione tra la distribuzione spaziale dei passaggi e il risultato delle partite.

Le attività comprendono:
- estrazione delle feature dalle heatmap;
- appiattimento delle matrici tramite `flatten()`;
- costruzione del dataset di addestramento;
- classificazione tramite `RandomForestClassifier` di Scikit-learn;
- valutazione mediante accuracy, confusion matrix, precision, recall e F1-score;
- analisi dell'importanza delle feature spaziali.

Sono stati inoltre analizzati i problemi legati all'elevata dimensionalità delle feature e allo sbilanciamento delle classi.

### 4. Deep Learning: reti neurali convoluzionali (CNN)

È stata sviluppata una rete neurale convoluzionale tramite TensorFlow e Keras per elaborare le heatmap come rappresentazioni bidimensionali.

L'esperimento è stato impostato come problema di regressione, con l'obiettivo di stimare l'indice di creatività individuale di un calciatore (Kevin De Bruyne).

L'architettura comprende:
- livelli convoluzionali `Conv2D`;
- livelli di riduzione dimensionale `MaxPooling2D`;
- funzione di attivazione ReLU;
- livello `Flatten`;
- livelli fully connected `Dense`;
- regolarizzazione tramite `Dropout`.

La valutazione è stata effettuata utilizzando MSE come funzione di perdita e MAE come metrica di valutazione.

### 5. Transfer Learning con VGG16

È stato sperimentato il Transfer Learning utilizzando l'architettura VGG16 pre-addestrata.

Gli strati convoluzionali pre-addestrati sono stati mantenuti congelati, mentre la testa classificatrice è stata adattata al problema di classificazione degli esiti delle partite.

Sono state sviluppate diverse configurazioni sperimentali:
- utilizzo di heatmap spaziali a singolo canale;
- generazione di rappresentazioni RGB multicanale;
- separazione delle informazioni in tre canali:
  - Rosso: eventi offensivi, come tiri e passaggi chiave;
  - Verde: passaggi e costruzione del gioco;
  - Blu: eventi difensivi, come duelli, intercetti, blocchi e spazzate;
- bilanciamento delle classi tramite undersampling;
- applicazione di tecniche di Data Augmentation, tra cui RandomFlip, RandomTranslation e RandomRotation.

### 6. Explainable AI: Grad-CAM

Per analizzare il comportamento della rete neurale è stata applicata la tecnica Grad-CAM (Gradient-weighted Class Activation Mapping).

Questa tecnica permette di visualizzare le regioni spaziali della heatmap che contribuiscono maggiormente alle predizioni della CNN, offrendo un supporto all'interpretazione del modello.

## Risultati sperimentali

Tra i risultati riportati nella tesi:

| Esperimento | Risultato |
|---|---|
| Random Forest con nove macro-zone | Accuracy del 72,64% |
| CNN per regressione dell'indice di creatività | MAE pari a 1,13 |
| VGG16 con heatmap RGB e Data Augmentation | Accuracy del 37,50% |

I risultati devono essere interpretati considerando le dimensioni e le caratteristiche dei dataset utilizzati, lo sbilanciamento delle classi e i limiti degli esperimenti.

In particolare, l'accuratezza della classificazione multiclasse con VGG16 evidenzia la difficoltà di ricavare previsioni affidabili dell'esito di una partita utilizzando esclusivamente rappresentazioni spaziali aggregate.

Il progetto ha quindi permesso di confrontare approcci differenti e analizzare criticamente le prestazioni e i limiti dei modelli implementati.

## Tecnologie e librerie

- **Linguaggio:** Python
- **Elaborazione dati:** NumPy, Pandas
- **Visualizzazione:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn
- **Deep Learning:** TensorFlow, Keras
- **Architetture e tecniche:** Random Forest, CNN, VGG16, Transfer Learning, Grad-CAM
- **Dataset:** StatsBomb Open Data

## Struttura del repository

```text
Tecniche-di-Computer-Vision-per-classificazione-di-Soccer-Heatmap/
│
├── Codice/
│   └── Script Python degli esperimenti
│
├── Immagini/
│   └── Immagini e visualizzazioni del progetto
│
├── Pdf/
│   └── Documenti PDF correlati alla tesi
│
├── README.md
├── Roma_Tre_nuovo_logo.png
└── roma3NuovoLogo.jpg
```

## Come eseguire il codice

Gli esperimenti sono organizzati in script Python distinti all'interno della cartella `Codice`.

### 1. Clonare il repository

```bash
git clone https://github.com/marco2321/Tecniche-di-Computer-Vision-per-classificazione-di-Soccer-Heatmap.git
cd Tecniche-di-Computer-Vision-per-classificazione-di-Soccer-Heatmap
```

### 2. Installare le librerie

Per l'esperimento Random Forest documentato nel repository:

```bash
pip install pandas numpy matplotlib scikit-learn seaborn
```

Per gli esperimenti di Deep Learning sono inoltre necessarie le librerie TensorFlow e Keras, disponibili tramite:

```bash
pip install tensorflow
```

### 3. Configurare il dataset

Scaricare gli StatsBomb Open Data e predisporre localmente i file JSON necessari.

Nei singoli script verificare e aggiornare i percorsi delle cartelle contenenti i dati, in particolare le directory `matches` ed `events`.

### 4. Avviare un esperimento

Per eseguire l'esperimento di classificazione del risultato del Barcellona basato sulle nove macro-zone:

```bash
cd Codice
python predizioneBarca526PartiteConMacroZone.py
```

Gli altri esperimenti devono essere avviati separatamente, facendo riferimento ai rispettivi script e alle relative configurazioni.

**Nota:** i percorsi dei dataset e le eventuali dipendenze specifiche devono essere configurati in base all'esperimento che si desidera eseguire.

## Possibili sviluppi futuri

Tra le possibili estensioni del lavoro:
- integrazione di informazioni temporali tramite architetture CNN-LSTM;
- utilizzo di Autoencoder per l'estrazione di rappresentazioni spaziali e l'individuazione di anomalie;
- integrazione di tracking data per analizzare le posizioni dei calciatori durante l'intera partita.

## Autore

**Marco Antonio Genovese**  
Studente di Ingegneria Informatica – Università degli Studi Roma Tre

[GitHub Profile](https://github.com/marco2321)
