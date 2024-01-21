# **PUBLIC HEALTH SIGNIFICANCE AND THE HARDSHIP INDEX**

### *PROJECT OVERVIEW*

In this project we will be critically looking into the relation between the income and earnings of a group of people in chicago during the year 2008 to 2012 as to how it affect thier health. it is a socioeconomical collection to look into indicators that determine the above mentioned. This project investigates the Public Health implications associated with socioeconomic hardship, focusing on the Hardship Index as a key metric. By analyzing the correlation between the Hardship Index and Public Health indicators, we aim to identify vulnerable communities, highlight health disparities, and inform targeted interventions. The significance lies in providing evidence-based insights for policy development, resource allocation, and initiatives that address the unique needs of communities facing economic and social challenges. Through statistical analysis and data-driven recommendations, the project seeks to contribute to the promotion of health equity and well-being.

### *DATA SOURCES*

This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” by Chicago community area, for the years 2008 – 2012. The indicators are the percent of occupied housing units with more than one person per room (i.e., crowded housing); the percent of households living below the federal poverty level; the percent of persons in the labor force over the age of 16 years that are unemployed; the percent of persons over the age of 25 years without a high school diploma; the percent of the population under 18 or over 64 years of age (i.e., dependency); and per capita income. Indicators for Chicago as a whole are provided in the final row of the table. See the full dataset description for more information at: [CLICK HERE](https://data.cityofchicago.org/api/views/fwb8-6aw5/files/A5KBlegGR2nWI1jgP6pjJl32CTPwPbkl9KU3FxlZk-A?download=true&filename=P:\EPI\OEPHI\MATERIALS\REFERENCES\ECONOMIC_INDICATORS\Dataset_Description_socioeconomic_indicators_2012_FOR_PORTAL_ONLY.pdf) The Data Provided By
U.S. Census Bureau, under the category of health and human services. The data is license here [click here](http://factfinder2.census.gov) 

### Tools
  - SQl (structured query language) Dow
  - python  matplotlib
  -         seaborn

### Data cleaning and preparation

The data was updated from time to time by chichago data portal so there was little or no cleaning to do. The data was arranged in tabular form with the following specification Selected data above shows Socioeconomic Indicators in Chicago.
The city of Chicago released a dataset of socioeconomic data to the Chicago City Portal. This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” for each Chicago community area, for the years 2008 – 2012.

Scores on the hardship index can range from 1 to 100, with a higher index number representing a greater level of hardship.

A detailed description of the dataset can be found on the city of Chicago's website, but to summarize, the dataset has the following variables:

.Community Area Number (ca): Used to uniquely identify each row of the dataset

.Community Area Name (community_area_name): The name of the region in the city of Chicago

.Percent of Housing Crowded (percent_of_housing_crowded): Percent of occupied housing units with more than one person per room

.Percent Households Below Poverty (percent_households_below_poverty): Percent of households living below the federal poverty line

.Percent Aged 16+ Unemployed (percent_aged_16_unemployed): Percent of persons over the age of 16 years that are unemployed

.Percent Aged 25+ without High School Diploma (percent_aged_25_without_high_school_diploma): Percent of persons over the age of 25 years without a high school education

.Percent Aged Under 18 or Over 64:Percent of population under 18 or over 64 years of age (percent_aged_under_18_or_over_64): (ie. dependents)

.Per Capita Income (per_capita_income_): Community Area per capita income is estimated as the sum of tract-level aggragate incomes divided by the total population

.Hardship Index (hardship_index): Score that incorporates each of the six selected socioeconomic indicators

### Exploratory Data Analysis

poverty continues to be a ravaging pandemy in our society and the war to fight and 


### Data Analysis
For the anaylsis sqlite and python was used to analysis the data 
Connect to the database
Let us first load the SQL extension and establish a connection with the database

The syntax for connecting to magic line sql using sqllite is
%sql sqlite://DatabaseName

where DatabaseName will be your .db file
```%load_ext sql```

```import csv
import sqlite3

con = sqlite3.connect("socioeconomic.db")
cur = con.cursor()
!pip install -q pandas==1.1.5```

```%sql sqlite:///socioeconomic.db```
'Connected: @socioeconomic.db'

After creating the database, the next thing to import the c.s.v file from the given url into pandas dataframes.we will use the df.to_sql() function and convert the csv into a table in sqlite.

```import pandas
df = pandas.read_csv('https://data.cityofchicago.org/resource/jcxq-k9xf.csv')
df.to_sql("chicago_socioeconomic_data", con, if_exists='replace', index=False,method="multi")```

Now the data is now in the frame and to verify, you can use the select clause to view the import table but limit to 10

```%sql select * from chicago_socioeconomic_data limit 10;```
 * sqlite:///socioeconomic.db
Done.

![image](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/562aa86b-d093-415a-9dc0-5a3d876acd61)
