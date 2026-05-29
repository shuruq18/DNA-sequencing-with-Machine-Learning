# DNA-sequencing-with-Machine-Learning
In this notebook, I will apply a classification model that can predict a gene's function based on the DNA sequence of the coding sequence alone.
https://nbviewer.org/github/shuruq18/DNA-sequencing-with-Machine-Learning/blob/main/DNA_Sequencing_NB_classifier%20.ipynb

---

## Overview

This project treats DNA sequences as a natural language and applies NLP-based feature extraction to classify genes into one of 7 functional classes. The core idea is that DNA sequences — like human language — can be broken down into meaningful "words" (k-mers) and analyzed using text classification methods.

---

## How It Works

### K-mer Counting (Bag of Words for DNA)

DNA sequences are converted into overlapping subsequences called **k-mers** (analogous to n-grams in NLP). For example, using a k-mer size of 6 (hexamers):

```
ATGCATGCA → ['ATGCAT', 'TGCATG', 'GCATGC', 'CATGCA']
```

These k-mer "words" are then joined into sentences and fed into a `CountVectorizer` with an n-gram range of `(4, 4)` to build a numerical feature matrix — effectively counting k-mer occurrences across all sequences.

### Classification

Two classifiers are trained and evaluated:

- **Logistic Regression** — used as a baseline
- **Multinomial Naive Bayes** (alpha=0.1) — the primary model, tuned via grid search

---

## Dataset

- **Source:** Human DNA coding sequence data (`human_data.txt`)
- **Target:** 7 gene function classes (relatively balanced distribution)
- **Preprocessing:** Missing class labels are filled using the mode; sequences are lowercased and split into k-mers

---

## Project Structure

```
├── DNA_Sequencing_NB_classifier_.ipynb   # Main notebook
└── sample_data/
    ├── human_data.txt                    # Input dataset
    └── download.png                      # Class label reference image
```

---

## Requirements

```
numpy
pandas
matplotlib
scikit-learn
```

Install dependencies with:

```bash
pip install numpy pandas matplotlib scikit-learn
```

---

## Usage

1. Clone the repository and navigate to the project folder.
2. Place `human_data.txt` in `sample_data/`.
3. Open and run the notebook:

```bash
jupyter notebook DNA_Sequencing_NB_classifier_.ipynb
```

---

## Results

The Multinomial Naive Bayes classifier achieves strong performance on the held-out test set (80/20 train-test split), evaluated using:

| Metric    | Description                                      |
|-----------|--------------------------------------------------|
| Accuracy  | Overall fraction of correct predictions          |
| Precision | Weighted precision across all 7 classes          |
| Recall    | Weighted recall across all 7 classes             |
| F1 Score  | Harmonic mean of precision and recall            |

The model generalizes well to unseen data with no signs of significant overfitting.

---

## Key Concepts

- **K-mer counting** — genomic equivalent of n-gram tokenization
- **CountVectorizer** — converts k-mer sentences into a sparse feature matrix
- **Multinomial Naive Bayes** — well-suited for high-dimensional count data
- **Gene function classification** — predicts one of 7 functional gene groups from sequence alone

---

## References

- [scikit-learn: MultinomialNB](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.MultinomialNB.html)
- [scikit-learn: CountVectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html)
- [pandas: DataFrame.fillna](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.fillna.html)
