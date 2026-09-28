# Life Expectancy Prediction

This project focuses on **data preprocessing, feature engineering, feature selection, feature extraction, and regression modeling** using the **Life Expectancy** dataset.

The main goal is to investigate how different data preprocessing and dimensionality reduction techniques affect the performance of a regression model.

---

## Dataset

The dataset contains information about life expectancy and various health, demographic, and economic indicators for different countries over multiple years.

### Dataset dimensions

* **Rows:** 2,938
* **Columns:** 22
* **Target variable:** `Life Expectancy`

The target variable is continuous, therefore the problem is treated as a **regression task**.

---

## Project Workflow

The project follows these main steps:

1. Data loading
2. Data exploration
3. Exploratory Data Analysis (EDA)
4. Missing value handling
5. Feature transformation
6. Outlier treatment
7. Categorical encoding
8. Feature splitting
9. Feature scaling
10. Baseline regression model
11. Feature selection with SelectKBest
12. Feature selection using the `scikit-feature` library approach
13. Feature extraction using PCA
14. Model evaluation and comparison

---

## 1. Data Exploration

The dataset was initially examined using:

* Dataset shape and information
* Descriptive statistics
* Missing value analysis
* Duplicate value detection
* Categorical variable distribution
* Number of unique values

The dataset contains missing values in several numerical features, while no duplicate rows were identified.

---

## 2. Exploratory Data Analysis

EDA was performed to better understand the structure and relationships within the dataset.

The analysis included:

* Distribution of the `Status` variable
* Correlation analysis between numerical features
* Correlation heatmap

The correlation analysis was used to investigate relationships between variables and identify potentially redundant or strongly related features.

---

## 3. Feature Engineering

### Missing Value Imputation

Missing numerical values were handled using **KNN Imputation**.

### Feature Transformation

Several transformations were investigated for numerical variables, including:

* Log transformation
* Square-root transformation
* Square transformation
* Reciprocal transformation
* Power transformation

These transformations were considered to modify feature distributions and reduce the effect of skewness.

### Outlier Treatment

Outliers were investigated using boxplots and treated using **Winsorization based on the IQR method**.

### Categorical Encoding

Two categorical variables were handled:

* `Status` was encoded using ordinal encoding.
* `Country` was transformed using one-hot encoding.

### Feature Splitting

The dataset was divided into:

* Feature matrix `X`
* Target variable `y = Life Expectancy`

The data was then split into training and testing sets.

---

## 4. Feature Scaling

Numerical features were standardized using `StandardScaler`.

The scaler was fitted on the training data and then applied to the test data.

---

## 5. Baseline Model

A **Linear Regression** model was used as the baseline model.

The baseline model was trained using all available processed features.

### Evaluation Metrics

The following metrics were used:

* R² Score
* Mean Absolute Error (MAE)
* Mean Absolute Percentage Error (MAPE)
* Root Mean Squared Error (RMSE)

### Baseline Results

| Metric | Result |
| ------ | -----: |
| R²     | 0.8540 |
| MAE    | 2.6472 |
| MAPE   | 0.0413 |
| RMSE   | 3.7018 |

---

## 6. Feature Selection with SelectKBest

Feature selection was performed using **SelectKBest** with `f_regression` as the scoring function.

The top **10 features** were selected.

The Linear Regression model was then trained using only the selected features.

### Results

| Metric | Result |
| ------ | -----: |
| R²     | 0.8347 |
| MAE    | 2.9035 |
| MAPE   | 0.0452 |
| RMSE   | 3.9393 |

Compared with the baseline model, using only the selected 10 features resulted in a decrease in predictive performance for this train/test split.

---

## 7. Feature Selection with scikit-feature

The open-source **scikit-feature** library was investigated for feature selection methods.

The `low_variance` method was examined. This method is implemented using the `VarianceThreshold` approach from scikit-learn.

Features with low variance were removed and the Linear Regression model was evaluated again.

### Results

| Metric | Result |
| ------ | -----: |
| R²     | 0.8540 |
| MAE    | 2.6472 |
| MAPE   | 0.0413 |
| RMSE   | 3.7018 |

The results were almost identical to the baseline model, indicating that the low-variance feature removal used in this experiment did not materially change the model's predictive performance.

---

## 8. Feature Extraction with PCA

For feature extraction, **Principal Component Analysis (PCA)** was used.

PCA was applied to the scaled training data while retaining **95% of the variance**.

The learned transformation was then applied to the test data.

Unlike feature selection, PCA does not simply remove individual original features. Instead, it transforms the original features into a smaller set of principal components.

### Results

| Metric | Result |
| ------ | -----: |
| R²     | 0.8405 |
| MAE    | 2.7499 |
| MAPE   | 0.0428 |
| RMSE   | 3.8695 |

PCA reduced the dimensionality of the feature space while retaining 95% of the variance. The resulting model showed a moderate decrease in performance compared with the baseline.

---

## 9. Overall Comparison

| Method            |     R² |    MAE |   MAPE |   RMSE |
| ----------------- | -----: | -----: | -----: | -----: |
| All Features      | 0.8540 | 2.6472 | 0.0413 | 3.7018 |
| SelectKBest       | 0.8347 | 2.9035 | 0.0452 | 3.9393 |
| VarianceThreshold | 0.8540 | 2.6472 | 0.0413 | 3.7018 |
| PCA               | 0.8405 | 2.7499 | 0.0428 | 3.8695 |

The comparison shows how different feature selection and feature extraction approaches affect the performance of the same Linear Regression model.

---

## Libraries

The project was implemented using Python and the following libraries:

* pandas
* NumPy
* scikit-learn
* scikit-feature
* Matplotlib
* Seaborn
* Yellowbrick
* Feature-engine

---

## Conclusion

This project demonstrates a complete workflow for preparing a real-world dataset for regression modeling.

Different preprocessing, feature selection, and feature extraction techniques were investigated and compared using the same Linear Regression model and evaluation metrics.

The results demonstrate that reducing the feature space does not necessarily improve predictive performance. In this experiment, the baseline model using all processed features achieved an R² of approximately **0.854**, while SelectKBest and PCA resulted in lower R² values. The VarianceThreshold approach produced almost identical results to the baseline model.

The notebook therefore provides a practical comparison of **data cleaning, feature engineering, feature selection, and feature extraction** techniques on the Life Expectancy dataset.
