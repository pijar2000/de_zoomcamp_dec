# Question 1 - 5

### Question 1. dbt Lineage and Execution

Given a dbt project with the following structure:

```
models/
├── staging/
│   ├── stg_green_tripdata.sql
│   └── stg_yellow_tripdata.sql
└── intermediate/
    └── int_trips_unioned.sql (depends on stg_green_tripdata & stg_yellow_tripdata)
```

If you run `dbt run --select int_trips_unioned`, what models will be built?

- this is theoritic question, you can tried find it here, don't forget to chech another forum and tried it yourself in terminal and analyze the result
- https://docs.getdbt.com/reference/node-selection/syntax

### Question 2. dbt Tests

You've configured a generic test like this in your `schema.yml`:

```yaml
columns:
  - name: payment_type
    data_tests:
      - accepted_values:
          arguments:
            values: [1, 2, 3, 4, 5]
            quote: false
```

Your model `fct_trips` has been running successfully for months. A new value `6` now appears in the source data.

What happens when you run `dbt test --select fct_trips`?

- You can also tried it yourself and analyze the error, edit the `schema.yml` in folder models -> marts -> `schema.yml`
- scroll down all the way until you find something like this

```yml
 - name: payment_type
        description: Payment method code
        data_type: integer
      - name: payment_type_description
        description: Human-readable payment method description
        data_type: string
```

edit it to become like this 

```yml
- name: payment_type
        description: Payment method code
        data_type: integer
        data_tests:
          - accepted_values:
              arguments:
                values: [1, 2, 3, 4, 5]
                quote: false
      - name: payment_type_description
        description: Human-readable payment method description
        data_type: string
```

then run the command and analyze it the output


### Question 3. Counting Records in `fct_monthly_zone_revenue`

After running your dbt project, query the `fct_monthly_zone_revenue` model.

What is the count of records in the `fct_monthly_zone_revenue` model?

<img width="559" height="200" alt="image" src="https://github.com/user-attachments/assets/33991d3d-6800-4c3f-a311-f38a67583845" />

- use count function of sql in big query for table fct_monthly_zone_revenue, i believe in this state you already familiar with count function


### Question 4. Best Performing Zone for Green Taxis (2020)

Using the `fct_monthly_zone_revenue` table, find the pickup zone with the **highest total revenue** (`revenue_monthly_total_amount`) for **Green** taxi trips in 2020.

- also use sql function to order by the highest revenue and where filter for years, I believe in your skill

### Question 5. Green Taxi Trip Counts (October 2019)

Using the `fct_monthly_zone_revenue` table, what is the **total number of trips** (`total_monthly_trips`) for Green taxis in October 2019?

- Use where filter for year and sum function for this problem, i believe in your skill
