
# Exercise 01 — Appliance Energy Prediction

## Overview

This exercise focuses on solving a **regression problem** using the **Appliances Energy Prediction** dataset.

The objective is to predict household appliance energy consumption and evaluate different regression algorithms based on their performance on the test set.

The workflow includes data exploration, correlation analysis, preprocessing, comparison of multiple regression models, hyperparameter tuning, and feature importance analysis.

## Dataset

The **Appliances Energy Prediction** dataset contains measurements related to household energy consumption, indoor and outdoor temperatures, humidity levels, and weather conditions.

Dataset source:

[UCI Machine Learning Repository — Appliances Energy Prediction](https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction)

The target variable is:

* **Appliances** — appliance energy consumption in Wh

An initial analysis showed that approximately **90.25%** of the appliance consumption values are below 200 Wh.

## Data Exploration and Visualization

The dataset was explored using statistical analysis and visualization techniques.

The following analyses were performed:

* Distribution of the input features
* Distribution of the target variable
* Correlation heatmap
* Analysis of highly correlated feature pairs
* Feature relationship with appliance energy consumption

The correlation analysis showed strong relationships among several temperature and humidity variables.

For example:

* `T6` and `T_out` have a correlation of approximately **0.975**
* `T7` and `T9` have a correlation of approximately **0.944**
* `T5` and `T9` have a correlation of approximately **0.910**
* `RH_3` and `RH_4` have a correlation of approximately **0.900**

The two random variables (`rv1` and `rv2`) were also found to have no useful predictive role.

Based on the correlation analysis, the following features were removed before model training:

* `rv1`
* `rv2`
* `Visibility`
* `T6`
* `T9`

The resulting feature set contained **21 input features**.

## Data Preprocessing

The dataset was divided into independent variables (`X`) and the target variable (`y`).

The target variable was:

* `Appliances`

The input features were standardized using `StandardScaler`.

The final training and testing datasets were then used for training and evaluating the regression models.

## Regression Models

Several regression algorithms were implemented and compared:

1. Lasso Regression
2. Ridge Regression
3. K-Nearest Neighbors Regressor
4. Support Vector Regression (SVR)
5. Random Forest Regressor
6. Extra Trees Regressor
7. Gradient Boosting Regressor
8. XGBoost Regressor
9. Multi-Layer Perceptron Regressor

The models were evaluated using:

* Training $R^2$
* Testing $R^2$
* Testing RMSE
* Training time

## Model Comparison

The obtained results were:

| Model                       | Train $R^2$ | Test $R^2$ | Test RMSE |
| --------------------------- | ----------: | ---------: | --------: |
| Lasso                       |       0.000 |      0.000 |     1.000 |
| Ridge                       |       0.138 |      0.121 |     0.937 |
| KNeighborsRegressor         |       0.681 |      0.486 |     0.717 |
| SVR                         |       0.236 |      0.210 |     0.889 |
| Random Forest               |       0.939 |      0.556 |     0.667 |
| **Extra Trees Regressor**   |   **1.000** |  **0.633** | **0.606** |
| Gradient Boosting Regressor |       0.334 |      0.232 |     0.876 |
| XGBRegressor                |       0.855 |      0.470 |     0.728 |
| MLPRegressor                |       0.299 |      0.243 |     0.870 |

Among the evaluated models, the **Extra Trees Regressor** achieved the highest test $R^2$ and the lowest test RMSE in the initial comparison.

## Hyperparameter Tuning

Since the Extra Trees Regressor achieved the strongest test performance, **GridSearchCV** was used to tune its hyperparameters.

The following parameters were searched:

* `max_depth`: 80, 150, 200, 250
* `n_estimators`: 100, 150, 200, 250
* `max_features`: `sqrt`, `log2`

A **5-fold cross-validation** strategy was used with $R^2$ as the scoring metric.

The best parameter combination obtained from the executed GridSearchCV was:

```text
max_depth = 80
max_features = sqrt
n_estimators = 150
```

The tuned model achieved:

* **Training $R^2$:** 1.000
* **Testing $R^2$:** 0.632
* **Testing RMSE:** 0.607

Compared with the initial Extra Trees model, the tuned model produced a similar test performance, with the test $R^2$ remaining around 0.63.

The training $R^2$ of 1.0 compared with the lower test $R^2$ indicates a substantial difference between training and unseen-data performance.

## Feature Importance

Feature importance was extracted from the tuned Extra Trees Regressor.

The five most important features were:

1. `RH_8`
2. `RH_1`
3. `RH_out`
4. `T3`
5. `RH_3`

The five least important features were:

1. `T4`
2. `T7`
3. `Windspeed`
4. `T1`
5. `T5`

The model was then retrained using only the five most important features.

### Reduced Feature Set Results

| Metric         |   Score |
| -------------- | ------: |
| Training $R^2$ | 0.99998 |
| Testing $R^2$  | 0.47519 |
| Testing RMSE   | 0.72444 |

The test $R^2$ decreased substantially from approximately **0.63** to **0.48** after reducing the feature set to five features.

Therefore, using only the five most important features did not preserve the predictive performance of the full f
