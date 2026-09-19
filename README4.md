# ECE2112 PA 4
## Submitted by: Jia Bernice C. Magcamit
## Section: 2ECE-A

This repository presents a detailed analysis and discussion of the fourth programming assignment completed on September 8, 2026, which covers Module 4 — Data Wrangling and Data Visualization.

## Objectives

Upon completing this laboratory exercise, the student is expected to be able to:

1. Filter tabular data using a combination of categorical and numeric criteria.
2. Construct targeted DataFrames by isolating pertinent attributes.
3. Analyze and summarize relationships between categorical factors and numerical metrics.
4. Present data comparisons through accurately labeled and structured plots.

## A. VISAYAS COMMUNICATION DATAFRAME

Isolate records for students hailing from Visayas who are enrolled in the Communication track. Extract only the following columns in exact sequence:

`Name, Gender, Math, Electronics, Average`

Display the filtered DataFrame alongside its total record count, ensuring all selection criteria are evaluated prior to column extraction.

```
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_excel('board2.xlsx')
df['Average'] = (df.Math + df.Electronics + df.GEAS + df.Communication) / 4

display(df)

VisComm = df[(df['Hometown'] == 'Visayas') & 
             (df['Track'] == 'Communication')
            ][['Name', 'Gender', 'Math', 'Electronics', 'Average']]

display(VisComm)

print("Number of rows:", len(VisComm))
```
Key operations implemented in this solution:

`df = pd.read_excel('board2.xlsx')`: Imports the Excel dataset into a primary DataFrame.

`df['Average'] = ...` : Generates an 'Average' field by calculating the mean across all subject areas.

`VisComm`: Defines a subset DataFrame by applying boolean filtering for Visayas hometown and Communication track, then isolating specific fields.

`len(VisComm)`: Evaluates the total number of entries in the filtered result.

## B. VISAYAS FEMALE DATAFRAME

Construct a secondary DataFrame named VisFemale containing female students based in Visayas. Retain the specified attribute order:

`Name, Track, GEAS, Electronics, Average`

Display VisFemale, then render a sub-selection containing individuals with an Average score of 60 or higher without altering the base VisFemale structure.

```
VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
display(VisFemale)

print("\nFemale Students in Visayas whose average in GEAS and Electronics is at least 60")
display(VisFemale[VisFemale['Average'] >= 60])

```

Key operations implemented in this solution:

`VisFemale`: Generates a targeted dataset filtering for female students from Visayas and selecting designated features.

`display(VisFemale[VisFemale['Average'] >= 60])`: Outputs entries from VisFemale where the overall average score reaches or exceeds 60.

## C. CATEGORY-AVERAGE VISUALIZATION

Examine variations in the recorded Average metric across three categorical variables: Track, Gender, and Hometown.

a. Calculate group means for the Average metric across each distinct category.
b. Render the three corresponding statistical summary tables.
c. Plot a single figure displaying three bar graphs: mean Average across Track, Gender, and Hometown.
d. Provide three brief observations identifying the group with the highest mean score within each category.

```
mean_track = df.groupby('Track')['Average'].mean().reset_index()
mean_gender = df.groupby('Gender')['Average'].mean().reset_index()
mean_hometown = df.groupby('Hometown')['Average'].mean().reset_index()

print("\nMean Average by Track")
display(mean_track)

print("\nMean Average by Gender")
display(mean_gender)

print("\nMean Average by Hometown")
display(mean_hometown)

fig, axes = plt.subplots(1, 3, figsize=(18, 5), sharey=True)
fig.suptitle('Mean of Board Exam Average across the three Categorical Features', fontsize=16, fontweight='bold')

axes[0].bar(mean_track['Track'], mean_track['Average'], color='#2b5c8f')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average Score')
axes[0].set_ylim(0, 100)

axes[1].bar(mean_gender['Gender'], mean_gender['Average'], color='#2e7d32')
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average Score')

axes[2].bar(mean_hometown['Hometown'], mean_hometown['Average'], color='#e65100')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average Score')

plt.tight_layout()
plt.show()

highest_track = mean_track.loc[mean_track['Average'].idxmax(), 'Track']
highest_gender = mean_gender.loc[mean_gender['Average'].idxmax(), 'Gender']
highest_hometown = mean_hometown.loc[mean_hometown['Average'].idxmax(), 'Hometown']

print("\nInterpretation Statements")
print(f"\n1. Among the tracks, the {highest_track} track obtained the highest sample mean for Average.")
print(f"2. Between genders, {highest_gender} students achieved the highest sample mean for Average.")
print(f"3. Across the hometown regions, students from {highest_hometown} recorded the highest sample mean for Average.")

```

Key operations implemented in this solution:

`mean_track = df.groupby('Track')['Average'].mean().reset_index()`: Aggregates data by Track category, computes average scores for each group, and formats the result as a structured DataFrame.

`fig, axes = plt.subplots(1, 3, figsize=(18, 5), sharey=True)`: Initializes a 1x3 grid of subplots sharing a unified y-axis scale.

`fig.suptitle(...)` : Configures the main figure heading.

`axes[0].bar(...)`: Constructs a vertical bar chart plotting mean scores per track.

`axes[0].set_title(...) / set_xlabel(...) / set_ylabel(...)`: Defines subplot labels and titles.

`axes[0].set_ylim(0, 100)`: Restricts the y-axis boundaries from 0 to 100.

`plt.tight_layout()`: Formats element layout to ensure titles and labels do not overlap.

`plt.show()`: Renders the generated visualization.

`highest_track = mean_track.loc[mean_track['Average'].idxmax(), 'Track']`: Identifies the top-performing category using index location of the maximum score.





