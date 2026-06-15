Step 1: Upload Dataset

Open Google Colab:

https://colab.research.google.com/

Create New Notebook.

Upload:

Unemployment in India.csv
Step 2: Import Libraries

Run:

import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns

import warnings
warnings.filterwarnings('ignore')
Step 3: Load Dataset
df = pd.read_csv("Unemployment in India.csv")

df.head()

You should see:

Region
Date
Frequency
Estimated Unemployment Rate (%)
Estimated Employed
Area
Step 4: Check Dataset Information
df.shape

Output:

(768,7)

Check columns:

df.columns
Step 5: Clean Column Names

Your dataset has extra spaces.

Run:

df.columns=df.columns.str.strip()

df.columns
Step 6: Check Missing Values
df.isnull().sum()
Step 7: Remove Missing Data
df.dropna(inplace=True)

Check again:

df.isnull().sum()
Step 8: Convert Date Format

Your date is like:

31-05-2019

Convert:

df['Date']=pd.to_datetime(
    df['Date'],
    dayfirst=True
)

Check:

df.info()
Step 9: Basic Statistics
df.describe()

Find average unemployment:

avg = df['Estimated Unemployment Rate (%)'].mean()

print(
"Average Unemployment Rate:",
avg
)
Step 10: Unemployment Trend Analysis

Plot overall trend:

plt.figure(figsize=(14,6))

plt.plot(
    df['Date'],
    df['Estimated Unemployment Rate (%)']
)

plt.title(
"Unemployment Rate Trend in India"
)

plt.xlabel("Date")
plt.ylabel("Unemployment Rate (%)")

plt.xticks(rotation=45)

plt.show()
Step 11: Covid-19 Impact Analysis

Create year column:

df['Year']=df['Date'].dt.year

Before Covid:

before_covid=df[
df['Year']<2020
]

During Covid:

covid=df[
df['Year']==2020
]

Compare:

print(
"Before Covid:",
before_covid[
'Estimated Unemployment Rate (%)'
].mean()
)


print(
"During Covid:",
covid[
'Estimated Unemployment Rate (%)'
].mean()
)
Step 12: Covid Visualization
plt.figure(figsize=(14,6))


sns.lineplot(
data=df,
x='Date',
y='Estimated Unemployment Rate (%)'
)


plt.axvline(
pd.Timestamp('2020-03-01')
)


plt.title(
"Impact of Covid-19 on Unemployment"
)


plt.show()
Step 13: State Wise Unemployment

Find top affected states:

state=df.groupby(
'Region'
)['Estimated Unemployment Rate (%)'].mean()


state=state.sort_values(
ascending=False
)


state.head(10)

Plot:

plt.figure(figsize=(12,6))


state.head(10).plot(
kind='bar'
)

plt.title(
"Top 10 States with High Unemployment"
)

plt.ylabel(
"Unemployment Rate (%)"
)

plt.show()
Step 14: Rural vs Urban Analysis
area=df.groupby(
'Area'
)['Estimated Unemployment Rate (%)'].mean()

area

Graph:

area.plot(
kind='bar',
figsize=(6,4)
)

plt.title(
"Urban vs Rural Unemployment"
)

plt.show()
Step 15: Monthly Seasonal Analysis

Create month:

df['Month']=df['Date'].dt.month

Average:

monthly=df.groupby(
'Month'
)['Estimated Unemployment Rate (%)'].mean()


monthly

Plot:

monthly.plot(
kind='bar',
figsize=(10,5)
)

plt.title(
"Monthly Unemployment Pattern"
)

plt.show()
Step 16: Correlation Analysis
corr=df.corr(
numeric_only=True
)

plt.figure(figsize=(8,6))

sns.heatmap(
corr,
annot=True
)

plt.title(
"Correlation Analysis"
)

plt.show()
Step 17: Final Insights

Write these in your report:

Findings:
Unemployment increased significantly during Covid-19 lockdown period.
2020 shows the highest unemployment spike.
Some states have higher unemployment compared to others.
Urban and rural areas show different unemployment patterns.
Seasonal changes affect unemployment rate.
Step 18: Save Clean Dataset
df.to_csv(
"cleaned_unemployment_data.csv",
index=False
)
Step 19: GitHub Files

Upload:

Unemployment-Analysis-Python

│
├── Unemployment in India.csv
├── unemployment_analysis.ipynb
├── cleaned_unemployment_data.csv
├── README.md
└── requirements.txt

This will complete your Data Science + Python project with:
✅ Data cleaning
✅ EDA
✅ Covid analysis
✅ Visualization
✅ Insights
✅ GitHub ready project# Code-Alpha-Unemployment-Analysis-with-Python
