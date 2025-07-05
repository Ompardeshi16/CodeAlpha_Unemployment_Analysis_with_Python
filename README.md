# CodeAlpha_Unemployment_Analysis_with_Python

# Unemployment Analysis with Python

This project analyzes unemployment trends in India using Python. It covers data cleaning, exploration, visualization, and policy insights, with a focus on regional disparities, the impact of COVID-19, and seasonal patterns.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Code Walkthrough](#code-walkthrough)
    - [1. Importing Libraries](#1-importing-libraries)
    - [2. Data Loading](#2-data-loading)
    - [3. Data Cleaning & Exploration](#3-data-cleaning--exploration)
    - [4. Visualizations](#4-visualizations)
    - [5. Policy Insights & Recommendations](#5-policy-insights--recommendations)
- [Key Findings](#key-findings)
- [How to Run](#how-to-run)
- [License](#license)

---

## Project Overview

This notebook provides an in-depth analysis of unemployment in India, highlighting:
- Regional differences in unemployment rates
- The impact of the COVID-19 pandemic
- Seasonal and distributional trends
- Actionable policy recommendations

---

## Dataset

- **Source:** [Unemployment in India.csv](D:/Python/Internship/Datasets/Unemployment%20in%20India.csv)
- **Columns Used:**  
  - `Region`: Name of the state/region  
  - `Estimated Unemployment Rate (%)`: Unemployment rate as a percentage  
  - `Date`: Date of observation

---

## Project Structure

- `Unemployment Analysis with Python.ipynb`: Main Jupyter notebook with all code, analysis, and visualizations.

---

## Code Walkthrough

### 1. Importing Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')
```
*Standard libraries for data analysis and visualization. Warnings are suppressed for cleaner output.*

---

### 2. Data Loading

```python
df = pd.read_csv("D:/Python/Internship/Datasets/Unemployment in India.csv")
df.head()
```
*Loads the dataset into a pandas DataFrame.*

---

### 3. Data Cleaning & Exploration

```python
df_clean = df.dropna(subset=['Region', ' Estimated Unemployment Rate (%)', ' Date'])
print("Unique Regions:", df_clean['Region'].unique())
print("\nDate Range:", df_clean[' Date'].max(), "to", df_clean[' Date'].min())
```
- Removes rows with missing values in key columns.
- Prints unique regions and the date range for context.

---

### 4. Visualizations

#### a. Unemployment Trend Over Time (Sample Region)

```python
sample_region = df_clean['Region'].dropna().unique()[0]
region_data = df_clean[df_clean['Region'] == sample_region]
plt.figure(figsize=(12, 6))
plt.plot(region_data[' Date'], region_data[' Estimated Unemployment Rate (%)'], marker='o', zorder=2)
plt.title(f'Unemployment Rate Trend in {sample_region}')
plt.xlabel('Date')
plt.ylabel('Estimated Unemployment Rate (%)')
plt.grid(True)
plt.xticks(rotation=45)
plt.show()
```
*Shows how unemployment changes over time for a sample region (e.g., Andhra Pradesh).*

#### b. Average Unemployment Rate by Region

```python
plt.figure(figsize=(14, 6))
avg_unemployment = df_clean.groupby('Region')[' Estimated Unemployment Rate (%)'].mean().sort_values()
sns.barplot(x=avg_unemployment.index, y=avg_unemployment.values, palette='viridis')
plt.xticks(rotation=90)
plt.title('Average Unemployment Rate by Region')
plt.xlabel('Region')
plt.ylabel('Average Estimated Unemployment Rate')
plt.tight_layout()
plt.show()
```
*Compares average unemployment rates across all regions.*

#### c. Distribution of Unemployment Rate

```python
unemployment_rate = df[' Estimated Unemployment Rate (%)']
plt.figure(figsize=(8, 5))
sns.histplot(unemployment_rate, kde=True, bins=30, color='blue')
plt.title('Estimated Unemployment Rate Graph(%)')
plt.xlabel('Estimated Unemployment Rate (%)')
plt.ylabel('Frequency')
plt.show()
```
*Shows the distribution and skewness of unemployment rates.*

#### d. COVID-19 Impact Analysis

```python
df_clean[' Date'] = pd.to_datetime(df_clean[' Date'], dayfirst=True)
pre_covid = df_clean[df_clean[' Date'] < '2020-03-01']
covid = df_clean[(df_clean[' Date'] >= '2020-03-01') & (df_clean[' Date'] <= '2020-06-30')]
pre_covid_avg = pre_covid[' Estimated Unemployment Rate (%)'].mean()
covid_avg = covid[' Estimated Unemployment Rate (%)'].mean()
print(f"Average Unemployment Rate (Pre-Covid): {pre_covid_avg:.2f}%")
print(f"Average Unemployment Rate (Covid Period): {covid_avg:.2f}%")
plt.figure(figsize=(6, 4))
plt.bar(['Pre-Covid', 'Covid (Mar-Jun 2020)'], [pre_covid_avg, covid_avg], color=['green', 'red'])
plt.title('Average Unemployment Rate: Pre-Covid vs Covid Period')
plt.ylabel('Estimated Unemployment Rate (%)')
plt.show()
```
*Compares average unemployment rates before and during the COVID-19 lockdown.*

#### e. Seasonal Trends

```python
df_clean['Month'] = df_clean[' Date'].dt.month
monthly_avg = df_clean.groupby('Month')[' Estimated Unemployment Rate (%)'].mean()
plt.figure(figsize=(10, 5))
sns.lineplot(x=monthly_avg.index, y=monthly_avg.values, marker='o')
plt.title('Average Unemployment Rate by Month (All Regions)')
plt.xlabel('Month')
plt.ylabel('Average Estimated Unemployment Rate (%)')
plt.xticks(range(1, 13))
plt.grid(True)
plt.show()
```
*Shows average unemployment rates by month to reveal seasonal patterns.*

---

### 5. Policy Insights & Recommendations

- **Regional Disparities:**  
  States like Haryana and Tripura have average unemployment rates above 20%, while Meghalaya and Odisha are below 5%.  
  _Recommendation:_ Implement targeted job creation and skill development programs in high-unemployment regions.

- **COVID-19 Impact:**  
  Unemployment rose from ~9.5% pre-COVID to ~17.8% during the lockdown (an 87% increase).  
  _Recommendation:_ Strengthen social safety nets and support small businesses to build resilience.

- **Seasonal Trends:**  
  Unemployment spikes in April and May (over 20% in May 2020), compared to a yearly average of ~10%.  
  _Recommendation:_ Time employment schemes to coincide with periods of higher unemployment.

- **Urban-Rural Differences:**  
  Address unique challenges in both rural and urban areas with tailored interventions.

- **Labour Participation:**  
  Encourage higher workforce participation, especially among underrepresented groups.

---

## Key Findings

- **Significant regional disparities** in unemployment rates across India.
- **COVID-19 pandemic** caused a sharp, temporary increase in unemployment.
- **Seasonal spikes** in unemployment, especially during national crises.
- **Most months** have unemployment rates below 10%, but some periods see rates above 20%.

---

## How to Run

1. Clone this repository.
2. Ensure you have Python 3.x and the required libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`) installed.
3. Place the dataset in the specified path or update the path in the notebook.
4. Open the notebook in Jupyter or VS Code and run the cells.

---

## License

This project is for
