# ECE-2112-PA-4

**Made by: Jia Bernice C. Magcamit**

The content of this repository contains the Programming Assignment 4 for our course "Advance Computer Programming" this S.Y. 2025-2026. This project covers three python problems pertaining to Module 4 - Data Analysis and Visualization using `pandas` and `matplotlib.pyplot` libraries on a board exam dataset (`board2.xlsx`).

# **1. Visayas Communication Dataframe**

Filter and extract specific student data from the Visayas region pursuing the Communication track.

The following functions and methods were used in this problem:

• `pd.read_excel()` - a pandas function used to load the Excel dataset (`board2.xlsx`) into a DataFrame.

• `df['Average'] = ...` - creates a new column by computing the arithmetic mean across Math, Electronics, GEAS, and Communication scores for each student.

• `Boolean Indexing` - filters the DataFrame rows based on multiple logical conditions connected by bitwise operators (e.g., `(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')`).

• `len()` - a built-in Python function used to count the total number of filtered rows returned in the resulting DataFrame.

Combining them all, the final code for this problem is as follows;


```
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_excel('board2.xlsx')
df['Average'] = (df.Math + df.Electronics + df.GEAS + df.Communication) / 4

VisComm = df[(df['Hometown'] == 'Visayas') & 
             (df['Track'] == 'Communication')
            ][['Name', 'Gender', 'Math', 'Electronics', 'Average']]

display(VisComm)
print("Number of rows:", len(VisComm))
```
# **2. Visayas Female Dataframe**
Extract female students originating from the Visayas region and further filter those achieving an overall average grade of at least 60 in GEAS and Electronics subjects.

The following functions and methods were used in this problem:

Boolean indexing was utilized to first extract female students located in the Visayas region;

`VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]`

In order to filter students who achieved an average grade threshold of at least 60, a secondary conditional selection was applied to the subset DataFrame;

`VisFemale[VisFemale['Average'] >= 60]`

Combining them all, the final code for this problem is as follows;

```
VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
display(VisFemale)

print("\nFemale Students in Visayas whose average in GEAS and Electronics is at least 60")
display(VisFemale[VisFemale['Average'] >= 60])
```

# **3. Category-Average Visualization**

Analyze and compare the mean examination averages grouped across different categorical variables: Track, Gender, and Hometown.

The following functions and methods were used in this problem:

• `.groupby()` - a pandas method used to split the dataset into groups based on categorical column values (Track, Gender, Hometown).

• `.mean()` - calculates the numerical average of the specified column (Average) for each distinct group.

• `.reset_index()` - converts the grouped series back into a standard pandas DataFrame with a clean index for presentation.

Combining them all, the final code for this problem is as follows;

