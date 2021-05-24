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

## 0 SELECT basics
1.
```
SELECT name FROM world
WHERE name = 'germany'
```
2.
```
SELECT name, population FROM world
WHERE name IN ('sweden', 'norway', 'denmark')
```
3.
```
SELECT name, area FROM world
WHERE area BETWEEN 200000 AND 250000
```

## 1 SELECT name
1.
```
SELECT name FROM world
WHERE name LIKE 'y%'
```
2.
```
SELECT name FROM world
WHERE name LIKE '%y'
```
3.
```
SELECT name FROM world
WHERE name LIKE '%x%'
```
4.
```
SELECT name FROM world
WHERE name LIKE '%land'
```
5.
```
SELECT name FROM world
WHERE name LIKE 'c%ia'
```
6.
```
SELECT name FROM world
WHERE name LIKE '%oo%'
```
7.
```
SELECT name FROM world
WHERE name LIKE '%a%a%a%'
```
8.
```
SELECT name FROM world
WHERE name LIKE '_t%'
```
9.
```
SELECT name FROM world
WHERE name LIKE '%o__o%'
```
10.
```
SELECT name FROM world
WHERE name LIKE '____'
```
11.
```
SELECT name FROM world
WHERE capital = name
```
12.
