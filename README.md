# App Behavior Analysis

## Overview
This repository contains code for analyzing user behavior within a mobile app. The primary focus is on understanding user interactions and their correlation with enrollment in the app.

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

