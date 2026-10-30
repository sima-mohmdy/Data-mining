# Fraud Detection on PaySim Dataset

## Overview
This project focuses on detecting fraudulent mobile money transactions using machine learning, clustering, and anomaly detection techniques. It explores the challenges of fraud detection in a highly imbalanced dataset and compares different approaches for identifying fraudulent transactions.

## Dataset
The project uses the **PaySim Synthetic Financial Dataset for Fraud Detection**.

- **Dataset:** [PaySim – Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1)
- **File name:** `PS_20174392719_1491204439457_log.csv`
- **Size:** Approximately 6.36 million transactions
- **Number of features:** 10 input features and 1 target variable
- **Target variable:** `isFraud`

The dataset contains approximately 6.35 million legitimate transactions and 8,213 fraudulent transactions, making it highly imbalanced.

The dataset is not included in this repository due to its large file size. Download it from Kaggle and place the CSV file in the project directory before running the notebook.

## Methods

### Supervised Classification
- Logistic Regression
- Naive Bayes (BernoulliNB and MultinomialNB)
- Stochastic Gradient Descent (SGD)
- Random Forest

### Imbalanced Data Handling
- Original dataset with class weighting
- Random undersampling
- SMOTE oversampling

### Dimensionality Reduction
- Principal Component Analysis (PCA)

### Unsupervised Learning
- K-Means clustering
- Isolation Forest for anomaly detection

## Evaluation

The models are evaluated using metrics suitable for imbalanced classification:

- Precision
- Recall
- F1-score
- Average Precision (AP)
- ROC-AUC
- Confusion Matrix

The project also examines the effects of different sampling strategies, dimensionality reduction, clustering, and anomaly detection parameters.

## Results & Key Findings

### 1. Supervised Classification and Sampling Strategies

Random Forest achieved the strongest overall balance between precision and recall among the tested classification approaches.

The following table compares its performance under different training strategies on the test set:

| Training Strategy | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Original Data + Class Weighting | **97.86%** | 80.71% | **88.46%** |
| Random Undersampling | 23.20% | **97.32%** | 37.46% |
| SMOTE Oversampling | 54.39% | 96.96% | 69.69% |

**Key observations:**
- Random Forest trained on the original dataset with `class_weight='balanced'` achieved the highest F1-score and precision among the tested strategies.
- Random undersampling achieved the highest fraud recall, but generated considerably more false positives.
- SMOTE improved fraud detection recall while maintaining better precision than random undersampling.
- These results highlight the trade-off between detecting more fraudulent transactions and minimizing false alarms.

### 2. Dimensionality Reduction

PCA was applied to reduce the feature space to two principal components.

- The two-component PCA representation considerably reduced Random Forest's fraud recall.
- This suggests that the two-dimensional representation discarded information useful for distinguishing fraudulent transactions.
- PCA's performance depends on the number of retained components and the amount of information preserved.

### 3. K-Means Clustering

K-Means was applied with three clusters to explore natural groupings in transaction data.

Evaluation on a sample of 10,000 transactions produced the following results:

| Metric | Score |
|---|---:|
| Silhouette Score | 0.6589 |
| Adjusted Rand Index (ARI) | -0.00006 |
| Normalized Mutual Information (NMI) | 0.00065 |

**Key observations:**
- The Silhouette Score suggests that the resulting clusters were reasonably separated in the feature space.
- ARI and NMI values close to zero indicate almost no agreement between the discovered clusters and the actual fraud labels.
- Therefore, the clusters captured general transaction patterns rather than clearly separating fraudulent transactions.

### 4. Isolation Forest

Isolation Forest was explored as an unsupervised anomaly detection method.

The model was evaluated using different contamination rates and decision thresholds.

**Key observations:**
- Increasing the contamination rate generally increased fraud recall while also increasing false positive detections.
- The best F1-score among the tested contamination values on the training data was obtained with `contamination=0.005`.
- On the test set, using this contamination setting resulted in approximately:
  - Precision: 1.50%
  - Recall: 5.72%
  - F1-score: 2.25%
- Despite a relatively high ROC-AUC on the training data, the test results showed that Isolation Forest was not effective as a standalone fraud classifier in this experiment.

These findings demonstrate that detecting unusual transactions does not necessarily mean accurately identifying fraudulent transactions.

## Overall Conclusion

Among the tested approaches, **Random Forest trained on the original dataset with class weighting** achieved the best overall balance between precision and recall.

SMOTE and random undersampling improved fraud recall, but resulted in more false positive predictions.

PCA with only two components reduced classification performance, while K-Means identified meaningful geometric groupings that did not correspond closely to fraud labels.

Isolation Forest provided an opportunity to explore unsupervised anomaly detection, but its test performance showed limitations for direct fraud identification.

Overall, the experiments demonstrate the importance of selecting evaluation metrics carefully and considering the trade-off between missed fraud cases and false alarms when working with highly imbalanced financial datasets.

## Tools & Libraries
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Imbalanced-learn

## Objective

The main objective of this project is to compare supervised classification, sampling strategies, dimensionality reduction, clustering, and anomaly detection techniques for identifying fraudulent financial transactions and understanding their strengths and limitations.
