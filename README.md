# 🛍️ E-Commerce Sales Pipeline using Databricks (Lakehouse Architecture)

## 🔍 Project Overview

This project simulates a production-grade data engineering pipeline for a fictional e-commerce company. The goal is to build a scalable and optimized sales analytics platform using the **Databricks Lakehouse architecture**, transforming raw transactional data into business-ready insights.

---

## 🧾 Dataset

- **Source**: [Online Retail II – UCI](https://www.kaggle.com/datasets/carrie1/ecommerce-data/data)
- **Timeframe**: December 1, 2010 to December 9, 2011
- **Description**: Contains invoice-level sales data for a UK-based online gift retailer, including customer, product, and transaction details.

---

## 🧱 Architecture

| Layer   | Purpose                                     | Technology                |
|---------|---------------------------------------------|---------------------------|
| Bronze  | Raw data ingestion with metadata            | Databricks Delta Lake     |
| Silver  | Cleaned, transformed, enriched data         | PySpark, Delta Lake       |
| Gold    | Aggregated, business-ready summary tables   | Delta Lake                |
| Visuals | Interactive dashboards for insights         | Databricks SQL Dashboard  |

---

## ⚙️ Pipeline Flow

1. **Ingestion (Bronze Layer)**  
   - Read raw `.csv` data from `/FileStore/tables/`
   - Add `ingest_time` and `source_file` metadata
   - Save as Delta table: `retail_demo.bronze_sales`

2. **Transformation (Silver Layer)**  
   - Drop duplicates and nulls
   - Rename columns for consistency
   - Add derived features: `invoice_ts`, `hour`, `weekday`, `total_sales`, etc.
   - Save as Delta table: `retail_demo.silver_sales`

3. **Aggregation (Gold Layer)**  
   Created 5 Gold tables for analytics:
   - `retail_demo.gold_sales`: Daily sales by country  
   - `retail_demo.gold_sales_by_product`: Product-wise revenue  
   - `retail_demo.gold_sales_by_customer`: Total spend per customer  
   - `retail_demo.gold_hourly_sales`: Hourly trend  
   - `retail_demo.gold_weekly_sales`: Weekly summary by country  

4. **Dashboard**  
- 📈 **Line & Area Charts** – for daily, monthly, and weekly sales trends
- 📊 **Bar & Pie Charts** – for country comparisons and product performance
- 🧮 **Histograms** – to visualize customer spend distribution
- 🔥 **Line Charts** – for hourly sales activity 

---

## 📊 Dashboard Components

| Chart Title                            | Based On Table                  | Chart Type | X-Axis         | Y-Axis             | Description |
|----------------------------------------|----------------------------------|------------|----------------|--------------------|-------------|
| **Total Sales (Excluding UK)**         | `gold_sales`                    | Bar        | `Country`      | `total_sales`      | Compares country-wise sales revenue, excluding the UK |
| **Sales Distribution**                 | `gold_sales`                    | Pie        | `Country`      | `total_sales`      | Visualizes the proportional revenue share by country |
| **Monthly Sales Trend**                | `gold_sales`                    | Area       | `invoice_date` (Month) | `total_sales` | Shows seasonal trends and revenue progression over time |
| **Top 10 Products by Revenue**         | `gold_sales_by_product`         | Bar        | `product`      | `total_revenue`    | Highlights best-selling products |
| **Customer Spend Distribution**        | `gold_sales_by_customer`        | Histogram  | `spend_bucket` | `customer_count`   | Groups customers into spend brackets |
| **Hourly Sales Trend**                 | `gold_hourly_sales`             | Line       | `hour`         | `total_sales`      | Identifies peak hours for transactions |
| **Weekly Sales Trend – United Kingdom**| `gold_weekly_sales`             | Area       | `week_start`   | `weekly_sales`     | Tracks weekly revenue movement in the UK market |

---

## 🚀 Optimization Steps

- Used `OPTIMIZE` and `ZORDER` for faster queries

---

## 📌 Key Learnings

- Applied the **Medallion architecture** for data refinement  
- Used **Delta Lake features**: schema enforcement, versioning, ZORDER  
- Built reusable and scalable ETL logic with PySpark  
- Designed an end-to-end pipeline suitable for production  

---

## 🧠 Future Improvements

- Add **data quality checks** using expectations or DLT
- Automate pipeline via **Databricks Jobs**
- Simulate incremental ingestion with Auto Loader
- Add alerts or anomaly detection on KPI deviations

## 📁 Folder Structure

├── Readme.md

├── 01_bronze_ingest_data.ipynb

├── 02_silver_clean_validate.ipynb

├── 03_gold_aggregate_metrics.ipynb

├── 04_Optimization_track_versioning.ipynb

└── Retail_dashboard

---
<img width="2536" height="1432" alt="image" src="https://github.com/user-attachments/assets/4675f37d-c471-4349-b8a4-5ea7f610e909" />
---

## 👤 Author

**Joby Chacko**  
Databricks Data Engineer Associate Certified  
🔗 [LinkedIn](https://www.linkedin.com/in/joby-chacko)
---

##
