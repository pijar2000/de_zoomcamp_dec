## Question 3

How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?

- After you ingest the corresponding period, you can open dbeaver or pgadmin, connect to `ny_taxi` database and run a query to count row for respecting time, there's lot of method to count you can make, but the simplest way is like this

```sql
SELECT COUNT(*) AS total_rows
FROM yellow_tripdata
WHERE EXTRACT(YEAR FROM tpep_pickup_datetime) = 2020;
```

## Question 4

How many rows are there for the Green Taxi data for all CSV files in the year 2020?

- It's the same for question 3 but the table should be different

```sql
SELECT COUNT(*) AS total_rows
FROM green_tripdata
WHERE EXTRACT(YEAR FROM tpep_pickup_datetime) = 2020;
```

## Question 5

How many rows are there for the Yellow Taxi data for the March 2021 CSV file?

- careful the sql query is strict about datetime, makesure you include time from 00:00 to 23:59 

```sql
SELECT COUNT(*) AS total_rows
FROM yellow_tripdata
WHERE tpep_pickup_datetime >= '2021-03-01 00:00:00'
  AND tpep_pickup_datetime < '2021-04-01 00:00:00';
```
