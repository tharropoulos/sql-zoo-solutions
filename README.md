# SQL Zoo Solutions
My Solutions Of The [SQL ZOO Tutorial]( https://sqlzoo.net/wiki/SQL_Tutorial)

## Sections
0) [SELECT Basics](#select-basics)
1) [SELECT Names](#select-names)
2) [SELECT From World](#select-from-world)
3) [SELECT From Nobel](#select-from-nobel)
4) [SELECT Within SELECT] (#select-within-select)

# SELECT Basics
##  1. **Show the population of Germany.**

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

## 11. **Find all details of the prize won by PETER GRÜNBERG.**
```sql 
SELECT *
  FROM nobel
 WHERE winner = 'PETER GRÜNBERG'
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