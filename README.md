# Contoso-Retail-Data-Analysis

## 1. Overview
This project implements a complete ETL (Extract, Transform, Load) process using SQL Server Integration Services (SSIS) to analyze and transform data from the Contoso Retail Data Warehouse into curated datasets for business intelligence and analytics.

The ETL workflows consist of 6 separate pipelines, each targeting a different aspect of sales and business performance:

1. Sales Performance by Customer
2. Sales Over Time
3. Product Analysis
4. Channel Analysis
5. Geographic Insights
6. Inventory Analysis

---

## 2. Contoso Retail Data Warehouse
The `ContosoRetailDW` database is a sample data warehouse provided by Microsoft. It follows a **star schema design**, with:

- **Fact Tables**: containing transactional and aggregated metrics (e.g., `FactSales`).
- **Dimension Tables**: containing descriptive attributes for customers, products, channels, stores, dates, and locations.

In this project, `ContosoRetailDW` serves as the source system for all ETL pipelines.

---

## 3. Objective of Project
The main goals are to:

- Extract relevant sales and operational data from the Contoso Retail DW.
- Transform the data by applying lookups, derived fields, aggregations, sorting, conditional splits, and classification logic.
- Load the processed datasets into a curated analysis database (`Contoso_Retail_Analysis`) for reporting, visualization, and decision-making.

---

## 4. Pipelines

### 4.1 Sales Performance by Customer
**Objective:** Measure and analyze sales performance metrics at the customer level.

**Steps:**
1. **Source:** Extract customer-level sales from `FactSales`.
2. **Lookup Customer:** Retrieve customer details from `DimCustomer`.
3. **Derived Column:** Compute calculated fields such as Net Sales.
4. **Aggregate:** Summarize sales by customer.
5. **Destination:** Load results into `SalesPerformance` table in analysis DB.


---

### 4.2 Product Analysis
**Objective:** Analyze product performance and classify products using ABC analysis.

**Steps:**
1. **Source:** Extract product sales data.
2. **Derived Column:** Calculate Net Sales.
3. **Lookup Product:** Get product details from `DimProduct`.
4. **Lookup Category & Subcategory:** Retrieve hierarchical product information.
5. **Aggregate:** Summarize sales by product.
6. **Sort:** Order by Net Sales descending.
7. **Script Component:** Calculate cumulative % and assign ABC class.
8. **Destination:** Load into `ProductAnalysis` table.

---

### 4.3 Channel Analysis
**Objective:** Evaluate sales performance across different sales channels.

**Steps:**
1. **Source:** Extract sales data from `FactSales`.
2. **Aggregate1 & Aggregate2:** Summarize sales by different grouping levels (e.g., channel totals).
3. **Sort 1 & Sort 2:** Sort datasets for merging.
4. **Merge Join:** Combine aggregated datasets.
5. **Derived Column:** Calculate performance metrics (e.g., market share).
6. **Destination:** Load into `ChannelAnalysis` table.

---

### 4.4 Geographic Insights
**Objective:** Provide geographic-level sales analysis by city, state, and region.

**Steps:**
1. **Source:** Extract sales transactions.
2. **Lookup Store:** Retrieve store details from `DimStore`.
3. **Lookup Geography:** Get geographic attributes from `DimGeography`.
4. **Aggregate:** Summarize sales by geographic location.
5. **Conditional Split:** Separate data into different categories or regions if needed.
6. **Destination:** Load into `GeoInsights` table.

---

### 4.5 Sales Over Time
**Objective:** Track sales trends over time for reporting and forecasting.

**Steps:**
1. **Source:** Extract time-based sales data.
2. **Derived Column:** Compute Net Sales and Orders.
3. **Lookup Date:** Map transactions to `DimDate` attributes (Year, Month).
4. **Aggregate:** Summarize by date period.
5. **Destination:** Load into `SalesOverTime` table.

---

### 4.6 Inventory Analysis
**Objective:** Analyze inventory movement and stock performance.

**Steps:**
1. **Source:** Extract inventory-related data.
2. **Lookup Product:** Get product details from `DimProduct`.
3. **Lookup Store:** Retrieve store details from `DimStore`.
4. **Aggregate:** Summarize inventory metrics.
5. **Destination:** Load into `InventoryAnalysis` table.

---

## 5. Tools & Technologies
- **SQL Server Integration Services (SSIS):** ETL development & execution.
- **SQL Server:** Source (`ContosoRetailDW`) and target (`Contoso_Retail_Analysis`) databases.
- **T-SQL:** Queries for extraction, transformation, and testing.
