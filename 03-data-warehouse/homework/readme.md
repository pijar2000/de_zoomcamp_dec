# Module 3 Homework Solutions

This is for solutions for homework

## Setup Instructions

Before answering the questions, you need to follow the steps below:

1. Make sure you have access and billing enabled for GCP.
2. Authenticate with Google Cloud SDK:
   ```bash
   gcloud auth application-default login
   ```
3. Set your bucket name in `load_yellow_taxi_data.py` (e.g., `BUCKET_NAME = "de-zoomcamp-2026-484615"`).
4. Run the upload script. While using `uv` is recommended for easier dependency management, it is not mandatory. The essential requirement is having the `google-cloud-storage` library installed.

   **Option A: Using Standard Python**
   ```bash
   # Install the required library first
   pip install google-cloud-storage
   
   # Run the script
   python load_yellow_taxi_data.py
   ```

   **Option B: Using `uv` (Recommended for ease of use)**
   ```bash
   uv run load_yellow_taxi_data.py
   ```

---

## Question 1:
What is the count of records for the 2024 Yellow Taxi Data?

### Task Explanation:
This task requires calculating the total number of records (rows) within the **Yellow Taxi** dataset for the period of January - June 2024. The objective is to validate the data ingestion process, ensuring that all data uploaded to Google Cloud Storage and subsequently imported into BigQuery has been fully accounted for without any missing records.

### Query Function:
**Query:**
```sql
-- Query executed on the materialized table
SELECT COUNT(*) FROM `de-zoomcamp-2026-484615.nytaxi.yellow_tripdata_2024_homework`;
```

**Query Breakdown:**
1.  **`SELECT`**: The fundamental SQL keyword used to retrieve data from a database.
2.  **`COUNT(*)`**: An aggregate function that counts **every row** in the table, including rows that may contain null values. This is the most standard and efficient method in BigQuery to determine total data volume.
3.  **`FROM`**: Specifies the data source or the specific table to be queried.
4.  **``de-zoomcamp-2026-484615.nytaxi.yellow_tripdata_2024_homework``**: The *fully-qualified name* of the table (ProjectID.DatasetID.TableName).

**Multiple Choice Options:**
- 65,623
- 840,402
- **20,332,093**
- 85,431,289

**Answer:** `20,332,093`