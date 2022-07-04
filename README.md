# SQL Zoo Solutions
My Solutions Of The [SQL ZOO Tutorial]( https://sqlzoo.net/wiki/SQL_Tutorial)

## Sections
0) [SELECT Basics](#select-basics)
1) [SELECT From World](#select-from-world)

# SELECT Basics
1. The example uses a WHERE clause to show the population of 'France'. Note that strings (pieces of text that are data) should be in 'single quotes';
**Modify it to show the population of Germany**

```sql
  SELECT population FROM world
  WHERE name = 'Germany'
```

2. Checking a list The word IN allows us to check if an item is in a list. The example shows the name and population for the countries 'Brazil', 'Russia', 'India' and 'China'.
**Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.**

```sql
  SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark')
```

3. Which countries are not too small and not too big? BETWEEN allows range checking (range specified is inclusive of boundary values). The example below shows countries with an area of 250,000-300,000 sq. km. **Modify it to show the country and the area for countries with an area between 200,000 and 250,000.**

```sql
    SELECT name, area FROM world
    WHERE area BETWEEN 200000 AND 250000
```


# SELECT From World

1. [Read the notes about this table](https://sqlzoo.net/wiki/Read_the_notes_about_this_table.). Observe the result of running this SQL command to show the name, continent and population of all countries. 

```sql
  SELECT name, continent, population FROM world
```

2. Give the `name` and the per capita GDP for those countries with a population of at least 200 million. 

```sql
  SELECT name, (gdp / population ) AS per_capita from world
  WHERE population > 200000000
```

4. Show the `name` and `population` in millions for the countries of the `continent` 'South America'. Divide the population by 1000000 to get population in millions. 

```sql
  SELECT name, (population / 1000000) AS population_millions from world
  WHERE continent = 'South America'
```  

5. Show the `name` and `population` for France, Germany, Italy 

```sql
  SElECT name, population FROM world
  WHERE name IN ('France', 'Germany', 'Italy');
```

6. Show the countries which have a `name` that includes the word 'United'

```sql 
  SELECT name FROM world
  WHERE name LIKE '%United%'
```

7. Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.
**Show the countries that are big by area or big by population. Show name, population and area.**

```sql
  SELECT name, population, area FROM world
  WHERE area > 3000000 OR population > 250000000
```

8. Exclusive OR (XOR). **Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area**

```sql
  SELECT name, population, area FROM world
  WHERE area > 3000000 AND population < 250000000
  OR area < 3000000 AND population > 250000000
```

9. Show the `name` and `population` in millions and the GDP in billions for the countries of the `continent` 'South America'. Use the ROUND function to show the values to two decimal places.
**For South America show population in millions and GDP in billions both to 2 decimal places.**

```sql
  SELECT name, ROUND(population / 1000000, 2) AS population_in_mil, ROUND(gdp / 1000000000, 2) AS gdp_bils FROM world
  WHERE continent = 'South America'
```

10. Show the `name` and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
**Show per-capita GDP for the trillion dollar countries to the nearest $1000.**

```sql
  SELECT name, ROUND(gdp  / population,-3) FROM world
  WHERE GDP > 1000000000000
```
11. Greece has capital Athens. Each of the strings 'Greece', and 'Athens' has 6 characters. **Show the name and capital where the name and the capital have the same number of characters.**

```sql
  SELECT name, capital FROM world
  WHERE LEN(name) = LEN(capital)
```

12. The capital of Sweden is Stockholm. Both words start with the letter 'S'.
**Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.**

```sql
  SELECT name, capital FROM world
  WHERE LEFT(name,1) = LEFT(capital,1) AND name != capital
```

13. Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name. **Find the country that has all the vowels and no spaces in its name.**
```sql
  SELECT name FROM world
  WHERE name LIKE '%a%'
    AND name LIKE '%e%'
    AND name LIKE '%i%'
    AND name LIKE '%o%'
    AND name LIKE '%u%'
    AND name NOT LIKE '% %'
  ```