# Cleaning and Exploratory Data Analysis of Google Play Store Data

## Introduction
This project involves cleaning the Google Play Store dataset to ensure the data is prepared for analysis. The data cleaning process addresses issues such as missing values, duplicate entries, and inconsistent formatting. Following data cleaning, exploratory data analysis (EDA) is conducted to gain insights and understand the dataset better.

## Problem Statement
With millions of apps available on the Google Play Store, having clean and reliable data is essential for understanding trends and deriving meaningful insights. This project aims to address data quality issues to ensure accurate results in subsequent analyses.

## Data Collection
The dataset consists of:
- 20 columns
- 10,841 rows

## Steps Followed
1. Data Cleaning
2. Exploratory Data Analysis
3. Feature Engineering

## Data Cleaning Steps
1. **Handling Missing Values**
   - Identified columns with missing values.
   - Applied strategies such as removal and imputation to handle missing values.

2. **Removing Duplicate Entries**
   - Detected and removed duplicate rows to ensure data integrity.

3. **Standardizing Formats**
   - Standardized formats for numerical values (e.g., size, price).
   - Normalized text data (e.g., app names, categories).

4. **Data Type Conversion**
   - Converted columns to appropriate data types (e.g., integers, floats, strings).

5. **Handling Outliers**
   - Identified and addressed outliers that could skew analysis results.

6. **Date and Time Parsing**
   - Parsed and formatted date columns to ensure consistency.

## Code Implementation
Here's a brief overview of the code used for data cleaning:

```python
import pandas as pd
import numpy as np

# Load the dataset
df = pd.read_csv('https://raw.githubusercontent.com/krishnaik06/playstore-Dataset/main/googleplaystore.csv')

# Handling missing values
df = df.dropna()  # Example: Remove rows with missing values

# Removing duplicate entries
df = df.drop_duplicates()

# Standardizing numerical values
df['Size'] = df['Size'].str.replace('M', '000').str.replace('k', '').replace('Varies with device', np.nan).astype(float)

# Normalizing text data
df['App'] = df['App'].str.lower()  # Example: Convert app names to lowercase

# Converting data types
df['Reviews'] = df['Reviews'].astype(int)

# Handling outliers
df = df[df['Size'] < df['Size'].quantile(0.99)]  # Example: Remove top 1% size outliers

# Parsing date columns
df['Last Updated'] = pd.to_datetime(df['Last Updated'])
df['Day'] = df['Last Updated'].dt.day
df['Month'] = df['Last Updated'].dt.month
df['Year'] = df['Last Updated'].dt.year

# Save the cleaned dataset
df.to_csv('data/google_cleaned.csv', index=False)
