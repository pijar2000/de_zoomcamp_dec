## Question 1

What is count of records for the 2024 Yellow Taxi Data?

```sql
SELECT COUNT(*) AS total_records
FROM `zoomcamp-pijar.nytaxi.yellow_tripdata_2024`;
```

## Queation 2

Write a query to count the distinct number of PULocationIDs for the entire dataset on both the tables.

What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?

- For external table

```sql
SELECT COUNT(DISTINCT PULocationID) AS distinct_pu
FROM `zoomcamp-pijar.nytaxi.external_yellow_tripdata_2024`;
```

- For materialized table

```sql
SELECT COUNT(DISTINCT PULocationID) AS distinct_pu
FROM `zoomcamp-pijar.nytaxi.yellow_tripdata_2024`;
```

<img width="679" height="160" alt="image" src="https://github.com/user-attachments/assets/0ce7edd0-5717-4edb-bebb-c3734f094aff" />

Just block the query and it will show the number

## Question 3

It's theory undestanding of columnar storage, see this documentation

- https://docs.cloud.google.com/bigquery/docs/storage_overview
- https://docs.cloud.google.com/bigquery/docs/storage_overview#storage_layout

## Question 4

How many records have a fare_amount of 0?

```sql
SELECT COUNT(*) AS zero_fare_trips
FROM `zoomcamp-pijar.nytaxi.yellow_tripdata_2024`
WHERE fare_amount = 0;
```

## Question 5

- Make your own partition table first

```sql
CREATE OR REPLACE TABLE
`zoomcamp-pijar.nytaxi.yellow_tripdata_2024_partition`
PARTITION BY DATE(tpep_dropoff_datetime)
AS
SELECT *
FROM `zoomcamp-pijar.nytaxi.yellow_tripdata_2024`;
```

Its also theory understanding, you can read it here

- http://developers.google.com/machine-learning/clustering/overview
- https://docs.cloud.google.com/bigquery/docs/partitioned-tables

## Question 6

Use the materialized table you created earlier in your from clause and note the estimated bytes. Now change the table in the from clause to the partitioned table you created for question 5 and note the estimated bytes processed. What are these values?

- Test your normal table
```sql
SELECT *
FROM `zoomcamp-pijar.nytaxi.yellow_tripdata_2024`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15'
ORDER BY VendorID;
```


- Test your partition table
```sql
SELECT *
FROM `zoomcamp-pijar.nytaxi.yellow_tripdata_2024_partition`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15'
ORDER BY VendorID;
```

## Question 7

Where is the data stored in the External Table you created?

It's theory, you can read this
- https://docs.cloud.google.com/bigquery/docs/external-tables

## Question 8

It is best practice in Big Query to always cluster your data?
There is no exact answer, what do you think?

## Question 9

Just `SELECT count(*)` from your own table and see how long it will be, then make your own conclusion.
