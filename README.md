# Samsung-Sales-Analysis-using-SQL

## Project Overview

**Project Title**: Samsung Mobiles sales overview  
**DBMS used**: MySQL
**Database**: `Mobile_sales`

This project demonstrates the application of SQL skills to explore and analyze retail sales data of Samsung mobile devices. The goal is to set up a structured retail sales database, perform exploratory data analysis (EDA), and derive insights from the sales data to answer specific business questions. 

## Objectives

1. **Set up a retail sales database**: Create and populate a database with the provided sales data.
2. **Exploratory Data Analysis (EDA)**: Conduct basic exploratory analysis to understand the dataset.
4. **Business Analysis**: Employ SQL queries to answer key business questions and extract actionable insights.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `Mobile_sales`.
- **Table Creation**: A table named `data` is created to store the sales data. The table structure includes columns for Year, Quarter, Product Model,	5G Capability,	Units Sold,	Revenue ($),	Market Share (%),	Regional 5G Coverage (%),	5G Subscribers (millions),	Avg 5G Speed (Mbps),	Preference for 5G (%), and Region

```sql
CREATE DATABASE Mobile_sales;

CREATE TABLE data
(
    Year INT,
    Quarter INT,
    Product Model VARCHAR(255),
    5G Capability BOOLEAN,
    Units Sold INT,
    Revenue ($) DECIMAL(10,2),
    Market Share (%) DECIMAL(5,2),
    Regional 5G Coverage (%) DECIMAL(5,2),
    5G Subscribers (millions) DECIMAL(10,2),
    Avg 5G Speed (Mbps) DECIMAL(10,2),
    Preference for 5G (%) DECIMAL(5,2),
    Region VARCHAR(255)
);
```

### 2. Data Exploration

- **Record Count**: Determine the total number of records in the dataset.
- **Product Count**: Find out how many unique Product Models are in the dataset.
- **Model Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
-- Record Count
SELECT * FROM data;
SELECT COUNT(*) FROM data; 

-- Name of product model
SELECT DISTINCT `Product Model` FROM data ORDER BY `Product Model`;

-- Count unique product models
SELECT COUNT(DISTINCT `Product Model`)
FROM data
ORDER BY `Product Model`;

```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Write a SQL query to retrieve all sales for specific models**:
```sql
SELECT * FROM data WHERE `Product Model` = 'Galaxy A14 5G'; -- 1
SELECT * FROM data WHERE `Product Model` = 'Galaxy Note10'; -- 2 
SELECT * FROM data WHERE `Product Model` = 'Galaxy S10'; -- 3 
SELECT * FROM data WHERE `Product Model` = 'Galaxy S20'; -- 4
SELECT * FROM data WHERE `Product Model` = 'Galaxy S22 5G'; -- 5
SELECT * FROM data WHERE `Product Model` = 'Galaxy Z Flip3 5G'; -- 6
SELECT * FROM data WHERE `Product Model` = 'Galaxy A14 5G'; -- 7
SELECT * FROM data WHERE `Product Model` = 'Galaxy A32 5G'; -- 8
SELECT * FROM data WHERE `Product Model` = 'Galaxy A52 5G'; -- 9
SELECT * FROM data WHERE `Product Model` = 'Galaxy Note20'; -- 10
SELECT * FROM data WHERE `Product Model` = 'Galaxy S21'; -- 11
SELECT * FROM data WHERE `Product Model` = 'Galaxy Z Fold2 5G'; -- 12
SELECT * FROM data WHERE `Product Model` = 'Galaxy Z Fold3 5G'; -- 13
SELECT * FROM data WHERE `Product Model` = 'Galaxy S23'; -- 14
SELECT * FROM data WHERE `Product Model` = 'Galaxy Z Flip5 5G'; -- 15
```

2. **Write a SQL query to retrieve all Sales of models (Based on year)**:
```sql
SELECT `Product Model`,
		`ï»¿Year` as Year,
		SUM(`Units Sold`) as Units_sold
FROM data
GROUP BY `Product Model`, `Year`;
```

3. **Write a SQL query to calculate the total sales per model.**:
```sql
SELECT `Product Model`,
		SUM(`Units Sold`) as Units_sold
FROM data
GROUP BY `Product Model`;
```

4. **Write a SQL query to find the number of models with and without 5G capability.**:
```sql
-- Product with 5G capability
SELECT DISTINCT `Product Model`,
				`ï»¿Year` as Year
FROM data
WHERE `5G Capability` = 'Yes';

-- Number
SELECT COUNT(DISTINCT `Product Model`) FROM data WHERE `5G Capability` = 'Yes';

-- Without 5G capability
SELECT DISTINCT `Product Model`,
				`ï»¿Year` as Year
FROM data
WHERE `5G Capability` = 'No';

-- Count 
SELECT COUNT(DISTINCT `Product Model`) FROM data WHERE `5G Capability` = 'No';
```
5. **Write a SQL query to find the number of best selling model in each year.**:
```sql
SELECT 
		Year,
        `Product Model`,
        sales
FROM 
(
	SELECT
		`ï»¿Year` as Year,
        `Product Model`,
        SUM(`Units Sold`) as sales,
        RANK() OVER(PARTITION BY `ï»¿Year` ORDER BY(SUM(`Units Sold`)) DESC) as Rank_sale
	FROM data
    GROUP BY Year, `Product Model`
) as Rk
WHERE Rank_sale = 1;
```

## Findings

- **Product Diversity**: Significant variation in product models and options over the years.
- **5G Adoption**: Gradual increase in 5G capable devices, reflecting market demand and technological advancement.
- **Sales Trends**: Identification of peak sales periods and best-selling models provides insights into consumer preferences and effective marketing strategies.

## Reports

- **Detailed Sales Report**: A comprehensive overview of sales figures, trends, and model performance.
- **Market Analysis**: Insights into market dynamics, 5G adoption, and consumer preferences.
- **trategic Recommendations**: Based on analysis, suggesting areas for increased focus or potential adjustments in marketing strategies.

## Conclusion

The project successfully applies SQL to analyze retail sales data, providing a deep dive into Samsung's mobile sales performance. The insights derived can assist in strategic decision-making and future planning for Samsung’s retail and product development strategies.

