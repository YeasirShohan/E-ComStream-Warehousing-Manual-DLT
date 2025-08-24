# 🧪 Delta Live Tables Pipeline for E-Commerce Data Modeling

## 📌 Overview

This project implements a **Delta Live Tables (DLT)** pipeline using **Databricks** to process and model streaming data from an e-commerce platform. The pipeline follows a **star schema design** and transforms raw silver-level data into curated gold-level dimension and fact tables, enabling downstream analytics and reporting.

---

## 🧱 Architecture

- **Source Table**: `silver_table` (Streaming)
- **Technologies**: Delta Live Tables (DLT), PySpark, Structured Streaming, Window Functions
- **Schema Modeled**: Star Schema
  - Dimensions:
    - `dim_product`
    - `dim_customer`
    - `dim_payment`
    - `dim_shipment`
  - Fact Table:
    - `fact_order`

---

## 🔄 Pipeline Workflow

1. **Ingest Streaming and Enriched Data** from the silver table.
2. **Deduplicate and Generate Surrogate Keys** for dimensions using `ROW_NUMBER()`.
3. **Create Dimension Tables** by selecting distinct records and enriching with surrogate keys.
4. **Build Fact Table** by joining the streaming source with dimension tables using natural keys.
5. **Output Tables** are managed by Delta Live Tables and are updated continuously.

---

## 📁 Table Definitions

| Table Name       | Type      | Description |
|------------------|-----------|-------------|
| `dim_product`    | Dimension | Product master data with surrogate keys |
| `dim_customer`   | Dimension | Customer master data with surrogate keys |
| `dim_payment`    | Dimension | Payment method and status information |
| `dim_shipment`   | Dimension | Shipment carrier and delivery information |
| `fact_order`     | Fact      | Order facts joined with all dimensions |

---

## 🛠️ Setup & Deployment

### 1. Prerequisites
- Databricks Workspace with access to Delta Live Tables
- Streaming Bronze and Silver table.
- Cluster with Unity Catalog and DLT permissions enabled

### 2. Deploying the Pipeline
1. Navigate to **Workflows > Delta Live Tables** in your Databricks workspace.
2. Click **Create Pipeline**.
3. Provide the following:
   - **Notebook path**: Path to this DLT notebook
   - **Pipeline name**: E.g., `ecommerce_dlt_pipeline`
   - **Target schema**: E.g., `datamodeling_p2.gold`
   - **Storage location**: A DBFS or external location for pipeline logs/checkpoints
4. Select **Continuous** mode for real-time streaming.
5. Click **Start** to begin processing.

---

## ✅ Data Quality Notes

- Surrogate keys are generated using `ROW_NUMBER()` with `Window.orderBy(...)`.
- Dimension tables are deduplicated using `.distinct()` to ensure uniqueness.
- Fact table is built only after dimensions are available to ensure referential integrity.
- Consider adding `@dlt.expect()` for data quality enforcement.

---

## 📈 Example Use Cases

- Build dashboards on product sales by category and shipment status.
- Analyze customer order frequency and preferred payment methods.
- Track revenue trends by date and payment method.

---

## 👥 Contributors

- **Yeasir Arafat Shohan** 

---

## 📄 License

This project is for educational and internal use. For commercial or production use, follow your organization's data governance and licensing policies.

---

## 🗨️ Support

For issues or feature requests, contact your data engineering team or open an internal support ticket within Databricks.

