# netfilx
# Step 1: Import required libraries

import zipfile
import pandas as pd

# Path to your zip file
zip_path = "C:/Users/iamal/Downloads/netflix_titles.csv.zip"

# Open the ZIP file and read the CSV inside it
with zipfile.ZipFile(zip_path, 'r') as zip_ref:
    csv_files = [name for name in zip_ref.namelist() if name.endswith('.csv')]
    print("CSV files found in the zip:", csv_files)

    # Read the first CSV file inside the same block
    with zip_ref.open(csv_files[0]) as file:
        df = pd.read_csv(file)

# Now you can work with 'df' outside the block
df.head()
# Initial data exploration
df.size
df.columns
print(df.info())
print(df.isnull().sum())
df.isna().sum()
df[df['director'].isna()]

# Data cleaning and preprocessing
df['director']=df['director'].fillna('Unknown')
df.isna().sum()
for a in ['cast','country','date_added','rating','duration']:
    df[a] = df[a].fillna(df[a].mode()[0])

    print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")
print("\nColumn Data Types:\n", df.dtypes)
print("\nMissing Values:\n", df.isna().sum())
print("\n Description for the dataset:\n",df.describe())
df.describe()

print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")
print("\nColumn Data Types:\n", df.dtypes)
print("\nMissing Values:\n", df.isna().sum())
print("\n Description for the dataset:\n",df.describe())
df['type'].unique()

df['date_added'] = df['date_added'].str.strip()
df['date_added'] = pd.to_datetime(df['date_added'], format='%B %d, %Y')

df.dtypes
#date format

df['date']=df['date_added'].dt.day
df['month']=df['date_added'].dt.month
df['year']=df['date_added'].dt.year


df.duplicated().sum()
