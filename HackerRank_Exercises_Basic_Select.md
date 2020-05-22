**Exercise 1** [revising the select query I](https://www.hackerrank.com/challenges/revising-the-select-query/problem)  
_Query all columns for all American cities in CITY with populations larger than 100000. The CountryCode for America is USA._  
**Solution**  
SELECT * FROM CITY  
WHERE POPULATION > 100000 AND COUNTRYCODE = 'USA';  
   
**Exercise 2** [revising the select query II](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem)  
_Query the names of all American cities in CITY with populations larger than 120000. The CountryCode for America is USA._  
**Solution**  
SELECT NAME FROM CITY  
WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA';  

**Exercise 3** [Select all](https://www.hackerrank.com/challenges/select-all-sql/problem)  
_Query all columns (attributes) for every row in the CITY table._  
**Solution**  
SELECT * FROM CITY;  
   
**Exercise 4** [Select By ID](https://www.hackerrank.com/challenges/select-by-id/problem)  
_Query all columns for a city in CITY with the ID 1661._  
**Solution**
SELECT * FROM CITY  
WHERE ID = 1661;  
  
**Exercise 5 ** [Japanese Cities' Attributes](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem)  
_Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN._  
**Solution**  
SELECT * FROM CITY  
wHERE COUNTRYCODE = 'JPN';  
  
**Exercise 6** [Weather Observation Station 1](https://www.hackerrank.com/challenges/weather-observation-station-1/problem)  
_Query a list of CITY and STATE from the STATION table._  
**Solution**  
SELECT CITY,STATE   
FROM STATION;  
  
**Exercise 7** [Weather Observation Station 3](https://www.hackerrank.com/challenges/weather-observation-station-3/problem)  
_Query a list of CITY names from STATION with even ID numbers only. You may print the results in any order, but must exclude duplicates from your answer._  
**Solution**  
_#MySQL, MS SQL Server_  
SELECT DISTINCT(CITY)  
FROM STATION  
WHERE (ID%2) = 0;   
_#Oracle_    
SELECT DISTINCT(CITY)  
FROM STATION  
WHERE MOD(ID,2) = 0;  
  
**Exercise 8** [Weather Observation Station 4](https://www.hackerrank.com/challenges/weather-observation-station-4/problem)  
_Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table._  
**Solution**  
SELECT COUNT(CITY)-COUNT(DISTINCT(CITY))  
FROM STATION;  
  
**Exercise 9** [Weather Observation Station 5](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?h_r=next-challenge&h_v=zen)  
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths.  
**Solution**  
_MySQL_  
SELECT CITY, LENGTH(CITY)   
FROM STATION   
ORDER BY LENGTH(CITY), CITY LIMIT 1;  
SELECT CITY, LENGTH(CITY)  
FROM STATION  
ORDER BY LENGTH(CITY) DESC,CITY LIMIT 1;  

**Exercise 10** [Weather Observation Station 6](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)  
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.  
**Solution**  
_#MS SQL Server_  
SELECT CITY FROM STATION  
WHERE CITY LIKE '[aeiou]%';    
_#MySQL_  
SELECT CITY FROM STATION  
WHERE CITY LIKE 'a%' OR CITY LIKE 'e%' OR CITY LIKE 'i%' OR CITY LIKE 'o%' OR CITY LIKE 'u%';  
_#Oracle_  
SELECT CITY FROM STATION      
WHERE CITY LIKE 'A%' OR CITY LIKE 'E%' OR CITY LIKE 'I%' OR CITY LIKE 'O%' OR CITY LIKE 'U%';  
  
**Exercise 11** [Weather Observation Station 7](https://www.hackerrank.com/challenges/weather-observation-station-7/problem)  
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.  
**Solution**  
_#MySQL, Oracle_  
SELECT DISTINCT(CITY)  
FROM STATION  
WHERE CITY LIKE '%a' OR CITY LIKE '%e' OR CITY LIKE '%i' OR CITY LIKE '%o' OR CITY LIKE '%u';  
_#MS SQL Server_  
SELECT DISTINCT CITY 
FROM STATION
WHERE CITY LIKE '%[aeiou]';  
  
**Exercise 12**[Weather Observation Station 8](https://www.hackerrank.com/challenges/weather-observation-station-8/problem)  
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.  
**Solution**  
_#MySQL_  
SELECT DISTINCT CITY  
FROM STATION  
WHERE CITY RLIKE '[aeiou]$' AND CITY RLIKE '^[aeiou]';    
  
**Exercise 13**[Weather Observation Station 9](https://www.hackerrank.com/challenges/weather-observation-station-9/problem)  
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.  
**Solution**  
SELECT DISTINCT(CITY) FROM STATION  
WHERE CITY RLIKE '^[^aeiou]'  
ORDER BY CITY 
  
**Exercise 14**[Weather Observation Station 10](https://www.hackerrank.com/challenges/weather-observation-station-10/problem)  
Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.  
**Solution**  
SELECT DISTINCT(CITY)  
FROM STATION  
WHERE CITY RLIKE '[^aeiou]$'; 
  
**Exercise 15**[[Weather Observation Station 11](https://www.hackerrank.com/challenges/weather-observation-station-11/problem)  
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.  
**Solution**  
SELECT DISTINCT(CITY)  
FROM STATION  
WHERE CITY RLIKE '^[^aeiou]' OR CITY RLIKE '[^aeiou]$'  
ORDER BY CITY;  
  
**Exercise 16**[[Weather Observation Station 12](https://www.hackerrank.com/challenges/weather-observation-station-12/problem)
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.  
**Solution**  
SELECT DISTINCT(CITY)  
FROM STATION  
WHERE CITY RLIKE '^[^aeiou]' AND CITY RLIKE '[^aeiou]$'  
ORDER BY CITY;  
  
**Exercise 17**[Higher Than 75 Marks](https://www.hackerrank.com/challenges/more-than-75-marks/problem)  
Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.  
**Solution**  
SELECT NAME FROM STUDENTS  
WHERE MARKS > 75  
ORDER BY RIGHT(NAME,3), ID;  
  
**Exercise 18**[Employee Names](https://www.hackerrank.com/challenges/name-of-employees/problem)  
Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.  
**Solution**  
SELECT NAME FROM EMPLOYEE  
ORDER BY NAME;  
  
**Exercise 19**[Employee Salaries](https://www.hackerrank.com/challenges/salary-of-employees/problem)  
Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id.  
**Solution**  
SELECT NAME FROM EMPLOYEE  
WHERE SALARY > 2000 AND MONTHS < 10  
ORDER BY EMPLOYEE_ID;  


