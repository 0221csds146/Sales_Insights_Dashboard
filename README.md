# Atliq Hardware Sales Data Analysis(Interactive Dashboard creation using PowerBi)
This Power BI Dashboard is a comprehensive business intelligence project that transforms raw sales data into meaningful and interactive visual insights. It enables businesses to track performance, identify trends, and make data-driven decisions with confidence.

# Dataset used
<a href="https://github.com/0221csds146/Sales_Insights_Dashboard/blob/main/db_dump_version_2.sql">Dataset</a>

# 📊 Key Features
- Market-wise Profit Analysis: Identify high and low-performing cities based on profit margin.
-	Time-Series Trends: Track revenue and profit changes from 2017 to 2020.
-	Regional Contribution: View revenue and profit contribution by market.
-	Customer Insights: Analyze revenue and profitability by customer.

# 🛠️ Tools and Technologies Used
-	Power BI – For data visualization and dashboard development.
-	MySQL – For data cleaning, preprocessing, and analytical queries.
-	Power Query – For data transformation.

# Process
-	Data Collection: Gathered raw sales data from structured sources (sql files).
-	Data Analysis & Cleaning: Using MYSQL, Identified and addressed data quality issues to prepare it for transformation.
-	Data Modelling (Power BI): Created a star schema by defining relationships between fact and dimension tables to support efficient querying and reporting.
-	ETL Process :Used Power BI’s Power Query Editor to perform Extract, Transform, Load (ETL) operations including filtering, merging, and shaping data for visualization.
-	Dashboard Development (Power BI):Designed an interactive and visually engaging dashboard.Including KPIs, slicers, charts, and graphs for deep insights into revenue, profit, and customer behavior.

# Data Analysis using MySQL :
Completed the Data discovery and then used mySQL for data analysis.
The import of data is done from an already existing MySQL file. This file has to be loaded into MySQL workbench for further data analysis.
Analysis of data by looking into different tables and reflecting garbage values

We can see that garbage value that the table market cantains certain values which are incorrect.

SELECT * FROM sales.market;

And then we can check that transacation table we can see that ceratin negative value in amount which is not possible. and we can see that certain transactions are in USD. Hence, filtration of that is also needed by converting into INR.

SELECT * FROM sales.transactions;

Analysis of different SQL statement on data base

1.To find of all customers records

SELECT * FROM sales.customers;

2.To find total number of customers

SELECT count(*) From sales.customers;

3.To find transactions for Chennai market (market code for chennai is Mark001

SELECT * FROM sales.transactions where market_code='Mark001';

4.To find distrinct product codes that were sold in chennai

SELECT distinct product_code FROM sales.transactions where market_code='Mark001';

5.To find transactions for Chennai market (market code for chennai is Mark002

SELECT * FROM sales.transactions where market_code='Mark002';

6.To find distrinct product codes that were sold in mumbai

SELECT distinct product_code FROM sales.transactions where market_code='Mark002';

7.To find transactions where currency is US dollars

SELECT * from sales.transactions where currency="USD";

8.To find transactions in 2020 join by date table

SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;

8.To find transactions in 2019 join by date table

SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019;

9.To find total revenue in year 2020,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";

10.To find total revenue in year 2019,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";

11.To find total revenue in year 2020, January Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

12.To find total revenue in year 2020, February Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

13.To find total revenue in year 2019, January Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

14.To find total revenue in year 2019, February Month,

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");

15.To find total revenue in year 2020 in Chennai

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";

16.To find total revenue in year 2020 in Mumbai

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark002";

Similarly, if we want different of any other particular city the market code of that city is used on the mysql workbench.

# Data Analysis (DAX):
Measures used in all visualization are:

Key Measures:

Profit Margin % = DIVIDE([Total Profit Margin],[Revenue],0)
Profit Margin Contribution % = DIVIDE([Total Profit Margin],CALCULATE([Total Profit Margin],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))
Revenue = SUM('sales transactions'[sales_amount])
Revenue Contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))
Revenue LY = CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))
sales quntity = SUM('sales transactions'[sales_qty])
Total Profit Margin = SUM('Sales transactions'[Profit_Margin])
Profit Target:

Profit Target1 = GENERATESERIES(-0.05, 0.15, 0.01)
Profit Target Value = SELECTEDVALUE('Profit Target1'[Profit Target])
Target Diff = [Profit Margin %]-'Profit Target1'[Profit Target Value]

# PowerBi Dashboard
<a href="https://github.com/0221csds146/Sales_Insights_Dashboard/blob/main/Project1.pbix">View Dashboard</a>

# 💡 Key Insights
-	Overall Performance Metrics: ₹960M total revenue, 2M sales quantity, ₹24.66M profit margin.
-	Delhi NCR & Mumbai dominate sales and profit contribution (over 70% combined).
-	Revenue showed consistent growth from 2017 to 2019, followed by a decline in 2020 — possibly due to market or external factors.
-	Excel Stores and Info Stores are top revenue contributors, though some high-revenue customers generate low profits.
-	Bengaluru and Kanpur report negative profit margins, indicating underperformance.
-	Low-contributing markets like Patna, Surat, and Bhubaneswar present opportunities for targeted growth.
-	Overall profit margin is modest (2.57%), suggesting a need for pricing or cost strategy review.



