# Data Roles Analysis using Python

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

Link to my notebook for more details: [2_Skill_Demand](https://github.com/julielsa/Python-data-roles-analysis/blob/main/2_Skill_Demand.ipynb)

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

2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the most optimal skills to learn for Data Analysts?

# Learnings and Takeaways

# Challenges

# Conclusion
