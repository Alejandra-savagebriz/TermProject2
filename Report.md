# Term Project 2 Intersections of Global Progress: Unveiling Socioeconomic Trends
Data Engineering 1  
Central European University  
Team 2: Alejandra Savage, Jesús Eduardo Ibarra, Yahya Kocakale, Zunaira Pusha

## Table of Contents
- [Overview](#overview)
  - [Data Sources](#data-source)
    - [Data Schema](#data-schema)
  - [Analytics Plan](#analytics-plan)
- [Operational layer](#operational-layer)
  - [Architecture](#architecture)
  - [EER Diagram](#eer-diagram)
- [Analytical Layer](#analytical-layer)
  - [Datawarehouse](#datawarehouse)
- [ETL Pipeline Knime](#etl-pipeline)
  - [Nodes and components](#events-and-stored-procedures)
- [Visualizations](#datamarts)
- [Reproducibility](#reproducibility)
- [Conclusions](#conclusions)
- [Extras](#extras)


# Overview
## Introduction
<p align="justify"> This report embarks on an extensive exploration of the interwoven realms of global economics, social landscapes, and educational landscapes, spanning the period from 2021 to 2023. Through the compilation and analysis of data from three diverse public sources, and using Data Engineering concepts, this project unveils a rich tapestry of insights, shedding light on the intricate interplay of socioeconomic factors that influence our world.

## Data Source 
<p align="justify"> This project draws its data from three distinct public sources, compiling an extensive array of economic, social, and educational indicators spanning from 2021 to 2023.

**_Dataset 1: Country Insights and GDP per Capita_**

The primary dataset serves as a comprehensive reference table, encompassing fundamental country-level details, including country codes, ids, region ids, capital cities, income levels, and essential governmental characteristics. This foundational information lays the groundwork for subsequent data integration processes, providing a robust framework for analysis.

Augmenting the economic dataset, GDP per capita information sourced from the **World Bank API** was seamlessly integrated into the MongoDB database. This step ensures data uniformity and precision in the GDP per capita figures.

**_Dataset 2: World Bank data GDP per Capita_**
GDP per capita information, along with government education expenditures as shares of GDP by country, meticulously sourced from the **World Bank database**, has been seamlessly integrated and stored in the **MongoDB Atlas** database. This strategic step ensures not only data uniformity but also precision in capturing and retaining crucial economic indicators for in-depth analysis and future insights.


**_Dataset 3: Socioeconomic Metrics - Education, Life Expectancy, Birth Rate, and Enrollments_**


Expanding the analytical horizon, the third dataset introduces additional socioeconomic markers, including education expenses, life expectancy, birth rates, and both primary and tertiary enrollment ratios. These crucial statistics were harmoniously integrated into the MongoDB database, completing the comprehensive data assembly. This dataset was retrieved from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/countries-of-the-world-2023) and later uploaded it with a public URL into **Amazon Web Services S3 storage buckets** in order to access it directly from Knime without the need to do manual work.



<p align="justify"> By joining these diverse datasets, the project established an exhaustive repository of economic, social, and educational indicators, empowering thorough analysis and exploration of global trends. Leveraging the MongoDB NoSQL database, the Amazon Web services bucket storage, and the API queries provided not only scalability but also flexibility in managing data, enabling seamless access and manipulation throughout the project lifecycle.

## Analytics Plan
<p align="justify"> By harmonizing these diverse datasets, the project establishes an exhaustive repository of indicators. The subsequent visualizations provide critical insights:

* _Education Spending Priorities of Top 10 Richest Nations_: Linked to GDP per capita, showcasing fiscal priorities in education across affluent nations.
Correlation between Education, Unemployment Rate, and GDP per Capita: Highlighting the interplay among these crucial socio-economic factors.

* _GDP per Capita vs. Education Scatterplot_: Exploring the relationship between economic prosperity and education.

* _Life Expectancy and Birth Rate Bar Chart_: Illustrating population health indicators across nations.

* _Bubble Chart for Unemployment Rate, Education Expenses, and GDPPC_: Providing a multi-dimensional view of socio-economic metrics.

* _Top 10 Countries with Highest GDPPC vs. Birth Rate and Life Expectancy_: A comparative analysis showcasing the correlation between economic status and vital societal indicators.

# Operational Layer
## Architecture

This is the architecture followed for creating the Operational layer:
![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/894d94b6-bf30-458e-9ded-38fabdf8b83d)



  ## EER Diagram        

<p align="justify"> The following Enhanced-Entity-Relationship Diagram (ERR) was created within MySQL Workbench, considering the distinctive attributes and interconnections inherent in each of the three datasets associated with World Bank available data. This diagram shows the primary keys, serving as unique identifiers for records within each dataset, and the consequential establishment of corresponding foreign keys that underpin pivotal connections and associations between the datasets.      

![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/89bac56c-bfca-42e3-be6c-b95dd2d8ab73)

# Analytical Layer
## Datawarehouse
To create the analytical layer after loading all the tables from the Entity-Relationship Diagram (EER), it is essential to understand the primary keys within each table. This was crucial for determining the best way to link and join these tables efficiently enabling the extraction of valuable insights.

![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/f03376ab-9723-45e0-a1f2-754f97ebd0e3)



# ETL Pipeline Knime
After identifying the specific attributes and features necessary for the data warehouse, the start of data processing through the ETL (Extract, Transform, Load) procedure becomes a pivotal step. The Knime ETL workflow:
![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/dc455bb3-1efc-44af-b9e4-50b062446733)

## Extract
The **Extract** part consisted in extracting and joining data from the 3 source tables (AWS dataset, MongoDB dataset, and World Bank data).
![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/0e74e57b-570f-410b-b6ae-a07efd5f3dbe)

## Transform
The **Transform** part consisted in renaming columns, replacing missing values, rounding values, filtering columns, and modifying special characters in the data:
![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/063a001f-691f-429c-9b01-d59b4094123c)

## Load
The **Load** part consisted in joining the three datasets in order to have a final table with the different data in order to proceed with the analytics plan by doing the datamarts and visualizations:
![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/7bb12de0-6f35-4af3-b7af-2b4fd85c1b88)

## Nodes and components
<p align="justify">The components and nodes used in the Knime workflow:

- **EXTRACT**: GET Request, JSON Path, MongoDB Connector, MongoDB Aggregation, File Reader
- **TRANSFORM**: Ungroup, Column Renamer, JSON to Table, Row Filter, Column, Filter, String Manipulation (Multi Column), Round Double, Double to Integer, Top k       Row Filter
- **LOAD**: Joiner, Pivot
- **VIEWS**: Pie Chart, Scatter Plot (Plotly), Bar Char, Bubble Char (Plotly), Line Plot

# Visualizations
<p align="justify">The datamarts and visualizations stated in the Analytics plan had the following results:

* _Education Spending Priorities of Top 10 Richest Nations_:
  ![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/c5266aad-f987-4181-8ac3-73e4aa70b7a0)

Some insights from the pie chart:

* The Nordic countries (Iceland, Denmark, Sweden, and Norway) spend a lot on education. This is consistent with their strong social welfare systems and focus on human capital development.
  
* The Netherlands, Australia, Luxembourg, and Switzerland all spend more than 5% of their GDP on education. This shows that even high-income countries recognize the importance of investing in education.

* _GDP per Capita vs. Education Scatterplot_:
  ![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/7aaead80-52b7-4f56-8d31-12eeaa70483e)

<p align="justify"> The scatterplot shows a positive correlation between the two variables, meaning that countries with higher GDP per capita tend to spend more on education as a percentage of GDP. It also shows some variation in education spending as a percentage of GDP among the top 10 richest nations. 

<p align="justify"> The graph also shows that it is possible to achieve high levels of economic development without spending the highest possible percentage of GDP on education. For example, Switzerland has one of the highest GDP per capita in the world, but it spends less on education as a percentage of GDP than some other high-income countries. This suggests that it is important to spend wisely on education, rather than simply spending more money.

<p align="justify"> Overall, the graph suggests that there is a strong link between economic development and education spending. Countries with higher GDP per capita tend to spend more on education as a percentage of GDP. This is likely due to a number of factors, including the ability to afford to spend more on education, the demand for education, and the need for a highly educated workforce in knowledge-based economies.


* _Life Expectancy and Birth Rate Bar Chart_: Illustrating population health indicators across nations.
  ![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/959cc462-0b97-41bb-8373-10b96d9557e7)



<p align="justify">The graph shows a negative correlation between the two variables, meaning that countries with higher life expectancies tend to have lower birth rates. For example, Iceland has a birth rate of 11.5 births per 1,000 people, while Singapore has a birth rate of just 8.6 births per 1,000 people. This variation is likely due to a number of factors, such as cultural differences, government policies, and the availability of childcare.

<p align="justify">Overall, the graph suggests that there is a link between economic development and birth rates. Countries with higher life expectancies tend to have lower birth rates. This is likely due to a number of factors, including the later childbearing, higher education levels, and rising cost of living.


* _Bubble Chart for Unemployment Rate, Education Expenses, and GDPPC_: Providing a multi-dimensional view of socio-economic metrics.
  ![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/5be1293a-e6f3-4523-af51-8909b3996ad7)

<p align="justify">The graph shows a positive correlation between the two variables, meaning that countries with higher GDP per capita tend to have higher unemployment rates. 


* _Top 10 Countries with Highest GDPPC vs. Birth Rate and Life Expectancy_: A comparative analysis showcasing the correlation between economic status and vital societal indicators.
  ![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/dc889e96-ae6c-4e09-ac6e-38f25b533f17)

<p align="justify">The chart shows a clear positive correlation between GDP per capita and life expectancy, and a negative correlation between GDP per capita and birth rate. This is consistent with the findings of other studies, which have shown that countries with higher GDP per capita tend to have lower birth rates and higher life expectancies. It is important to note that the correlations shown in the chart do not necessarily mean that GDP per capita directly causes changes in birth rates and life expectancy. There are many other factors that can influence these variables, such as cultural norms, government policies, and environmental conditions.

<p align="justify">Overall, the chart provides a useful snapshot of the relationship between GDP per capita, birth rate, and life expectancy in the top 10 richest countries in the world. It suggests that economic development is associated with a number of positive outcomes, including better health and well-being.

# Reproducibility
The Knime workflow has been tested in multiple computers in order to be easy to execute without the need of passwords or connections to a local instance.


# Conclusions
<p align="justify">Overall, the chart provides a useful snapshot of the relationship between GDP per capita, birth rate, and life expectancy in the top 10 richest countries in the world. It suggests that economic development is associated with a number of positive outcomes, including better health and well-being.
This project has helped to show the intricate relationships between education, economic prosperity, and demographic trends. It has demonstrated the importance of education as a driving force for socioeconomic development and highlighted the interconnectedness of various socioeconomic factors. 

<p align="justify">Overall, the chart provides a useful snapshot of the relationship between GDP per capita, birth rate, and life expectancy in the top 10 richest countries in the world. It suggests that economic development is associated with a number of positive outcomes, including better health and well-being.
From the foundational dataset encompassing country-level details to the integration of World Bank API's GDP per capita figures and the addition of crucial socioeconomic metrics, the project established a comprehensive repository. Visualizations elucidated critical correlations, highlighting the relationship between economic prosperity, education spending, health indicators, and birth rates. 

These discoveries highlight how important it is to invest smartly in education, health, and social and economic policies. It's about taking a broad approach to support strong and long-lasting global progress. This project proves how using Data Engineering can help us understand complicated social issues. It gives us valuable insights that we need to make smart decisions and create policies that will lead to a fairer and more successful world for everyone.



# Extras
In order to enhance the project, the following extras were considered:
- Usage of NoSQL database: MongoDB data
- Usage of cloud instead of local servers: AWS S3 data
- Creation of visualizations using the Plotly Knime extension

