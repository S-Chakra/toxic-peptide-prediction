# Toxic Peptide Prediction

Predicting whether a peptide is toxic from its amino acid sequence, using k-mer features and supervised machine learning. Final project for Bioinformatics and Computational Biology II at George Mason University.

## Why it matters

Antimicrobial peptides (AMPs) are a promising alternative to antibiotics, but some are toxic to human cells. A fast sequence-based screen can flag risky candidates before anyone spends time in the lab.

## Data

- `toxic_peptides.csv`: 2,000 peptide sequences labeled toxic or non-toxic
- `natural_amps.fasta`: 3,306 naturally occurring AMPs from the Antimicrobial Peptide Database

## Approach

1. Split each sequence into overlapping 3-mers and counted them, giving a bag-of-words feature vector per peptide.
2. Compared which 3-mers show up most often in toxic peptides versus non-toxic ones.
3. Split the data 70/30 (stratified) into training and test sets.
4. Trained a logistic regression model and a support vector classifier with scikit-learn.
5. Evaluated both with confusion matrices, accuracy, precision, recall, and ROC AUC.
6. Wrote a FASTA parser and ran both models on the 3,306 natural AMPs.

## Results (held-out test set)

| Model | Accuracy | Precision | Recall | ROC AUC |
|---|---|---|---|---|
| Logistic regression | 0.765 | 0.787 | 0.909 | 0.830 |
| Support vector classifier | 0.733 | 0.732 | 0.976 | 0.802 |

Logistic regression did better overall. The SVC caught more of the toxic peptides but flagged more safe ones too.

## Limitations and next steps

Both models have high recall but low specificity: they rarely miss a toxic peptide, but they also flag many non-toxic ones, and together they flag 2,945 of the 3,306 natural AMPs. The test set is imbalanced (419 toxic vs. 181 non-toxic), which likely pushes the models toward predicting "toxic." Next steps would be rebalancing the classes, tuning the decision threshold, and trying other values of k.

## Run it

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
jupyter notebook finalProject3.ipynb
```

Built with Python, pandas, NumPy, scikit-learn, and Matplotlib.
