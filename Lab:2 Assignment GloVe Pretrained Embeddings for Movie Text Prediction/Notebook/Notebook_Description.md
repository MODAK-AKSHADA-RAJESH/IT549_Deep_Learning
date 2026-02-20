# IT549 – Deep Learning  
## Lab 2: GloVe-Based Movie Text Prediction  

### Notebook Description

This notebook implements the complete workflow for Lab 2, demonstrating the use of pretrained GloVe embeddings for text-based prediction tasks on movie metadata.

The notebook is organized into the following stages:

---

## 1. Data Preparation

- Load the movie dataset.
- Retain only the required columns:
  - `overview`
  - `tagline`
  - `keywords`
  - `genre`
  - `voting_average`
- Perform text preprocessing:
  - Lowercasing
  - Removal of URLs, punctuation, and numbers
  - Tokenization
  - Stopword removal
  - Lemmatization
- Create reproducible train/validation/test splits (70/15/15).

---

## 2. GloVe Embedding Construction

- Download and load pretrained GloVe embeddings (`glove.6B.100d.txt`).
- Map each word to its 100-dimensional vector.
- Compute embedding coverage for the dataset vocabulary.
- Construct document-level embeddings using weighted averaging of GloVe vectors.
- Ensure consistent embedding dimensionality (100D) across all experiments.

These embeddings serve as the foundational representation for all downstream models.

---

## 3. Rating Prediction (Regression)

- Train a neural regression model using document embeddings.
- Predict `voting_average`.
- Compare performance with a baseline model (global mean).
- Report:
  - Mean Squared Error (MSE)
  - Root Mean Squared Error (RMSE)
- Repeat experiments for multiple single-text inputs.

---

## 4. Multi-Label Genre Classification

- Encode genre labels using a multi-label format.
- Train a neural classifier with sigmoid outputs.
- Use `BCEWithLogitsLoss` for optimization.
- Evaluate using:
  - Micro-F1
  - Macro-F1
  - Hamming Loss
  - Jaccard Score
- Compare results across different text inputs.

---

## 5. Text Analysis

- Identify frequent words per genre.
- Extract genre-indicative words using TF-IDF combined with logistic regression.
- Interpret how vocabulary differs across genres.

---

## Summary

This notebook demonstrates how pretrained semantic embeddings can be integrated into regression and multi-label classification pipelines, while also providing interpretable linguistic insights into genre-specific language patterns.
