# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
```
Write a SQL query to Delete customers from 'customer' table where 'AGENT_CODE' is either 'A003' or 'A008'.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```
Code
```sql
DELETE FROM Customer
WHERE AGENT_CODE = 'A003' OR AGENT_CODE = 'A008';
```

**Output:**

<img width="1242" height="961" alt="image" src="https://github.com/user-attachments/assets/3af0ac5c-3a2f-4c3d-bf46-8e163ff5c828" />

**Question 2**
```
Write a SQL statement to change salary of employee to 8000 whose Employee ID is 105, if the existing salary is less than 5000.


Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
```
Code
```sql
UPDATE Employees
set salary = 8000
where employee_id = 105 AND salary < 5000
```

**Output:**

<img width="1237" height="327" alt="image" src="https://github.com/user-attachments/assets/7c9514e5-ce75-4d64-a92a-968d82ae2130" />

**Question 3**
```
write a SQL query to find customers who are either from the city 'New York' or who do not have a grade greater than 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```
Code
```sql
SELECT customer_id,cust_name,city,grade,salesman_id from customer where city = 'New York' OR grade <= 100;
```

**Output:**

<img width="1240" height="518" alt="image" src="https://github.com/user-attachments/assets/3874fb0d-b602-411f-a2c1-cc407587a32c" />

**Question 4**
```
Write a SQL query to categorize value1 in the Calculations table as 'High' if it is greater than 50, otherwise 'Low'.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
```
Code
```sql
select id,value1,
CASE 
 when value1 < 50 then 'Low'
 else 'High'
 end as value_category
 from Calculations;
 
```

**Output:**

<img width="1240" height="384" alt="image" src="https://github.com/user-attachments/assets/2fef65f0-f556-4c4b-8b94-129d56e2cde6" />

**Question 5**
```
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_city' should begin with the letter 'L',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```
Code
```sql
DELETE FROM customer
where cust_city like ('L%');
```

**Output:**

<img width="1236" height="954" alt="image" src="https://github.com/user-attachments/assets/0476c9c5-6634-4ea6-8874-79e6eba300e6" />

**Question 6**
```
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```
Code
```sql
DELETE FROM Doctors
WHERE specialization = '' OR specialization IS NULL;
```

**Output:**

<img width="1234" height="951" alt="image" src="https://github.com/user-attachments/assets/e9e3b00d-d5a8-44cb-846a-223745d27b78" />

**Question 7**
```
Write a SQL query to retrieve all employee names in lower case. 

Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT
```
Code
```sql
SELECT LOWER(ename) as EmpName from emp;
```

**Output:**

<img width="1240" height="641" alt="image" src="https://github.com/user-attachments/assets/843e1702-66a7-4d5c-ab42-9e78dcae41a4" />

**Question 8**
```
write a SQL query to identify customers who do not belong to the city of 'New York' or have a grade value that exceeds 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```
Code
```sql
SELECT customer_id,cust_name,city,grade,salesman_id from customer
where city <> 'New York' AND grade <= 100;
```

**Output:**

<img width="1233" height="482" alt="image" src="https://github.com/user-attachments/assets/aa8daa0e-6719-44b6-ab66-f84c96959937" />

**Question 9**
```
Write a SQL query to calculate the final price after applying both the discount and the tax. Return product_id, original_price, discount_percentage, tax_rate, and final_price.

Sample table: Products

product_id | original_price | discount_percentage | tax_rate

 ------------+----------------+---------------------+--------- 

101 | 50.00 | 0.10 | 0.08 

102 | 75.00 | 0.15 | 0.05 

103 | 100.00 | 0.20 | 0.10
```
Code
```sql
SELECT product_id,original_price,discount_percentage,tax_rate,
(original_price * (1-discount_percentage)*(1+tax_rate)) as final_price from Products;
```

**Output:**

<img width="1236" height="376" alt="image" src="https://github.com/user-attachments/assets/5af0b43e-8025-4e47-9899-ad6ee5767cff" />

**Question 10**
```
 Write a SQL query to locate the details of customers with grade values above 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
```
Code
```sql
SELECT customer_id,cust_name,city,grade,salesman_id 
from customer where grade > 100;
```

**Output:**

<img width="1232" height="544" alt="image" src="https://github.com/user-attachments/assets/4d993247-1f94-43d5-8fe6-17e965be3a5d" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
