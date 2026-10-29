
# Fraud Detection on PaySim Dataset

##  Overview
This project focuses on detecting fraudulent mobile money transactions using machine learning and anomaly detection techniques. It explores the challenges of fraud detection in a highly imbalanced dataset and compares different approaches for identifying fraudulent transactions.

##  Dataset
The project uses the **PaySim Synthetic Financial Dataset for Fraud Detection**.

- **Dataset:** [PaySim – Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1)
- **File name:** `PS_20174392719_1491204439457_log.csv`
- **Size:** Approximately 6.36 million transactions
- **Target variable:** `isFraud`

The dataset is not included in this repository due to its large file size. Download it from Kaggle and place the CSV file in the project directory before running the notebook.

##  Methods
- Data preprocessing and feature scaling
- Logistic Regression
- Naive Bayes
- Stochastic Gradient Descent (SGD)
- Random Forest
- Random undersampling
- SMOTE oversampling
- PCA for dimensionality reduction
- K-Means clustering
- Isolation Forest for anomaly detection

##  Evaluation
The models are evaluated using metrics suitable for imbalanced classification:

- Precision
- Recall
- F1-score
- Average Precision
- Confusion Matrix
- ROC-AUC, where applicable

The project also compares sampling strategies, examines the effect of dimensionality reduction, and explores the sensitivity of anomaly detection to different contamination rates and decision thresholds.

##  Key Findings
- Random Forest without resampling achieved an F1-score of approximately **0.89**, with fraud recall around **80.7%**.
- Random Forest trained on SMOTE-resampled data achieved fraud recall around **97.0%**, with a precision of approximately **54.4%**.
- Random undersampling increased fraud recall to approximately **97.3%** for Random Forest, but reduced precision to around **23.2%**.
- PCA with two components reduced the Random Forest model's fraud recall considerably.
- K-Means clustering revealed structure in the feature space but showed almost no agreement with the actual fraud labels.
- Isolation Forest was explored as an unsupervised anomaly detection approach.

These results illustrate the trade-off between detecting more fraudulent transactions and generating false alarms.

##  Tools & Libraries
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Imbalanced-learn

##  Objective
The main objective is to compare supervised classification, sampling strategies, dimensionality reduction, clustering, and anomaly detection for identifying fraudulent financial transactions.
