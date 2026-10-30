# Microsoft-Fabric-Sales-Analytics

## End-to-End Sales Analytics Solution with Microsoft Fabric

An end-to-end sales analytics project built with Microsoft Fabric and Power BI. The solution ingests sales data, organizes it using the Bronze–Silver–Gold medallion architecture, transforms it with PySpark, models it in a warehouse using a star schema, and presents business insights in an interactive Power BI dashboard.

## Project at a glance

- **Platform:** Microsoft Fabric
- **Data ingestion and orchestration:** Fabric Data Pipeline and Copy Data activities
- **Data storage:** Fabric Lakehouse / Delta tables
- **Data transformation:** PySpark notebooks
- **Warehouse and querying:** Fabric Data Warehouse and T-SQL
- **Semantic/reporting layer:** Power BI, DirectLake, DAX
- **Data-model design:** Star schema with a sales fact table and dimension tables
- **Security:** Row-Level Security (RLS), as part of the project design

## Business objective

Create a repeatable analytics workflow that turns raw sales records into curated, analysis-ready data and a dashboard that helps users explore revenue, order volume, quantities sold, product-category performance, regional performance, monthly trends, and high-value customers.

## Architecture and workflow

The pipeline shown in the project follows this sequence:

1. **CopyRawSalesCSV** — ingests the source sales CSV from an HTTP source.
2. **Copydatatodelta** — copies the ingested data into the Lakehouse/Delta layer.
3. **TransformBronzeToSilver** — uses a notebook to clean and prepare the raw records.
4. **BuildGoldLayer** — creates curated, analysis-ready outputs for reporting.
5. **transformsilvertowarehouse** — loads prepared data into the Fabric Data Warehouse.

The pipeline is parameterized with a source-file parameter, making the source path easier to configure without hard-coding it in every activity.

### Medallion architecture

- **Bronze:** Raw ingested sales data is retained as the starting layer. The Lakehouse screenshot shows a `bronze_sales` table.
- **Silver:** Cleaned and transformed records are prepared for reliable analysis. The project includes silver-layer tables/dataflow outputs.
- **Gold:** Curated business-level outputs, including a sales summary, are prepared for downstream reporting.

This separation makes it easier to trace data from its raw source through transformations to reporting-ready outputs.

## Data preparation and modeling

### PySpark transformations

Fabric notebooks are used in the transformation stages to process and prepare sales data. The goal is to move data from the raw layer into consistent, analysis-ready tables before loading the warehouse. Document the exact cleaning rules here if you want to make the implementation reproducible—for example, how missing values, data types, duplicates, and invalid records were handled.

### Warehouse star schema

The warehouse screenshot shows these tables in the `analytics` schema:

- `fact_sales` — central sales/transaction fact table
- `dim_customer` — customer attributes
- `dim_date` — date attributes for time-based analysis
- `dim_product` — product attributes
- `dim_region` — region attributes

The fact table stores measurable business events, while the dimension tables provide descriptive context for slicing and filtering the facts. This star-schema design supports simpler analytical queries and reporting.

### Semantic model and Power BI

The reporting layer uses Power BI with DirectLake, DAX measures, interactive filters, and Row-Level Security (RLS). The dashboard includes date, month, quarter, and year filters, plus KPI cards, trend visuals, category breakdowns, regional comparisons, and a customer ranking table.

## Dashboard screenshots

### Sales Analytics Overview

<img width="1595" height="986" alt="Purple Sales Analytics Dashboard" src="https://github.com/user-attachments/assets/1d64d44f-e914-4d62-ae40-ef370cda90a1" />

### Fabric pipeline orchestration

<img width="1682" height="935" alt="1ST" src="https://github.com/user-attachments/assets/024e6ab7-14a5-4219-b02d-985e908fba97" />

### Lakehouse bronze layer

<img width="1682" height="935" alt="2ND" src="https://github.com/user-attachments/assets/887877ab-e12a-440d-8871-fe43a7599ac8" />

### Data Warehouse schema
<img width="1693" height="929" alt="3RD" src="https://github.com/user-attachments/assets/efc7d6cc-34ba-44c7-8688-b851d3b5afd5" />

## Dashboard findings

The figures below are read from the dashboard screenshot. Values are rounded/formatted as displayed and may change when filters are applied.

### KPI summary

| KPI | Dashboard result |
|---|---:|
| Total Revenue | ₹7.7M |
| Total Revenue (USD) | $92.5K |
| Total Orders | 778 |
| Total Quantity Sold | 5,580 |
| Average Revenue per Order | ₹48.6K |
| Average Quantity per Order | 35.3 |

### Monthly trend

| Month | Revenue shown |
|---|---:|
| April | ₹2.0M |
| May | ₹2.7M |
| June | ₹3.0M |

The displayed monthly revenue increases from April through June, with June showing the highest revenue among the three months in view.

### Revenue by product category

| Category | Revenue shown |
|---|---:|
| Electronics | ₹4.8M |
| Furniture | ₹2.4M |
| Office Supplies | ₹0.4M |

Electronics is the largest revenue contributor in the displayed category comparison, followed by Furniture and Office Supplies.

### Revenue by region

| Region | Revenue shown |
|---|---:|
| West | ₹2.7M |
| North | ₹2.2M |
| East | ₹1.8M |
| South | ₹0.9M |

West leads the displayed regional revenue comparison, while South has the lowest displayed revenue.

### Orders by region

| Region | Orders shown |
|---|---:|
| West | 210 |
| East | 206 |
| North | 192 |
| South | 170 |

West has the highest displayed order count, followed by East, North, and South.

### Orders by product category

The doughnut chart shows 778 orders distributed across the three categories:

| Category | Orders shown | Share shown |
|---|---:|---:|
| Office Supplies | 270 | 34.7% |
| Furniture | 256 | 32.9% |
| Electronics | 252 | 32.39% |

### Quantity sold by product category

| Category | Quantity shown | Share shown |
|---|---:|---:|
| Office Supplies | 3,646 | 65.34% |
| Furniture | 1,186 | 21.25% |
| Electronics | 748 | 13.41% |

Office Supplies accounts for the largest share of units sold in the displayed chart, even though Electronics contributes the most revenue. This is a useful example of why revenue and volume should be reviewed together.

### Top customers by revenue

The dashboard also includes a **Top 10 Customers by Revenue** table, with customer name, total revenue, and total orders. The table is designed to identify high-value customers and compare their revenue contribution with their order frequency.

## Business takeaways

1. **Electronics drives the most revenue** in the displayed category view.
2. **Office Supplies drives the most unit volume and category orders** in the displayed charts.
3. **The West region leads both revenue and order count** in the visible regional comparisons.
4. **Monthly revenue rises across April, May, and June** in the displayed trend.
5. **Customer-level ranking adds another analysis angle** by showing both revenue and order counts for the top ten customers.

## Tools and technologies

- Microsoft Fabric Data Pipelines
- Microsoft Fabric Lakehouse
- Delta Lake tables
- Fabric Notebooks and Apache PySpark
- Microsoft Fabric Data Warehouse
- T-SQL
- Power BI
- DirectLake
- DAX
- Star-schema dimensional modeling
- Row-Level Security (RLS)

