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
SELECT population FROM world
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
WHERE capital = CONCAT(name, ' city')
```
13.
```sql
SELECT capital, name FROM world
WHERE capital LIKE CONCAT(name, '%')
```
14.
```sql
SELECT capital, name FROM world
WHERE capital LIKE CONCAT(name, '%')
AND capital <> name
```
15.
```sql
SELECT name, REPLACE(capital, name, '') AS extension
FROM world
WHERE capital LIKE CONCAT(name, '%')
AND capital <> name
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
SELECT name, population, area FROM world
WHERE area > 3000000
XOR
population > 250000000
```
9.
```sql
SELECT name,
ROUND(population/1000000,2),
ROUND(GDP/1000000000,2)
FROM world
WHERE continent = 'south america'
```
10.
```sql
SELECT name, ROUND(GDP/population,-3)
FROM world
WHERE GDP >= 1000000000000
```
11.
```sql
SELECT name, capital FROM world
WHERE LENGTH(name) = LENGTH(capital)
```
12.
```sql
SELECT name, capital FROM world
WHERE LEFT(name,1) = LEFT(capital,1)
AND name <> capital
```
13.
```sql
SELECT name FROM world
WHERE name NOT LIKE '% %'
AND name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
```
## 3 SELECT from Nobel
1.
```sql
SELECT * FROM nobel
WHERE yr = 1950
```
2.
```sql
SELECT winner FROM nobel
WHERE yr = 1962
AND subject = 'literature'
```
3.
```sql
SELECT yr, subject FROM nobel
WHERE winner = 'albert einstein'
```
4.
```sql
SELECT winner FROM nobel
WHERE subject = 'peace'
AND yr >= 2000
```
5.
```sql
SELECT * FROM nobel
WHERE subject = 'literature'
AND yr BETWEEN 1980 AND 1989
```
6.
```sql
SELECT * FROM nobel
WHERE winner IN ('theodore roosevelt',
                  'woodrow wilson',
                  'jimmy carter',
                  'barack obama')
```
7.
```sql
SELECT winner FROM nobel
WHERE winner LIKE 'john%'
```
8.
```sql
SELECT yr, subject, winner FROM nobel
WHERE subject = 'physics' AND yr = 1980
OR
subject = 'chemistry' AND yr = 1984
```
9.
```sql
SELECT yr, subject, winner FROM nobel
WHERE yr = 1980
AND subject NOT IN ('chemistry', 'medicine')
```
10.
```sql
SELECT yr, subject, winner FROM nobel
WHERE subject = 'medicine' AND yr < 1910
OR
subject = 'literature' AND yr >= 2004
```
11.
```sql
# ALT + 0 2 2 0 for Ü / ALT + 0 2 5 2 for ü (windows)

SELECT * FROM nobel
WHERE winner LIKE 'peter grünberg'
```
12.
```sql
# Escaping single quotes:
# You can't put a single quote in a quote string directly. You can use two single quotes within a quoted string.

SELECT * FROM nobel
WHERE winner = 'eugene o''neill'
```
13.
```sql
SELECT winner, yr, subject FROM nobel
WHERE winner LIKE 'sir%'
ORDER BY yr DESC, winner
```
14.
```sql
SELECT winner, subject FROM nobel
WHERE yr = 1984
ORDER BY subject IN('chemistry', 'physics'), subject, winner
```
## 4 SELECT within SELECT
1.
```sql
SELECT name FROM world
WHERE population >
  (SELECT population FROM world
  WHERE name = 'russia')
```
2.
```sql
SELECT name FROM world
WHERE continent = 'europe'
AND GDP/population >
    (SELECT GDP/population FROM world
    WHERE name = 'united kingdom')
```
3.
```sql
SELECT name, continent FROM world
WHERE continent IN
  (SELECT continent FROM world
  WHERE name IN ('argentina', 'australia'))
ORDER BY name
```
4.
```sql
SELECT name, population FROM world
WHERE population >
  (SELECT population FROM world
  WHERE name = 'canada')
AND population <
  (SELECT population FROM world
  WHERE name = 'poland')
```
5.
```sql
SELECT name, 
  CONCAT(
    ROUND(
      population / (SELECT population FROM world WHERE name = 'germany') * 100
    ,0)
  ,'%')
AS percentage
FROM world
WHERE continent = 'europe'
```
