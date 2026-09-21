# Appliance Energy Prediction – Regression

## Overview

This assignment focuses on predicting appliance energy consumption using regression techniques. The dataset contains measurements related to indoor environmental conditions, outdoor weather conditions, humidity, temperature, and other variables.

The main objective is to compare several regression models, evaluate their performance, perform hyperparameter tuning, and analyze feature importance.

## Dataset

**Dataset:** Appliances Energy Prediction
**Source:** UCI Machine Learning Repository

The dataset contains environmental and weather-related measurements collected from a residential building. The target variable is:

* `Appliances` – appliance energy consumption

The dataset file used in this assignment is:

`Appliances-energy-prediction.csv`

## Workflow

The assignment follows these main steps:

1. Data loading and exploration
2. Data visualization
3. Correlation analysis
4. Data preprocessing
5. Feature scaling
6. Regression model implementation
7. Model evaluation
8. Hyperparameter tuning
9. Feature importance analysis
10. Feature selection and re-evaluation

## Data Preprocessing

Highly redundant or irrelevant features were removed based on correlation analysis and the structure of the dataset.

The removed features were:

* `rv1`
* `rv2`
* `Visibility`
* `T6`
* `T9`

After preprocessing, **21 input features** were used for model training.

`StandardScaler` was used for feature scaling. The scaler was fitted on the training data and then applied to the test data.

## Regression Models

The following regression models were evaluated:

* Lasso Regression
* Ridge Regression
* K-Nearest Neighbors Regression
* Support Vector Regression (SVR)
* Random Forest Regression
* Extra Trees Regression
* Gradient Boosting Regression
* XGBoost Regression
* Multi-Layer Perceptron Regression (MLP)

The models were evaluated using:

* R² Score
* RMSE
* Training Time

## Model Comparison

Among the evaluated models, **Extra Trees Regressor** achieved the highest test performance before hyperparameter tuning.

The tuned Extra Trees model used:

* `max_depth = 80`
* `n_estimators = 150`
* `max_features = sqrt`
* `random_state = 40`

### Tuned Extra Trees Results

| Metric | Training | Testing |
| ------ | -------: | ------: |
| R²     |     1.00 |  ≈ 0.64 |
| RMSE   |        — |  ≈ 0.58 |

The training R² is very high while the test R² is considerably lower. This noticeable gap suggests **possible overfitting**. In this assignment, no additional optimization specifically aimed at reducing overfitting was performed.

## Feature Importance

Feature importance was extracted from the tuned Extra Trees model to identify the variables that contributed most to the predictions.

The five most important features were:

* `RH_8`
* `RH_1`
* `RH_out`
* `T3`
* `RH_3`

The model was then retrained using only these five features.

### Five-Feature Model Results

| Metric | Training | Testing |
| ------ | -------: | ------: |
| R²     |   ≈ 1.00 | ≈ 0.496 |
| RMSE   |        — | ≈ 0.699 |

Using only the five most important features resulted in lower test performance compared with the model using the full feature set.

This indicates that although these features had the highest individual feature importance, the remaining features still contributed useful information to the overall prediction.

## Conclusion

Several regression models were compared for appliance energy prediction. Among them, the Extra Trees Regressor achieved the strongest test performance in this experiment.

Hyperparameter tuning produced a tuned Extra Trees model with a test R² of approximately **0.64** and a test RMSE of approximately **0.58**.

Feature selection using only the five most important features reduced the test R² to approximately **0.496**, showing that restricting the model to these five variables was not beneficial in this experiment.

The difference between training and testing performance also suggests possible overfitting. Since the main goal of this assignment was regression modeling, evaluation, tuning, and feature-importance analysis, additional methods for reducing overfitting were not explored here.

