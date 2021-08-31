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

## VIEW

```sql
CREATE VIEW myview AS
    SELECT city, temp_lo, temp_hi, prcp, date, location
        FROM weather, cities
        WHERE city = name;

SELECT * FROM myview;
```

## FOREIGN KEY

Check the city before insert weather.
```sql
CREATE TABLE cities (
        city     varchar(80) primary key,
        location point
);

CREATE TABLE weather (
        city      varchar(80) references cities(city),
        temp_lo   int,
        temp_hi   int,
        prcp      real,
        date      date
);
```

## TRANSACTION

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100.00
    WHERE name = 'Alice';
-- etc etc
COMMIT;
```

## INHERTANCE

```sql
CREATE TABLE cities (
  name       text,
  population real,
  altitude   int     -- (in ft)
);

CREATE TABLE capitals (
  state      char(2)
) INHERITS (cities);
```

```sql
-- all cities
SELECT name, altitude
    FROM cities
    WHERE altitude > 500;

-- non capital
SELECT name, altitude
    FROM ONLY cities
    WHERE altitude > 500;
```

## SPECIAL CHARATAR

Operator | Function |
--|--|
$ | 其後接著數字的話，用來表示函數宣告或預備指令的參數編號。其他的用法還有識別項的一部份，或是錢字引號常數。 |
( ) | 一般用來強調表示式並且優先運算。還有某些情況用於表示某些 SQL 指令的部份的必要性。 |
[ ] | 用於組成陣列的各個元素。詳情請參閱 8.15 節有關於陣列的內容。 |
, | 用於一般語法上的結構需要，來分隔列表中的單元。 |
; | 表示 SQL 指令的結束。它不能出現在指令中的其他位置，除非是在字串常數當中，或是引號識別項。 |
: | 用在取得陣列的小項。（參閱 8.15 節）在某些 SQL 分支（篏入式 SQL 之類的）中，冒號用來前置變數名稱。 |
\* | 用來表示表格中所有的欄位，或複合性的內容。它也可以用於函數宣告時，不限制固定數量的參數。 |
. | 用在數值常數之中，也用於區分結構、表格、及欄位名稱。 |
-- | comment |
/* */ | multiline comment |

## Reference

https://docs.postgresql.tw/