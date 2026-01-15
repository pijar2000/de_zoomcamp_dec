## Understanding Join, Multiple Join, MAX(), GROUP BY AND DATETIME HANDLING

Question 6 : For the passengers picked up in the zone named "East Harlem North" in November 2025, which was the drop off zone that had the largest tip? 


### Note
Before we start to do the task, makesure you have upload the dataset for the task in postgreSQL via jupyter notebook or python script:
1. Green taxi trips data for November 2025: https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet
2. Taxi zone: https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv

If you have problem with uploading parquet file to postgreSQL, you can follow tutorial in the link below:
1. https://github.com/pijar2000/de_zoomcamp_dec/blob/main/01-docker-terraform/method-homework/parquet-ingestion.ipynb

For csv file, you can follow tutorial in the link below:
1. https://github.com/pijar2000/de_zoomcamp_dec/tree/main/01-docker-terraform/source-modul/docker-sql


### Guideline Tips And Trick
If you are reading this, I assume you have finished uploading the Green taxi trips data for November 2025 and Taxi zone to Postgresql.
If so, for the first step, make sure that the table for the data already exists in the Postgresql database.

<img width="299" height="88" alt="image" src="https://github.com/user-attachments/assets/9e070176-b3e0-4087-bc3b-b07806e61173" />

To start querying, select the query tools menu at the top of the menu list, making sure that the query menu appears on the pgadmin display.

<img width="800" height="800" alt="image" src="https://github.com/user-attachments/assets/b3dc93e7-221d-4e99-b845-cfe46045fbb6" />

Alright, now let's get into the main discussion. As stated in the question above, we have to find the highest tip amount among the drop-off zones where the passenger was picked up from the “East Harlem North” zone in November 2025. To do this, we can use multiple joins and max() in SQL.

Multiple joins is a process where we will perform multiple joins on the same table.

For example:


