**Exercise 1: 175. Combine Two Tables**
SELECT p.FirstName, p.LastName, a.City, a.State
FROM Person as p
LEFT JOIN Address as a on p.PersonId = a.PersonId;  

**Exercise 2: 176. Second Highest Salary**  
SELECT IF(Salary = NULL,NULL,Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (SELECT(MAX(Salary)) FROM Employee)
ORDER BY Salary DESC 
LIMIT 1 ;

**Exercise 3: 177. Nth Highest Salary**   
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
 
declare var int;
SET var = N-1;
RETURN (  
SELECT  
    IFNULL(  
      (SELECT DISTINCT Salary  
       FROM Employee  
       ORDER BY Salary DESC  
       LIMIT 1 OFFSET var  
       ),  
    NULL)   
  );  
END  
  
**Exercise 4: 178. Rank Scores** 
_MS SQL Server_
SELECT Score, 
       DENSE_RANK() OVER(ORDER BY Score DESC) AS Rank
FROM Scores;  
  
**Exercise 5: 180. Consecutive Numbers**  
SELECT DISTINCT (l1.Num) AS ConsecutiveNums  
FROM Logs l1, Logs l2, Logs l3  
WHERE l1.Num = l2.Num AND l2.Num = l3.Num AND l1.Id = l2.Id + 1 AND l2.Id = l3.Id +1;  
  
**Exercise 6: 181. Employees Earning More Than Their Managers**  
SELECT e1.Name AS Employee
FROM Employee e1, Employee e2
WHERE e1.ManagerId = e2.ID AND e1.Salary > e2.Salary  
  
**Exercise 7: 182. Duplicate Emails**  
_Solution1:_  
SELECT DISTINCT(LOWER(p1.Email)) AS Email  
FROM Person p1, Person p2  
WHERE p1.Email = p2.Email AND p1.Id <> p2.Id;  
_Solution2:_   
SELECT Email 
FROM 
(SELECT Email, COUNT(Email) AS Num  
FROM Person  
GROUP BY Email) AS Stats  
WHERE Num >1;  
_Solution3:_  
SELECT Email  
FROM Person  
GROUP BY (Email)  
HAVING COUNT(Email) > 1;  
  
**Exercise 8: 183. Customers Who Never Order**
SELECT Name AS Customers  
FROM Customers c  
LEFT JOIN Orders as o on o.CustomerId = c.Id  
WHERE o.CustomerId IS NULL  
  
**Exercise 9: 184. Department Highest Salary**  
SELECT d.Name as Department, e.Name as Employee, e.Salary  
FROM Employee e  
JOIN Department d ON d.Id = e.DepartmentId  
WHERE (e.DepartmentId,e.Salary) IN (SELECT DepartmentId, MAX(Salary)   
FROM Employee GROUP BY DepartmentId)  
  
**Exercise 10: Department Top Three Salaries**  
_MS SQL Server_  
SELECT d.Name AS Department, e.Name AS Employee, e.Salary  
FROM Employee e  
JOIN Department d   
ON d.Id = e.DepartmentId  
JOIN (SELECT Id,DENSE_RANK() OVER (PARTITION BY DepartmentId ORDER BY Salary DESC) as Rank FROM Employee) AS r   
ON r.Id = e.Id   
WHERE r.RANK <= 3  
_MY SQL_  
SELECT  
    d.Name AS 'Department', e1.Name AS 'Employee', e1.Salary  
FROM  
    Employee e1  
        JOIN  
    Department d ON e1.DepartmentId = d.Id  
WHERE  
    3 > (SELECT  
            COUNT(DISTINCT e2.Salary)  
        FROM  
            Employee e2  
        WHERE  
            e2.Salary > e1.Salary  
                AND e1.DepartmentId = e2.DepartmentId  
        )  
  
**Exercise 11: 196. Delete Duplicate Emails**  
DELETE p2  
FROM Person p1, Person p2  
WHERE p1.Email = p2.Email AND p2.Id > p1.Id  
  
**Exercise 12: 197. Rising Temperature**
SELECT w1.id  
FROM    
Weather w1, Weather w2  
WHERE TO_DAYS(w1.RecordDate) = TO_DAYS(w2.RecordDate) + 1  
AND w1.Temperature > w2.Temperature  
  
**Exercise 13: 262. Trips and Users**  
SELECT t.Request_at AS Day, ROUND((COUNT(*)-
(t.Status = 'completed'))/ COUNT(*),2) AS 'Cancellation Rate'   
FROM Trips t  
JOIN   
Users u ON u.Users_Id = t.Client_Id OR u.Users_Id = t.Driver_ID  
WHERE u.Banned = "No" AND (t.Request_at Between "2013-10-01" AND "2013-10-03")  
GROUP BY t.Request_at  
_Solution_  
SELECT t.Request_at AS Day, ROUND((COUNT(*)-SUM(t.Status = 'completed'))/ COUNT(*),2) AS 'Cancellation Rate'   
FROM Trips t  
LEFT JOIN Users u1 ON u1.Users_Id = t.Driver_Id   
LEFT JOIN Users u2 ON u2.Users_Id = t.Client_Id  
WHERE u1.Banned = "No" AND u2.Banned = "No" AND t.Request_at Between "2013-10-01" AND "2013-10-03"  
GROUP BY t.Request_at  
ORDER BY t.Request_at  
  
**Exercise 14: 511. Game Play Analysis I**  
SELECT player_id, MIN(event_date) as first_login
FROM Activity  
GROUP BY player_id   
  
**Exercise 15: 512. Game Play Analysis II**  
SELECT a.player_id, a.device_id  
FROM Activity a  
INNER JOIN (SELECT player_id, MIN(event_date) AS event_date FROM Activity GROUP BY player_id) as f
ON a.event_date = f.event_date AND a.player_id = f.player_id  

**Exercise 16: 534. Game Play Analysis III**
_MS SQL Server_  
SELECT player_id, event_date,   
       SUM(games_played) OVER(PARTITION BY player_id ORDER BY event_date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS   games_played_so_far  
FROM Activity  
  
**Exercise 17: 550. Game Play Analysis IV**  
SELECT ROUND(f.cd/(COUNT(DISTINCT(Activity.player_id))),2) AS fraction   
FROM Activity,   
 (SELECT count(a.player_id) AS cd    
  FROM Activity a  
  INNER JOIN (SELECT M.player_id,DATE_ADD(M.event_date, INTERVAL 1 DAY) as event_date    
                 FROM (SELECT player_id, MIN(event_date) as event_date FROM Activity GROUP BY player_id) AS M) as c
  on c.event_date = a.event_date AND c.player_id = a.player_id) as f  
  
**Exercise 18: 569. Median Employee Salary**  
_MS SQL Server_  
select id,company,salary  
from(select *,row_number() over (partition by company order by salary) as salary_order,count(salary)over(partition by company) as emp_num  
from employee) tmp  
where (emp_num%2 = 1 and salary_order= emp_num/2+1)  
    or (emp_num%2=0 and (salary_order = emp_num/2 or salary_order=emp_num/2+1))  

**Exercise 19: 570. Managers with at Least 5 Direct Reports**  
SELECT NAME  
FROM Employee  
WHERE ID IN (SELECT ManagerId FROM Employee GROUP BY ManagerId  HAVING COUNT(ManagerId) >=5 )  
_Faster Solution with Join_
SELECT NAME  
FROM Employee e   
JOIN (SELECT ManagerId FROM Employee GROUP BY ManagerId  HAVING COUNT(ManagerId) >=5 ) f  
ON f.ManagerId = e.Id  
  
**Exercise 20: 571. Find Median Given Frequency of Numbers**  
SELECT ROUND(SUM(Number)/COUNT(Number),2)  AS median  
FROM (SELECT Number, Frequency, SUM(Frequency) OVER (ORDER BY Number ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS s, SUM(Frequency) OVER() AS t  
FROM Numbers ) AS tmp  
where t/2 BETWEEN s- Frequency AND s  
 
