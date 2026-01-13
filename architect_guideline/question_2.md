# Question 2. Understanding Docker networking and docker-compose

```yaml
services:
  db:
    container_name: postgres
    image: postgres:17-alpine
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "postgres"
      POSTGRES_DB: "ny_taxi"
    ports:
      - "5433:5432"
    volumes:
      - vol-pgdata:/var/lib/postgresql/data

  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4:latest
    environment:
      PGADMIN_DEFAULT_EMAIL: "pgadmin@pgadmin.com"
      PGADMIN_DEFAULT_PASSWORD: "pgadmin"
    ports:
      - "8080:80"
    volumes:
      - vol-pgadmin_data:/var/lib/pgadmin

volumes:
  vol-pgdata:
    name: vol-pgdata
  vol-pgadmin_data:
    name: vol-pgadmin_data
```

### Guidleine by pijar for question 2
- The question is which host and port that postgres use in this setting

we need to know which is our PC port or Docker port, in this case
ports: - '5433:5432'

you also can read this documentation to figure out which is pc port or container port

Docker documentation regarding hostname and port :
https://docs.docker.com/reference/compose-file/services/?utm_source=copilot.com#ports

based on this data, the fastest method is to try docker-compose up directly and find it yourself :

1. go to your folder make `docker-compose.yaml ` file
2. paste setup above
3. open docker desktop -> go to terminal and run `docker-compose up`
4. it shoul pulling pgadmin and postgres services
5. after that try to open in http://localhost:8080/ (this is pc port for pgadmin)
6. what is username and password? you can figure out in setup above
   - PGADMIN_DEFAULT_EMAIL:
   - PGADMIN_DEFAULT_PASSWORD:
7. click add new server
8. fill the name (anything)
9. go to connection
10. <img width="1068" height="833" alt="image" src="https://github.com/user-attachments/assets/97c57df7-076c-4346-878f-7d57640a8ca1" />

11. you shoul fill the host based on above setup, according to docker documentation in link above it should be

    - hostname : db, port: 5432

12. fill the rest according to this setup

```yaml
db:
  container_name: postgres
  image: postgres:17-alpine
  environment:
    POSTGRES_USER: "postgres"
    POSTGRES_PASSWORD: "postgres"
    POSTGRES_DB: "ny_taxi"
  ports:
    - "5433:5432"
  volumes:
    - vol-pgdata:/var/lib/postgresql/data
```

13. The database should work, if that database work, it means you input the right hostname and port for the question
