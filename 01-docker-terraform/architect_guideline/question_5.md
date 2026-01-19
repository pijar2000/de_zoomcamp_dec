## Question 5. Biggest pickup zone

Guideline by pijar
- You need to load the data from question 3, check the question_3 note

Which was the pickup zone with the largest `total_amount` (sum of all trips) on November 18th, 2025?

- First you should aware there's no zone column in green taxi trip data
- It separet in csv zone file
- Load the file into two dataset variable (for example df_trip and df_zone)
- Check the column type of the data
- You should choose what exactly the `primary key` for join the data, for example

```python3
df_trip_zone = df_trip.merge(
    df_zone,
    left_on="PULocationID",
    right_on="LocationID",
    how="left"
)
```

- After merge the data into one dataset you good to go to analyze the rest
- Use pick up time and zone column in the data, group it

```python
df_day = df_trip_zone[
    df_trip_zone["lpep_pickup_datetime"].dt.date == pd.to_datetime("2025-11-18").date()
]

zone_group = df_day.groupby("Zone")["total_amount"].sum().reset_index()
```

- Finally determine the largest  `total_amount`

```python3
zone_largest = zone_amounts.nlargest(1, "total_amount")
```
