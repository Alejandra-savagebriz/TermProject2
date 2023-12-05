# Term Project 2: Add title
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
  - [NoSQL data](#triggers-2)
  - [Cloud services and data](#testing)

# Overview
## Introduction
<p align="justify"> This report embarks on an extensive exploration of the interwoven realms of global economics, social landscapes, and educational landscapes, spanning the period from 2021 to 2023. Through the compilation and analysis of data from three diverse public sources, and using Data Engineering concepts, this project unveils a rich tapestry of insights, shedding light on the intricate interplay of socioeconomic factors that influence our world.

## Data Source 
<p align="justify"> This project draws its data from three distinct public sources, compiling an extensive array of economic, social, and educational indicators spanning from 2021 to 2023.

**_Dataset 1: Country Insights and GDP per Capita_**


<p align="justify">The primary dataset encompasses fundamental country-level details such as country codes, general characteristics, and the corresponding GDP per capita values for each nation. Uploaded into the **MongoDB instance**, this dataset lays the groundwork for subsequent data integration processes.

**_Dataset 2: World Bank API's GDP per Capita_**


Augmenting the economic dataset, GDP per capita information sourced from the **World Bank API** was seamlessly integrated into the MongoDB database. This step ensures data uniformity and precision in the GDP per capita figures.

**_Dataset 3: Socioeconomic Metrics - Education, Life Expectancy, Birth Rate, and Enrollments_**


Expanding the analytical horizon, the third dataset introduces additional socioeconomic markers, including education expenses, life expectancy, birth rates, and both primary and tertiary enrollment ratios. These crucial statistics were harmoniously integrated into the MongoDB database, completing the comprehensive data assembly. This dataset was retrieved from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/countries-of-the-world-2023) and later uploaded it with a public URL into **Amazon Web Services S3 storage buckkets** in order to access it directly from Knime without the need to do manual work.



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


  ## EER Diagram        

<p align="justify"><p align="justify"> The following Enhanced-Entity-Relationship Diagram (ERR) was created within MySQL Workbench, considering the distinctive attributes and interconnections inherent in each of the three datasets associated with World Bank available data. This diagram shows the primary keys, serving as unique identifiers for records within each dataset, and the consequential establishment of corresponding foreign keys that underpin pivotal connections and associations between the datasets.      

![image](https://github.com/Alejandra-savagebriz/TermProject2/assets/88064979/89bac56c-bfca-42e3-be6c-b95dd2d8ab73)


               
# Analytical Layer
## Data Warehouse
To create the analytical layer after loading all the tables from the Entity-Relationship Diagram (EER), it is essential to understand the primary keys in each table.This was crucial for determining the best way to link and join these tables efficiently enabling the extraction of valuable insights.


# ETL Pipeline Knime
After identifying the specific attributes and features necessary for the data warehouse, the start of data processing through the ETL (Extract, Transform, Load) procedure becomes a pivotal step. 


The **Extract** part consisted in extracting and joining data from the following source tables (orders, customers, order_items, products, category_name_t, seller, reviews, payments) based on common keys (customer_id, order_id, product_id, product_category_name, seller_id).

The **Transform** part consisted in the following:
  - `UPPER(TRIM(orders.order_status)) AS OrderStatus`: Converts the order status to uppercase and removes leading and trailing spaces.
  - `UPPER(TRIM(customers.customer_city)) AS City`: Converts the customer city to uppercase and removes leading and trailing spaces.
  - `ROUND(AVG(reviews.review_score), 2) AS AverageReviewScore`: Calculates the average review score from the 'reviews' table and rounds it to two decimal places.
  - `ROUND(SUM(order_items.price + order_items.freight_value), 2) AS TotalRevenue`: Calculates the total revenue by summing the price and freight value from the 'order_items' table and rounds the result to two decimal places.
  - `ROUND(AVG(order_items.price + order_items.freight_value), 2) AS AverageOrderValue`: Calculates the average order value by averaging the sum of price and freight value from the 'order_items' table and rounds the result to two decimal places.
  - `YEAR(orders.order_purchase_timestamp) AS OrderYear`: Transforms the date timestamp into years.
  - `MONTHNAME(orders.order_purchase_timestamp) AS OrderMonth`: Transforms the date timestamp into months and returns only the month name.
  - `UPPER(TRIM(payments.payment_type)) AS PaymentType`: Converts payment types to uppercase and removes leading and trailing spaces.

The **Load** part consisted in creating a new table _Supermarket_info_ and loading it with the result of the transformation.

To optimize the process and ensure repeatability, a stored procedure named **CreateSupermarket_info** was created, streamlining the formation of this filtered table (**Supermarket_info**) by extracting details from the array of datasets. This approach simplifies the procedure, enabling a more efficient conversion of unprocessed data into well-structured, insightful data within the MySQL database.  


# Nodes and components
The components and nodes used in the Knime workflow:

# Reproducibility

# Visualizations

# Conclusions


# Extras
## NoSQL data

## Cloud services and data
