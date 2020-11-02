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
  
**Exercise 21: 1179. Reformat Department Table**  
_MS SQL Server_  
SELECT Id, [Jan] AS [Jan_Revenue],[Feb] AS[Feb_Revenue],[Mar] AS [Mar_Revenue],[Apr] AS [Apr_Revenue],[May] AS [May_Revenue],[Jun] AS [Jun_Revenue],[Jul] AS [Jul_Revenue],[Aug] AS [Aug_Revenue],[Sep] AS [Sep_Revenue],[Oct] AS [Oct_Revenue],[Nov] AS [Nov_Revenue],[Dec] AS [Dec_Revenue]  
FROM (SELECT id, month, revenue  
FROM Department) AS src  
PIVOT  
(SUM(revenue) FOR [month] IN ([Jan],[Feb],[Mar],[Apr],[May],[Jun],[Jul],[Aug],[Sep],[Oct],[Nov],[Dec])) AS pvt  
_MY SQL_  
SELECT id,
    SUM(IF(month = 'Jan', revenue, NULL)) AS Jan_Revenue,  
    SUM(IF(month = 'Feb', revenue, NULL)) AS Feb_Revenue,  
    SUM(IF(month = 'Mar', revenue, NULL)) AS Mar_Revenue,  
    SUM(IF(month = 'Apr', revenue, NULL)) AS Apr_Revenue,  
    SUM(IF(month = 'May', revenue, NULL)) AS May_Revenue,  
    SUM(IF(month = 'Jun', revenue, NULL)) AS Jun_Revenue,  
    SUM(IF(month = 'Jul', revenue, NULL)) AS Jul_Revenue,  
    SUM(IF(month = 'Aug', revenue, NULL)) AS Aug_Revenue,  
    SUM(IF(month = 'Sep', revenue, NULL)) AS Sep_Revenue,  
    SUM(IF(month = 'Oct', revenue, NULL)) AS Oct_Revenue,  
    SUM(IF(month = 'Nov', revenue, NULL)) AS Nov_Revenue,  
    SUM(IF(month = 'Dec', revenue, NULL)) AS Dec_Revenue  
FROM Department  
GROUP BY id;  
  
**Exercise 22 597. Friend Requests I: Overall Acceptance Rate**  
select  
round(  
    ifnull(  
    (select count(*) from (select distinct requester_id, accepter_id from request_accepted) as A)  
    /  
    (select count(*) from (select distinct sender_id, send_to_id from friend_request) as B),  
    0)  
, 2) as accept_rate;  
  
**Exercise 23 1270. All People Report to the Given Manager**  
SELECT employee_id FROM Employees
WHERE manager_id IN (SELECT employee_id FROM Employees 
WHERE manager_id IN (SELECT employee_id FROM Employees WHERE manager_id = 1)) AND manager_id <>1

**Exercise 24 1212. Team Scores in Football Tournament**  
SELECT t.team_id, t.team_name, IFNULL(SUM(num_points),0) AS num_points    
FROM Teams t  
LEFT JOIN (SELECT host_team,  
       SUM(CASE  
       WHEN host_goals > guest_goals THEN 3  
       WHEN host_goals = guest_goals THEN 1  
       ELSE 0  
            END        ) AS num_points  
FROM Matches  
GROUP BY host_team  
UNION ALL  
SELECT guest_team, SUM(CASE  
       WHEN host_goals < guest_goals THEN 3  
       WHEN host_goals = guest_goals THEN 1  
       ELSE 0  
            END        ) AS num_points  
FROM Matches  
GROUP BY guest_team) AS u ON u.host_team = t.team_id  
GROUP BY team_id  
ORDER BY num_points DESC, team_id ASC ;  
  
**Exercise 25 626. Exchange Seats**   
select s1.id, s2.student      
from seat s1, seat s2  
where (s1.id % 2 = 1 AND if(s1.id +1 > (select max(id) from seat),s1.id = s2.id,s1.id +1 = s2.id)) OR (s1.id %2 =0 AND s1.id -1= s2.id)  
ORDER BY s1.id   
  
**Exercise 26 1098. Unpopular Books**
select book_id, name
from books
where available_from <'2019-05-23'
and book_id not in
(select book_id 
from orders 
where dispatch_date>'2018-06-23'
group by book_id
having sum(quantity)>=10)

