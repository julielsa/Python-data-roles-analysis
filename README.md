# Data Roles Analysis Using Python

# Overview

Welcome to my analysis of the data job market, specifically targeting data analyst roles. It examines the top-paying and most in-demand skills to identify optimal job opportunities for data analysts.

Using data from [Luke Barousse's Python Course](https://lukebarousse.com/python)  the analysis includes detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I investigate key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

# The Questions

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying) 

# Areas of Skill

Python: The core tool for my analysis, enabling me to process and extract key insights from the data.
  - Pandas: Used for data manipulation and analysis.
  - Matplotlib: Employed for data visualization.
  - Seaborn: Enhanced my visualizations with more advanced and aesthetically pleasing graphics.

# Data Prep and Cleaning
  ### - Import and Clean Data
  I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.


```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```
  ### - Filter US Jobs
  To focus my analysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.

```python
df_US = df[df['job_country'] == 'United States']

```
# Analysis
Each Jupyter notebook for this project is aimed at analyzing specific aspects of the data job market. 
Here’s how I approached each question:

## 1. What are the most in-demand skills for the top 3 most popular data roles?
To identify the most in-demand skills for the top three data roles, I filtered job positions to determine the most popular roles and extracted the top five skills for each. This analysis reveals the key skills for each prominent job title, helping to understand which skills to prioritize based on the targeted role.

View my notebook with detailed steps here: [2_Skill_Demand](https://github.com/julielsa/Python-data-roles-analysis/blob/main/2_Skill_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```
### Results
![Likelihood of Skills Requested in the US Job Postings](https://github.com/julielsa/Python-data-roles-analysis/blob/main/Visualization%20images/Likelihood%20of%20skills%20in%20US.png)
*Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*

### Insights
  - SQL is the most in-demand skill across all roles. For Data Analysts, Data Engineers, and Data Scientists, SQL appears as a highly requested skill, with 51%, 68%, and 51% respectively. This indicates that SQL is fundamental across various data roles, underscoring the importance of database management and querying skills in the data industry.
  - Python is notably prominent for Data Engineers and Data Scientists, with a 65% and 72% likelihood respectively. This highlights Python's versatility and essential role in both data engineering tasks, like data pipeline creation, and data science tasks, such as machine learning and data analysis. For Data Analysts, Python also shows a significant presence at 27%, illustrating its growing importance in analytical roles.
  - Specific Tools and Technologies for Each Role: The chart shows distinct skills that are uniquely emphasized in different roles. For example:
    - Data Analysts: Excel (41%) and Tableau (28%) are more specific to this role, reflecting the need for data visualization and spreadsheet proficiency.
    - Data Engineers: AWS (43%) and Azure (32%) are key, indicating the importance of cloud computing skills for managing data infrastructure.
    - Data Scientists: R (24%) and SAS (24%) are listed, which are commonly used in statistical analysis and advanced analytics, highlighting the role's focus on in-depth data analysis and modeling.

## 2. How are in-demand skills trending for Data Analysts?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [3_Skill_Trend](https://github.com/julielsa/Python-data-roles-analysis/blob/main/3_Skill_Trend.ipynb)

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```

### Results
![Trending Top Skills for Data Analysts in the US](https://github.com/julielsa/Python-data-roles-analysis/blob/main/Visualization%20images/Top%20trending%20skills.png)
*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Insights
  - Throughout 2023, SQL remains the most demanded skill for Data Analysts, consistently maintaining a likelihood above 60%. This reinforces the importance of SQL in data analysis for database management and querying capabilities.
  - Stable Demand for Excel, Fluctuations in Python and Tableau:
      - Excel maintains a steady demand, hovering around 40-45%, indicating its essential role in data manipulation and analysis.
      - Python and Tableau exhibit fluctuations in demand. Python's likelihood shows an increase toward the end of the year, suggesting a growing emphasis on programming and data analysis capabilities. Tableau shows slight variability but remains an important tool for data visualization.
   - Power BI remains relatively low in demand compared to other skills, with a likelihood around 20%. While still a valuable tool, it appears less critical compared to SQL, Excel, Python, and Tableau for Data Analysts in the US during this period.

## 3. How well do jobs and skills pay for Data Analysts?
To identify the highest-paying roles and skills, I focused on job listings in the United States and analyzed their median salaries. I first examined the salary distributions for common data roles such as Data Scientist, Data Engineer, and Data Analyst to understand which positions offer the highest compensation.

View my notebook with detailed steps here: [4_Salary_Analysis](https://github.com/julielsa/Python-data-roles-analysis/blob/main/4_Salary_Analysis.ipynb)

### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```
### Results
![Salary Distributions of Data Jobs in the US](https://github.com/julielsa/Python-data-roles-analysis/blob/main/Visualization%20images/Salary%20distribution.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

### Insights
  - Senior Data Scientist and Senior Data Engineer roles have higher median salaries and wider salary ranges compared to their non-senior counterparts. This indicates that experience and seniority in data roles significantly impact earning potential.
  - Senior Data Scientist and Senior Data Engineer positions exhibit considerable salary variability, with a noticeable number of outliers extending beyond the $300K mark. This suggests that while senior positions generally offer higher salaries, the pay can vary greatly based on factors like company, location, and individual expertise.
  - Data Scientist positions, even at non-senior levels, show a substantial median salary and a wide range of earnings. This underscores the value and demand for data scientists in the market, making it a lucrative career choice within the data field.

## Highest Paid & Most Demanded Skills for Data Analysts
Next, I refined my analysis to focus specifically on data analyst roles. I examined the highest-paid and most in-demand skills within this category. To illustrate these findings, I created two bar charts.

### Visualize Data
```python

fig, ax = plt.subplots(2, 1)  

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analystsr')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```
### Results
Here's the breakdown of the highest-paid & most in-demand skills for data analysts in the US:

![The Highest Paid & Most In-Demand Skills for Data Analysts in the US](https://github.com/julielsa/Python-data-roles-analysis/blob/main/Visualization%20images/Highest%20paid%20vs%20highest%20in%20demand.png)
*Two separate bar graphs visualizing the highest-paid skills and most in-demand skills for data analysts in the US.*

### Insights

## 4. What are the most optimal skills to learn for Data Analysts?

View my notebook with detailed steps here:

### Visualize Data

### Results

### Insights

# Learnings and Takeaways

# Challenges

# Conclusion
