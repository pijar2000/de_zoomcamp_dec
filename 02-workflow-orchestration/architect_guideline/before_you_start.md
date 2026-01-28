## Installing Kestra

Guideline by Pijar

- Run this

```bash
cd 02-workflow-orchestration
docker compose up -d
```

Kestra will be pulled in docker, based on docker yaml the we can acces on

- Keep in mind that this kestra also insttalling postgres on port 5432 of your pc.

- If you want access the database, but your port 5432 is not empty (for example you have postgres installed on 5432, you should move it to another port) for me it's like this

```yaml
pgdatabase:
  image: postgres:18
  environment:
    POSTGRES_USER: root
    POSTGRES_PASSWORD: root
    POSTGRES_DB: ny_taxi
  ports:
    - "5442:5432" # host port 5442 → container port 5432
```

- Then, you can access in your localhost port of 5442 in dbeaver od pgadmin with database name `ny_taxi`

- After you done with your kestra set-up you shoul ingest the remaining data of `ny_taxi` from 2019 to 2021, you can modified the flow corresponding to your needs

- the flow name is `05_postgres_taxi.yaml` load the yaml to flow managament with create flow

- paste the code to flow code

- the important part for backfill is here

```yaml
variables:
  file: "{{inputs.taxi}}_tripdata_{{trigger.date | date('yyyy-MM')}}.csv"
  staging_table: "public.{{inputs.taxi}}_tripdata_staging"
  table: "public.{{inputs.taxi}}_tripdata"
  data: "{{outputs.extract.outputFiles[inputs.taxi ~ '_tripdata_' ~ (trigger.date | date('yyyy-MM')) ~ '.csv']}}"
```

- You will backfill (it means load the data from exact periode of time to one another), clict trigger then click backfill, fill it to 2019 to 2021
