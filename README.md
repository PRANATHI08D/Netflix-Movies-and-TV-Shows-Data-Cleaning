# Netflix-Movies-and-TV-Shows-Data-Cleaning
#This project is a data cleaning and preparation task using Python with Pandas.
import pandas as pd
import numpy as np

# Load the dataset
df = pd.read_csv('netflix_movies_and_tv_shows.csv')

# Check for missing values
print(df.isnull().sum())

# Handle missing values (e.g., fill with mean, median, or mode)
df['director'].fillna('Unknown', inplace=True)
df['cast'].fillna('Unknown', inplace=True)

# Check for duplicate rows
print(df.duplicated().sum())

# Remove duplicate rows
df.drop_duplicates(inplace=True)

# Standardize text values (e.g., title, genre)
df['title'] = df['title'].str.title()
df['genre'] = df['genre'].str.title()

# Convert date formats to a consistent type (e.g., dd-mm-yyyy)
df['release_date'] = pd.to_datetime(df['release_date'], format='%d-%m-%Y')

# Rename column headers to be clean and uniform (e.g., lowercase, no spaces)
df.columns = [col.lower().replace(' ', '_') for col in df.columns]

# Check data types
print(df.dtypes)

# Fix data types (e.g., rating should be float, release_date as datetime)
df['rating'] = df['rating'].astype(float)
df['release_date'] = pd.to_datetime(df['release_date'])

# Save the cleaned dataset
df.to_csv('cleaned_netflix_movies_and_tv_shows.csv', index=False)

