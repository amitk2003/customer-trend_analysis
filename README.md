# 📊 Customer Shopping Behavior Analysis

## 📌 Overview
This project analyzes customer shopping behavior to extract meaningful business insights using a complete end-to-end data analytics pipeline. It combines Python for data preprocessing, SQL for business analysis, and Power BI for visualization.

---

## 🚀 Tech Stack
- Python (Pandas, NumPy, matplotlib)
- PostgreSQL (pgAdmin)
- Power BI

---

## 🔄 Workflow

### 1️⃣ Data Cleaning & EDA (Python)
- Handled missing values and inconsistent formats  
- Converted column names to SQL-friendly format (snake_case)  
- Performed exploratory data analysis (EDA) to understand patterns  

---

### 2️⃣ Feature Engineering
- Created new features such as:
  - purchase_amount
  - Customer segmentation indicators  
- Prepared structured dataset for SQL analysis  

---

### 3️⃣ SQL Analysis (PostgreSQL)
Solved real-world business problems using SQL:

#### 🔹 Revenue by Gender (with % contribution)
SELECT gender,
       SUM(purchase_amount) AS revenue,
       ROUND(
           SUM(purchase_amount) * 100.0 /
           SUM(SUM(purchase_amount)) OVER (),
           2
       ) AS revenue_percentage
FROM customer_table
GROUP BY gender;

#### 🔹 High-Value Customers Using Discount
SELECT customer_id, purchase_amount
FROM customer_table
WHERE LOWER(discount_applied) = 'yes'
  AND purchase_amount >= (
      SELECT AVG(purchase_amount)
      FROM customer_table
  );
  ### what are the top 3 most purchased products within each category
with item_counts as(
select category, item_purchased, COUNT(customer_id) as total_orders,
ROW_NUMBER() over(partition by category order by COUNT(customer_id) DESC) as item_rank
from customer_table
group by category,item_purchased
);

select item_rank, item_purchased, total_orders
from item_counts
where item_rank<=3


### segment customers into new,returning and loyl based on their total number of previous purchases and show count of each segment
with customer_type as (
select customer_id, previous_purchases,
CASE 
    WHEN previous_purchases =1 THEN 'New'
	WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
	ELSE 'Loyal'
	END AS customer_segment
from customer_table
);
---

### 4️⃣ Data Visualization (Power BI)
- Built interactive dashboards to visualize:
  - Revenue trends  
  - Customer segmentation  
  - Discount impact analysis  

---

## 📊 Key Insights
- Revenue contribution varies significantly across genders  
- Discount usage does not always correlate with higher spending  
- A small group of customers contributes a large portion of revenue  
- Customer purchasing behavior varies across segments  

---



## 💡 Business Value
- Helps understand customer spending behavior  
- Identifies high-value customers  
- Evaluates effectiveness of discounts  
- Supports data-driven decision making  

---

## 🔥 Future Improvements
- Add predictive modeling (ML) for customer segmentation  
- Deploy dashboard using Streamlit  
- Automate ETL pipeline  

---

## 👨‍💻 Author
Amit Kumar  
GitHub: https://github.com/amitk2003  

---

## ⭐ If you like this project
Give it a ⭐ on GitHub!
