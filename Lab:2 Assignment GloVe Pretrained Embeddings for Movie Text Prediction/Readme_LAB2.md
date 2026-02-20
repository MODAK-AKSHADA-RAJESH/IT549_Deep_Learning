# IT549 – Deep Learning  
## Lab 2 Assignment  
### GloVe Pretrained Embeddings for Movie Text Prediction  

**Name:** Akshada Modak  
**Student ID:** 202301485  

---

## 1. Project Overview

This project demonstrates the use of pretrained GloVe word embeddings for two predictive tasks using movie metadata text:

1. Rating Prediction (Regression): Predict `voting_average` from a single text column.
2. Genre Prediction (Multi-Label Classification): Predict movie genres from a single text column.

In addition, text-based analysis is conducted to:
- Identify frequent words per genre.
- Extract genre-indicative words using TF-IDF combined with logistic regression.

The goal is to evaluate how textual metadata captures semantic information useful for structured prediction tasks.

---

## 2. Dataset

Dataset: Movie Dataset (Kaggle)

Only the following columns were used:

- `overview` (text)
- `tagline` (text)
- `keywords` (text)
- `genre` (multi-label target)
- `voting_average` (regression target)

Each experiment was conducted using only one text column at a time, as required.

---

## 3. Task 1 – Data Preparation

### Preprocessing Steps

- Retained only the allowed columns.
- Removed rows with missing target values.
- Filled missing text fields with empty strings.
- Converted text to lowercase.
- Removed URLs.
- Removed numbers.
- Removed punctuation.
- Tokenized text.
- Removed stopwords.
- Applied lemmatization.

### Data Splits

The dataset was split into:

- 70% Training
- 15% Validation
- 15% Test

The split was made reproducible using `random_state = 42`.

---

## 4. Task 2 – GloVe Embedding Pipeline

### Embedding Configuration

- Pretrained GloVe embeddings: 100-dimensional vectors
- File used: `glove.6B.100d.txt`
- Embedding dimension was kept consistent across all experiments.

### Document Embedding Construction

Each document embedding was computed using TF-IDF weighted averaging of GloVe word vectors:

Document Embedding =  
(sum of TF-IDF(word) × GloVe(word)) / (sum of TF-IDF(word))

This approach combines:
- Semantic representation from GloVe.
- Importance weighting from TF-IDF.

### Embedding Coverage

Embedding coverage was computed as the percentage of unique dataset tokens present in the GloVe vocabulary.

---

## 5. Task 3 – Model A: Rating Prediction (Regression)

### Objective

Predict `voting_average` using document embeddings derived from text.

### Baseline Model

A baseline model was implemented that predicts the global mean rating of the training set.

### Neural Regression Model

Architecture:

- Linear(100 → 64) + ReLU
- Linear(64 → 32) + ReLU
- Linear(32 → 1)

Training Details:

- Loss function: MSELoss
- Optimizer: Adam
- Epochs: 30

### Evaluation Metrics

- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)

### Experiments Conducted

Experiments were conducted using:

- `overview`
- `tagline`

Results were compared against the baseline model.

### Observations

- `overview` performed best due to richer contextual information.
- `tagline` showed weaker performance due to limited textual content.
- The neural model outperformed the baseline, indicating that text contains predictive signal for ratings.

---

## 6. Task 4 – Model B: Genre Prediction (Multi-Label Classification)

### Objective

Predict multiple genres per movie using document embeddings.

### Multi-Label Setup

- One-vs-Rest formulation.
- Sigmoid activation per genre.
- Loss function: `BCEWithLogitsLoss`.

### Neural Network Architecture

- Linear(100 → 128) + ReLU
- Linear(128 → 64) + ReLU
- Linear(64 → Number of Genres)

### Evaluation Metrics

- Micro-F1 Score
- Macro-F1 Score
- Hamming Loss
- Jaccard Score

### Experiments Conducted

Experiments were conducted using:

- `overview`
- `tagline`

### Observations

- `overview` achieved higher Micro-F1 and Macro-F1 scores.
- Macro-F1 was lower than Micro-F1 due to genre imbalance.
- Textual descriptions provide strong signal for genre prediction.

---

## 7. Task 5 – Frequent Words per Genre

For each genre:

- Top 10 most frequent content words were extracted.
- Bottom 10 least frequent words (with frequency ≥ 3) were identified.

### Observed Patterns

- Action movies contained frequent conflict-related words such as war, battle, and mission.
- Romance movies emphasized relational vocabulary such as love and marriage.
- Horror movies contained fear-inducing words such as ghost and haunted.

Frequent word analysis confirmed intuitive semantic patterns associated with each genre.

---

## 8. Task 6 – Genre-Indicative Words Using TF-IDF

### Method

- TF-IDF features were computed from the text.
- One logistic regression classifier was trained per genre.
- Highest positive-weight coefficients were extracted to identify indicative words.

### Interpretation

High positive-weight words strongly increase the probability of a genre. For example:

- Action: war, battle, soldier
- Horror: haunted, ghost, killer
- Romance: love, relationship, marriage

Unlike frequency-based analysis, this method identifies discriminative words that differentiate genres from others.

---

## 9. Technologies Used

- Python
- NumPy
- Pandas
- Scikit-learn
- PyTorch
- NLTK
- Pretrained GloVe embeddings

---

## 10. Reproducibility

- Random seed fixed for dataset split.
- Embedding dimension fixed at 100.
- TF-IDF fitted only on training data to avoid data leakage.

---

## 11. Conclusion

This project demonstrates that pretrained word embeddings combined with TF-IDF weighting provide meaningful document representations. Textual metadata contains significant predictive signal for both rating prediction and multi-label genre classification. Linear models further provide interpretability by identifying genre-indicative vocabulary.
