## Installing Kestra

Guideline by Pijar

- Run this

```bash
cd 02-workflow-orchestration
docker compose up -d
```

<img width="689" height="452" alt="Screenshot 2026-01-28 223733" src="https://github.com/user-attachments/assets/21a20659-b7c0-4191-8c1e-0f4867637fa2" />

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

<img width="565" height="300" alt="Screenshot 2026-01-28 235904" src="https://github.com/user-attachments/assets/438f0e0f-f007-4fa0-8ecb-143141c65396" />

- paste the code to flow code

- the important part for backfill is here

```yaml
variables:
  file: "{{inputs.taxi}}_tripdata_{{trigger.date | date('yyyy-MM')}}.csv"
  staging_table: "public.{{inputs.taxi}}_tripdata_staging"
  table: "public.{{inputs.taxi}}_tripdata"
  data: "{{outputs.extract.outputFiles[inputs.taxi ~ '_tripdata_' ~ (trigger.date | date('yyyy-MM')) ~ '.csv']}}"
```

<img width="1397" height="522" alt="Screenshot 2026-01-29 000138" src="https://github.com/user-attachments/assets/e91f1bcd-f73d-4df1-9d0f-cc4f05b7f53e" />

- You will backfill (it means load the data from exact periode of time to one another), clict trigger then click backfill, fill it to 2019 to 2021



