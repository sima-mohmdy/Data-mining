# Clustering-On-Customer-Credit-Card

## Overview

This project explores customer segmentation using unsupervised learning techniques. The goal is to group customers with similar purchasing behaviors and financial characteristics using clustering algorithms.

The analysis is performed on the **Credit Card Customers dataset** (`CC GENERAL.csv`). Four clustering algorithms are evaluated, and Principal Component Analysis (PCA) is applied to investigate how dimensionality reduction affects clustering performance.

## Dataset

- **Dataset:** Credit Card Customers (`CC GENERAL.csv`)
- **Number of customers:** 8,950
- **Number of numerical features used:** 17

The dataset contains customer financial and behavioral information, including credit limits, purchase amounts, cash advances, installment purchases, payments, and account activity.

## Methodology

### 1. Data Preprocessing

The preprocessing steps include:

- Removing the customer ID column.
- Checking for missing values and duplicate records.
- Handling missing values in `MINIMUM_PAYMENTS` using the median.
- Removing records with missing `CREDIT_LIMIT`.
- Filtering extreme values in `CASH_ADVANCE` and `INSTALLMENTS_PURCHASES`.
- Standardizing numerical features using `StandardScaler`.

After preprocessing, the dataset contains **8,947 customers and 17 features**.

### 2. Clustering Algorithms

Four unsupervised learning algorithms are applied:

- **K-Means:** Partitions customers into clusters by minimizing within-cluster distances.
- **Gaussian Mixture Model (GMM):** Models the data as a mixture of Gaussian distributions.
- **Agglomerative Clustering:** Builds clusters using a hierarchical, bottom-up approach.
- **DBSCAN:** Identifies dense regions and detects noise points without requiring a predefined number of clusters.

### 3. Dimensionality Reduction with PCA

PCA is applied to the standardized 17-dimensional feature space to reduce it to two principal components.

Clustering is then performed in the reduced feature space, allowing the results before and after PCA to be compared. The two-dimensional representation also supports visualization of the resulting clusters.

### 4. Evaluation Metrics

The clustering results are evaluated using:

- **Silhouette Score:** Measures how well-separated and cohesive the clusters are. Higher values generally indicate better-defined clusters.
- **Calinski–Harabasz Index:** Compares between-cluster dispersion with within-cluster dispersion. Higher values generally indicate better-defined clustering.

For DBSCAN, the Silhouette Score before PCA is calculated after excluding noise points. After PCA, DBSCAN identifies only one cluster, so its Silhouette Score cannot be calculated.

## Results

### Before PCA

| Algorithm | Clusters | Silhouette Score | Calinski–Harabasz Score |
|---|---:|---:|---:|
| K-Means | 3 | 0.251 | 1624.36 |
| GMM | 2 | 0.193 | 1196.95 |
| Agglomerative Clustering | 2 | 0.181 | 1449.57 |
| DBSCAN (`eps=3`) | 4 | 0.413* | Not calculated |

### After PCA

| Algorithm | Clusters | Silhouette Score | Calinski–Harabasz Score |
|---|---:|---:|---:|
| K-Means | 2 | 0.461 | 4118.43 |
| GMM | 8 | 0.376 | 4438.85 |
| Agglomerative Clustering | 2 | 0.385 | 3249.11 |
| DBSCAN (`eps=3.5`) | 1 | Not calculable | Not calculated |

\* The DBSCAN Silhouette Score before PCA excludes noise points and is therefore not directly comparable to scores calculated using all samples.

## Conclusion

The results show that PCA improved both the Silhouette Score and the Calinski–Harabasz Index for K-Means, GMM, and Agglomerative Clustering in this experiment.

After PCA, K-Means achieved the highest Silhouette Score of **0.461**, indicating better cluster separation according to this metric. GMM achieved the highest Calinski–Harabasz Index of **4438.85**.

DBSCAN performed differently after dimensionality reduction, identifying only one cluster and six noise points with the selected parameters. Consequently, a valid Silhouette Score could not be obtained for this result.

Overall, the experiment demonstrates that clustering performance depends on the algorithm, its parameters, the feature representation, and the evaluation metric. PCA can improve clustering results in some cases, but the resulting clusters should also be interpreted using their distributions and visualizations.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook / Google Colab

## Key Concepts

Unsupervised Learning, Customer Segmentation, Data Preprocessing, Feature Scaling, K-Means, Gaussian Mixture Models, Agglomerative Clustering, DBSCAN, Principal Component Analysis (PCA), Silhouette Score, Calinski–Harabasz Index.

