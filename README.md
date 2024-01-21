# **PUBLIC HEALTH SIGNIFICANCE AND THE HARDSHIP INDEX**

## TABLE OF CONTENTS

-[PROJECT OVERVIEW](#project-overview)

-[DATA SOURCES](#data-sources)

-[TOOLS](#tools)

-[DATA CLEANING AND PREPARATION](#Data-cleaning-and-preparation)

-[EXPLORATORY DATA ANALYSIS](#Exploratory-Data-Analysis)

-[DATA ANALYSIS](#Data-Analysis)

-[VISUALIZATION](#visualization)

-[RESULTS AND FINDINGS](#results-and-findings)

-[RECOMMENDATIONS](#recommendations)

-[REFERENCES](#references)


### *PROJECT OVERVIEW*

In this project we will be critically looking into the relation between the income and earnings of a group of people in chicago during the year 2008 to 2012 as to how it affect thier health. it is a socioeconomical collection to look into indicators that determine the above mentioned. This project investigates the Public Health implications associated with socioeconomic hardship, focusing on the Hardship Index as a key metric. By analyzing the correlation between the Hardship Index and Public Health indicators, we aim to identify vulnerable communities, highlight health disparities, and inform targeted interventions. The significance lies in providing evidence-based insights for policy development, resource allocation, and initiatives that address the unique needs of communities facing economic and social challenges. Through statistical analysis and data-driven recommendations, the project seeks to contribute to the promotion of health equity and well-being.

### *DATA SOURCES*

This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” by Chicago community area, for the years 2008 – 2012. The indicators are the percent of occupied housing units with more than one person per room (i.e., crowded housing); the percent of households living below the federal poverty level; the percent of persons in the labor force over the age of 16 years that are unemployed; the percent of persons over the age of 25 years without a high school diploma; the percent of the population under 18 or over 64 years of age (i.e., dependency); and per capita income. Indicators for Chicago as a whole are provided in the final row of the table. See the full dataset description for more information at: [CLICK HERE](https://data.cityofchicago.org/api/views/fwb8-6aw5/files/A5KBlegGR2nWI1jgP6pjJl32CTPwPbkl9KU3FxlZk-A?download=true&filename=P:\EPI\OEPHI\MATERIALS\REFERENCES\ECONOMIC_INDICATORS\Dataset_Description_socioeconomic_indicators_2012_FOR_PORTAL_ONLY.pdf) The Data Provided By
U.S. Census Bureau, under the category of health and human services. The data is license here [click here](http://factfinder2.census.gov) 

### Tools
  - SQl (structured query language) Dow
  - python  matplotlib
  -         seaborn

### DATA CLEANING AND PREPARATION

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

### EXPLORATORY DATA ANALYSIS

poverty continues to be a ravaging pandemic in our society irrespective of the country and the war in fighting has never been won. The project rises a peep on what could make this stubborn head persist. taking a sample from groups of community in chichago, following question were asked.
 - what is the level of poverty
 - what are main indicators of these persistance
 - what class of these sample is the most affected
 - how is hardship measured by poverty
 - what is the income strength compared to poverty against unemployment
 - what is the effect of all the on general health of the population


### DATA ANALYSIS

For the anaylsis sqlite and python was used to analysis the data 
Connect to the database
Let us first load the SQL extension and establish a connection with the database

The syntax for connecting to magic line sql using sqllite is
%sql sqlite://DatabaseName

where DatabaseName will be your .db file
```
%load_ext sql
```

```import csv
import sqlite3

con = sqlite3.connect("socioeconomic.db")
cur = con.cursor()
!pip install -q pandas==1.1.5
```

```
%sql sqlite:///socioeconomic.db
```
'Connected: @socioeconomic.db'

#### After creating the database, the next thing to import the c.s.v file from the given url into pandas dataframes.we will use the df.to_sql() function and convert the csv into a table in sqlite.

```import pandas
df = pandas.read_csv('https://data.cityofchicago.org/resource/jcxq-k9xf.csv')
df.to_sql("chicago_socioeconomic_data", con, if_exists='replace', index=False,method="multi")
```

#### Now the data is now in the frame and to verify, you can use the select clause to view the import table but limit to 10

```
%sql select * from chicago_socioeconomic_data limit 10;
```
    * sqlite:///socioeconomic.db
      Done.

#### Retriving The Table for Analysis
![table](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/8c9a67cd-5251-46a7-85ab-420cd949efd7)


```
%sql PRAGMA table_info("chicago_socioeconomic_data");
```
* sqlite:///socioeconomic.db
Done.
![table structure](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/15d60196-2db7-47e7-b4b2-3048318eae43)

```
%sql select count(*) from chicago_socioeconomic_data
```

#### To start the analysis, we have to start by looking at the hardship index, the maximum, minimum and the average.
#### maximum hardship index

```
%sql select max(hardship_index)from chicago_socioeconomic_data
```

#### minimum hardship index
```
%sql select min(hardship_index) from chicago_socioeconomic_data
```

#### mean of hardship index
```
%sql select avg(hardship_index) from chicago_socioeconomic_data
```

#### hardship index greater than average
```
%sql select count(*) from chicago_socioeconomic_data where hardship_index > 50
```

```
%sql select count(*) from chicago_socioeconomic_data where hardship_index < 50
```

#### lets look at per capita income
```
%sql select avg(per_capita_income_) from chicago_socioeconomic_data
```

```
%sql select community_area_name,hardship_index from chicago_socioeconomic_data where per_capita_income_ > 25597.0
```

```
%sql select count (community_area_name) from chicago_socioeconomic_data where per_capita_income_ > 25597.0
```

```
%sql select community_area_name from chicago_socioeconomic_data where hardship_index = (select max(hardship_index)from chicago_socioeconomic_data)
```

```
%sql select avg(percent_households_below_poverty)from chicago_socioeconomic_data;
```

```
%sql select count(percent_aged_16_unemployed) from chicago_socioeconomic_data where percent_households_below_poverty < 22
```

```
%sql select avg(percent_of_housing_crowded)from chicago_socioeconomic_data
```

```
%sql select count (*) from chicago_socioeconomic_data where percent_of_housing_crowded < 4.920512820512823
```

```
%sql select sum(per_capita_income_) from chicago_socioeconomic_data
```

```
%sql select avg(percent_aged_under_18_or_over_64) from chicago_socioeconomic_data where( percent_aged_under_18_or_over_64)-( select sum(per_capita_income_) from chicago_socioeconomic_data)
```

### VISUALIZATION

#### in order to create more clarity, visualization is apparent to start this we will  look at the correction or the relationship of some variable.  to do this we will import matplotlib and seaborn
 #### Creating a scatter plot using the variables per_capita_income_ and hardship_index. Explain the correlation between the two variables.

```
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
```

```income_vs_hardship = %sql SELECT per_capita_income_, hardship_index FROM chicago_socioeconomic_data;
   plot = sns.jointplot(x='per_capita_income_',y='hardship_index', data=income_vs_hardship.DataFrame())
```
![HARDSHIP VS INCOME](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/d0b9a37e-177a-4124-a4d9-e3293765f15f)


```
The barchat is the showing the distribution of housing crowding index
# Replace "chicago_socioeconomic_data" with the actual table name
housing_crowd = %sql SELECT percent_of_housing_crowded FROM chicago_socioeconomic_data;

# Check if the result set is not None and has rows
if housing_crowd is not None and len(housing_crowd) > 0:
    # Convert the result set to a Pandas DataFrame
    housing_crowd_df = housing_crowd.DataFrame()

    # Create a bar chart for housing crowd distribution
    plt.figure(figsize=(10, 6))
    sns.barplot(x=housing_crowd_df.index, y=housing_crowd_df.percent_of_housing_crowded)

    # Set plot labels and title
    plt.xlabel('Index')  # or use your actual x-axis label
    plt.ylabel('Percent of Housing Crowded')
    plt.title('Bar Chart: Housing Crowd Distribution')

    # Show the plot
    plt.show()
else:
    print("Query result is None or empty.")
```
![BAR CHAT HOUSING CROWDED](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/bf9ebd89-e777-4976-bf56-e3016b644aaa)


```
income_vs_poverty = %sql SELECT per_capita_income_, percent_households_below_poverty FROM chicago_socioeconomic_data;
plot = sns.lineplot(x='per_capita_income_',y='percent_households_below_poverty', data=income_vs_poverty.DataFrame())
```
![POVERTY VS INCOME](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/2d441d89-8abf-4079-b7d0-18541ded0c1c)


```income_vs_crowded = %sql SELECT per_capita_income_, percent_of_housing_crowded FROM chicago_socioeconomic_data;
plot = sns.barplot(x='per_capita_income_',y='percent_of_housing_crowded', data=income_vs_crowded.DataFrame())
```
![HOUSING VS INCOME](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/427d56e6-bb8f-4605-90f6-468ecc81ee8d)


```
crowded_vs_hardship = %sql select percent_of_housing_crowded, hardship_index FROM chicago_socioeconomic_data;
plot = sns.boxplot(x='percent_of_housing_crowded',y='hardship_index', data=crowded_vs_hardship.DataFrame())
```
![HARDSHIP VS HOUSING](https://github.com/Emperorian/Public-Health-Significance-And-The-Hardship-Index-/assets/101293550/2e01d774-b78e-4459-b86e-70e49cf02196)


### *RESULTS AND FINDINGS*
The results of the analysis is summarised as follows
1. out of the 78 data samples presented, it clearly shows that the communities listed in the sample are poor below average
2. the maximum level of hardship index is 98.0 which is really while minimum is 1.0 and average 49.5
3. the average income of the sample stands at 25597.0 and about 28 community from this sample earn below this. RIVERDALE is the poorest of all
4. an avearage of 21.7 percent of the household live below the poverty line
5. 47 percentage of the of ages above 16 are unemployed
6. 49 out of 78 are living in a croweded housing enviroment
7. 35.7 percent are aged over 18 and 64, which means they are eligible to work or are too old to work hereby increasing the level of dependence
8. From the visualisations, The lower the income the higher the hardship.
9. lower income equals to poverty and more poverty equals to housing inaffordability leading to croweded housing
10. crowded housing leads to major public health problems. like airborne disease,infections and socioeconomic instabilty.


### RECOMMENDATIONS
.Poverty and hardship remines a major economic panademic that only proper fiscal planning can solve
.The government should come with insentives for allievates poverty
.For poeple who are unemployed and uneducated skill development programmes should be provided
.prices of housing shpuld be brought down by building more affordable housing unit or a deal should be reached  between the government and house owners/landlords
.For poeple especally children below 16 ages, free feeding at school and free tuition should be provide this will go along way to provide for their parent
.finally salary and minimum wages should be review to make earns match with the inflation.


### REFERENCES
- Chicago data portal
- The united states census bereau
- IBM data laboratory
- factfinder2.gov



