# CrediFraud — Adaptive Credit Card Fraud Detection

An adaptive machine learning system for detecting fraudulent credit card transactions while addressing **extreme class imbalance and concept drift**.

## Overview

CrediFraud is a machine learning-based credit card fraud detection system developed using the **ULB Credit Card Fraud Detection dataset**. The system combines data preprocessing, class-imbalance handling, ensemble learning, adaptive online learning, and concept-drift monitoring to provide reliable fraud detection.

The project evaluates multiple machine learning models and uses **XGBoost as the primary static fraud detection model**, while an **SGD-based adaptive classifier** is used to adapt to changing fraud patterns.

## Key Features

* Credit card fraud classification
* Exploratory Data Analysis and visualization
* Feature scaling and normalization
* **SMOTE** for handling severe class imbalance
* Comparison of multiple ML models
* XGBoost-based fraud detection
* Adaptive **SGDClassifier** for changing fraud patterns
* Concept drift monitoring
* Real-time transaction risk prediction
* Low / Medium / High risk classification
* Streamlit-based web interface
* Model serialization for deployment

## Dataset

The project uses the **ULB Credit Card Fraud Detection dataset** containing:

| Property                |        Value |
| ----------------------- | -----------: |
| Total transactions      |      284,807 |
| Fraudulent transactions |          492 |
| Fraud ratio             |       ~0.17% |
| Features                |           30 |
| PCA features            |       V1–V28 |
| Additional features     | Time, Amount |

The extreme imbalance makes conventional classification challenging because a model can achieve high accuracy while failing to detect fraudulent transactions.

## Machine Learning Pipeline

```text
Transaction Dataset
        |
        v
Exploratory Data Analysis
        |
        v
Feature Scaling
        |
        v
SMOTE Oversampling
        |
        v
Train / Validation Split
        |
        +----------------------+
        |                      |
        v                      v
 Static Model            Adaptive Model
   XGBoost                SGDClassifier
        |                      |
        +----------+-----------+
                   |
                   v
          Fraud Prediction
                   |
                   v
          Risk Classification
                   |
                   v
        Concept Drift Monitoring
                   |
                   v
          Streamlit Interface
```

## Preprocessing

The `Time` and `Amount` features are scaled before model training. Since the dataset contains very few fraudulent transactions, **SMOTE (Synthetic Minority Over-sampling Technique)** is applied to generate synthetic minority-class samples and improve fraud-pattern learning.

## Models Implemented

The project compares five classification approaches:

| Model               | Purpose                        |
| ------------------- | ------------------------------ |
| Logistic Regression | Baseline classifier            |
| Decision Tree       | Tree-based classification      |
| Random Forest       | Ensemble learning              |
| Gradient Boosting   | Boosting-based classification  |
| XGBoost             | Primary high-performance model |

The system additionally uses **SGDClassifier** for adaptive online learning so the classifier can update its decision boundary as new transaction patterns arrive.

## Concept Drift Handling

Fraud patterns are not static. Attackers continuously change their techniques, causing the underlying transaction distribution to evolve.

CrediFraud addresses this using:

* Statistical error-rate monitoring
* Concept-drift warnings
* Experimental drift simulation
* Adaptive SGD-based online learning
* Continuous model updates

When the monitored error rate increases, the system can identify a potential change in fraud behavior and allow the adaptive model to respond.

## Performance

### Model Comparison

| Model               |   Accuracy |  Precision |     Recall |         F1 |    ROC-AUC |
| ------------------- | ---------: | ---------: | ---------: | ---------: | ---------: |
| **XGBoost**         | **99.92%** |     71.79% |     85.71% |     78.14% | **98.07%** |
| Gradient Boosting   |     98.67% |     10.55% |     89.80% |     18.88% |     98.07% |
| Logistic Regression |     97.43% |      5.81% | **91.84%** |     10.94% |     96.98% |
| Random Forest       |     99.95% | **85.26%** |     82.65% | **83.94%** |     96.83% |
| Decision Tree       |     99.70% |     34.08% |     77.55% |     47.35% |     88.65% |

XGBoost provided the strongest overall balance between fraud detection, precision, recall, and ROC-AUC.

## XGBoost Confusion Matrix

|                   | Predicted Legitimate | Predicted Fraud |
| ----------------- | -------------------: | --------------: |
| Actual Legitimate |               56,831 |              33 |
| Actual Fraud      |                   14 |              84 |

The model correctly detected **84 of 98 fraudulent transactions**, achieving an **85.71% fraud recall** with only 33 false positives.

## Web Application

The project includes a **Streamlit interface** where users can:

* Enter transaction information
* Select predefined test cases
* Receive fraud probability scores
* View Low / Medium / High risk classifications
* Receive recommended actions
* Monitor model behavior

The trained model is serialized using Pickle for low-latency inference.

## Tech Stack

**Languages**

* Python

**Machine Learning**

* Scikit-learn
* XGBoost
* Imbalanced-learn / SMOTE

**Data Processing**

* Pandas
* NumPy

**Visualization**

* Matplotlib
* Seaborn

**Deployment**

* Streamlit
* Pickle

**Development**

* Jupyter Notebook

## Project Structure

```text
CrediFraud/
│
├── data/
│   └── creditcard.csv
│
├── notebooks/
│   └── fraud_detection.ipynb
│
├── models/
│   └── xgboost_model.pkl
│
├── app/
│   └── app.py
│
├── src/
│   ├── preprocessing.py
│   ├── train.py
│   ├── prediction.py
│   └── drift_detection.py
│
├── requirements.txt
└── README.md
```

## Installation

```bash
git clone <repository-url>
cd CrediFraud

pip install -r requirements.txt
```

## Run the Application

```bash
streamlit run app/app.py
```

The application opens a web interface for testing transactions and viewing their predicted fraud risk.

## Evaluation Metrics

Because the dataset is highly imbalanced, accuracy alone is not sufficient.

The project focuses primarily on:

* **Precision** — How many predicted fraud transactions are actually fraudulent
* **Recall** — How many actual fraud transactions are detected
* **F1-Score** — Balance between precision and recall
* **ROC-AUC** — Overall class-separation capability
* **Accuracy** — Overall prediction correctness

Recall is particularly important because failing to detect an actual fraudulent transaction can result in significant financial loss.

## Results & Conclusion

CrediFraud demonstrates that combining **SMOTE, ensemble learning, and adaptive concept-drift handling** can provide a stronger foundation for real-world fraud detection.

Among the evaluated models, **XGBoost achieved the best overall balance**, with 99.92% accuracy, 71.79% precision, 85.71% recall, 78.14% F1-score, and 98.07% ROC-AUC.

The adaptive component further addresses an important limitation of conventional fraud detection systems: **fraud patterns evolve over time**, meaning a model trained once on historical data may gradually become less effective.

## Future Scope

* Real-time transaction stream integration
* More advanced concept-drift detection
* Deep learning-based fraud detection
* Automated model retraining
* Explainable AI for fraud decisions
* Production-scale deployment
* Integration with banking/payment systems

## Team

**Manipal Institute of Technology — School of Computer Engineering**

* Devansh Prejit
* Varun Nayak
* Trisha Shetty
* Shawn Brian Dsouza
* Kia Masand
* Rishit Bisani
