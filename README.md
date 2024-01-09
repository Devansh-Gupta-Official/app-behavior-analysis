# App Behavior Analysis

## Overview
This repository contains code for analyzing user behavior within a mobile app. The primary focus is on understanding user interactions and their correlation with enrollment in the app.

## Introduction
Often, some companies provide free products/services in an attempt to transition their customers to a paid membership. Since marketing efforts are never free, these companies need to know exactly who to target with offers and promotions.

## Business Challenge
- In this project, we will work with a company (hypothetical) that will allow customers to track all of their finances in one place.
- The company has tasked us to identify which users will most likely NOT enroll in the paid product. Because of marketing costs, the company does not want to offer them to everyone espacially customers who were going to enroll anyways.

## Dataset
The analysis uses the appdata10.csv dataset, consisting of various user attributes and their activities within the app. The data are manufactured fields based on trends found in real world case studies. The fields describe what companies usually track from their users, and the data is based on observed distributions.

This data requires cleaning and a lot of pre-processing is needed to get it ready for modelling.

## Step 1: Importing Libraries and Dataset:
- The code starts by importing necessary libraries like Pandas, NumPy, Matplotlib, Seaborn, and dateutil. 
- It then loads a dataset named 'appdata10.csv' using Pandas' read_csv function.

## Step 2: Data Cleaning:
- Initial data exploration and cleaning are performed using df.describe() to understand basic statistics and identify potential issues. Cleaning operations include converting the 'hour' column from string to integer format using string slicing.
- The columns are described again to confirm the changes after cleaning.

## Step 3: Visualizing the Data:
- Histograms are plotted for numerical columns using Matplotlib to visualize the distribution of each feature.
  
![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/ef9e43a6-6718-4a0d-b964-1db885767bfb)

- Correlation analysis is conducted between numerical columns and the 'enrolled' column using Pandas' corrwith function. A bar plot is created to visualize these correlations.

![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/62ee3f63-2786-4543-9ed3-13a3398d7de1)

  
- A correlation matrix heatmap using Seaborn's heatmap function is generated to visualize the correlations between all pairs of numerical features.

![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/77c09762-6233-49a3-a9ca-a4bbb1cca1b8)


## Step 4: Feature Engineering - Response:
- Feature engineering begins with transforming date columns ('first_open' and 'enrolled_date') to datetime objects for further analysis.
- A new feature 'dataset_diff' is created by calculating the time difference between 'enrolled_date' and 'first_open'.
- Histograms are plotted to understand the distribution of time since enrollment and identify the time window where most enrollments occur.

![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/bb47961b-f5e0-4414-b41c-2d9c8cd20eac)
![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/2d734422-02e0-4a57-ac86-aa93b1c3c13f)

Based on the histogram analysis, the 'enrolled' column is modified to set a time limit (48 hours) for considering user enrollment after the app opening.

## Step 5: Feature Engineering - Screen List:
- Feature engineering continues by processing the 'screen_list' column, which contains comma-separated strings of screens.
- It involves creating binary columns for each top screen, checking if the screen appears in the 'screen_list', and counting any remaining screens as 'Other'.
- **Funnel analysis** is applied to group related screens ('Saving' screens) into a single column named 'SavingCount' to avoid correlation between individual screens.

## Step 6: Saving the Model:
- The updated dataframe is saved to new_data.csv using the to_csv function.

## Step 7: Data Preprocessing and Feature Engineering:
1. Data Loading: The initial step typically involves loading the dataset into memory. This could be from a CSV file, a database, or any other data source. For instance:
```
import pandas as pd
data = pd.read_csv('new_data.csv')
```

2. Feature Engineering: Converting categorical variables to numerical using techniques like one-hot encoding or label encoding.

## Step 8: Model Training:
1. Data Splitting: The dataset is divided into predictor variables (X) and the target variable ('enrolled').
```
X = df.drop('enrolled', axis=1)
y = df['enrolled']
```

2. Model Instantiation and Training:
   
- Choosing a Model: In this case, Logistic Regression is chosen. Other models could be utilized based on the problem type (classification/regression) and data characteristics.
- Splitting Data for Training and Testing
- Training the Model

3. Model Prediction: After training, the model can be used to predict on the test data.

## Step 9: Evaluation Metrics:
1. Calculating evaluation metrics such as accuracy, precision, recall, and F1-score using functions from the sklearn.metrics module.
```
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
accuracy = accuracy_score(y_test, predictions)
precision = precision_score(y_test, predictions)
recall = recall_score(y_test, predictions)
f1 = f1_score(y_test, predictions)
```
2. Creating a confusion matrix.

![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/416ab555-b82b-4ccc-abf5-32f6cfb93a46)


## Step 10: K-Fold Cross-Validation:
Utilizing k-fold cross-validation to evaluate model performance using the cross_val_score function from sklearn.model_selection.
```
from sklearn.model_selection import cross_val_score
accuracies = cross_val_score(estimator=classifier, X=X_train, y=y_train, cv=10)
```

## Step 11: Results Interpretation:
- Displaying and interpreting the evaluation metrics, cross-validation scores, and potentially feature importance scores.\
- Creating a dataframe with these three columns:

![image](https://github.com/Devansh-Gupta-Official/app-behavior-analysis/assets/100591612/642ab220-1bc8-47b7-a2d5-4806053aa707)
