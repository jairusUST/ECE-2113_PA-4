# ECE2112-PA4

Created by: Jairus Gabriel Ramos | 2ECE-D

# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION

This repository contains my Programming Assignment 4 for our Advanced Computer Programming and Algorithms course. It covers data wrangling and data visualization using Pandas and Matplotlib.

## Objective

The objective of this activity is to practice filtering data using multiple conditions, creating DataFrames, calculating averages, and visualizing data using bar graphs.

## A. Visayas Communication DataFrame

For the first problem, I loaded the ECE Board Exam 2 dataset using Pandas.

```python
import pandas as pd
df = pd.read_excel('/content/board2.xlsx')
```

I created a copy of the DataFrame and calculated the Average of the numerical scores.

```python
VisComm = df.copy()

Average = df.mean(axis=1, numeric_only=True)
print(Average)
```

I then filtered the students whose Hometown is Visayas and whose Track is Communication.

```python
VisComm['Average'] = Average

VisComm = VisComm.loc[
    (VisComm['Hometown'] == 'Visayas') &
    (VisComm['Track'] == 'Communication'),
    ['Name', 'Gender', 'Math', 'Electronics', 'Average']
]
```

The resulting DataFrame contains 5 students.

```python
VisComm.shape[0]
```

## B. Visayas Female DataFrame

For the second problem, I created a copy of the original DataFrame and added the calculated Average.

```python
VisFemale = df.copy()
VisFemale['Average'] = Average
```

I then selected students whose Hometown is Visayas and whose Gender is Female.

```python
VisFemale = VisFemale.loc[
    (VisFemale['Hometown'] == 'Visayas') &
    (VisFemale['Gender'] == 'Female'),
    ['Name', 'Gender', 'Math', 'Electronics', 'Average']
]
```

I then created another copy of the original DataFrame and added the Average again.

```python
VisFemale = df.copy()
VisFemale['Average'] = Average
```

I filtered the students from Visayas who are Female and have an Average of at least 60.

```python
VisFemale = VisFemale.loc[
    (VisFemale['Average'] >= 60) &
    (VisFemale['Hometown'] == 'Visayas') &
    (VisFemale['Gender'] == 'Female'),
    ['Name', 'Gender', 'Math', 'Electronics', 'Average']
]
```

The filtered result contains 4 students.

## C. Category-Average Visualization

For the third problem, I created a copy of the dataset and added the calculated Average.

```python
df_average = df.copy()
df_average['Average'] = Average
```

I calculated the mean Average for Track, Gender, and Hometown using Pandas.

```python
track_average = df_average.groupby('Track')['Average'].mean()
gender_average = df_average.groupby('Gender')['Average'].mean()
hometown_average = df_average.groupby('Hometown')['Average'].mean()
```

I then displayed the results and created three bar charts for Track, Gender, and Hometown.

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 5))

track_average.plot.bar(
    ax=axes[0],
    legend=False,
    title="Mean Average by Track"
)

gender_average.plot.bar(
    ax=axes[1],
    legend=False,
    title="Mean Average by Gender"
)

hometown_average.plot.bar(
    ax=axes[2],
    legend=False,
    title="Mean Average by Hometown"
)

plt.tight_layout()
plt.show()
```

I also identified the category with the highest mean Average for each feature.

```python
print("Highest Track:", track_average.idxmax())
print("Highest Gender:", gender_average.idxmax())
print("Highest Hometown:", hometown_average.idxmax())
```

The results were:

- Highest Track: Communication
- Highest Gender: Male
- Highest Hometown: Luzon
