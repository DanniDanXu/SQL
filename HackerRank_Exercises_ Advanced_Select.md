**Exerise 1** [Type of Triangle](https://www.hackerrank.com/challenges/what-type-of-triangle/problem)  
_Write a query identifying the type of each record in the TRIANGLES table using its three side lengths._  
**Solution**  
SELECT  
(CASE  
WHEN A = B AND A = C THEN 'Equilateral'  
WHEN A + B > C AND A - B < C AND (A = B OR A = C OR B = C) THEN 'Isosceles'  
WHEN A + B > C AND A - B < C AND (A <> B AND A <> C AND B <> C )THEN 'Scalene'  
ELSE 'Not A Triangle'  
END)  
FROM TRIANGLES;  
  
**Exercise 2** [The PADS](https://www.hackerrank.com/challenges/the-pads/problem)  
**Solution**  
SELECT CONCAT(Name,'(',LEFT(Occupation,1),')')    
FROM OCCUPATIONS    
ORDER BY Name;      
SELECT CONCAT('There are a total of ', COUNT(Occupation),' ', LOWER(Occupation),'s.')   
FROM OCCUPATIONS    
GROUP BY Occupation   
ORDER BY COUNT(Occupation)  



