# 1. PhiUSIIL Baseline Implementation

## Reference
**Paper:** PhiUSIIL: A Diverse Security Profile Empowered Phishing URL Detection Framework Based on Similarity Index and Incremental Learning

**Original code:** https://github.com/arvindbitm/PhiUSIIL

**Dataset:** https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset

## Implementation

This implementation adapts the authors' `MainModel_SplitBased_OneTime90.ipynb` notebook for Google Colab.

- Dataset: PhiUSIIL Phishing URL Dataset
- Training: 90%
- Online evaluation: 10%
- Classifiers: Bernoulli Naive Bayes, Passive-Aggressive, SGD
- Evaluation modes: LowSecurity, BestSecurity, HighSecurity

## Results

| Mode | Accuracy | Phishing F1 | MCC |
|---|---:|---:|---:|
| LowSecurity | 98.664% | 98.402% | 0.97291 |
| BestSecurity | 99.843% | 99.815% | 0.99679 |
| HighSecurity | 99.190% | 99.055% | 0.98360 |

The results were obtained using incremental evaluation, where predictions are generated before the models are updated with the corresponding examples.

## Reproduction

1. Open `PhiUSIIL_Implementation.ipynb` in Google Colab.
2. Run the cells in order.
3. The notebook loads the dataset, trains the models, evaluates them, and saves the metrics.

## Limitations

This experiment includes URL and webpage-derived features and is not a URL-only pre-navigation evaluation.

# 2. GramBeddings Baseline Implementation

## Reference

**Paper:** GramBeddings: A New Neural Network for URL Based Identification of Phishing Web Pages Through N-gram Embeddings

**Original code:** https://github.com/fcdalgic/GramBeddings

**Dataset:** Official GramBeddings dataset from Hacettepe University.

## Implementation

This baseline adapts the authors' GramBeddings implementation to run on Kaggle with TensorFlow.

The model uses character-level and n-gram embeddings with parallel CNN, BiLSTM, and attention branches for phishing URL classification.

**Configuration:**
- Training examples: 636,803
- Validation examples: 159,188
- N-grams: 3, 4, 5
- Maximum sequence length: 128
- Embedding dimension: 15
- LSTM cell size: 256
- Batch size: 128
- Epochs: 5
- GPU: Kaggle T4

The implementation includes compatibility changes to the authors' original code, including an update to the pooling operation.

## Results

| Metric | Value |
|---|---:|
| Validation accuracy | 98.08% |
| Validation precision | 98.56% |
| Validation recall | 97.57% |
| Validation F1-score | 98.06% |
| Validation AUC | 0.9976 |

Reported best epoch: 1.

These are validation results, not independent held-out test results.

## Reproduction

1. Download the original GramBeddings dataset.
2. Open `GramBeddings_Implementation.ipynb` in Kaggle.
3. Attach the dataset and enable a GPU.
4. Run the notebook cells in order.
5. The notebook trains the model and exports the evaluation metrics.

## Limitations

The original implementation required compatibility modifications for the current TensorFlow and scikit-learn environment. In particular, a pooling layer was modified, so this is an adaptation of the published architecture rather than an exact reproduction.

The validation set is also used during model selection.

# 3. BERT-Based Malicious URL Detection

## Reference

**Paper:** BERT-Based Approaches to Identifying Malicious URLs (Sensors, 2023)

**Dataset:** https://www.kaggle.com/datasets/sid321axn/malicious-urls-dataset

## Implementation

This is an independent reimplementation of the paper's BERT-based URL classification approach using Hugging Face Transformers on Kaggle.

The model classifies raw URLs into four categories: **benign, defacement, phishing, and malware**.

**Training configuration:**
- Model: `bert-base-cased`
- Maximum sequence length: 128
- Learning rate: 1e-5
- Batch size: 16
- Epochs: 3
- Data split: 72% train / 8% validation / 20% test
- Optimizer: AdamW

Two experiments were conducted:
- **40K:** Balanced dataset with 10,000 URLs per class.
- **100K:** Larger dataset preserving the original class distribution.

## Results

| Metric | 40K | 100K |
|---|---:|---:|
| Accuracy | 95.59% | 97.77% |
| Macro Precision | 95.66% | 97.01% |
| Macro Recall | 95.59% | 95.63% |
| Macro F1 | 95.60% | 96.27% |

Results were obtained on held-out test sets.

## Reproduction

1. Open `BERT_URL_Implementation.ipynb` in Kaggle.
2. Attach the Malicious URLs Dataset and enable GPU.
3. Configure the dataset size and run all cells.
4. Export the evaluation metrics and confusion matrix.

## Limitations

The authors' original code was unavailable, so the implementation follows the published methodology. Training was limited to 3 epochs, and only URL-string classification was implemented. The two experiments have different class distributions, so their results are not directly comparable as a controlled dataset-size experiment.
