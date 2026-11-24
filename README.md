# Description
This project builds a unified analytics platform on **Microsoft Fabric** that integrates mobility data (NYC Taxi), environmental data (OpenAQ air quality), and macro-economic indicators (GDP & FX rates) into a single Lakehouse and Data Warehouse.


## Sources
* **Mobility:** NYC TLC Trip Record Data & Taxi Zone Lookup
* **Environment:** OpenAQ Air Quality Measurements (`PM2.5`, `O3`, `Temperature`)
* **Macro-Economics:** GDP & Foreign Exchange (FX) Rates

## The main ETL file
[Notebook_1.ipynb](notebooks/Notebook_1.ipynb)

It shows transformation through layers : bronze → silver → gold

### 1. Bronze Layer
* Ingested raw datasets from original sources into Spark DataFrame

### 2. Silver Layer
* Standardized schemas, column names, and data types across all datasets (suffixed with `_clean`).
* Removed invalid/corrupted records, dropped unused columns, handled missing values, and applied business filters (by date range and revenue).
* Mapped NYC boroughs using the official `taxi_zones` lookup table and created `df_stations` to map air quality monitoring stations to NYC boroughs, linking both datasets via a shared zone mapping.

### 3. Gold Layer
* Built a **Star Schema** [star_schema](images/star_schema.png) in Microsoft Fabric:
  * **Dimensions:** `dim_date`, `dim_zone`, `dim_fx`, `dim_gdp`
  * **Fact Tables:** `fact_taxi`, `fact_air_quality`
## Dashboards & Data Quality
* Created dashboards using tools in  MS Fabric
[Dashboards](dashboards/Dashboards.pdf)
* Created a data quality checker 
  [telegram bot](data-quality-checker)
