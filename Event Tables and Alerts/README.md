# Snowflake Event Tables & Alerts - Data Pipeline Project

## Overview
This project demonstrates a real-world use case for using **event tables** and **alerts** in Snowflake. The data pipeline processes JSON data from an untrusted source, parsing valid records while handling bad data through a **Dead Letter Queue (DLQ)** mechanism. An alert system is integrated to notify users via email when bad records are detected.

### Key Features:
- **JSON Data Processing**: Parses incoming JSON data using Python.
- **Dead Letter Queue (DLQ)**: Identifies and logs invalid records.
- **Event Tables**: Stores bad records for monitoring and analysis.
- **Automated Alerts**: Sends email notifications when bad data is detected.
- **Task Scheduling**: Automates data transformation workflows.

## Prerequisites
Before setting up this project, ensure you have:
- A **Snowflake Account** (Sign up at [Snowflake](https://www.snowflake.com/))
- Familiarity with **SQL** and **Python**
- Access to Snowflake's **Task and Alert** features

## What You Will Learn
By completing this project, you will learn:
- How to log and monitor bad records using **event tables**.
- How to create and schedule **tasks** for automated data transformation.
- How to set up **alerts** to detect and notify users of issues in data pipelines.

## Project Architecture
1. **Data Ingestion**: JSON records are received from an external source.
2. **Data Processing (Python & SQL)**: Valid records are parsed and stored in a **Snowflake table**.
3. **Error Handling (DLQ)**: Invalid records are stored separately in an **event table**.
4. **Automated Alerts**: An alert is triggered when bad data exceeds a threshold.
5. **Task Scheduling**: A Snowflake task automates the pipeline workflow.

---

## Step 1: Setting Up Snowflake Environment

### 1.1 Create a Snowflake Database and Schema
```sql
CREATE DATABASE event_logging;
CREATE SCHEMA data_pipeline;
```

### 1.2 Create the Main Data Table
```sql
CREATE TABLE data_pipeline.valid_records (
    id INT,
    event_time TIMESTAMP,
    data VARIANT
);
```

### 1.3 Create an Event Table for Bad Records
```sql
CREATE TABLE data_pipeline.bad_records (
    id INT,
    event_time TIMESTAMP,
    error_message STRING,
    raw_data STRING
);
```

### 1.4 Create an Alert for Bad Data
```sql
CREATE ALERT data_pipeline.bad_data_alert
WAREHOUSE = my_warehouse
SCHEDULE = '1 MINUTE'
IF (SELECT COUNT(*) FROM data_pipeline.bad_records WHERE event_time > DATEADD(MINUTE, -1, CURRENT_TIMESTAMP)) > 10
THEN
  CALL SYSTEM$SEND_EMAIL(
      'admin@example.com',
      'Bad Data Alert',
      'More than 10 bad records detected in the last minute.'
  );
```

---

## Step 2: Python Script for Data Processing
Use the following **Python script** to process incoming JSON data.

### 2.1 Install Dependencies
```bash
pip install snowflake-connector-python
```

### 2.2 Python Code for Data Processing
```python
import snowflake.connector
import json

# Connect to Snowflake
conn = snowflake.connector.connect(
    user='your_username',
    password='your_password',
    account='your_account'
)
cur = conn.cursor()

# Sample JSON data
json_data = '[{"id": 1, "event_time": "2025-03-26T12:00:00", "data": "valid"}, {"id": 2, "event_time": "2025-03-26T12:05:00", "data": "invalid"}]'

data_list = json.loads(json_data)

for record in data_list:
    try:
        # Validate JSON format
        if "id" in record and "event_time" in record and "data" in record:
            cur.execute(f"""
                INSERT INTO data_pipeline.valid_records (id, event_time, data)
                VALUES ({record['id']}, '{record['event_time']}', '{record['data']}')
            """)
        else:
            raise ValueError("Invalid JSON structure")
    except Exception as e:
        cur.execute(f"""
            INSERT INTO data_pipeline.bad_records (id, event_time, error_message, raw_data)
            VALUES ({record.get('id', 'NULL')}, CURRENT_TIMESTAMP, '{str(e)}', '{json.dumps(record)}')
        """)

conn.commit()
cur.close()
conn.close()
```

---

## Step 3: Automate Data Processing with Snowflake Tasks

### 3.1 Create a Snowflake Task
```sql
CREATE OR REPLACE TASK data_pipeline.process_data_task
WAREHOUSE = my_warehouse
SCHEDULE = 'USING CRON 0 * * * * UTC'
AS
CALL data_pipeline.process_data();
```

### 3.2 Enable the Task
```sql
ALTER TASK data_pipeline.process_data_task RESUME;
```

---

## Step 4: Testing the Pipeline
- **Insert sample data** and check if valid records go into `valid_records` while bad records go into `bad_records`.
- **Trigger the alert** by inserting multiple bad records.
- **Monitor the event tables** for bad data logs.

## Step 5: Deployment & Monitoring
- Deploy the Python script on a cloud service (AWS Lambda, Google Cloud Functions, etc.).
- Use **Snowflake's built-in monitoring tools** to track pipeline performance.

## Conclusion
This project provides a **robust data pipeline** to process, monitor, and alert on bad data in Snowflake. By following these steps, you ensure **data integrity** and **automate issue detection** for real-time processing.

---

## Contribution
Feel free to fork this repository, suggest improvements, or contribute by adding new features!

## License
This project is licensed under the MIT License.

## Contact
For any queries, reach out via [your_email@example.com].

---

### 🌟 **If you found this useful, give it a ⭐ on GitHub!**

