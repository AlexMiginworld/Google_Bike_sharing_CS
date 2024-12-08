# Cyclistic bike-share analysis case study
[For Google Data Analytics Professional Certificate](https://www.coursera.org/professional-certificates/google-data-analytics)

### Overview and main goal

In the process of this assignment, my goal was to improve my knowledge in data analysis based on Google data analysis field of knowlage. By applying the methods and approaches of this course, I was able to identify certain indicators and patterns that could help the marketing team in designing marketing strategies aimed at converting casual riders into annual members.

### Scenario:

As a junior data analyst on Cyclistic's marketing team, I'm tasked with understanding the differences between casual riders and annual members. Our goal is to uncover insights that will help convert more casual riders into annual memberships. To achieve this, I'll be analyzing historical bike trip data, creating visualizations, and presenting my findings to the marketing team and executives. The insights I gain will be crucial in developing a new marketing strategy to boost annual memberships.

### Core Questions

1. How do annual members and casual riders use Cyclistic bikes dierently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to inuence casual riders to become members?

### Key Tools
*For my data analysis project, I relied on the following tools:*

- **Python:** The core programming language for data manipulation & analysis. Also Pandas library for data cleaning and manipulation.
- **Jupyter Notebooks:** An interactive environment that allowed me to combine code and explanatory text in a single document.
- **Visual Studio Code:** A powerful code editor for writing and running Python scripts.
- **Git & GitHub:** Version control tools for tracking changes and sharing my code with collaborators.
- **Tableau public:** Powerfull tool for data visualization.


## Data Preparation, Processing and Analyze
This section details of three steps in data analysis - Preparation, Processing and Analyze. 

### Import & Clean Up Data

To begin, I prepared the necessary Python libraries and uploaded the four separate datasets, each representing a quarter of historical bike trip data. Prior to analysis, I cleaned and standardized these datasets to ensure data quality and consistency. Subsequently, I merged the cleaned datasets into a single, comprehensive dataset for subsequent analysis and visualization.


```python
# Uploading libraries
import ast
import pandas as pd
import seaborn as sns
import numpy as np
from datasets import load_dataset
import datetime
import matplotlib.pyplot as plt
from matplotlib.ticker import FuncFormatter
from adjustText import adjust_text


# Uploading datasets
df_2019_q1 = pd.read_csv('Original_data_Q1_2019_Q1_2020/Divvy_Trips_2019_Q1.csv')
df_2019_q2 = pd.read_csv('Original_data_Q1_2019_Q1_2020/Divvy_Trips_2019_Q2.csv')
df_2019_q3 = pd.read_csv('Original_data_Q1_2019_Q1_2020/Divvy_Trips_2019_Q3.csv')
df_2019_q4 = pd.read_csv('Original_data_Q1_2019_Q1_2020/Divvy_Trips_2019_Q4.csv')

```

After identifying key research questions, I narrowed down my preparing & cleaning into those datasets. By deleting unnecessary and creating necessary columns I brought this data to the general view and after unite them in one database. 

```python
columns_to_drop = ["tripduration", "from_station_id", "from_station_name", "to_station_id", "to_station_name", "gender", "birthyear", "bikeid"]
df_clean_2019_q1 = df_2019_q1.drop(columns=columns_to_drop)
```
There were some columns with inccorect data types
```python
# Formatted columns start_time & end_time from Series to date&time then created new column where calculated trip duration

df_clean_2019_q1['start_time'] = pd.to_datetime(df_clean_2019_q1['start_time'], format='%Y-%m-%d %H:%M:%S')
df_clean_2019_q1['end_time'] = pd.to_datetime(df_clean_2019_q1['end_time'], format='%Y-%m-%d %H:%M:%S')

df_clean_2019_q1['ride_length_seconds'] = (df_clean_2019_q1['end_time'] - df_clean_2019_q1['start_time']).dt.total_seconds()

df_clean_2019_q1['ride_length_seconds'] = df_clean_2019_q1['ride_length_seconds'].astype(int)

def seconds_to_hhmmss(seconds):
    hours, remainder = divmod(seconds, 3600)
    minutes, seconds = divmod(remainder, 60)
    return f"{hours:02d}:{minutes:02d}:{seconds:02d}"

df_clean_2019_q1['ride_length'] = df_clean_2019_q1['ride_length_seconds'].apply(seconds_to_hhmmss)

df_clean_2019_q1.sample(10)
```

Then in the last round of the section I had to finally merge & export the dataset

```python
df_merged_2019 = pd.concat([df_2019_q1_clean,df_2019_q2_clean,df_2019_q3_clean,df_2019_q4_clean], ignore_index=True)
df_merged_2019.to_csv('All_trips_2019.csv', index=False)
```

# Data Visualization & Answering Questions

*For this section I put my hands on Tableau in order to creat vesualization and get insights from it. Feel free to check my researching on [Tableau Public](https://public.tableau.com/app/profile/alex.kaplenko/viz/Casestudybike-sharing/Casestudystory)!*

<img src="Tableau/Customers comparison.png" alt="Customers comparison" width="1360" height="760">

<img src="Tableau/Weekly Ride Trends.png" alt="Tableau/Weekly Ride Trends.png" width="1360" height="760">


