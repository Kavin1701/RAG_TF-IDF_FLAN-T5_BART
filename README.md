# 🧠 Retrieval-Augmented Generation using TF-IDF + BART/FLAN-T5

## 📌 Project Overview

This project implements a smart **question-answering system** that combines:

- **TF-IDF Retrieval:** Identifies the most relevant parts of a document for a user’s query.
- **Answer Generation with Transformers:** Uses models like **BART** or **FLAN-T5** to generate accurate, context-aware answers.

Think of it as an AI student — it first reads the notes (documents) and then writes the answer using its language skills!

---

## ⚙️ How It Works

### 1. 📄 Load and Clean the Documents
- Supports **PDF** and **.txt** files.
- Preprocessing includes:
  - Lowercasing
  - Removing extra spaces
  - Basic text cleanup

### 2. ✂️ Break into Sentences (Tokenization)
- Splits long text into overlapping chunks of sentences for contextual understanding.

### 3. 🧮 Build a TF-IDF Index
- Converts each chunk into numerical vectors using **TF-IDF**.
- Enables similarity comparison between user questions and document chunks.

### 4. 🔍 Retrieve Top Matches
- Calculates **cosine similarity** to retrieve the most relevant text chunks based on the question.

### 5. 🧠 Generate Answer
- Feeds the best-matching chunks into one of the following models to generate the final answer:
  - `facebook/bart-base`
  - `a-ware/bart-squadv2`
  - `google/flan-t5-base`
  - `sjrhuschlee/flan-t5-large-squadv2`

---

## 📊 Evaluation

We evaluate the answer quality using:
- **Exact Match (EM):** Is the answer exactly the same as the ground truth?
- **F1 Score:** Measures the overlap between the predicted and correct answers.

### 📈 Average Scores

| Model              | Exact Match (EM) | F1 Score         |
|--------------------|------------------|------------------|
| FLAN-T5            | 0.36             | 0.61             |
| FLAN-T5 (SQuAD2)   | 0.59             | 0.83             |
| BART               | 0.00             | 0.05             |
| BART (SQuAD2)      | 0.11             | 0.57             |

> 🔍 *FLAN-T5 fine-tuned on SQuAD2 achieved the best performance across both EM and F1 metrics.*

---

## 🛠 Installation

Before running the code, install the dependencies:

```bash
pip install spacy PyPDF2 transformers sentence-transformers scikit-learn
python -m spacy download en_core_web_sm
