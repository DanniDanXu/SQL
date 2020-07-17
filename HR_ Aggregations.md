**Exercise 1** [Revising Aggregations - The Count Function](https://www.hackerrank.com/challenges/revising-aggregations-the-count-function/problem)  
Query a count of the number of cities in CITY having a Population larger than 100,000.  
**Solution**  
SELECT COUNT(POPULATION)  
FROM CITY  
WHERE POPULATION > 100000;  
  
**Exercise 2** [Top Earners](https://www.hackerrank.com/challenges/earnings-of-employees/problem?h_r=next-challenge&h_v=zen)  
Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings.   
**Solution**  
SELECT max(months * salary), count(*)   
FROM Employee  
GROUP BY (months * salary)  
ORDER BY (months * salary) DESC  
LIMIT 1  
  
**Exercise 3** [Revising Aggregations - The Sum Function](https://www.hackerrank.com/challenges/revising-aggregations-sum/problem)
Query the total population of all cities in CITY where District is California.
**Solution**
SELECT sum(population)  
FROM CITY  
WHERE DISTRICT = 'California'  
  
**Exercise 4** [Revising Aggregations - Averages](https://www.hackerrank.com/challenges/revising-aggregations-the-average-function/problem)  
Query the average population of all cities in CITY where District is California.  
**Solution**  
SELECT avg(population)    
FROM CITY   
WHERE DISTRICT = 'California'  
  
**Exercise 5** [Average Population](https://www.hackerrank.com/challenges/average-population/problem)  
Query the average population for all cities in CITY, rounded down to the nearest integer.  
**Solution**  
SELECT round(avg(population),0)  
FROM CITY  
  
**Exercise 6** [Japan Population](https://www.hackerrank.com/challenges/japan-population/problem)  
Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.
**Solution**
SELECT sum(population)        
FROM CITY       
WHERE COUNTRYCODE = 'JPN'  
  
**Exercise 7** [Population Density Difference](https://www.hackerrank.com/challenges/population-density-difference/problem)  
Query the difference between the maximum and minimum populations in CITY.  
**Solution**  
SELECT MAX(POPULATION)-MIN(POPULATION)  
FROM CITY  
  
**Exercise 8** [The Blunder](https://www.hackerrank.com/challenges/the-blunder/problem)  
Write a query calculating the amount of error (i.e.:  average monthly salaries), and round it up to the next integer.  
**Solution**  
SELECT CEILING(AVG(SALARY) - AVG(REPLACE(SALARY,'0','') ))   
FROM Employees;  
  
**Exercise 9** [Weather Observation Station 2](https://www.hackerrank.com/challenges/weather-observation-station-2/problem)
Query the following two values from the STATION table:  
The sum of all values in LAT_N rounded to a scale of  decimal places.  
The sum of all values in LONG_W rounded to a scale of  decimal places.  
**Solution**  
SELECT ROUND(sum(LAT_N),2),ROUND(sum(LONG_W),2)  
FROM STATION  
  
**Exercise 10** [Weather Observation Station 13](https://www.hackerrank.com/challenges/weather-observation-station-13/problem)  
Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than  and less than . Truncate your answer to  decimal places.  
**Solution**  
SELECT ROUND(sum(LAT_N),4)  
FROM STATION  
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345  
  
**Exercise 11** [Weather Observation Station 14](https://www.hackerrank.com/challenges/weather-observation-station-14/problem)  
Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to  decimal places.
**Solution**  
SELECT ROUND(Max(LAT_N),4)  
FROM STATION  
WHERE LAT_N < 137.2345  
  
**Exercise 12** [Weather Observation Station 15](https://www.hackerrank.com/challenges/weather-observation-station-15/problem) 
Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.  
**Solution**
SELECT ROUND(LONG_W,4)  
FROM STATION  
WHERE LAT_N = (SELECT MAX(LAT_N) FROM STATION WHERE LAT_N < '137.2345') 
  
**Exercise 13** [Weather Observation Station 16](https://www.hackerrank.com/challenges/weather-observation-station-16/problem)  
Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7780 . Round your answer to 4 decimal places.
SELECT ROUND(MIN(LAT_N),4)  
FROM STATION 
WHERE LAT_N > 38.7780 
  
**Exercise 14** [Weather Observation Station 17](https://www.hackerrank.com/challenges/weather-observation-station-17/problem)
Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780 . Round your answer to 4 decimal places.
**Solution**  
SELECT ROUND(LONG_W,4)  
FROM STATION  
WHERE LAT_N = (SELECT MIN(LAT_N) FROM STATION WHERE LAT_N > 38.7780) 
  
**Exercise 15** [Weather Observation Station 18](https://www.hackerrank.com/challenges/weather-observation-station-18/problem)  
Query the Manhattan Distance  
SELECT ROUND(ABS(MAX(LAT_N)-MIN(LAT_N))+ ABS(MAX(LONG_W)-MIN(LONG_W)),4)  
FROM STATION  
  
**Exercise 16** [Weather Observation Station 19](https://www.hackerrank.com/challenges/weather-observation-station-19/problem)  
Query the Euclidean Distance  
**Solution**  
SELECT ROUND(SQRT(POW(MIN(LAT_N)-MAX(LAT_N), 2) + POW(MIN(LONG_W)-MAX(LONG_W), 2)), 4)   
FROM STATION;

















 
