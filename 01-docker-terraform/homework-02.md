# Question 2

Given the `docker-compose.yaml`, what hostname and port should pgAdmin use to connect to the Postgres database? (1 point)

1. postgres:5433
2. localhost:5432
3. db:5433
4. postgres:5432
5. db:5432

## Answer

Take a look at the `docker-compose.yaml` file:

```bash
...
image: postgres:18
    environment:
      POSTGRES_USER: "root"
      POSTGRES_PASSWORD: "root"
      POSTGRES_DB: "ny_taxi"
    volumes:
      - "ny_taxi_postgres_data:/var/lib/postgresql"
    ports:
      - "5432:5432"
...
```

You can see that the hostname is `localhost` and the port is `5432`.
So, the answer is `2. localhost:5432`.

## Answer
> 2. localhost:5432