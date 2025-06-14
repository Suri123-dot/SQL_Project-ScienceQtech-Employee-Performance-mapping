# SQL_Project-ScienceQtech-Employee-Performance-mapping

## Objective
To facilitate a better understanding, managers have provided ratings for each employee which will help the HR department to finalize the employee performance mapping. As a DBA, you should find the maximum salary of the employees and ensure that all jobs are meeting the organization's profile standard. You also need to calculate bonuses to find extra cost for expenses. This will raise the overall performance of the organization by ensuring that all required employees receive training.

## Problem Scenario
ScienceQtech is a startup that works in the Data Science field. ScienceQtech has worked on fraud detection, market basket, self-driving cars, supply chain, algorithmic early detection of lung cancer, customer sentiment, and the drug discovery field. With the annual appraisal cycle around the corner, the HR department has asked you (Junior Database Administrator) to generate reports on employee details, their performance, and on the project that the employees have undertaken, to analyze the employee database and extract specific data based on different requirements.

## The task to be performed
1.	Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

2.	Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is: 
●	less than two
●	greater than four 
●	between two and four

3.	Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.

4.	Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).
5.	
6.	Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.

7.	Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.

8.	Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.

9.	Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

10.	Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

11.	Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.

12.	Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

13.	Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.

The standard being:
For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST',
For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',
For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',
For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
For an employee with the experience of 12 to 16 years assign 'MANAGER'.

14.	Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.

15.	Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).

16.	Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

## Sample SQL Queries
4.	Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is: 
●	less than two
●	greater than four 
●	between two and four

select emp_id, first_name, last_name, gender, dept, emp_rating 

from emp_record

where emp_rating < 2;


select emp_id, first_name, last_name, gender, dept, emp_rating 

from emp_record

where emp_rating > 4;


select emp_id, first_name, last_name, gender, dept, emp_rating 

from emp_record

where emp_rating between 2 and 4;

7. Write a query to list down all the employees from the healthcare and financedepartments using union. Take data from the employee record table.

select first_name, last_name, dept from emp_record

where dept='healthcare’

union

select first_name, last_name, dept from emp_record

where dept='finance’;

8. Write a query to list down employee details such as EMP_ID, FIRST_NAME,LAST_NAME, ROLE, DEPARTMENT, and EMP_RATINGgrouped by dept. Also include the respective employee rating along with the max emp rating for the department.

select emp_id, first_name, last_name, role, dept, emp_rating,emp_rating

as max_rating

from emp_record where(dept, emp_rating)

IN (select dept, max(emp_rating)

from emp_record

group by dept;

10. Write a query to assign ranks to each employee based on their experience.

select emp_id, first_name, last_name, exp,

dense_rank()

over(order by exp desc) 

from emp_record;

14. Write a query using stored functions in the project table to check whether the job
profile assigned to each employee in the data science team matches the
organization’s set standard.
The standard being:
For an employee with experience less than or equal to 2 years assign 'JUNIOR
DATA SCIENTIST’,
For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA
SCIENTIST’,
For an employee with the experience of 5 to 10 years assign 'SENIOR DATA
SCIENTIST’,
For an employee with the experience of 10 to 12 years assign 'LEAD DATA
SCIENTIST’,
For an employee with the experience of 12 to 16 years assign 'MANAGER'.

DELIMITER $$


USE `employee`$$

CREATE PROCEDURE `Assign_role` ()

BEGIN

select emp_id, first_name, last_name,gender, role, dept, exp,

country, continent, salary, emp_rating, manager_id, proj_id,

case

when exp <=2 then 'JUNIOR DATA SCIENTIST'

when exp between 2 and 5 then 'ASSOCIATE DATA SCIENTIST'

when exp between 5 and 10 then 'SENIOR DATA SCIENTIST'

when exp between 10 and 12 then 'LEAD DATA SCIENTIST'

when exp between 12 and 16 then 'manager’

END as Assigned_role

from emp_record;

END$$

DELIMITER ;

call assign_role;





