## 1. Overview


In this Quickstart, we will investigate how a financial company builds a BI dashboard using customer transactional data housed on a PostgreSQL database. The data is brought into Snowflake via the Snowflake Connector for PostgreSQL. The main idea is gain insights on potential ways to increase customer spending with promotions.

What You Will Build
Visualize customer data and gain insights ingesting data from PostgreSQL DB to Snowflake using the Snowflake Connector for PostgreSQL Native App and Dynamic Tables
What You Will Learn
How to connect PostgreSQL data to Snowflake using the Snowflake Connector for PostgreSQL
How to visualize data using Dynamic Tables and display visualizations within Streamlit in Snowflake (SiS)
Prerequisites
Docker installed on your local machine
A tool available for connecting to the PostgreSQL database
This can be a database-specific tool or a general-purpose tool such as Visual Studio Code or PyCharm
Familiarity with basic Python and SQL
Familiarity with data science notebooks
Go to the Snowflake sign-up page and register for a free account. After registration, you will receive an email containing a link that will take you to Snowflake, where you can sign in.


## 2. Snowflake Environment
Overview
You will use Snowsight, the Snowflake web interface to create Snowflake objects (warehouse, database, schema, role).

Creating Objects and Loading Data
Navigate to Worksheets, click + in the top-right corner to create a new Worksheet, and choose SQL Worksheet
Copy and paste the following code to create Snowflake objects (warehouse, database, schema) and click Run All at the top of the Worksheet


```bash
USE ROLE accountadmin;

/*---------------------------*/
-- Create our Database
/*---------------------------*/
CREATE OR REPLACE DATABASE cdc_prod;

/*---------------------------*/
-- Create our Schema
/*---------------------------*/
CREATE OR REPLACE SCHEMA cdc_prod.analytics;

/*---------------------------*/
-- Create our Warehouse
/*---------------------------*/

-- data science warehouse
CREATE OR REPLACE WAREHOUSE cdc_ds_wh
   WAREHOUSE_SIZE = 'xsmall'
   WAREHOUSE_TYPE = 'standard'
   AUTO_SUSPEND = 60
   AUTO_RESUME = TRUE
   INITIALLY_SUSPENDED = TRUE
   COMMENT = 'data science warehouse for cdc';

-- Use our Warehouse
USE WAREHOUSE cdc_ds_wh;
/*---------------------------*/
-- sql completion note
/*---------------------------*/
SELECT 'cdc sql is now complete' AS note;
```
