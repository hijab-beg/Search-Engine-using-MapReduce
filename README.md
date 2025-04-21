# TF-IDF Based Search Engine using MapReduce
## Overview

This project implements a **document retrieval system** using the **TF-IDF (Term Frequency-Inverse Document Frequency)** algorithm. It allows users to search a corpus of text sections and retrieves the most relevant ones using cosine similarity.

The system is broken into stages handled via two main scripts (`mapper.py` and `reducer.py`) and supported by several outputs including relevance scores, TF-IDF vectors, and cleaned data.

---

## Project Structure

```
.
├── base_code/                  # Additional helper code
├── mapper.py                  # MapReduce-style preprocessing: cleaning, tokenizing, stopword removal
├── reducer.py                 # TF-IDF computation, query vector comparison, ranking
├── sampled_data.csv           # Raw dataset samples
├── cleaned_dataset.csv        # Output of cleaned & tokenized data
├── tf_idf.txt                 # Document-wise TF-IDF vectors
├── term_frequency.txt         # Raw term frequencies per document
├── idf.txt                    # Inverse document frequency per term
├── query_vector.txt           # Vector representation of the user query
├── relevance.txt              # Document relevance scores (cosine similarity to query)
├── Top_Relevant_documents.txt # Final ranked output of documents
```

---

## Workflow

### 1. **Text Cleaning (mapper.py)**
- Removes HTML tags, punctuation, digits, and extra spaces.
- Converts to lowercase and removes stopwords using NLTK.
- Assigns a unique `ARTICLE_ID` to each cleaned section.
- Saves the cleaned output to `cleaned_dataset.csv`.

---

### 2. **TF-IDF Computation (reducer.py)**
- Loads the cleaned data.
- Constructs a vocabulary.
- Calculates:
  - **TF (Term Frequency)** from `term_frequency.txt`
  - **IDF (Inverse Document Frequency)** from `idf.txt`
  - **TF-IDF vectors** from `tf_idf.txt`
- A sample **query vector** is loaded from `query_vector.txt`.
- Cosine similarity is used to compute relevance (stored in `relevance.txt`).
- Top relevant results are saved in `Top_Relevant_documents.txt`.

---

## Output Files

| File | Description |
|------|-------------|
| `cleaned_dataset.csv` | Contains cleaned text with `ARTICLE_ID`. |
| `term_frequency.txt` | TF values: word frequency in each doc. |
| `idf.txt` | IDF values based on word document frequencies. |
| `tf_idf.txt` | TF-IDF vector for each document. |
| `query_vector.txt` | Vectorized representation of the input query. |
| `relevance.txt` | Cosine similarity scores between the query and documents. |
| `Top_Relevant_documents.txt` | Final ranked list of top results. |

---

## Notes

- The system simulates **MapReduce-style** processing for scalability.
- Results rely heavily on text preprocessing; accuracy improves with better query formulation and corpus quality.
- You can use any vectorized query as input by editing `query_vector.txt`.

---

