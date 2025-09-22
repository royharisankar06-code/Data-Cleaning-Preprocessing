# Data-Cleaning-Preprocessing
# Data Cleaning and Preprocessing Project
import pandas as pd
import numpy as np
   df = pd.read_csv('data/marketing_campaign.csv', sep='\t')
    print("Dataset loaded successfully!")
except FileNotFoundError:
    print("Error: The 'marketing_campaign.csv' file was not found. "
          "Please make sure it's in the 'data/' folder.")
    exit()
    print("\n--- Initial Data Snapshot ---")
print(df.head())
print("\n--- Data Information ---")
print(df.info())
df.columns = df.columns.str.lower().str.replace(' ', '_')
df = df.rename(columns={'dt_customer': 'enrollment_date'})

print("\n--- Columns after renaming ---")
print(df.columns)
print("\n--- Missing Values Check ---")
print(df.isnull().sum())
df.dropna(subset=['income'], inplace=True)
print("\n--- Missing Values Check After Dropping Rows ---")
print(df.isnull().sum())
print("\n--- Duplicates Check ---")
print(f"Number of duplicate rows: {df.duplicated().sum()}")
df['enrollment_date'] = pd.to_datetime(df['enrollment_date'], format='%d-%m-%Y')
print("\n--- Data Types After Correction ---")
print(df.info())
print("\n--- Value Counts for 'Marital_Status' ---")
print(df['marital_status'].value_counts())
df['marital_status'] = df['marital_status'].replace(['YOLO', 'Absurd', 'Alone'], 'Other')
print("\n--- Marital_Status after standardization ---")
print(df['marital_status'].value_counts())
print("\n--- Final Cleaned Dataset Snapshot ---")
print(f"Final dataset shape: {df.shape}")
print(df.head())
df.to_csv('data/marketing_campaign_cleaned.csv', index=False)
print("\nCleaned dataset saved as 'data/marketing_campaign_cleaned.csv'")

