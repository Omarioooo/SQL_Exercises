**1) Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.**

**The `CITY` table is described as follows:**

| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT *
FROM city 
WHERE population > 100000 AND countrycode = 'USA';

```
___

**2) Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.**

**The `CITY` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT name 
FROM city
WHERE CountryCode ='USA'
AND population > 120000;
```
___

**3) Query all columns (attributes) for every row in the CITY table.**

**The `CITY` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT * 
FROM city;
```
___

**4)Query all columns for a city in CITY with the ID 1661.**

**The `CITY` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT * 
FROM city
WHERE id = '1661';
```
___

**5) Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.**

**The `CITY` table is described as follows:**

| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT * 
FROM city
WHERE countrycode = 'jpn';
```

**6) Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.**

**The `CITY` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT name
From city
WHERE countrycode = 'JPN';
```
___

**7) Query a list of CITY and STATE from the STATION table.**
**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT city, state 
FROM station;
```
___

**8) Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city 
FROM station
WHERE id%2 =0;
```
___

**9) Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.**

**The STATION table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT COUNT(city) - COUNT(DISTINCT city) 
FROM station;
```
___

**10) Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
-- Shortest city name
SELECT TOP 1 CITY, LEN(CITY) AS NAME_LENGTH
FROM STATION
ORDER BY LEN(CITY) ASC, CITY ASC;

-- Longest city name
SELECT TOP 1 CITY, LEN(CITY) AS NAME_LENGTH
FROM STATION
ORDER BY LEN(CITY) DESC, CITY ASC;
```
___

**11) Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE LOWER(LEFT(city, 1)) IN ('a', 'e', 'i', 'o', 'u');
```
___

**12) Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE LOWER(RIGHT(city, 1)) IN ('a', 'e', 'i', 'o', 'u');
```
___

**13) Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE 
    LOWER(LEFT(city, 1)) IN ('a', 'e', 'i', 'o', 'u')
 AND
    LOWER(RIGHT(city, 1)) IN ('a', 'e', 'i', 'o', 'u');
```
___

**14) Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE LEFT(LOWER(city), 1) NOT IN ('a', 'e', 'i', 'o', 'u');
```
___


**15) Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE LOWER(RIGHT(city, 1)) NOT IN ('a', 'e', 'i', 'o', 'u');
```
___

**16) Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE 
    LOWER(LEFT(city, 1)) NOT IN ('a','e','i','o','u')
 OR
    LOWER(RIGHT(city, 1)) NOT IN ('a','e','i','o','u');
```
___

**17) Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.**

**The `STATION` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| CITY        | VARCHAR2(21)  |
| STATE       | VARCHAR2(21)  |
| LAT_N       | NUMBER(20)    |
| LONG_W      | NUMBER        |

```SQL
SELECT DISTINCT city
FROM station
WHERE 
    LOWER(RIGHT(city, 1)) NOT IN ('a', 'i', 'o', 'u', 'e') 
 AND
    LOWER(LEFT(city, 1)) NOT IN ('a', 'i', 'o', 'u', 'e');
```
___

**18) Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.**

**The `Employee` table containing employee data for a company is described as follows:**
| Field       | Type          |
|-------------|---------------|
| employee_id | integer       |
| name        | String        |
| months      | integer       |
| salary      | integer       |

```SQL
SELECT name
FROM Employee
ORDER BY name;
```
___

**19) Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id.**

**The `Employee` table containing employee data for a company is described as follows:**
| Field       | Type          |
|-------------|---------------|
| employee_id | integer       |
| name        | String        |
| months      | integer       |
| salary      | integer       |

```SQL
SELECT name
FROM Employee
where salary > 2000 AND months < 10 
ORDER BY employee_id ASC;
```

**20) Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:**

**- `Equilateral`: It's a triangle with  sides of equal length.**
**- `Isosceles`: It's a triangle with  sides of equal length.**
**- `Scalene`: It's a triangle with  sides of differing lengths.**
**- `Not A Triangle`: The given values of A, B, and C don't form a triangle.**

**The `TRIANGLES` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| A           | integer       |
| B           | integer       |
| C           | integer       |

```SQL
SELECT 
   CASE
      WHEN (A + B <= C) OR (B + C <= A) OR (A + C <= B) THEN 'Not A Triangle'
      WHEN A = B AND A = C THEN 'Equilateral'
      WHEN (A = B AND A != C) OR (B = C AND B != A) OR (A = C AND A != B) THEN 'Isosceles'
      ELSE 'Scalene'
   END AS Triangle_Type
FROM TRIANGLES
WHERE A > 0 AND B > 0 AND C > 0;
```
___

**21) Query a count of the number of cities in CITY having a Population larger than .**

**The CITY table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT count(*)
FROM CITY
WHERE Population > 100000    
```
___

**22) Query the total population of all cities in CITY where District is California.**

**The `CITY` table is described as follows:**

| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT SUM(population) 
FROM City 
WHERE district = 'California'
```
___

**23) Query the average population of all cities in CITY where District is California.**

**The `CITY` table is described as follows:**
| Field       | Type          |
|-------------|---------------|
| ID          | NUMBER        |
| NAME        | VARCHAR2(17)  |
| COUNTRYCODE | VARCHAR2(3)   |
| DISTRICT    | VARCHAR2(20)  |
| POPULATION  | NUMBER        |

```SQL
SELECT AVG(population)
FROM city 
WHERE district = 'California'
```
___

**24) **
```SQL
```
___

**25) **

```SQL
```
___

**26) **
```SQL
```
___

**27) **
```SQL
```
___

**28) **
```SQL
```
___

**29) **

```SQL

```
___

**30)**
```SQL

```
___

**31)**
```SQL

```
___

**32)**
```SQL

```
___

**33) **
```SQL

```

**34) **

```SQL

```
___

**35) **
```SQL
```
___

**36) **
```SQL
```
___

**37) **
```SQL
```
___

**38) **
```SQL
```
___

**39) **

```SQL
```
___

**40) **
```SQL
```
___

**41) **
```SQL
```
___

**42) **
```SQL
```
___


**43) **

```SQL

```
___

**44)**
```SQL

```
___

**45)**
```SQL

```
___

**46)**
```SQL

```
___

**47) **
```SQL

```

**48) **

```SQL

```
___

**49) **
```SQL
```
___

**50) **
```SQL
```
___

**51) **
```SQL
```
___

**52) **
```SQL
```
___

**53) **

```SQL
```
___

**54) **
```SQL
```
___

**55) **
```SQL
```
___

**56) **
```SQL
```
___


**57) **
```SQL
```
___

**58) **
```SQL
```