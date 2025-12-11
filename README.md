# Progetto Big Data – Classificazione di Articoli Wikipedia con PySpark

Questo repository contiene lo script `progetto_big_data_profai.py`, sviluppato come progetto didattico per il corso Big Data ProfAI.  
Il lavoro si concentra sull’analisi di un dataset di articoli di Wikipedia, sulla generazione di visualizzazioni testuali e sulla costruzione di un modello di classificazione tramite PySpark e Spark MLlib.

---

## 🎯 Obiettivi del progetto

- Analizzare articoli Wikipedia con tecniche di Big Data.
- Effettuare pulizia, preparazione e trasformazione del testo.
- Generare visualizzazioni qualitative (Word Cloud).
- Addestrare modelli di classificazione basati su Logistic Regression.
- Valutare qualità del modello tramite metriche come Accuracy e F1-score.

---

## 📂 Dataset


Contenuto del dataset:

- **title** – titolo dell’articolo  
- **categoria** – label di classificazione  
- **summary** – breve riassunto  
- **documents** – contenuto testuale esteso  
- Una colonna di indice non necessaria, rimossa durante il preprocessing  

---

## 🔍 Panoramica dello script

### 1. Installazione e import delle librerie

Lo script installa e utilizza:

- PySpark  
- pandas  
- numpy  
- matplotlib  
- wordcloud  
- nltk (stopwords)

Vengono scaricate automaticamente le stopwords inglesi.

---

### 2. Caricamento dati ed EDA

- Lettura del dataset con pandas  
- Conversione in Spark DataFrame  
- Rimozione colonna superflua  
- Conteggio articoli per categoria  
- Analisi valori nulli  
- Prime statistiche descrittive sul testo  

---

### 3. Pulizia dei dati

- Identificazione delle righe con `summary` e `documents` nulli  
- Eliminazione dei soli casi “totalmente vuoti”  
- Sostituzione dei valori nulli con stringhe vuote  
- Verifica della consistenza dei dati dopo la pulizia  

---

### 4. Feature Engineering

Lo script crea nuove colonne utili all’analisi:

- Numero parole nel `summary`  
- Numero parole nei `documents`  
- Totale parole per articolo  
- Aggregazioni per categoria:
  - numero articoli
  - media parole
  - minimo e massimo numero di parole

Viene creata inoltre la colonna `sum_doc`, combinazione di summary e documents.

---

### 5. Word Cloud per categoria

Per ogni categoria:

- concatenazione del testo di tutti gli articoli  
- rimozione delle stopwords  
- generazione della Word Cloud tramite la libreria `wordcloud`  
- visualizzazione delle parole più frequenti per categoria  

---

### 6. Pipeline di Machine Learning con PySpark

Lo script costruisce una pipeline completa per la classificazione testuale:

1. **Tokenizer**  
2. **StopWordsRemover**  
3. **CountVectorizer**  
4. **StandardScaler**  
5. **LogisticRegression**

Sono incluse funzioni riutilizzabili:

- `evaluate_model()` – calcolo accuracy e F1  
- `pipe_transf()` – costruzione della pipeline  
- `fit_and_transform()` – addestramento e predizioni  
- `print_evaluation()` – stampa metrica finale  

---

### 7. Preparazione alle predizioni

- Encoding della colonna `categoria` in label numerica tramite `StringIndexer`  
- Suddivisione del dataset in:
  - 80% training  
  - 20% test  

---

### 8. Modelli addestrati

Vengono addestrati due modelli diversi:

#### 📌 Modello 1 – Basato su `summary`
- Testo breve  
- Pipeline addestrata su `summary`  
- Valutazione su train e test

#### 📌 Modello 2 – Basato su `documents`
- Testo completo degli articoli  
- Pipeline addestrata su `documents`  
- Valutazione su train e test

Per entrambi vengono forniti:

- **Accuracy**  
- **F1-score**

---

## 🧠 Competenze sviluppate

- Gestione Big Data con Spark DataFrame  
- NLP di base con PySpark  
- Bag of Words, Tokenizzazione, Stopwords  
- Addestramento e valutazione modelli con Spark MLlib  
- Generazione di visualizzazioni testuali (Word Cloud)  
- Feature engineering per dati testuali su larga scala  

---

## ▶️ Come eseguire lo script

### 1. Clona il repository

```bash
git clone https://github.com/<tuo-username>/<repo-name>.git
cd <repo-name>
