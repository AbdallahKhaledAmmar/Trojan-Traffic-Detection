# Trojan Detection from Network Flows

Machine-learning experiment that tries to classify network flows as **Benign** or **Trojan** using CICFlowMeter-style features (packet sizes, inter-arrival times, TCP flags, etc.).

## Dataset
`Trojan_Detection1.csv`: 199 flows (110 Benign, 89 Trojan), 86 columns. Appears to be a sample from a CIC-style malware traffic capture (source/licence: **add the original source here**).

## Approach
1. Clean: strip column names, drop identifiers (`Flow ID`, IPs, `Timestamp`, row index), handle inf/NaN, drop constant columns.
2. Explore: class balance, duration distribution, correlations.
3. Compare Decision Tree, Random Forest, Gradient Boosting, Logistic Regression with stratified 5-fold CV, plus a majority-class baseline.
4. Evaluate the best model on a 30% hold-out set (precision/recall/F1, confusion matrix); visualise a decision tree and feature importances.

## Key findings
- **Data leakage:** the row-index column alone predicts the label with ~100% accuracy, so it is excluded.
- **Honest result:** with only flow features, models score near the baseline (~50% accuracy, F1 ≈ 0.3-0.4). On this small sample, flow features alone don't reliably separate Trojan from benign traffic.
- Future work: larger dataset (e.g. CIC-InvAndMal2017), host-grouped CV, per-host / time-window aggregation.

## Run
```bash
pip install -r requirements.txt
jupyter notebook Trojan_Detection.ipynb
```

## Structure
```
├── Trojan_Detection.ipynb
├── Trojan_Detection1.csv
├── requirements.txt
└── README.md
```
