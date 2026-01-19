## Before you Start

Download the green taxi trips data for November 2025:
- green taxi trips has 2 file, trip data and zone data

```bash
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet
```

You will also need the dataset with zones:

```bash
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
```

## Question 3. Counting short trips
Guidline by pijar

For the trips in November 2025 (lpep_pickup_datetime between '2025-11-01' and '2025-12-01', exclusive of the upper bound), how many trips had a `trip_distance` of less than or equal to 1 mile?

- For this question, the fastest analysis is using pandas
- Start from anlyze which column you need such as

```python
import pandas as pd

df = pd.read_parquet("green_tripdata_2025-11.parquet")
print(df.dtypes)
```

- You can determine what you need to solve
- If the corresponding column in datetime already you're good to go

```python
# date filter
filter_date = (df["lpep_pickup_datetime"] >= "2025-11-01") & (df["lpep_pickup_datetime"] < "2025-12-01")

# distance filter
filter_distance = df["trip_distance"] <= 1
```

- This is one of method to determine which data coverage you should take 
