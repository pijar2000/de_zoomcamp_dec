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

---

## Question 4:
Write a query to retrieve the PULocationID from the table (not the external table) in BigQuery. Now write a query to retrieve the PULocationID and DOLocationID on the same table. Why are the estimated number of Bytes different?

### Query Function:
**Query**
```sql
# 1. Write a query to retrieve PULocationIDs data
SELECT PULocationID 
FROM `zoomcamp-dw-486814.nytaxi.yellow_tripdata_2024`;

# 2. Write a query to retrieve PULocationIDs and DOLocationID data
SELECT PULocationID, DOLocationID
FROM `zoomcamp-dw-486814.nytaxi.yellow_tripdata_2024`;
```

**Query Result**
1. Query to retrieve PULocationIDS data will process 155.12 MB when run.
2. Query to retrieve PULocationIDS and DOLocationID data will process 310.24 MB when run.

### Explanation
The estimated number of bytes is different because BigQuery is Columnar Storage Architecture or columnar database and only scans the columns referenced in the query. Traditional databases (like PostgreSQL or MySQL) usually store data in rows. If you want one piece of information from a row, the database often has to "read" the entire row into memory to find it. BigQuery does the opposite. It stores each column in its own separate file or block of memory.
   - Efficiency: When you run the first query, BigQuery only opens the file containing `PULocationID`. It completely ignores all other columns (like VendorID,    passenger_count, etc.).
   - Additive Cost: When you add `DOLocationID` to your SELECT statement, BigQuery now has to open and scan a second set of files. Since you are reading more physical data off the disk, the "Bytes Processed" increases proportionally.
   - Pricing Impact: This is exactly why `SELECT *` is considered a "sin" in BigQuery; it forces the engine to scan every single column file in the table, maximizing your costs.

**Answer:** `BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.`
