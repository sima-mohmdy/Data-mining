# Exploratory Data Analysis on Wine Dataset

## Overview

This exercise focuses on **Exploratory Data Analysis (EDA)** and data visualization using the Wine dataset provided by `scikit-learn`.

The main goal is to explore the structure, distribution, relationships, and possible outliers in the dataset through descriptive statistics and different visualization techniques.

## Dataset

The dataset is the **Wine Recognition Dataset** available through `scikit-learn`.

It contains:

* **178 samples**
* **13 numerical features**
* **3 wine classes**

  * Class 0
  * Class 1
  * Class 2
* No missing or null values

The dataset contains chemical measurements of wines and a target variable indicating the wine class.

## Exploratory Data Analysis

The following steps were performed:

### 1. Dataset Inspection

The dataset was loaded using `sklearn.datasets.load_wine()` and converted into a Pandas DataFrame.

Basic information was examined using:

* `shape`
* `dtypes`
* `info()`
* `describe()`
* Missing-value checks
* Target class information

All 13 input features were found to be numerical (`float64`), and the dataset contained no missing values.

### 2. Class Distribution

A count plot was used to examine the number of samples belonging to each wine class.

The class distribution is:

| Class   | Number of Samples |
| ------- | ----------------: |
| Class 0 |                59 |
| Class 1 |                71 |
| Class 2 |                48 |

This shows that the classes are not exactly equal in size, although there is no extremely severe class imbalance.

### 3. Scatter Plots

Scatter plots were used to visualize the relationship between individual features and the wine classes.

These plots provide a visual comparison of how the feature values are distributed across the three classes.

### 4. Box Plots

Box plots were generated for the features to examine their distributions and identify potential outliers.

The analysis was also repeated separately for each wine class to better understand class-specific distributions.

### 5. Histograms

Histograms were generated separately for each wine class to examine the distribution of individual features.

This helps identify differences in feature distributions between the three wine classes.

### 6. Pair Plot

A pair plot was generated using the target class as the hue.

This provides a visual overview of pairwise relationships between features and can help identify features that may provide useful separation between wine classes.

### 7. Correlation Analysis

A correlation matrix was calculated to investigate relationships between numerical variables.

A heatmap was used to visualize the correlation matrix.

The analysis also examined the correlation between the features and the target variable. Among the positively correlated variables, features such as:

* `color_intensity`
* `nonflavanoid_phenols`
* `alcalinity_of_ash`
* `malic_acid`

showed positive correlation with the target.

## Visualization Techniques

The following visualization techniques were used:

* Count Plot
* Scatter Plot
* Box Plot
* Histogram
* Pair Plot
* Correlation Heatmap

These visualizations were used to understand class distribution, feature distributions, possible outliers, feature relationships, and correlations within the dataset.

## Conclusion

This exercise demonstrated the basic workflow of **Exploratory Data Analysis** on a structured dataset.

The analysis showed that:

* The dataset contains 178 samples and 13 numerical features.
* There are three wine classes.
* No missing values were found.
* The classes have different numbers of samples.
* Feature distributions and potential outliers can be examined using histograms and box plots.
* Pair plots provide a useful visual overview of relationships between features.
* Correlation analysis can help identify relationships between variables and the target.

EDA provides an important first step before applying machine learning models because it helps us understand the data and identify useful patterns, relationships, and potential data-quality issues.

## Reference

This exercise was based on the following Kaggle notebook:

**EDA on Wine Dataset – Dave Aditya**
https://www.kaggle.com/code/daveaditya/eda-on-wine-dataset

The referenced notebook was used as an **educational resource**. Its workflow and code were studied and executed to understand the EDA and visualization process, reproduce the analysis, and examine and interpret the resulting outputs.
