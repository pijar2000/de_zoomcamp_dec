# Homework 4 Guideline

By Pijar HM

## 1. Before you start

- First make service account with privilage of bigquery admin and storage admin (all access to bigquery and gcs bucket feature)

- copy your json credentials file to your dbt user folder, for me it's in `C:\Users\pijar2000\.dbt\`

- Then you can ingest `yellow_taxi` and `green_taxi` data from 2019-2020 to your storage bucket, make the dataset with yellow and green trip data in big query (step module 3)

Then install dbt on your pc

```bash
pip install dbt-core
pip install dbt-bigquery
```

after that you can go to your folder where you can want initialize your dbt project with you project name

```bash
dbt init zoomcamp_dbt_pijar
```

- On init process you will be questioned by dbt project engine, choose big query, then service account as auth type, then you need path to your json credential files, and your gcp project id, choose 4 thread

<img width="359" height="504" alt="image" src="https://github.com/user-attachments/assets/b9cfa963-c0fb-405e-a728-0ad798567e75" />

you will see something like this 
but a few files not appear here like  `packages.yml`

you need copy these file from data enginering zoomcamp repo here

- https://github.com/DataTalksClub/data-engineering-zoomcamp/tree/main/04-analytics-engineering/taxi_rides_ny

The most importan file here is
- `packages.yml`
- `package-lock.yml`

all file in folder
- `macros`
- `models`
- `seeds`

after that you can install package that dbt needs with bash command down there, the packages detail in `packages.yml`, because of that this is important file

```bash
dbt deps
```

So here's the concept, dbt has modules folder, that's where you can modify the  `sources.yml` and `schema.yml`

- `sources.yml` mean you can modify your table pattern, here you should modify based on your tables in bigquery
- `schema.yml` mean you can determine your data parameter limit for your tables

- Open folder modules -> staging -> `sources.yml`
- modify the file, change GCP_PROJECT_ID to your project id, add line `identifier` to identify our table name, don't forget to modify green taxi and yellow taxi section in the file

```yml
rces:
  - name: raw
    description: Raw taxi trip data from NYC TLC
    #change zoomcamp-pijar-3 with your projetc id
    database: |
      {%- if target.type == 'bigquery' -%}
        {{ env_var('GCP_PROJECT_ID', 'zoomcamp-pijar-3') }}
      {%- else -%}
        taxi_rides_ny
      {%- endif -%}
    schema: |
      {%- if target.type == 'bigquery' -%}
        nytaxi
      {%- else -%}
        prod
      {%- endif -%}
    freshness:
      warn_after: { count: 24, period: hour }
      error_after: { count: 48, period: hour }
    tables:
      - name: green_tripdata
        identifier: green_tripdata_2019_2020 # add line with our table name in bigquery
        description: Raw green taxi trip records
        loaded_at_field: lpep_pickup_datetime
        columns:
```
- this is only green taxi section you should change your yellow taxi section too, scroll down in the file

The most Important thing also is you should edit your profile file `profiles.yml` in
`C:\Users\pijar2000\.dbt`

- dbt has concept to run in development environment and production environment, when you run in dev environtment (sandbox) you can trial and error with your dbt recipe

```yml
zoomcamp_dbt_pijar:
  target: dev
  outputs:
    # --- DEV Environtment ---
    dev:
      dataset: dbt_pijar_dataset
      job_execution_timeout_seconds: 300
      job_retries: 1
      keyfile: C:\Users\pijar2000\.dbt\zoomcamp-pijar-3-key.json
      location: US
      method: service-account
      priority: interactive
      project: zoomcamp-pijar-3
      threads: 4
      type: bigquery

    # --- PROD Environtment ---
    prod:
      dataset: dbt_pijar_dataset_prod
      job_execution_timeout_seconds: 300
      job_retries: 1
      keyfile: C:\Users\pijar2000\.dbt\zoomcamp-pijar-3-key.json
      location: US
      method: service-account
      priority: interactive
      project: zoomcamp-pijar-3
      threads: 4
      type: bigquery
```

- After that you can try to initialize your dbt build, run in your terminal with

```bash
dbt build --target prod
```
if succed you should see something like this in your gcp

<img width="382" height="670" alt="image" src="https://github.com/user-attachments/assets/a10fc28e-3d4b-4a4b-976c-1adbf8becd65" />

