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
RETURN (# Write your MySQL query statement below.
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
SELECT t.Request_at AS Day, ROUND((COUNT(*)-SUM(t.Status = 'completed'))/ COUNT(*),2) AS 'Cancellation Rate'   
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


