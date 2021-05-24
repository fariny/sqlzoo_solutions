# SQL Zoo solutions

- **0 SELECT basics**
- **1 SELECT name**
- **2 SELECT from World**
- **3 SELECT from Nobel**
- **4 SELECT within SELECT**
- **5 SUM and COUNT**
- **6 JOIN**
- **7 More JOIN operations**
- **8 Using Null**
- **8+ Numeric examples**

## 0 SELECT basics
1.
```sql
SELECT name FROM world
WHERE name = 'germany'
```
2.
```sql
SELECT name, population FROM world
WHERE name IN ('sweden', 'norway', 'denmark')
```
3.
```sql
SELECT name, area FROM world
WHERE area BETWEEN 200000 AND 250000
```

## 1 SELECT name
1.
```sql
SELECT name FROM world
WHERE name LIKE 'y%'
```
2.
```sql
SELECT name FROM world
WHERE name LIKE '%y'
```
3.
```sql
SELECT name FROM world
WHERE name LIKE '%x%'
```
4.
```sql
SELECT name FROM world
WHERE name LIKE '%land'
```
5.
```sql
SELECT name FROM world
WHERE name LIKE 'c%ia'
```
6.
```sql
SELECT name FROM world
WHERE name LIKE '%oo%'
```
7.
```sql
SELECT name FROM world
WHERE name LIKE '%a%a%a%'
```
8.
```sql
SELECT name FROM world
WHERE name LIKE '_t%'
```
9.
```sql
SELECT name FROM world
WHERE name LIKE '%o__o%'
```
10.
```sql
SELECT name FROM world
WHERE name LIKE '____'
```
11.
```sql
SELECT name FROM world
WHERE capital = name
```
12.
```sql
SELECT name FROM world
WHERE capital = concat(name, ' city')
```
13.
```sql

```
14.
```sql

```
15.
```sql

```
## 2 SELECT from World
1.
```sql
SELECT name, continent, population FROM world
```
2.
```sql
SELECT name FROM world
WHERE population >= 200000000
```
3.
```sql
SELECT name, GDP/population FROM world
WHERE population >= 200000000
```
4.
```sql
SELECT name, population/1000000
FROM world
WHERE continent = 'south america'
```
5.
```sql
SELECT name, population FROM world
WHERE name IN ('france', 'germany', 'italy')
```
6.
```sql
SELECT name FROM world
WHERE name LIKE '%united%'
```
7.
```sql
SELECT name, population, area FROM world
WHERE area > 3000000
OR
population > 250000000
```
8.
```sql

```
9.
```sql

```
10.
```sql

```
11.
```sql

```
12.
```sql

```
13.
```sql

```
