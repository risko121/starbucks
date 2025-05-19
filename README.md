# ☕ Starbucks Data Cleaning & Processing Project

A real-world SQL project that focuses on cleaning, processing, and analyzing Starbucks data using **PostgreSQL**. This project simulates common issues in real datasets—such as missing values, inconsistent formatting, and redundant records—and walks through practical solutions.

---

## 📌 Project Objectives

- Perform **Phase 1: Data Cleaning** in PostgreSQL
- Execute **Phase 2: Data Processing & Preparation**
- Prepare the cleaned dataset for downstream analytics tools (Power BI, Tableau)

---

## 📁 Dataset

- Starbucks sales data
- Columns include: `store_id`, `store_type`, `city`, `country`, `open_date`, `sale_id`, `sales_amount`, etc.
- Simulates issues like:
  - Null and duplicate values
  - Inconsistent text formats
  - Mixed data types

> _Note: Dataset has been created to resemble real-world problems in the FMCG sector._

---

## Phase 1: Data Cleaning Tasks

- ✅ Remove duplicate rows from tables
- ✅ Handle `NULL` values in key columns
- ✅ Normalize `city` and `country` values (trim spaces, capitalize)
- ✅ Convert data types (e.g., latitude/longitude to `NUMERIC`, dates to `TIMESTAMP`)
- ✅ Filter out unrealistic or corrupt entries (e.g., negative sales)

Example:
sql
-- Removing duplicates
DELETE FROM stores
WHERE ctid NOT IN (
  SELECT MIN(ctid)
  FROM stores
  GROUP BY store_id
); 

## Phase 2: Data Processing Tasks
🔁 Join sales and stores tables

📊 Calculate sales KPIs like:

Total sales by country/store

Weekly sales trends

Top 5 cities by revenue

Example:
sql
-- Creating a clean view of store sales
CREATE VIEW store_sales_summary AS
SELECT s.store_id, s.city, s.country, st.store_type, SUM(sl.sales_amount) AS total_sales
FROM stores s
JOIN sales sl ON s.store_id = sl.store_id
JOIN store_types st ON s.store_type = st.store_type_id
GROUP BY s.store_id, s.city, s.country, st.store_type;
