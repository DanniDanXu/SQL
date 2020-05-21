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
_MS SQL Server_  
SELECT CITY FROM STATION  
WHERE CITY LIKE '[aeiou]%';    
_MySQL_  
SELECT CITY FROM STATION  
WHERE CITY LIKE 'a%' OR CITY LIKE 'e%' OR CITY LIKE 'i%' OR CITY LIKE 'o%' OR CITY LIKE 'u%';  
_Oracle_  
SELECT CITY FROM STATION      
WHERE CITY LIKE 'A%' OR CITY LIKE 'E%' OR CITY LIKE 'I%' OR CITY LIKE 'O%' OR CITY LIKE 'U%';  
  
**Exercise 11**  

