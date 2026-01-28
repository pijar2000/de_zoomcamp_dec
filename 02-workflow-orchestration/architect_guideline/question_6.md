## Question 6

How would you configure the timezone to New York in a Schedule trigger?

- The timezone trigger would be placed here in flow code

```yaml
triggers:
  - id: green_schedule
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "0 9 1 * *"
    timezone: # Here you will input the timezone
    inputs:
      taxi: green

  - id: yellow_schedule
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "0 10 1 * *"
    timezone: # Here you will input the timezone
    inputs:
      taxi: yellow
```

- You can look at documentation here

https://kestra.io/docs/workflow-components/triggers/schedule-trigger