**Exercise 27 601. Human Traffic of Stadium**  
select s1.id,s1.visit_date,s1.people from stadium s1, stadium s2, stadium s3 where s1.id=s2.id-1 and s2.id=s3.id-1 and s1.people>=100 and s2.people>=100 and s3.people>=100  
union  
select s2.id,s2.visit_date,s2.people from stadium s1, stadium s2, stadium s3 where s1.id=s2.id-1 and s2.id=s3.id-1 and s1.people>=100 and s2.people>=100 and s3.people>=100  
union  
select s3.id,s3.visit_date,s3.people from stadium s1, stadium s2, stadium s3 where s1.id=s2.id-1 and s2.id=s3.id-1 and s1.people>=100 and s2.people>=100 and s3.people>=100  
order by id  

**Exercise 28 1350. Students With Invalid Departments**  
SELECT s.id, s.name  
FROM Students s  
LEFT JOIN Departments d ON d.id = s.department_id  
WHERE d.name IS NULL  
  
**Exercise 29 603. Consecutive Available Seats**  
SELECT c1.seat_id  
FROM cinema c1, cinema c2  
WHERE c1.free = 1 AND C2.free = 1 AND c1.seat_id + 1 = c2.seat_id   
UNION    
SELECT c2.seat_id  
FROM cinema c1, cinema c2  
WHERE c1.free = 1 AND C2.free = 1 AND c1.seat_id + 1 = c2.seat_id   
ORDER BY seat_id  
  
**Exercise 30 1341. Movie Rating**  
SELECT name AS results  
FROM (SELECT name,  c  
FROM Users u, (SELECT user_id,COUNT(movie_id) as c FROM Movie_Rating GROUP BY user_id)  AS n  
WHERE u.user_id =  n.user_id  
ORDER BY c DESC, name LIMIT 1) AS f  
UNION  
SELECT title AS results  
FROM (SELECT title, AVG(rating) as t   
FROM Movies m   
JOIN Movie_Rating mr ON m.movie_id = mr.movie_id  
WHERE MONTH(created_at) = 02 AND YEAR(created_at) =  2020   
GROUP BY mr.movie_id  
ORDER BY t DESC, title  
LIMIT 1 ) h  

**Exercise 31 1132. Reported Posts II** 
select round(avg(z.p),2) as average_daily_percent
from
(select (count(distinct r.post_id) *100/ count(distinct a.post_id) ) as P
from actions a left join removals r on a.post_id = r.post_id
where a.extra = 'spam'
group by a.action_date )Z
  
**Exercise 32 615. Average Salary: Departments VS Company**  
SELECT C.pay_Month, D.department_id, CASE   
                                    WHEN C_Avg < D_Avg THEN 'higher'  
                                    WHEN C_Avg > D_Avg THEN 'lower'  
                                    ELSE 'same'  
                                 END AS comparison  
FROM (SELECT AVG(amount) as C_Avg, SUBSTRING(pay_date,1,7) AS pay_month  
FROM salary  
GROUP BY MONTH(pay_date)) AS C  
JOIN   
(SELECT department_id,AVG(amount) as D_Avg, SUBSTRING(pay_date,1,7) AS pay_month  
FROM salary s  
JOIN employee e ON e.employee_id = s.employee_id  
GROUP BY department_id,MONTH(pay_date)) AS D  
ON D.pay_month = C.pay_month  
  
**Exercise 33 1142. User Activity for the Past 30 Days II**  
SELECT IFNULL(ROUND(COUNT(user_id)/COUNT(DISTINCT(user_id)),2),0) AS average_sessions_per_user   
FROM (SELECT user_id  
FROM Activity  
WHERE DATE_ADD(activity_date, INTERVAL 30 DAY)  > '2019-07-27'  
GROUP BY session_id) AS C  
  
**Exercise 34 1173. Immdediate Food DeliveryI**  
SELECT ROUND((im/COUNT(delivery_id))*100,2) AS immediate_percentage  
FROM Delivery, (SELECT COUNT(delivery_id) AS im  
FROM Delivery  
WHERE order_date = customer_pref_delivery_date) AS i  
  
**Exercise 35 1355. Activity Participants**  
WITH CTE AS (SELECT activity, COUNT(activity) AS ct  
FROM Friends  
GROUP BY activity)   
  
SELECT activity   
FROM CTE  
WHERE ct < (SELECT MAX(ct) FROM CTE) AND ct > (SELECT MIN(ct) FROM CTE)  
  
**Exercise 36 1517.Find Users With Valid E-Mails**  
SELECT * FROM Users WHERE REGEXP_LIKE(mail, '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode[.]com')  
  
**Exercise 37 627.Swap Salary**  
UPDATE salary  
SET  
    sex = CASE sex  
        WHEN 'm' THEN 'f'  
        ELSE 'm'  
    END;  
