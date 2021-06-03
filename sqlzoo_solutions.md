# SQL Zoo solutions

- **0 SELECT basics**
- **1 SELECT name**
- **2 SELECT from World**
- **3 SELECT from Nobel**
- **4 SELECT within SELECT**
- **5 SUM and COUNT**
- **5.5 Nobel Prizes: aggregate functions**
- **6 JOIN**
- **Old JOIN**
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
6.
```sql
SELECT name FROM world
WHERE GDP > ALL
   (SELECT GDP FROM world
   WHERE continent = 'europe'
   AND GDP > 0)
```
7.
```sql
SELECT continent, name, area FROM world x
WHERE area >= ALL
   (SELECT area FROM world y
   WHERE x.continent = y.continent)
```
8.
```sql
SELECT continent, name FROM world x
WHERE name <= ALL
   (SELECT name FROM world y
   WHERE x.continent = y.continent)
```
9.
```sql
SELECT name, continent, population FROM world x
WHERE 25000000 >= ALL
   (SELECT population FROM world y
   WHERE x.continent = y.continent)
```
10.
```sql

```
## 5 SUM and COUNT
1.
```sql
SELECT SUM(population) FROM world
```
2.
```sql
SELECT DISTINCT(continent) FROM world
```
3.
```sql
SELECT SUM(GDP) FROM world
WHERE continent = 'africa'
```
4.
```sql
SELECT COUNT(name) FROM world
WHERE area >= 1000000
```
5.
```sql
SELECT SUM(population) FROM world
WHERE name IN ('estonia', 'latvia', 'lithuania')
```
6.
```sql
SELECT continent, COUNT(name) FROM world
GROUP BY continent
HAVING COUNT(name)
```
7.
```sql
SELECT continent, COUNT(name) FROM world
WHERE population >= 10000000
GROUP BY continent
HAVING COUNT(name)
```
8.
```sql
SELECT continent FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```
## 5.5 Nobel Prizes: aggregate functions
1.
```sql
SELECT COUNT(winner) FROM nobel
```
2.
```sql
SELECT DISTINCT(subject) FROM nobel
```
3.
```sql
SELECT COUNT(winner) FROM nobel
WHERE subject = 'physics'
```
4.
```sql
SELECT subject, COUNT(winner) FROM nobel
GROUP BY subject
HAVING COUNT(winner)
```
5.
```sql
SELECT subject, MIN(yr) FROM nobel
GROUP BY subject
HAVING MIN(yr)
```
6.
```sql
SELECT subject, COUNT(winner) FROM nobel
WHERE yr = 2000
GROUP BY subject
HAVING COUNT(winner)
```
7.
```sql
SELECT subject, COUNT(DISTINCT(winner)) FROM nobel
GROUP BY subject
HAVING COUNT(DISTINCT(winner))
```
8.
```sql
SELECT subject, COUNT(DISTINCT(yr)) FROM nobel
GROUP BY subject
HAVING COUNT(DISTINCT(yr))
```
9.
```sql
SELECT yr FROM nobel
WHERE subject = 'physics'
GROUP BY yr
HAVING COUNT(winner) = 3
```
10.
```sql
SELECT winner FROM nobel
GROUP BY winner
HAVING COUNT(winner) > 1
```
11.
```sql
SELECT winner FROM nobel
GROUP BY winner
HAVING COUNT(DISTINCT(subject)) > 1
```
12.
```sql
SELECT yr, subject FROM nobel
WHERE yr >= 2000
GROUP BY yr, subject
HAVING COUNT(winner) = 3
```
## 6 JOIN
1.
```sql
SELECT matchid, player FROM goal
WHERE teamid = 'ger'
```
2.
```sql
SELECT id, stadium, team1, team2 FROM game
WHERE id = 1012
```
3.
```sql
SELECT player, teamid, stadium, mdate
FROM game JOIN goal ON (game.id = matchid)
WHERE teamid = 'ger'
```
4.
```sql
SELECT team1, team2, player
FROM game JOIN goal ON (game.id = matchid)
WHERE player LIKE 'mario%'
```
5.
```sql
SELECT player, teamid, coach, gtime
FROM goal JOIN eteam ON (teamid = eteam.id)
WHERE gtime <= 10
```
6.
```sql
SELECT mdate, teamname
FROM game JOIN eteam ON (team1 = eteam.id)
WHERE coach = 'fernando santos'
```
7.
```sql
SELECT player
FROM goal JOIN game ON (matchid = game.id)
WHERE stadium = 'national stadium, warsaw'
```
8.
```sql
SELECT DISTINCT(player)
FROM goal JOIN game ON (matchid = game.id)
WHERE teamid != 'ger' AND team1 = 'ger'
OR
teamid != 'ger' AND team2 = 'ger'
```
9.
```sql
SELECT teamname, COUNT(player)
FROM goal JOIN eteam ON (teamid = eteam.id)
GROUP BY teamname
```
10.
```sql
SELECT stadium, COUNT(player)
FROM game JOIN goal ON (game.id = matchid)
GROUP BY stadium
```
11.
```sql
SELECT matchid, mdate, COUNT(player)
FROM game JOIN goal ON (game.id = matchid)
WHERE team1 = 'pol' OR team2 = 'pol'
GROUP BY matchid, mdate
```
12.
```sql
SELECT matchid, mdate, COUNT(player)
FROM game JOIN goal ON (game.id = matchid)
WHERE teamid = 'ger'
GROUP BY matchid, mdate
```
13.
```sql

```
## Old JOIN
1.
```sql
SELECT who, name
FROM ttms JOIN country ON (ttms.country = country.id)
WHERE games = 2000
```
2.
```sql
SELECT who, color
FROM ttms JOIN country ON (ttms.country = country.id)
WHERE name = 'sweden'
```
3.
```sql
SELECT games
FROM ttms JOIN country ON (ttms.country = country.id)
WHERE name = 'china' AND color = 'gold'
```
4.
```sql
SELECT who
FROM ttws JOIN games ON (ttws.games = games.yr)
WHERE city = 'barcelona'
```
5.
```sql
SELECT city, color
FROM ttws JOIN games ON (ttws.games = games.yr)
WHERE who = 'jing chen'
```
6.
```sql
SELECT who, city
FROM ttws JOIN games ON (ttws.games = games.yr)
WHERE color = 'gold'
```
7.
```sql
SELECT games, color
FROM ttmd JOIN team ON (ttmd.team = team.id)
WHERE name = 'yan sen'
```
8.
```sql
SELECT name
FROM ttmd JOIN team ON (ttmd.team = team.id)
WHERE color = 'gold' AND games = 2004
```
9.
```sql
SELECT name
FROM ttmd JOIN team ON (ttmd.team = team.id)
WHERE country = 'fra'
```
## 7 More JOIN operations
1.
```sql
SELECT id, title FROM movie
WHERE yr = 1962
```
2.
```sql
SELECT yr FROM movie
WHERE title = 'citizen kane'
```
3.
```sql
SELECT id, title, yr FROM movie
WHERE title LIKE '%star trek%'
ORDER BY yr
```
4.
```sql
SELECT id FROM actor
WHERE name = 'glenn close'
```
5.
```sql
SELECT id FROM movie
WHERE title = 'casablanca'
```
6.
```sql
SELECT name
FROM actor JOIN casting ON (actor.id = casting.actorid)
WHERE movieid = 11768
```
7.
```sql
SELECT name
FROM actor
  JOIN casting ON (actor.id = casting.actorid)
  JOIN movie ON (casting.movieid = movie.id)
WHERE title = 'alien'
```
8.
```sql
SELECT title
FROM movie
  JOIN casting ON (movie.id = casting.movieid)
  JOIN actor ON (casting.actorid = actor.id)
WHERE name = 'harrison ford'
```
9.
```sql
SELECT title
FROM movie
  JOIN casting ON (movie.id = casting.movieid)
  JOIN actor ON (casting.actorid = actor.id)
WHERE name = 'harrison ford' AND ord != 1
```
10.
```sql
SELECT title, name
FROM movie
  JOIN casting ON (movie.id = casting.movieid)
  JOIN actor ON (casting.actorid = actor.id)
WHERE yr = 1962 AND ord = 1
```
11.
```sql
SELECT yr, COUNT(title)
FROM movie
  JOIN casting ON (movie.id = casting.movieid)
  JOIN actor ON (casting.actorid = actor.id)
WHERE name = 'rock hudson'
GROUP BY yr
HAVING COUNT(yr) > 2
```
12.
```sql

```
13.
```sql
SELECT name
FROM actor
  JOIN casting ON (actor.id = casting.actorid)
WHERE ord = 1
GROUP BY name
HAVING COUNT(ord) >= 15
```
14.
```sql

```
15.
```sql

```
