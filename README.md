# ECE2112-PA4

Created by: Jairus Gabriel Ramos | 2ECE-D

# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION

This repository contains my Programming Assignment 4 for our Advanced Computer Programming and Algorithms course. It covers data wrangling and data visualization using Pandas.

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

Average = VisComm.mean(axis = 1, numeric_only = True)
print(Average)
```

I then filtered the students whose Hometown is Visayas and whose Track is Communication.

```python
VisComm['Average'] = Average
VisComm = VisComm.loc[
    (VisComm['Hometown'] == 'Visayas') &
    (df['Track'] == 'Communication'),
    ['Name','Gender','Math','Electronics','Average']
]
```

I displayed the resulting DataFrame and its shape.

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
    ['Name', 'Track', 'GEAS', 'Electronics', 'Average']
]
```

I also filtered the DataFrame to show students whose Average is at least 60.

```python
VisFemale.loc[VisFemale['Average'] >= 60]
```

## C. Category-Average Visualization

For the third problem, I created a copy of the dataset with the calculated Average.

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

I then displayed the results and created bar charts for each category.

```python
track_average.plot.bar()
gender_average.plot.bar()
hometown_average.plot.bar()
```
