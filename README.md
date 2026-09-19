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
* Loading an Excel dataset into a Pandas DataFrame.
* Creating a calculated `Average` column.
* Filtering rows using multiple categorical conditions.
* Selecting specific columns from a DataFrame.
* Filtering numerical values using Boolean conditions.
* Computing group means using Pandas `groupby()`.
* Creating bar charts for categorical comparisons.
* Interpreting observed sample means without assuming causation.

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
