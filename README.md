
# BikeStores Sales Analysis & Executive Dashboard

This project features a comprehensive data analytics workflow, transforming raw relational data from a **SQL Server** database into actionable insights using **Excel** and **Tableau**.

##  Project Overview
Using the "BikeStores" sample database, I tracked key performance indicators (KPIs) to help stakeholders understand revenue drivers. The project covers data extraction, cleaning, multi-dimensional analysis, and final dashboard reporting.

### Tech Stack
* **SQL Server (T-SQL):** Data extraction and multi-table joins.
* **Excel:** Data cleaning, Pivot Table analysis, and initial prototyping.
* **Tableau:** Interactive data storytelling and executive-level visualization.

---

## 🛠️ Phase 1: Data Extraction (SQL)
To create a unified dataset for analysis, I wrote a complex SQL query to join sales, production, and staff data. This consolidated view allows for analysis by customer location, product category, and even individual sales representatives.

**The SQL Query:**
```sql
SELECT
	ord.order_id,
	CONCAT(cus.first_name, ' ', cus.last_name) AS 'customers',
	cus.city,
	cus.state,
	ord.order_date,
	SUM(ite.quantity) AS 'total_units',
	SUM(ite.quantity * ite.list_price) AS 'revenue',
	pro.product_name,
	cat.category_name,
	sto.store_name,
	CONCAT(sta.first_name, ' ', sta.last_name) AS 'sales_rep'

FROM sales.orders ord
JOIN sales.customers cus
ON ord.customer_id = cus.customer_id
JOIN sales.order_items ite
ON ord.order_id = ite.order_id
JOIN production.products pro
ON ite.product_id = pro.product_id
JOIN production.categories cat
ON pro.category_id = cat.category_id
JOIN sales.stores sto
ON ord.store_id = sto.store_id
JOIN sales.staffs sta
ON ord.staff_id = sta.staff_id

GROUP BY 
	ord.order_id,
	CONCAT(cus.first_name, ' ', cus.last_name),
	cus.city,
	cus.state,
	ord.order_date,
	pro.product_name,
	cat.category_name,
	sto.store_name,
	CONCAT(sta.first_name, ' ', sta.last_name)
```

---
## Phase 2: Excel Pivot & Analysis

The extracted data was imported into Excel for deep-dive analysis.
- Data Consolidation: Added missing brand names and cleaned date formats to ensure accurate time-series analysis.
- Pivot Analysis: Created summaries for Revenue per State, Year, and Store to identify top-performing regions.
- Dynamic Filtering: Implemented Slicers to allow users to toggle between different years and regions instantly.

---

## Phase 3: Tableau Executive Dashboard

The final interactive dashboard provides a high-level summary of the business health.
Key Features:
- Revenue Map: Geographic breakdown of sales across NY, CA, and TX.
- Trend Lines: Comparison of monthly revenue growth across 2016, 2017, and 2018.
- Executive Metrics: "Big Angry Numbers" for Total Revenue, Total Units, and Unique Customer counts.

---

## Repository Contents
- Book1.xlsx: Contains the raw data, Pivot Tables, and the Excel dashboard.
- Dashboard 1.jpg: A screenshot of the final Tableau visualization.
