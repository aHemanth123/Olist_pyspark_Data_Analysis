# 🛒 E-Commerce Transaction Analysis with PySpark (Olist Dataset)

## 📌 Project Summary

This project performs end-to-end **data engineering** and **data analysis** using the **Brazilian E-Commerce Olist dataset** (from Kaggle). Implemented entirely in **PySpark on Databricks**, it covers data cleaning, enrichment, analytical modeling, and customer insights such as **CLV**, **top products**, **funnel drop-off**, and more.


 
## 📂 Datasets Used

This project uses all **9 CSV files** from the [Olist Kaggle dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce):

1. `olist_orders_dataset.csv`
2. `olist_order_items_dataset.csv`
3. `olist_customers_dataset.csv`
4. `olist_sellers_dataset.csv`
5. `olist_products_dataset.csv`
6. `product_category_name_translation.csv`
7. `olist_order_payments_dataset.csv`
8. `olist_order_reviews_dataset.csv`
9. `olist_geolocation_dataset.csv`

 

## ✅ Project Steps Overview

### 🧱 1. Data Loading & Joining

- Read all datasets from `dbfs:/FileStore/tables/`
- Join datasets into a unified wide DataFrame using appropriate join keys:
  - `order_id`, `product_id`, `customer_id`, `seller_id`
- Used `inner`, `left`, and `outer` joins depending on context

 

### 🧹 2. Data Cleaning

- Removed duplicates based on key fields
- Handled null values:
  - Dropped rows with nulls in critical columns
  - Filled optional values with `0`, `"Unknown"`, or column averages
- Converted and formatted timestamp and numeric fields for consistency

 

### 🔍 3. Exploratory Data Analysis (EDA)

#### 📊 Top Selling Products per Region

- Grouped by `customer_state` and `product_category_name_english`
- Aggregated `units_sold` and `total_revenue`
- Used window function (`row_number()`) to rank top 5 per region

#### 💸 Customer Lifetime Value (CLV)

- CLV = Total revenue per customer / active days
- Grouped by `customer_unique_id` using `sum()`, `count()`, and `datediff()`

#### 🔻 Purchase Funnel Drop-Off

- Stages: Order placed → Delivered → Reviewed
- Counted unique orders at each stage
- Calculated drop-off percentages

#### 🐢 Delivery Delay Analysis

- Compared estimated vs actual delivery dates
- Identified and ranked delayed orders

#### 💰 Revenue Breakdown

- Seller and product-level revenue analysis
- Aggregated by state and seller_id



---

## 💻 Environment & Tools

| Tool          | Purpose                              |
|---------------|---------------------------------------|
| **Databricks**| Scalable Spark execution & notebooks  |
| **PySpark**   | All transformations & analysis        |
| **DBFS**      | File storage (`/FileStore/tables`)    |
| **Kaggle**    | Public source of raw data             |
 

## 📈 Future Work

- Churn prediction using PySpark MLlib
- Create Databricks dashboards
- Schedule ETL pipelines with Databricks Jobs
- Export data for downstream ML/BI systems.
- 

---
