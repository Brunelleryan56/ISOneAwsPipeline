# ISOneAwsPipeline
Data Pipeline for Power Grid Data and analysis
# Electricity Load Analytics: Cloud-Native Data Pipeline

This project demonstrates an end-to-end data engineering pipeline, moving raw energy consumption data from a cloud storage bucket into a data warehouse, followed by advanced pattern analysis and visualization.
## Architecture

## 1. Project Objective
The goal of this project was to ingest, model, and visualize electricity load data to identify consumption patterns, peak usage times, and load stability. This project serves as a demonstration of cloud-native data architecture and business intelligence best practices.

## 2. Architecture Overview
The pipeline follows a modern ELT (Extract, Load, Transform) pattern:
* **Storage:** Raw electricity load files extracted using EIA API key, then pushed and stored via cli to **Amazon S3**.
* **Warehouse:** Data is loaded and processed in **Amazon Redshift**, utilizing a Star Schema for optimized analytical queries.
* **Visualization:** **Power BI** connects to the Redshift warehouse to provide interactive analysis and trend discovery.

## 3. Methodology
### Data Modeling (Star Schema)
To ensure optimal performance and analytical clarity, I modeled the data into a Star Schema:
* **Fact Table:** `fact_energy_load` (contains core metrics like megawatt hours).
* **Dimension Tables:** `dim_time` (temporal attributes) and `dim_region` (location attributes).
* **Modeling:** Relationships were defined in Power BI to ensure proper filtering and aggregation across the data model.

### Engineering Challenges
* **Network & Security:** Configured AWS Security Groups and Redshift public accessibility settings to establish a secure, private connection between the cloud warehouse and the local BI environment.
* **Optimization:** Implemented a FinOps strategy by utilizing "Import" mode in Power BI, allowing for the Redshift cluster to remain "Paused" when not actively refreshing data, maintaining strict budget adherence.

## 4. Key Visualizations & Insights

### Hourly Trend & Peak Load
The line chart tracks the pulse of energy demand, allowing for the identification of volatility, while the KPI card provides instant visibility into peak system load.

### Load Pattern Heatmap
This matrix visual uses conditional formatting to create a "Heatmap," revealing seasonal and daily usage patterns. High-load hours are clearly distinguishable, enabling rapid identification of systemic peak consumption times.

### Load Stability (Histogram)
By applying binned histograms to the load data, the pipeline uncovers bimodal distribution patterns, illustrating stable versus volatile energy demand periods.

## 5. Technology Stack
* **Cloud:** AWS (S3, Redshift)
* **SQL:** PostgreSQL (Redshift syntax)
* **Visualization:** Power BI (DAX, Star Schema Modeling)
* **Engineering:** ETL Pipeline Design, FinOps Optimization
```mermaid
graph LR
    A[Amazon S3] -->|Raw Data| B(Amazon Redshift)
    B -->|Query/Import| C[Power BI]
    
    style B fill:#FF9900,stroke:#333,stroke-width:2px
    style C fill:#F2C811,stroke:#333,stroke-width:2px
