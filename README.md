# SQL Zoo Solutions

My Solutions Of The [SQL ZOO Tutorial](https://sqlzoo.net/wiki/SQL_Tutorial)

## Sections

0. [SELECT Basics](#select-basics)
1. [SELECT Names](#select-names)
2. [SELECT From World](#select-from-world)
3. [SELECT From Nobel](#select-from-nobel)
4. [SELECT Within SELECT](#select-within-select)
5. [SUM And COUNT](#sum-and-count)
6. [The JOIN Operation](#join)
7. [More JOIN Operations](#more-join)
8. [Using NULL](#null)

# SELECT Basics

## 1. **Show the population of Germany.**

```sql
SELECT population
  FROM world
 WHERE name = 'Germany'
```

## 2. **Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.**

```sql
SELECT name, population
  FROM world
 WHERE name IN ('Sweden', 'Norway', 'Denmark')
```

## 3. **Show the country and the area for countries with an area between 200,000 and 250,000.**

```sql
  SELECT name, area
    FROM world
   WHERE area BETWEEN 200000 AND 250000
```

# SELECT Names

## 1. **Find the country that start with Y.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE 'y%'
```

Or

```sql
  SELECT name
    FROM world
   WHERE left(name,1) = 'Y'
```

## 2. **Find the countries that end with y.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%y'
```

Or

```sql
  SELECT name
    FROM world
   WHERE right(name,1) = 'Y'
```

## 3. **Find the countries that contain the letter x.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%x%'
```

## 4. **Find the countries that end with land.**

```sql
  SELECT name FROM world
  WHERE name LIKE '%land'
```

Or

```sql
  SELECT name
    FROM world
   WHERE RIGHT(name, 4) = 'land'
```

## 5. **Find the countries that start with C and end with ia.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE 'C%'
     AND name LIKE '%ia'
```

Or

```sql
  SELECT name
    FROM world
   WHERE LEFT(name, 1) LIKE 'C'
     AND RIGHT(name, 2) LIKE 'ia'
```

## 6. **Find the country that has "oo" in the name.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%oo%'
```

## 7. **Find the countries that have [three or more a in the name](https://stackoverflow.com/questions/22748899/check-if-data-contains-multiple-instances-of-the-same-character)**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%a%a%a%'
```

## 8. **Find the countries that have "t" as the second character.**

```sql
  SELECT name
    FROM WORLD
   WHERE name LIKE '_t%'
```

## 9. **Find the countries that have two "o" characters separated by two others.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%o__o%'
```

## 10. **Find the countries that have exactly four characters.**

```sql
  SELECT name
    FROM world
   WHERE LEN(name) = 4
```

## 11. **Find the country where the name is the capital city.**

```sql
  SELECT name
    FROM world
   WHERE name = capital
```

## 12. **Find the country where the capital is the country plus "City".**

```sql
  SELECT name
    FROM world
   WHERE capital = concat(name, ' City')
```

## 13. **Find the capital and the name where the [capital includes the name of the country](https://stackoverflow.com/questions/1398720/how-to-use-like-with-column-name).**

```sql
  SELECT capital, name
    FROM world
   WHERE capital LIKE concat(name, '%')
```

## 14. **Find the capital and the name where the capital is an extension of name of the country.**

```sql
  SELECT capital, name
    FROM world
   WHERE capital LIKE concat(name, '_%')
```

## 15. **Show the name and the extension where the capital is an extension of name of the country.**

```sql
  SELECT name, SUBSTRING(capital, LEN(name)+1, LEN(capital) ) AS extention
    FROM world
   WHERE capital LIKE concat(name,'_%')
```

# SELECT From World

## 1. **[Read the notes about this table](https://sqlzoo.net/wiki/Read_the_notes_about_this_table.). Observe the result of running this SQL command to show the name, continent and population of all countries.**

```sql
  SELECT name, continent, population
    FROM world
```

## 2. **Give the `name` and the per capita GDP for those countries with a population of at least 200 million.**

```sql
  SELECT name, (gdp / population ) AS per_capita
    FROM world
   WHERE population > 200000000
```

## 4. **Show the `name` and `population` in millions for the countries of the `continent` 'South America'. Divide the population by 1000000 to get population in millions.**

```sql
  SELECT name, (population / 1000000) AS population_millions
    FROM world
   WHERE continent = 'South America'
```

## 5. **Show the `name` and `population` for France, Germany, Italy**

```sql
  SELECT name, population
    FROM world
   WHERE name IN ('France', 'Germany', 'Italy');
```

## 6. **Show the countries which have a `name` that includes the word 'United'**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%United%'
```

## 7. Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million. **Show the countries that are big by area or big by population. Show name, population and area.**

```sql
  SELECT name, population, area
    FROM world
   WHERE area > 3000000 OR population > 250000000
```

## 8. Exclusive OR (XOR). **Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area**

```sql
  SELECT name, population, area
    FROM world
   WHERE area > 3000000 AND population < 250000000
      OR area < 3000000 AND population > 250000000
```

## 9. Show the `name` and `population` in millions and the GDP in billions for the countries of the `continent` 'South America'. Use the ROUND function to show the values to two decimal places. **For South America show population in millions and GDP in billions both to 2 decimal places.**

```sql
  SELECT name, ROUND(population / 1000000, 2) AS population_in_mil,
               ROUND(gdp / 1000000000, 2) AS gdp_bils
    FROM world
   WHERE continent = 'South America'
```

## 10. Show the `name` and per-capita GDP for those countries with a GDP of at least one trillion. Round this value to the nearest 1000. **Show per-capita GDP for the trillion dollar countries to the nearest $1000.**

```sql
  SELECT name, ROUND(gdp  / population,-3)
    FROM world
   WHERE GDP > 1000000000000
```

## 11. **Show the name and capital where the name and the capital have the same number of characters.**

```sql
  SELECT name, capital
    FROM world
   WHERE LEN(name) = LEN(capital)
```

## 12. **Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.**

```sql
  SELECT name, capital
    FROM world
   WHERE LEFT(name,1) = LEFT(capital,1)
     AND name != capital
```

## 13. **Find the country that has all the vowels and no spaces in its name.**

```sql
  SELECT name
    FROM world
   WHERE name LIKE '%a%'
     AND name LIKE '%e%'
     AND name LIKE '%i%'
     AND name LIKE '%o%'
     AND name LIKE '%u%'
     AND name NOT LIKE '% %'
```

# SELECT From Nobel

## 1. **Change the query shown so that it displays Nobel prizes for 1950.**

```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

## 2. **Show who won the 1962 prize for literature.**

```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'literature'
```

## 3. **Show the year and subject that won 'Albert Einstein' his prize.**

```sql
SELECT yr, subject from nobel
 WHERE  winner = 'Albert Einstein'
```

## 4. **Give the name of the 'peace' winners since the year 2000, including 2000.**

```sql
SELECT winner, yr FROM nobel
 WHERE subject = 'peace'
  AND yr >= 2000
```

## 5. **Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.**

```sql
SELECT *
  FROM nobel
 WHERE subject = 'literature'
   AND  yr BETWEEN 1980 AND 1989
```

## 6. **Show all details of the presidential winners**

```sql
SELECT *
  FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter',
                  'Barack Obama')
```

## 7. **Show the winners with first name John.**

```sql
SELECT winner
  FROM nobel
 WHERE  winner LIKE 'John%'
```

## 8. **Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.**

```sql
SELECT *
 FROM nobel
WHERE subject = 'physics'
  AND yr = 1980
   OR  subject = 'chemistry'
  AND yr = 1984
```

## 9. **Show the year, subject, and name of winners for 1980 excluding chemistry and medicine.**

```sql
SELECT *
  FROM nobel
 WHERE yr = 1980 A
   AND subject NOT IN ('chemistry')
```

## 10. **Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004).**

```sql
SELECT *
  FROM nobel
 WHERE subject = 'medicine'
   AND yr < 1910
    OR subject = 'literature'
   AND yr >= 2004
```

## 11. **Find all details of the prize won by PETER GR??NBERG.**

```sql
SELECT *
  FROM nobel
 WHERE winner = 'PETER GR??NBERG'
```

## 12. **Find all details of the prize won by EUGENE O'NEILL.**

```sql
SELECT *
  FROM nobel
 WHERE winner = 'EUGENE O''NEILL'
```

## 13. **List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.**

```sql
SELECT winner, yr, subject
  FROM nobel
 WHERE winner LIKE 'Sir%'
  ORDER BY yr DESC, winner
```

## 14. **Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.**

```sql
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject in ('Chemistry','Physics') DESC, subject, winner
```

# SELECT Within SELECT

## 1. **List each country name where the population is larger than that of 'Russia'.**

```sql
SELECT name FROM world
  WHERE population >
           (SELECT population
              FROM world
             WHERE name='Russia')
```

## 2. **Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.**

```sql
SELECT name FROM world
 WHERE continent = 'Europe'
   AND gdp/population > (SELECT gdp/population
                           FROM world
                          WHERE name = 'United Kingdom')
```

## 3. **List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.**

```sql
SELECT name, continent
  FROM world
 WHERE continent IN (SELECT continent
                       FROM world
                      WHERE name IN ('Argentina','Australia')
                     )
 ORDER BY name
```

## 4. **Which country has a population that is more than United Kingom but less than Germany? Show the name and the population.**

```sql
SELECT name, population
  FROM world
 WHERE population > (SELECT population
                       FROM world
                      WHERE name = 'United Kingdom')
   AND population < (SELECT population
                       FROM world
                      WHERE name = 'Germany')
```

## 5. **Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.**

```sql
SELECT name, CONCAT(ROUND(population/(SELECT population
                                        FROM world
                                       WHERE name = 'Germany')*100, 0), '%')
    AS percentage
  FROM world
 WHERE continent = 'Europe'
```

## 6. **Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)**

```sql
SELECT name
  FROM world
 WHERE gdp > ALL(SELECT gdp
                    FROM world
                   WHERE continent = 'Europe'
                     AND gdp > 0)
```

## 7. **Find the largest country (by area) in each continent, show the continent, the name and the area.**

```sql
SELECT continent, name, area
  FROM world x
  WHERE area >= ALL(SELECT area
                      FROM world y
                     WHERE y.continent=x.continent
                       AND area>0)
```

## 8. **List each continent and the name of the country that comes first alphabetically.**

```sql
SELECT continent, name
  FROM world x
 WHERE name <= ALL(SELECT name
                     FROM world y
                    WHERE y.continent = x.continent)
```

## 9. **Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.**

```sql
SELECT name, continent, population
  FROM world x
 WHERE 25000000 >= ALL(SELECT population
                         FROM world y
                        WHERE x.continent = y.continent
                          AND y.population > 0)
```

## 10. **Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.**

```sql
SELECT name, continent
  FROM world x
 WHERE population >= ALL(SELECT population * 3
                           FROM world y
                          WHERE x.continent = y.continent
                            AND x.name NOT LIKE y.name)
```

# SUM And COUNT

## 1. **Show the total** `population` **of the world.**

```sql
SELECT SUM(population)
  FROM world
```

## 2. **List all the** `continents` **- just once each.**

```sql
SELECT DISTINCT continent
  FROM world
```

## 3. **Give the total** `gdp` **of Africa.**

```sql
SELECT SUM(gdp) AS total_gdp
  FROM world
 WHERE continent = 'Africa'
```

## 4. **How many countries have an** `area` **of at least 1000000.**

```sql
SELECT COUNT(name)
  FROM world
 WHERE area >= 1000000
```

## 5. **What is the total** `population` **of** `('Estonia', 'Latvia', 'Lithuania')`.

```sql
SELECT SUM(population)
  FROM world
 WHERE name in ('Estonia', 'Latvia', 'Lithuania')
```

## 6. **For each** `continent` **show the** `continent` **and number of countries.**

```sql SELECT continent, COUNT(name) AS number_of_countries
  FROM world
 GROUP BY continent
```

## 7. **For each** `continent` **show the** `continent` **and number of countries with populations of at least 10 million.**

```sql
SELECT continent, COUNT(name) AS number_of_countries
  FROM world
 WHERE population > 10000000
 GROUP BY continent
```

## 8. **List the continents that have a total population of at least 100 million.**

```sql
SELECT continent
  FROM world
 GROUP BY continent
 HAVING SUM(population) > 100000000
```

# The JOIN Operation

## 1. **Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for:** `teamid = 'GER'`

```sql
SELECT matchid, player
  FROM goal
 WHERE teamid LIKE 'GER'
```

## 2. Show id, stadium, team1, team2 for just game 1012.

```sql
SELECT id, stadium, team1, team2
  FROM game
 WHERE id = 1012
```

## 3. The code below shows the player (from the goal) and stadium name (from the game table) for every goal scored. **Modify it to show the player, teamid, stadium and mdate for every German goal.**

```sql
SELECT player,teamid, stadium, mdate
  FROM game
  JOIN goal ON (game.id=goal.matchid)
 WHERE goal.teamid = 'GER'
```

## 4. **Show the team1, team2 and player for every goal scored by a player called Mario** `player LIKE 'Mario%'`

```sql
SELECT team1, team2, player
  FROM game
  JOIN goal ON (game.id=goal.matchid)
 WHERE player LIKE 'Mario%'
```

## 5. **Show** ` player, teamid, coach, gtime` **for all goals scored in the first 10 minutes** `gtime<=10`

```sql
SELECT player, teamid, coach, gtime
  FROM goal
  JOIN eteam ON (goal.teamid = eteam.id)
 WHERE gtime <= 10
```

## 6. **List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.**

```sql
SELECT mdate, teamname
 FROM game
 JOIN eteam ON (game.team1 = eteam.id)
WHERE eteam.coach = 'Fernando Santos'
```

## 7. **List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'**

```sql
SELECT player
 FROM goal
 JOIN game on (goal.matchid = game.id)
WHERE stadium = 'National Stadium, Warsaw'
```

## 8. **Instead show the name of all players who scored a goal against Germany.**

```sql
SELECT DISTINCT player
 FROM game
 JOIN goal ON (game.id = goal.matchid)
 WHERE (game.team1 = 'GER' OR game.team2 = 'GER')
   AND goal.teamid != 'GER'
```

## 9. **Show** `teamname` **and the** `total number of goals` **scored.**

```sql
SELECT teamname, COUNT(goal.teamid) AS total_goals
  FROM eteam
  JOIN goal ON eteam.id = goal.teamid
 GROUP BY teamname
```

## 10. **Show the** `stadium` **and the** `number of goals` **scored in each** `stadium`**.**

```sql
SELECT stadium, COUNT(game.id) AS total_goals
  FROM goal
  JOIN game ON (goal.matchid = game.id)
 GROUP BY stadium
```

## 11. **For every match involving 'POL', show the** `matchid`**,** `date` **and the** `number of goals scored`**.**

```sql
SELECT matchid, mdate, COUNT(goal.teamid) AS total_goals
  FROM game
  JOIN goal ON goal.matchid = game.id
 WHERE (team1 = 'POL' OR team2 = 'POL')
 GROUP BY matchid, mdate
```

## 12. **For every match where 'GER' scored, show** `matchid`**,** `match date` **and the** `number of goals scored` **by 'GER'.**

```sql
SELECT matchid, mdate, COUNT(goal.matchid) AS total_goals
 FROM goal
 JOIN game ON (game.id = goal.matchid)
WHERE goal.teamid = 'GER'
GROUP BY matchid, mdate
```

## 13. **List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.**

|    mdate     | team1 | score1 | team2 | score2 |
| :----------: | :---: | :----: | :---: | :----: |
| 1 July 2012  |  ESP  |   4    |  ITA  |   0    |
| 10 June 2012 |  ESP  |   1    |  ITA  |   1    |
| 10 June 2012 |  IRL  |   1    |  CRO  |   3    |
|     ...      |

```
Haven't got it to work yet :)
```

# More JOIN Operations

## 1. **List the films where the** `yr` **is 1962.**

```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```

## 2. **When was Citizen Kane released?**

```sql
SELECT yr
 FROM movie
WHERE title = 'Citizen Kane'
```

## 3. **List all of the Star Trek movies, include the** `id`**,** `title` **and** `yr` **(all of these movies include the words Star Trek in the title). Order results by year.**

```sql
SELECT id, title, yr
  FROM movie
 WHERE title LIKE '%Star Trek%'
```

## 4. **What** `id` **number does the actor 'Glenn Close' have?**

```sql
SELECT id
  FROM actor
  WHERE name = 'Glenn Close'
```

## 5. **What is the** `id` **of the film 'Casablanca'.**

```sql
SELECT id
  FROM movie
 WHERE title = 'Casablanca'
```

## 6. **Obtain the cast list for 'Casablanca'.**

```sql
SELECT name
  FROM actor
  JOIN casting ON (casting.actorid = actor.id)
   AND casting.movieid = 27
```

Or

```sql
SELECT name
  FROM casting, actor
  WHERE actor.id = casting.actorid
    AND casting.movieid = 27
```

## 7. **Obtain the cast list for the film 'Alien'.**

```sql
SELECT name
  FROM casting
  JOIN actor ON (actor.id=casting.actorid)
  JOIN movie ON (movie.id = casting.movieid)
 WHERE title = 'Alien'
```

Or

```sql
SELECT name
 FROM casting, actor, movie
WHERE (actor.id=casting.actorid)
  AND (movie.id = casting.movieid)
  AND title = 'Alien'
```

## 8. **List the films in which 'Harrison Ford' has appeared.**

```sql
SELECT title
  FROM movie
  JOIN casting ON (casting.movieid = movie.id)
  JOIN actor ON (actor.id  = casting.actorid)
 WHERE actor.name = 'Harrison Ford'
```

Or

```sql
SELECT title
  FROM movie, casting, actor
  WHERE (casting.movieid = movie.id)
    AND (actor.id  = casting.actorid)
    AND actor.name = 'Harrison Ford'
```

## 9. **List the films where 'Harrison Ford' has appeared - but not in the starring role.**

```sql
SELECT title
  FROM movie
  JOIN casting ON (casting.movieid = movie.id)
  JOIN actor ON (casting.actorid = actor.id)
 WHERE actor.name = 'Harrison Ford'
   AND casting.ord != 1
```

Or

```sql
SELECT title
  FROM movie, casting, actor
 WHERE (casting.movieid = movie.id)
   AND (casting.actorid = actor.id)
   AND actor.name = 'Harrison Ford'
   AND casting.ord != 1
```

## 10. **List the films together with the leading star for all 1962 films.**

```sql
SELECT title, name
  FROM movie
  JOIN casting ON (casting.movieid = movie.id)
  JOIN actor ON (casting.actorid = actor.id)
  WHERE movie.yr = 1962
    AND casting.ord = 1

--You can use the same method as above to get the same outcome (listing all the tables in FROM and joining on WHERE), I just didn't bother (Theoretically it would be slower)
```

## 11. **Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.**

```sql
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
where name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```

## 12. **List the film title and the leading actor for all of the films 'Julie Andrews' played in.**

```sql
SELECT title, name
  FROM movie
  JOIN casting ON (movie.id = casting.movieid)
  JOIN actor ON (actor.id = casting.actorid)
 WHERE casting.ord = 1
     AND casting.movieid IN (SELECT casting.movieid
                               FROM casting
                               JOIN actor ON (casting.actorid = actor.id)
                              WHERE actor.name = 'Julie Andrews')
-- Hardest in the bunch
```

## 13. **Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.**

```sql
SELECT name
  FROM actor
  JOIN casting ON (casting.actorid = actor.id)
 WHERE casting.ord = 1
 GROUP BY actor.name
HAVING COUNT(casting.movieid) >= 15
```

## 14. **List the films released in the year 1978 ordered by the number of actors in the cast, then by title.**

```sql
SELECT COUNT(movieid)
FROM casting
 JOIN movie ON (movie.id = casting.movieid)
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(movieid) DESC
```

## 15. **List all the people who have worked with 'Art Garfunkel'.**

```sql
SELECT DISTINCT a.name
  FROM actor a
  JOIN casting l ON (l.actorid = a.id)
  JOIN casting k ON (l.movieid = k.movieid)
  JOIN actor b ON (k.actorid = b.id AND b.name = 'Art Garfunkel')
 WHERE a.id != b.id
 -- "b" is Garfunkel, "a" are the actors, "k" is the casting of "the other actors" and "l" is casting of Garfunkel
```

# Using NULL

## 1. **List the teachers who have NULL for their department.**

```sql
SELECT name
FROM teacher
WHERE dept IS NULL
```

## 2. **Note the INNER JOIN misses the teachers with no department and the departments with no teacher.**

```sql
SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
```

## 3. **Use a different JOIN so that all teachers are listed.**

```sql
   SELECT teacher.name, dept.name
     FROM teacher
LEFT JOIN dept ON (teacher.dept = dept.id)
```

Or

```sql
   SELECT teacher.name, dept.name
     FROM dept
RIGHT JOIN teacher ON (teacher.dept = dept.id)
```

## 4. Use a different JOIN so that all departments are listed.

```sql
    SELECT teacher.name, dept.name
      FROM teacher
RIGHT JOIN dept ON (teacher.dept = dept.id)
```

Or

```sql
   SELECT teacher.name, dept.name
     FROM dept
LEFT JOIN teacher ON (teacher.dept = dept.id)
```

## 5. **Show teacher name and mobile number or '07986 444 2266'.**

```sql
SELECT name, COALESCE(mobile, '07986 444 2266')
  FROM teacher
```

## 6. **Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.**

```sql
SELECT teacher.name, COALESCE(teacher.dept, 'None')
  FROM teacher
LEFT JOIN dept ON (teacher.dept = dept.id)
```

## 7. **Use COUNT to show the number of teachers and the number of mobile phones.**

```sql
SELECT COUNT(teacher.name), COUNT(teacher.mobile)
  FROM teacher
```

## 8. **Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.**

```sql
   SELECT d.name, COUNTd.dept)
     FROM dept d
LEFT JOIN teacher ON (teacher.dept = dept.id)
    GROUP BY d.name
```

## 9. **Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.**

```sql
    SELECT T.name,
 CASE WHEN T.dept IN (1,2)
      THEN 'Sci'
      ELSE 'Art'
       END
      FROM teacher T
```
