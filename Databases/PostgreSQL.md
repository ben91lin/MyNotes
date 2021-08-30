# PostgreSQL

## Database

```sql
    createdb dbname
    dropdb dbname
    psql dbname -- use database
```

## Table

```sql
    CREATE TABLE weather (
        city            varchar(80),
        temp_lo         int,           -- low temperature
        temp_hi         int,           -- high temperature
        prcp            real,          -- precipitation
        date            date
    );

    CREATE TABLE cities (
        name            varchar(80),
        location        point
    );
```

```sql
    DROP TABLE tablename;
```
## Insert

If the values aren't number, should be used apostrophe('value').

```sql
    INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');

    INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
        VALUES ('San Francisco', 43, 57, 0.0, '1994-11-29');

    --copy data from text file
    COPY weather FROM '/home/user/weather.txt'; 
```

## SELECT

```sql
    SELECT * FROM weather;

    SELECT city, temp_lo, temp_hi, prcp, date FROM weather;

    -- expression
    SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;

    -- where
    SELECT * FROM weather
        WHERE city = 'San Francisco' AND prcp > 0.0;

    -- order
    SELECT * FROM weather
        ORDER BY city, temp_lo;

    -- distinct, not duplicate
    SELECT DISTINCT city
        FROM weather;

    -- inner join
    SELECT weather.city, weather.temp_lo, weather.temp_hi, weather.prcp, weather.date, cities.location
        FROM weather, cities
        WHERE cities.name = weather.city;

    -- left outer join
    SELECT *
        FROM weather LEFT OUTER JOIN cities ON (weather.city = cities.name);

    -- self join
    SELECT W1.city, W1.temp_lo AS low, W1.temp_hi AS high,
        W2.city, W2.temp_lo AS low, W2.temp_hi AS high
        FROM weather W1, weather W2
        WHERE W1.temp_lo < W2.temp_lo
        AND W1.temp_hi > W2.temp_hi;

    -- rename table
    SELECT *
        FROM weather w, cities c
        WHERE w.city = c.name;
```

## UPDATE

```sql
    UPDATE weather
        SET temp_hi = temp_hi - 2,  temp_lo = temp_lo - 2
        WHERE date > '1994-11-28';
```

## DELETE

```sql
    DELETE FROM weather WHERE city = 'Hayward';

    -- attention!! del all row.
    DELETE FROM tablename;
```

## Reference

https://docs.postgresql.tw/