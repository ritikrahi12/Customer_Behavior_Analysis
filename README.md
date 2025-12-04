# Customer_Behavior_Analysis
Data Analytics Project
Customer Analytics Project — End-to-End (Python → MySQL → Power BI)

This project demonstrates a complete end-to-end data analytics workflow using Python (pandas) for EDA & preprocessing, MySQL for data storage & querying, and Power BI for dashboard reporting.

The goal is to analyze customer behavior, revenue patterns, discount usage, and product performance to generate actionable business insights.

Project Workflow Overview
1️⃣ Data Loading & Cleaning (Python)

Loaded the raw dataset using pandas.read_csv().

Performed initial inspection with:

df.info()

df.describe(include='all')

df.isnull().sum()

Standardized column names (lowercase + underscore formatting).

Renamed inconsistent fields (e.g., purchase_amount_(usd) → purchase_amount).

Handled missing values and cleaned inconsistencies as needed.

2️⃣ Exploratory Data Analysis (EDA)

Performed EDA to understand customer demographics, purchasing behavior, and product trends:

Checked dataset distribution and summary statistics.

Evaluated missing values, outliers, and abnormal patterns.

Explored relationships between age, gender, product category, discounts, and purchase amount.

Identified key trends for visualization and SQL analysis.

3️⃣ Feature Engineering

Created new, analysis-friendly features to improve segmentation:

Age Group Segmentation

df['age_group'] = pd.qcut(df['age'], q=4, labels=['Young Adult','Adult','Middle-aged','Senior'])


Purchase Frequency (Days)
Created a mapping from text to numeric frequency values:

frequency_mapping = {
    'Weekly': 7, 'Bi-Weekly': 14, 'Fortnightly': 14,
    'Monthly': 30, 'Every 3 Months': 90, 'Quarterly': 90,
    'Annually': 365
}
df['purchase_frequency_days'] = df['frequency_of_purchases'].map(frequency_mapping)


These engineered features helped with segmentation and dashboard insights.

 4️⃣ Loading Clean Data into MySQL

Used SQLAlchemy + PyMySQL to load cleaned data into a MySQL database.

engine = create_engine("mysql+pymysql://root:123456@localhost:3306/CUSTOMER")
df.to_sql("customers", engine, if_exists="replace", index=False)


Verified inserted records using:

pd.read_sql("SELECT * FROM customers LIMIT 5;", engine)

 5️⃣ SQL Analysis & KPI Generation

A set of optimized SQL queries were written to generate business KPIs:

Revenue by gender

Customers who used discount but spent above average

Top 5 products by review rating

Shipping type comparison

Subscriber vs non-subscriber spending

Top products by discount conversion

New vs Returning vs Loyal customer segmentation

Top 3 products per category (window functions)

Repeat buyer subscription likelihood

Age group revenue contribution

 6️⃣ Power BI Dashboard

Connected Power BI to MySQL and built interactive visualizations:

Dashboard Highlights

Revenue by gender, category, and age group

Top products by rating and sales

Discount impact analysis

Loyal vs new customer contribution

Subscription impact on revenue

Product performance by category

Review rating distribution

Data Refresh Automation

Configured ODBC connector + auto-refresh to ensure Power BI always pulls the latest MySQL data.

 7️⃣ Key Insights

Loyal customers (80%) contribute 78.28% of total revenue, showing high retention value.

Discount-based products showed noticeable uplift in sales volume.

Certain categories consistently performed well across all demographics.

Subscription customers had higher average purchase amounts than non-subscribers.

 8️⃣ Tools & Technologies Used
Purpose	Tools
Data Cleaning & EDA	Python, pandas
Feature Engineering	pandas, NumPy
Database	MySQL, SQLAlchemy, PyMySQL
Querying	SQL (CTEs, window functions, subqueries)
Visualization	Power BI
Automation	Python → MySQL → Power BI refresh
