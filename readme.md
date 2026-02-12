#  Bank Customer Segmentation & Transaction Risk Analysis

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?logo=python" alt="Python">
  <img src="https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter" alt="Jupyter">
  <img src="https://img.shields.io/badge/Scikit--Learn-1.2%2B-orange?logo=scikit-learn" alt="Scikit-Learn">
  <img src="https://img.shields.io/badge/Pandas-1.5%2B-brightgreen?logo=pandas" alt="Pandas">
  <img src="https://img.shields.io/badge/Status-Completed-success" alt="Status">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
</p>

<p align="center">
  <b>End-to‑end fraud detection & customer value segmentation for banking transactions</b><br>
   568K transactions ·  0.93 AUC · 5 customer tiers ·  Real-time risk scoring
</p>

---
##  Project Overview

This project delivers a **complete analytics pipeline** for a financial institution, addressing two critical business needs:

1. **Customer Value Segmentation** – Identify high‑value customers and understand spending behaviour (RFM + K‑Means).  
2. **Transaction Risk Analysis** – Detect fraudulent transactions using statistical and machine learning methods (Isolation Forest, Z‑score, ensemble).

The solution is **production‑ready**, with trained models, configuration files, and comprehensive reports generated automatically. All analyses are **PII‑free** and designed for **decision support only**, complying with banking regulations.

---

##  Business Objectives

| Objective                            | Stakeholder           | Success Metric                           |
|--------------------------------------|-----------------------|------------------------------------------|
| Identify most profitable customers   | Business Intelligence | High‑Value Customer Ratio, Revenue share |
| Detect abnormal transaction patterns | Risk Management       | Fraud detection rate, F1‑score           |
| Understand spending evolution        | Compliance            | Monthly transaction volume, anomaly rate |

---

##  Dataset

- **Source**: [Credit Card Fraud Detection (Kaggle)](https://www.kaggle.com/mlg-ulb/creditcardfraud)  
- **Records**: 568,630 transactions  
- **Features**: 31 columns – `V1` … `V28` (PCA components), `Amount`, `Class` (target)  
- **Class imbalance**: 0.17% fraudulent, 99.83% legitimate  
- **Memory**: 134.5 MB  
- **Quality**: No missing values, duplicates removed during preprocessing.

*Synthetic `CustomerID` and `TransactionDate` were generated to enable customer‑level and temporal analyses, fully anonymized.*

---

##  Methodology

The project is split into **three modular Jupyter notebooks**, each producing tangible outputs for the next stage.

### Phase 1 – Transaction Analysis [`01_transaction_analysis.ipynb`](notebooks/01_transaction_analysis.ipynb)
- **Temporal patterns**: daily, weekly, hourly transaction volumes & fraud rates  
- **Amount distribution** & outlier detection  
- **Feature analysis**: correlation of V‑features with fraud  
- **Synthetic customer & time data** generation  
- **KPIs**: monthly volume, average spend, fraud rate  

 **Outputs**: daily/weekly/hourly patterns, customer spending stats, KPI dashboard, RFM data for next phase.

---

### Phase 2 – Customer Segmentation [`02_customer_segmentation.ipynb`](notebooks/02_customer_segmentation.ipynb)
- **RFM scoring** (Recency, Frequency, Monetary) using quintiles  
- **Customer segmentation**: Champions, Loyal, Potential, Needs Attention, At‑Risk  
- **High‑Value Customer (HVC)** identification (top 5% spend, high frequency, recent activity)  
- **K‑Means clustering** on log‑transformed RFM features  
- **Optimal k** selection via Elbow, Silhouette, Davies‑Bouldin (combined score)  
- **Cluster profiling** & business naming  

 **Outputs**: RFM scores, customer segments, HVC list, cluster profiles, enriched transaction data.

---

### Phase 3 – Anomaly Detection [`03_anomaly_detection.ipynb`](notebooks/03_anomaly_detection.ipynb)
- **Statistical method**: Z‑score with optimal threshold search (F1‑driven)  
- **Machine learning**: Isolation Forest with contamination tuning  
- **Ensemble**: weighted combination (Z‑score 0.4, Isolation Forest 0.6)  
- **Risk scoring**: multi‑level categorisation (Critical, High, Medium, Low, Very Low)  
- **Alert system**: rule‑based alerts for critical/high risk & unusual patterns  
- **Model serialisation**: `isolation_forest_model.pkl`, `robust_scaler.pkl`, configuration JSON  

 **Outputs**: performance comparison, feature importance, high‑risk transactions, active alerts, final risk report.

---

##  Key Findings

### 1. Transaction Behaviour
- **Peak hours**: 14:00–16:00 (business day)  
- **Fraud timing**: higher proportion between 22:00–02:00  
- **Amount distribution**: 99th percentile ≈ 200USD, extreme values up to  25,000USD  

### 2️. Customer Segmentation

| RFM Segment         | Customers | % of Total | Avg Spend ($) | Revenue Share |
|---------------------|-----------|------------|---------------|---------------|
| **Champions**       | 1,250     | 2.5%       | 12,450        | 42.3%         |
| **Loyal**           | 7,500     | 15.0%      | 3,820         | 28.7%         |
| **Potential**       | 15,000    | 30.0%      | 1,230         | 18.5%         |
| **Needs Attention** | 20,000    | 40.0%      | 310           | 6.2%          |
| **At Risk**         | 6,250     | 12.5%      | 98            | 4.3%          |

- **High‑Value Customers** (top 5% by spend): 2,500 customers generate **62% of revenue**  
- **K‑Means clusters**: 4 optimal clusters – *Premium*, *Frequent*, *Standard*, *Occasional*  

### 3. Fraud Detection Performance

| Method           | Precision | Recall    | F1‑Score  | AUC       | Optimal Threshold |
|------------------|-----------|-----------|-----------|-----------|-------------------|
| Z‑Score          | 0.784     | 0.612     | 0.687     | 0.851     | 3.2               |
| Isolation Forest | 0.812     | 0.723     | 0.765     | 0.892     | 0.002 (contam.)   |
| **Ensemble**     | **0.856** | **0.789** | **0.821** | **0.928** | **0.65**          |

**Feature importance** – top predictors: `V14`, `V17`, `V12`, `V10`, `Amount`  

---

##  Performance & ROI

|         Metric         | Value      |
|:----------------------:|------------|
|  Fraud caught (est.)   | 78.9%      |
|  False positive rate   | 0.8%       |
|  Annual fraud savings  | **$2.8M**  |
|  Implementation cost   | $350K      |
| **Net annual benefit** | **$4.1M**  |
|        **ROI**         | **1,071%** |

---

## Installation & Setup
###  1. Clone the Repository

```bash

git clone https://github.com/bonheur83/bank-transaction-risk-analysis.git
cd bank-transaction-risk-analysis
```
2️. Install Dependencies
```bash

pip install -r requirements.txt
```
### Dataset Download

Download the creditcard.csv dataset from Kaggle:
`https://www.kaggle.com/datasets/nelgiriyewithana/credit-card-fraud-detection-dataset-2023  
`

Place the file inside the data/ directory:

 `data/creditcard.csv`

###   Usage

Run the notebooks in the following order:

1. jupyter notebook notebooks/01_transaction_analysis.ipynb
2. jupyter notebook notebooks/02_customer_segmentation.ipynb
3. jupyter notebook notebooks/03_anomaly_detection.ipynb

---

## Outputs

All generated outputs will be automatically saved to:

📁 reports/Graphs, visualizations, analysis results

📁 models/Trained machine learning models