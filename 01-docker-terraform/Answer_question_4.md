## Question 4. Longest trip for each day
Guideline by pijar
- You can analyze it with SQL inside database or simply pandas in python notebook
- For this question, the fastest analysis is using pandas
- You need to load the data from question 3, check the question_3 note

Which was the pick up day with the longest trip distance? Only consider trips with `trip_distance` less than 100 miles (to exclude data errors).

- 2025-11-14 <---
- 2025-11-20
- 2025-11-23
- 2025-11-25

How to answer:
```
# filter trip_distance kurang dari 100
df_lt_100 = df[df["trip_distance"] < 100]
# cari trip paling jauh
max_distance = df_lt_100["trip_distance"].max()
# ambil 1 baris data yang trip paling jauh
max_trip = df_lt_100[df_lt_100["trip_distance"] == max_distance]
# ambil tanggalnya
max_trip["lpep_pickup_datetime"].dt.date
```

<p align="center">
  <img width="60%" src="images/question_4.png" alt="answer_question_4">
</p>