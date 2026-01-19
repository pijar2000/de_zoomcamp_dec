## Before you Start

Download the green taxi trips data for November 2025:
- green taxi trips has 2 file, trip data and zone data (This is parquet type file)

```bash
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet
```
Green taxi trips data for November 2025: https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet

You will also need the dataset with zones: (This is csv type file)

```bash
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
```
Taxi zone: https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv

## Question 3. Counting short trips
Guidline by pijar

For the trips in November 2025 (lpep_pickup_datetime between '2025-11-01' and '2025-12-01', exclusive of the upper bound), how many trips had a `trip_distance` of less than or equal to 1 mile?

- You can analyze it with SQL inside database or simply pandas in python notebook

If you want to analyze it in database, the easiest way is to load the paquet file type into df in python notebook and convert into csv, then load the data to database, eg:

```python
import pandas as pd

df_parquet = pd.read_parquet("green_tripdata_2025-11.parquet")

df_parquet.to_csv("green_tripdata_2025-11.csv", index=False)
```

- Don't forget to check the column type of the data with pandas first and make it in database with `CREATE TABLE`

OR if you want to ingest the parquet data DIRECTLY to database, you could follow this guide

https://github.com/pijar2000/de_zoomcamp_dec/blob/main/01-docker-terraform/parquet-ingestion.ipynb


## BACK TO THE QUESTION
 
- For this question, the fastest analysis is using pandas
- Start from anlyze which column you need such as

```python
import pandas as pd

df = pd.read_parquet("green_tripdata_2025-11.parquet")
print(df.dtypes)
```

- You can determine what you need to solve
- If the corresponding column in datetime already you're good to go


- This is one of method to determine which data coverage you should take, in this case filter by date and by distance, one by one
```python
# date filter
filter_date = (df["lpep_pickup_datetime"] >= "2025-11-01") & (df["lpep_pickup_datetime"] < "2025-12-01")

# distance filter
filter_distance = df["trip_distance"] <= 1

df_filter = df[mask_date & mask_distance]
```

- you can count the rest by various method, for example `count` function 
