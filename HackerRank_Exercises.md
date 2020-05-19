**Exercise1** [revising-the-select-query I](https://www.hackerrank.com/challenges/revising-the-select-query/problem)  
Query all columns for all American cities in CITY with populations larger than 100000. The CountryCode for America is USA.  
**Solution**  
SELECT * FROM CITY  
WHERE POPULATION > 100000 AND COUNTRYCODE = 'USA';  
   
**Exercise2** [revising-the-select-query II](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem)  
Query the names of all American cities in CITY with populations larger than 120000. The CountryCode for America is USA.  
**Solution**
SELECT NAME FROM CITY
WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA';  

**Exercise3**[]()
