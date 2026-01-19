## Question 4. Longest trip for each day
Guideline by pijar

- You need to load the data from question 3, check the question_3 note

Which was the pick up day with the longest trip distance? Only consider trips with `trip_distance` less than 100 miles (to exclude data errors).

Use the pick up time for your calculations.
- Check column type
- Determine your column
- Limit the coverage of your data by 100 miles and take the `date` information
- Group by day
```python
df_1 = df[df["trip_distance"] < 100].copy()
df_1["pickup_day"] = df_valid["lpep_pickup_datetime"].dt.date

group_day = df_1.groupby("pickup_day")["trip_distance"].max().reset_index()
```


- you can choose various method to find the answer, for example you can function `nlargest`
```python
longest_day = group_day.nlargest(1, "trip_distance")
```
