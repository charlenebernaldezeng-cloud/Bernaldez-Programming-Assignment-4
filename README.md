# # ECE 2112 - Programming Assignment 4
### Name: Bernaldez, Charlene A.                                                                      
### Section: 2ECE-B

## Table of Contents
- [Overview](#overview)
- [Task Summary](#task-summary)
- [Problems & Solutions](#problems--solutions)
  - [A. Visayas Communication DataFrame](#a-visayas-communication-dataframe)
  - [B. Visayas Female DataFrame](#b-visayas-female-dataframe)
  - [C. Category-Average Visualization](#c-category-average-visualization)
- [Project File Structure](#project-file-structure)
- [How to Run](#how-to-run)

---

## Overview

This repository contains the Python-based solutions for Experiment 4:
Data Wrangling and Data Visualization. The exercises use Pandas to filter
and organize student data from the ECE Board Exam 2 dataset. The experiment
also involves calculating category means and presenting comparisons using
bar charts.

The main programming concepts demonstrated are:
* managing data using Pandas.
* Filtering and selecting DataFrame data.
* Calculating averages and group means.
* Creating bar charts for data comparison.
* Interpreting the observed results.

---

## Task Summary

| Task | Key DataFrame Operations | Expected Output |
| :--- | :--- | :--- |
| **A. Visayas Communication DataFrame** | Boolean filtering, column selection | DataFrame containing Visayas students in the Communication track and its number of rows |
| **B. Visayas Female DataFrame** | Boolean filtering, column selection, numerical filtering | VisFemale DataFrame and rows with Average at least 60 |
| **C. Category-Average Visualization** | `groupby()`, `.mean()`, bar charts | Three category-mean summary tables, one figure with three bar charts, and three interpretation statements |

---

## Problems & Solutions

### A. Visayas Communication DataFrame

* *Description:* Creates a DataFrame named `VisComm` containing students
whose Hometown is Visayas and whose Track is Communication. The required
columns are retained in the specified order. The number of rows is also
displayed.

code:

```python
# Read the Excel file
df = pd.read_excel('board2.xlsx')

# Generate the Average column
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

# Apply both filtering conditions to the source dataset first
VisComm = df[(df['Hometown'] == 'Visayas') & 
             (df['Track'] == 'Communication')]

# Select only the required columns in the given order
VisComm = VisComm[['Name', 'Gender', 'Math', 'Electronics', 'Average']]

# Display the resulting DataFrame
display(VisComm)

# Display the number of rows
print('\nNumber of rows:', len(VisComm))

```
### B. Visayas Female DataFrame

* *Description:* Creates a second DataFrame named VisFemale containing
female students whose Hometown is Visayas. Only the required columns are
retained. A second filter displays students whose Average is at least 60
without overwriting the original VisFemale DataFrame.

code:

```python
# Create VisFemale
VisFemale = df[(df['Hometown'] == 'Visayas') & 
               (df['Gender'] == 'Female')]

# Retain only the required columns
VisFemale = VisFemale[['Name', 'Track', 'GEAS', 'Electronics', 'Average']]

# Display VisFemale
display(VisFemale)

# Display students with Average at least 60
print('Students with Average >= 60:')
display(VisFemale[VisFemale['Average'] >= 60])


```
### C. Category-Average Visualization

* *Description:* Examines how the recorded Average differs across the
categorical features Track, Gender, and Hometown. The mean Average for
each category is calculated using Pandas, followed by three summary
tables and three bar charts in one figure.

code:
```python

# Read the Excel file
df = pd.read_excel('board2.xlsx')

# Generate the Average column
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

# a. Compute the mean Average for each category

track_mean = df.groupby('Track')['Average'].mean()
gender_mean = df.groupby('Gender')['Average'].mean()
hometown_mean = df.groupby('Hometown')['Average'].mean()

# b. Display the three summary tables

print('Mean Average by Track:')
display(track_mean.to_frame('Mean Average'))

print('Mean Average by Gender:')
display(gender_mean.to_frame('Mean Average'))

print('Mean Average by Hometown:')
display(hometown_mean.to_frame('Mean Average'))

# c. Create one figure containing three bar charts

fig, axes = plt.subplots(1, 3, figsize=(16, 5))

track_mean.plot(kind='bar', ax=axes[0])
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average')
axes[0].tick_params(axis='x', rotation=45)

gender_mean.plot(kind='bar', ax=axes[1])
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average')
axes[1].tick_params(axis='x', rotation=0)

hometown_mean.plot(kind='bar', ax=axes[2])
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average')
axes[2].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()

# d. Concise observations

print('Track: Communication has the highest sample mean Average at 67.97.')
print('Gender: Male has the highest sample mean Average at 67.18.')
print('Hometown: Luzon has the highest sample mean Average at 68.08.')

```
## Project File Structure
```text
Bernaldez---Programming-Assignment-4/
│
├── Bernaldez_Assignment_4.ipynb    # Main Jupyter Notebook
├── board2.xlsx                     # ECE Board Exam 2 source dataset
└── README.md                       # Project documentation
```
## How to Run
### Using Terminal / Command Prompt
1. Clone or download the repository to your local machine.
2. Ensure that the board2.xlsx dataset is saved in the exact same
directory as your notebook.
3. Open your terminal or command prompt and navigate to the project directory:
   ```bash
   git clone <your-github-repository-link> cd Bernaldez---Programming-Assignment-4

4. Launch Jupyter Notebook:
   ```bash
   jupyter notebook

 5. Open `Bernaldez_Assignment_4.ipynb` from the browser interface and run all cells sequentially (`Cell > Run All`).

### Using Jupyter Notebook / VS Code
1. Open the project folder in your preferred IDE (e.g., Visual Studio Code).
2. Ensure that your board2.xlsx dataset is saved in the same project folder.
3. Open `Bernaldez_Assignment_4.ipynb`.
4. Ensure your Python environment has the pandas library installed.
5. Execute the cells from top to bottom.
6. Ensure that your `board2.xlsx` dataset is saved in the exact same directory as your notebook.
