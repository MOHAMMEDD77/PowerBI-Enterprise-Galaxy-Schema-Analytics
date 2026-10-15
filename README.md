# Enterprise Sales, Inventory & Operations Analytics Portfolio

An end-to-end business intelligence solution built in Power BI, featuring an advanced Galaxy Star Schema data architecture, robust Power Query ETL pipelines, and a sophisticated DAX semantic layer utilizing window functions, dynamic parameters, and role-playing time intelligence.

---

## Executive Summary
This portfolio project simulates a global enterprise data warehouse environment. It consolidates multi-year sales transactions, inventory snapshots, marketing campaigns, customer master data, and supply chain fulfillment logs into a unified, high-performance analytical model optimized for executive decision-making.

---

## Data Architecture: Galaxy Star Schema

The data model uses a Galaxy Schema (Constellation Schema) where multiple fact tables share conformed dimension tables, ensuring cross-functional consistency across Sales, Inventory, Logistics, and Campaigns.

### Core Architecture Components:
* Dimension Tables (02_dim): dim_customer, dim_product, dim_calendar, dim_geo, dim_campaign, and dim_flag (Junk Dimension combining order channels, statuses, and priorities).
* Fact Tables (03_fact):
  * fact_sales (Granular line-item sales transactions)
  * fact_inventory (Monthly product stock level balances)
  * fact_order_process (Supply chain lead-time and milestone tracking)
  * fact_target_revenue (Budget vs. actual tracking)
* Bridge Tables: fact_campaign_product to resolve many-to-many relationships between marketing campaigns and promoted product SKUs.

---

## Power Query ETL Pipeline & Data Governance

* Staging & Load Separation: Maintained a dedicated 01_dataset group containing 22 raw staging queries with "Enable Load" disabled, ensuring zero redundant memory consumption in the VertiPaq engine.
* Structural Transformation: Transformed wide matrix formats in raw inventory sheets into tall, relational time-series structures via Unpivot operations.
* Surrogate Key Generation: Engineered clean integer-based surrogate keys (product_key, customer_id, flag_key, geo_key) across dimensions to maximize indexing and join performance.

---

## Advanced DAX Semantic Layer & Time Intelligence

### 1. Role-Playing Date Dimensions (USERELATIONSHIP)
To analyze supply chain performance across different milestones without relationship ambiguity, the model utilizes a primary active relationship on order_date and inactive relationships on ship_date, delivery_date, and pay_date.

### 2. Dynamic Rolling 6-Month Window Average
Leveraging modern DAX WINDOW functions to compute sliding financial trend analysis:
- Calculated over a 6-month sliding window dynamically adjusted by calendar sort index.

### 3. Dynamic Top-N Products with "Others" Grouping
Enables users to dynamically select N top products via parameter slicers while automatically grouping remaining tail items into an aggregated "Others" bucket.

### 4. Pareto (80/20) Cumulative Contribution Analysis
Calculates cumulative revenue share to identify core revenue-generating product tiers (e.g., top 30% or top 50% products).

---

## Dashboard Page Structure & UX/UI

1. Executive Overview Page: High-level KPI cards (Total Revenue, Gross Margin %, YoY Growth, Actual vs Target Variance) paired with monthly trend lines and regional performance maps.
2. Sales & Product Deep-Dive: Matrix breakdowns by subcategory, brand, and product name integrated with dynamic Top-N and Pareto segmentation filters.
3. Operations & Fulfillment: Lead-time analytics measuring processing duration from order placement to final delivery, alongside inventory stock health tracking.

---

## Tech Stack & Tools
* BI Engine: Power BI Desktop (VertiPaq Engine)
* ETL & Data Prep: Power Query (M Language)
* Data Modeling: Galaxy Star Schema, Junk Dimensions, Bridge Tables, Role-Playing Relationships
* Calculations: Advanced DAX (WINDOW, USERELATIONSHIP, TOPN, EXCEPT, Time Intelligence)
* Version Control: Git & GitHub
