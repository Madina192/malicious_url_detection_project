# PhiUSIIL Baseline Implementation

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
