# Experiment No. 1: Data Cleaning and Preprocessing

## Aim

To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

## Dataset

The dataset used for this experiment is `heartdisease.csv`. It contains
medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its
data structure, identify data types, and perform basic statistical
analysis for data-cleaning and preprocessing purposes.

## Algorithm

1.  Import essential Python libraries.
2.  Load the dataset using Pandas.
3.  View the dataset structure, data types, and memory usage.
4.  Check for missing values and duplicates.
5.  Perform data summary statistics using `describe()`.
6.  View initial and final records using `head()` and `tail()`.
7.  Sort and group the data based on key attributes.
8.  Rename columns or modify data where necessary.
9.  Save the cleaned dataset for further analysis.

## Functions and Methods Used in the Experiment

### 1. Data Loading and Basic Exploration

  Function / Method      Description  
  ---------------------- ------------------------------------------------------\
  `pd.read_csv()`        Reads a CSV file into a Pandas DataFrame.\
  `df.info()`            Displays column names, data types, and memory usage.\
  `df.dtypes`            Returns the data types of all columns.\
  `df['column'].dtype`   Returns the data type of a specific column.\
  `df.describe()`        Provides summary statistics for numerical columns.\
  `df.head()`            Displays the first 5 rows of the DataFrame.\
  `df.tail()`            Displays the last 5 rows of the DataFrame.\

### 2. Sorting and Grouping

  Function / Method    Description  
  -------------------- ---------------------------------------------  
  `df.sort_values()`   Sorts the DataFrame by one or more columns.  
  `df.groupby()`       Groups data based on one or more columns.  
  `groupby.sum()`      Returns the sum for each group.  
  `groupby.mean()`     Returns the mean for each group.  
  `groupby.median()`   Returns the median for each group.  
  `groupby.max()`      Returns the maximum value in each group.  
  `groupby.min()`      Returns the minimum value in each group.  

### 3. Data Summary and Manipulation  

  Function / Method   Description  
  ------------------- ----------------------------------------------  
  `df.mean()`         Calculates the mean for all numeric columns.  
  `df.rename()`       Renames columns in the DataFrame.  

### 4. Optional Additions  

  Function / Method         Description  
  ------------------------- ----------------------------------------------  
  `df.isnull().sum()`       Checks for missing values in each column.  
  `df.duplicated().sum()`   Counts duplicate rows.  
  `df.dropna()`             Removes rows containing missing values.  
  `df.fillna()`             Fills missing values with a specified value.  
  `df.drop_duplicates()`    Removes duplicate rows.  
  `df.shape`                Returns the number of rows and columns.  
  `df.columns`              Lists column names in the DataFrame.  

## Program & Output
import pandas as pd  
import numpy as np  

# Load the CSV file  
df=pd.read_csv("heartdisease.csv")    

# Display the dataset  
df.head()    

# Dataset information, including data types and memory usage  
df.info()  

# Data types of all columns  
print("\nData Types:")  
print(df.dtypes)  

# Data type of a specific column (replace 'column_name' with an actual column)  
# print(df['column_name'].dtype)  

# Number of rows and columns
print("\nDataset Shape:", df.shape)

# Column names
print("\nColumn Names:")
print(df.columns.tolist())

print("Missing values in each column:")
print(df.isnull().sum())

print("\nNumber of duplicate rows:")
print(df.duplicated().sum())

df.describe()

print("First five records:")
display(df.head())

print("Last five records:")
display(df.tail())

# Sort by the first column (change the column name if needed)
sort_column = df.columns[0]
sorted_df = df.sort_values(by=sort_column)
display(sorted_df.head())

# Group by the last column and calculate summary statistics
group_column = df.columns[-1]
grouped_df = df.groupby(group_column).mean(numeric_only=True)
display(grouped_df)

# Other group summaries (run if required)
# df.groupby(group_column).sum(numeric_only=True)
# df.groupby(group_column).median(numeric_only=True)
# df.groupby(group_column).max(numeric_only=True)
# df.groupby(group_column).min(numeric_only=True)

# Mean of numeric columns
print("Mean values:")
print(df.mean(numeric_only=True))

# Rename columns if required (edit the names to match your dataset)
# df = df.rename(columns={'old_column_name': 'new_column_name'})

# Work on a copy so the original DataFrame remains unchanged
cleaned_df = df.copy()

# Remove duplicate rows
cleaned_df = cleaned_df.drop_duplicates()

# Fill missing numeric values with each column's median
numeric_columns = cleaned_df.select_dtypes(include=np.number).columns
for column in numeric_columns:
    if cleaned_df[column].isnull().any():
        cleaned_df[column] = cleaned_df[column].fillna(cleaned_df[column].median())

# Fill missing categorical/text values with each column's mode
categorical_columns = cleaned_df.select_dtypes(include=['object', 'category', 'bool']).columns
for column in categorical_columns:
    if cleaned_df[column].isnull().any():
        mode_values = cleaned_df[column].mode()
        if not mode_values.empty:
            cleaned_df[column] = cleaned_df[column].fillna(mode_values.iloc[0])

print("Cleaned dataset information:")
cleaned_df.info()

print("\nMissing values after cleaning:")
print(cleaned_df.isnull().sum())

print("\nDuplicate rows after cleaning:")
print(cleaned_df.duplicated().sum())

cleaned_df.to_csv("cleaned_heartdisease.csv", index=False)
print("Cleaned dataset saved as cleaned_heartdisease.csv")





## Result

<< Enter the program execution result>>
