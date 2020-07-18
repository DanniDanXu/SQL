**Exercise 1** [Asian Population](https://www.hackerrank.com/challenges/asian-population/problem)  
_Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'_  
**Solution**  
SELECT SUM(C.POPULATION)   
FROM CITY AS C, COUNTRY AS CT     
WHERE C.COUNTRYCODE = CT.CODE AND CT.COUNTRYCODE = 'ASIA'  
  
**Exercise 2** [African Cities](https://www.hackerrank.com/challenges/african-cities/problem)  
_Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'._
SELECT C.NAME  
FROM CITY AS C  
JOIN COUNTRY AS CT ON CT.CODE = C.COUNTRYCODE  
WHERE CT.CONTINENT = 'Africa'  
  
**Exercise 3** [Average Population of Each Continent](https://www.hackerrank.com/challenges/average-population-of-each-continent) 
_Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations_
*Solution*  
SELECT CT.CONTINENT, FLOOR(AVG(C.POPULATION))  
FROM COUNTRY AS CT    
JOIN CITY AS C ON CT.CODE = C.COUNTRYCODE  
GROUP BY CT.CONTINENT  
  
**Exercise 4** [The Report](https://www.hackerrank.com/challenges/the-report/problem)  
**Solution**  
SELECT IF(G.Grade< 8,"NULL",S.Name),G.Grade, S.Marks  
FROM Students AS S   
JOIN Grades AS G on S.Marks >= G.Min_Mark AND S.Marks <= G.Max_Mark  
ORDER BY G.Grade DESC, S.Name ASC  
  
**Exercise 5** [Top Competitors](https://www.hackerrank.com/challenges/full-score/problem)  
**Solution**  
SELECT S.Hacker_ID, H.Name  
FROM Submissions as S  
LEFT JOIN Challenges as C on C.Challenge_ID = s.Challenge_ID  
LEFT JOIN Difficulty as D on D.Difficulty_level = C.Difficulty_level  
LEFT JOIN Hackers as H on H.Hacker_ID = S.Hacker_ID  
GROUP BY S.Hacker_ID  
having S.Score = D.Score  
Order by SUM(S.Score) DESC, Name ASC;  
  
**Exercise 6** [Challenges](https://www.hackerrank.com/challenges/challenges/problem)  
SELECT S.HACKER_ID,H.NAME,sum(challenge_id)
FROM SUBMISSIONS S
JOIN ON Hackers as H on H.Hacker_ID = S.HACKER_ID
GROUP BY(S.HACKER_ID)
ORDER BY SUM(CHALLENGE_ID) DESC, HACKER_ID











