
# 4. Road Traffic Severity Classification

## Overview
This project focuses on classifying road traffic accident severity using machine learning techniques. The main objective is to evaluate different classification models, tune their hyperparameters, and analyze their performance on an imbalanced dataset.

## Dataset
The project uses the **Road Traffic Accident (RTA) Dataset**, containing 12,316 records and 32 columns describing road traffic accidents.

The target variable is `Accident_severity`, which includes three classes:
- Slight Injury
- Serious Injury
- Fatal injury

The dataset is highly imbalanced, with fatal accidents representing only a small proportion of the observations. This imbalance makes the prediction of minority classes particularly challenging.

The dataset can be accessed from Kaggle:

[Road Traffic Accident Dataset – Kaggle](https://www.kaggle.com/datasets/ahmedsalahuddin/road-traffic-accidents)

Please refer to the original dataset page for download instructions and usage terms.

## Project Workflow

### 1. Data Exploration and Preprocessing
- Exploring the dataset and identifying missing values
- Handling missing categorical values
- Extracting the hour of the day from the time feature
- Selecting relevant features
- Encoding categorical variables

### 2. Feature Selection
Using `SelectKBest` with the chi-squared (`chi2`) statistical test to select relevant features.

### 3. Handling Class Imbalance
Applying SMOTE to the training data to address class imbalance.

### 4. Model Training and Evaluation
Three classification models were evaluated:
- **Decision Tree Classifier**
- **Multinomial Naive Bayes**
- **Multilayer Perceptron (MLP)**, a feedforward neural network

Model performance was evaluated using:
- Accuracy
- Precision
- Recall
- F1-score
- Macro F1-score
- Confusion matrix

### 5. Hyperparameter Tuning
`GridSearchCV` was used to explore hyperparameter combinations and optimize Macro F1-score.

The search included:
- **Decision Tree:** `max_depth`, `min_samples_leaf`, `min_samples_split`, `criterion`, and `class_weight`
- **Multinomial Naive Bayes:** `alpha` and `fit_prior`
- **Neural Network:** `hidden_layer_sizes` and `alpha`

### 6. Parameter Sensitivity Analysis
The effects of selected hyperparameters on cross-validation Macro F1-score were investigated to understand how model settings influence performance.

## Results

The following table summarizes the test-set results after hyperparameter tuning.

| Model | Accuracy | Macro F1-score |
|---|---:|---:|
| Decision Tree | 0.78 | 0.38 |
| Multinomial Naive Bayes | 0.51 | 0.32 |
| Neural Network (MLP) | 0.74 | 0.37 |

### Key Observations

- **Decision Tree:** Achieved the highest test accuracy among the evaluated models, but its performance on minority classes remained limited.
- **Multinomial Naive Bayes:** Achieved approximately 51% accuracy. It identified a larger proportion of fatal and serious injury cases, but also produced many false positives for these classes.
- **Neural Network:** Achieved approximately 74% accuracy and a Macro F1-score of 0.37. Its predictions were dominated by the majority class, and fatal injuries remained difficult to identify.

Although the Decision Tree achieved the highest accuracy, the differences in Macro F1-score were relatively small. None of the models demonstrated consistently strong performance across all three classes.

## Hyperparameter Tuning Results

| Model | Best hyperparameters | Best cross-validation Macro F1 |
|---|---|---:|
| Decision Tree | `criterion='entropy'`, `min_samples_leaf=5`, `class_weight='balanced'`, `max_depth=None`, `min_samples_split=2` | 0.8766 |
| Multinomial Naive Bayes | `alpha=0.01`, `fit_prior=False` | 0.5568 |
| Neural Network | `hidden_layer_sizes=(100,)`, `alpha=0.001` | 0.8997 |

The cross-validation scores were substantially higher than the corresponding test-set Macro F1-scores for the Decision Tree and Neural Network. This discrepancy highlights the importance of evaluating model generalization and using reliable validation procedures.

## Parameter Sensitivity Analysis

The sensitivity analysis examined how individual hyperparameters affected the mean cross-validation Macro F1-score.

- **Decision Tree:** Greater tree depth generally corresponded to higher cross-validation scores in the tested configurations.
- **Naive Bayes:** Performance changed only slightly across the tested `alpha` values and `fit_prior` settings.
- **Neural Network:** The configuration with 100 hidden neurons achieved a higher mean cross-validation score than the configuration with 50 hidden neurons. The tested `alpha` values produced very similar scores.

These findings describe the tested configurations and do not necessarily imply that the same settings will perform best on unseen data.

## Conclusion
This project compares Decision Tree, Multinomial Naive Bayes, and Neural Network classifiers for road traffic accident severity prediction. The workflow includes data preprocessing, feature selection, class-imbalance handling, hyperparameter tuning, and parameter sensitivity analysis.

The results demonstrate that relatively high accuracy does not necessarily indicate reliable classification of minority classes. Macro F1-score and class-specific recall provide important additional information when evaluating imbalanced classification tasks.

This project is an educational exercise, and the reported results reflect the challenges encountered during implementation.

## Technologies Used
- Python
- Pandas
- NumPy
- Scikit-learn
- Imbalanced-learn
- Matplotlib
- Seaborn

## Disclaimer
This project is intended for educational purposes and is not designed for real-world road safety decisions.
