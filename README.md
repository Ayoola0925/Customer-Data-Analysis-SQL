#### Customer Data Analysis SQL



### Table of Contents

- [Introduction and Objective](introduction-and-objective)


- [Customer Data Analysis](customer-data-analysis)
  
   - Query 1: How many unique customers are in the dataset?
    
     SQL Query
    
     Explanation

     Insight

  -  Query 2: What is the distribution of customers across different states?

    SQL Query
  
    Explanation
  
    Insight

-  Query 3: Which customers made the most orders?

    SQL Query

    Explanation

    Insight

-  Query 4: Identify the top 5 customers by revenue

     SQL Query

     Explanation

     Insight

-  Query 5: What is the average number of orders per customer?

    SQL Query

    Explanation

    Insight

-  Query 6: How many new customers were acquired in the last 12 months?

    SQL Query

    Explanation

    Insight



- [Tools Used](tools-used)

   SQL (MySQL)
  
   Database Management System (DBMS)

- [Challenges and Solutions](challenges-and-solutions)
  
   Handling Missing Customer Registration Dates
  
   Resolving Data Inconsistencies in Product Pricing

- [Conclusion and Business Recommendations](conclusion-andbusiness-recommendations)

   Key Insights from the Analysis

   Business Recommendations

- [Appendix (Sample Data Schema)](appendix-(sample-data-schema))

   Customers Table Sample Schema

   Orders Table Sample Schema


- [Final Words](final-words)

   Reflection on SQL Proficiency

   Value of Customer Data Analysis in Business


## Introduction and Objective
This portfolio focuses on customer data analysis using SQL queries to extract meaningful insights from multiple datasets: Customers, Orders, Products, Employees, and State data. Through this analysis, I aim to explore customer behavior, revenue generation, new customer acquisition, and more. Each SQL query is explained in detail, and relevant insights are provided for business use.

## Customer Data Analysis

# Query 1: How many unique customers are in the dataset?

This query calculates the total number of unique customers by counting distinct CustomerID.

sql
SELECT COUNT(DISTINCT CustomerID) AS unique_customers
FROM customers;

![Unique Customer](https://github.com/user-attachments/assets/05fa9b1d-d4e6-436c-9be0-970ac19c67e5)


Explanation:

DISTINCT ensures we only count each customer once, even if they appear multiple times.

Insight:
This helps the business understand the size of its customer base.

# Query 2: What is the distribution of customers across different states?

This query analyzes how customers are distributed across various states.

sql

SELECT State, COUNT(CustomerID) AS total_customers
FROM customers
GROUP BY State
ORDER BY total_customers DESC;

![Customer Across Various State](https://github.com/user-attachments/assets/8ec09667-0111-4264-90bf-f99a35ec56de)

Explanation:

The GROUP BY clause groups customers by state.

The ORDER BY DESC sorts states from highest to lowest number of customers.

Insight:

Identifying regions with the most customers can guide marketing strategies and resource allocation.

# Query 3: Which customers made the most orders?

This query identifies customers who have placed the highest number of orders.

sql

SELECT 
    c.CustomerID, 
    CONCAT(c.FirstName) AS CustomerName, 
    COUNT(o.OrderID) AS total_orders
FROM 
    customers c
JOIN 
    orders o ON c.CustomerID = o.CustomerID
GROUP BY 
    c.CustomerID, CustomerName
ORDER BY 
    total_orders DESC
LIMIT 10;


![Highest no of Order](https://github.com/user-attachments/assets/3b2d2d62-9a36-4d66-ae2c-d4e3573f83be)


Explanation:

We use an INNER JOIN to combine data from customers and orders.
GROUP BY ensures each customer’s total order count is aggregated.

Insight:

Knowing which customers order most frequently helps in building customer loyalty programs.


# Query 4: Identify the top 5 customers by revenue

This query identifies the most valuable customers based on the total revenue they generated.

sql

SELECT 
    c.CustomerID, 
    c.LastName AS CustomerName, 
    SUM(o.Quantity * p.Total_price) AS total_revenue
FROM 
    customers c
JOIN 
    orders o ON c.CustomerID = o.CustomerID
JOIN 
    products p ON o.ProductID = p.ProductID
GROUP BY 
    c.CustomerID, CustomerName
ORDER BY 
    total_revenue DESC
LIMIT 5;

![Valueable Customer](https://github.com/user-attachments/assets/02639c3c-799c-4c61-8eae-1a5d9e243ede)


Explanation:

This query joins the customers, orders, and products tables.

Revenue is calculated as Quantity * Total_price.

Insight:

Focusing on high-value customers can improve profit margins through personalized promotions.


# Query 5: What is the average number of orders per customer?

This query calculates the average order frequency across all customers.

sql

SELECT AVG(order_count) AS avg_orders_per_customer
FROM (
    SELECT 
        CustomerID, 
        COUNT(OrderID) AS order_count
    FROM 
        orders
    GROUP BY 
        CustomerID
) AS subquery;


![Average Order](https://github.com/user-attachments/assets/7c87d83e-a41f-4e0d-b6c7-4e75e2613da5)


Explanation:

The inner query counts orders per customer.

The outer query calculates the average of these counts.

Insight:
Understanding order frequency helps set realistic sales targets.


# Query 6: How many new customers were acquired in the last 12 months?

This query identifies new customers who registered within the past year.

sql

SELECT 
    COUNT(CustomerID) AS new_customers
FROM 
    customers
WHERE 
    RegistrationDate >= DATE_SUB(CURDATE(), INTERVAL 1 YEAR);

![Customer within the past year](https://github.com/user-attachments/assets/a839ed43-baad-4978-bf1e-5c066d55406d)

    
Explanation:

DATE_SUB() subtracts one year from the current date (CURDATE()), and only customers registered after that date are counted.

Insight:

This metric helps monitor the effectiveness of customer acquisition campaigns.

## Tools Used

- SQL (MySQL): For querying the datasets.

- Database Management System (DBMS): For managing and connecting datasets.

## Challenges and Solutions

- Challenge: Missing customer registration dates for some records.

Solution: Used the first order date as a proxy for registration.

- Challenge: Data inconsistencies in product pricing.

Solution: Verified pricing with product management teams and corrected entries.

## Conclusion and Business Recommendations

The customer data analysis revealed several valuable insights:

- Top customers contribute the most revenue, and maintaining relationships with them should be a priority.

- Target regions with the highest customer concentration for new marketing campaigns.

- Monitor new customer acquisition trends to adjust promotional efforts.

- Future analysis could focus on customer churn prediction and product bundle recommendations using basket analysis.

## Appendix (Sample Data Schema)

- Customers Table:
CustomerID	FirstName	LastName	Email	State	RegistrationDate

- Orders Table:
OrderID	CustomerID	ProductID	Quantity	OrderDate


## Final Words

This portfolio demonstrates my SQL proficiency in customer data analysis. By using SQL queries effectively, I extracted meaningful insights that can drive business decisions and improve profitability. I am confident that this experience will add value to my future data analysis roles
