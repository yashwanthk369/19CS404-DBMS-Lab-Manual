# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
```
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)
```
Code
```sql
SELECT p.first_name AS patient_name,d.specialization AS Doctor_speciali FROM PATIENTS p
INNER JOIN DOCTORS d
ON p.doctor_id = d.doctor_id
WHERE admission_date > '01-01-2024' AND admission_date < '31-01-2024' AND p.first_name = 'Alice';
```

**Output:**

<img width="1237" height="493" alt="image" src="https://github.com/user-attachments/assets/35b078d0-862f-44a8-a400-40931af4c0e4" />

**Question 2**
```
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```
Code
```sql
SELECT DISTINCT o.ord_no,o.purch_amt,c.cust_name,c.city FROM orders o
JOIN customer c
ON o.salesman_id = c.salesman_id
WHERE purch_amt > 500 AND purch_amt < 2000 AND city <> 'London';
```

**Output:**

<img width="1236" height="581" alt="image" src="https://github.com/user-attachments/assets/d472d080-c26c-4af5-b4c8-775470a6a48c" />

**Question 3**
```
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.
```
Code
```sql
SELECT p.date_of_birth , a.* from Patients p
INNER JOIN APPOINTMENTS a
ON p.patient_id = a.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**

<img width="1241" height="512" alt="image" src="https://github.com/user-attachments/assets/af3bc5c8-3208-486e-97d9-9043ee9d3d53" />

**Question 4**
```
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.
```
Code
```sql
SELECT p.first_name AS patient_name , t.* FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id
WHERE test_name = 'Blood Pressure';
```

**Output:**

<img width="1238" height="511" alt="image" src="https://github.com/user-attachments/assets/3c2b921f-3099-4e0d-8332-b69d6f4938d0" />

**Question 5**
```
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column.
```
Code
```sql
SELECT c.cust_name FROM CUSTOMER c
LEFT JOIN orders o
ON c.customer_id = o.customer_id;
```

**Output:**

<img width="1244" height="892" alt="image" src="https://github.com/user-attachments/assets/053a2729-97c5-411b-bf96-78a83af2e504" />

**Question 6**
```
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
Code
```sql
SELECT o.ord_no,o.ord_date,o.purch_amt,c.cust_name AS 'Customer Name',c.grade,s.name AS Salesman , s.commission 
from orders o
join customer c
on o.customer_id=c.customer_id
join salesman s
on o.salesman_id=s.salesman_id;
```

**Output:**

<img width="1240" height="896" alt="image" src="https://github.com/user-attachments/assets/ec553bef-93ce-486b-aa8d-b44c29f7698a" />

**Question 7**
```
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
Code
```sql
SELECT c.cust_name,c.city,c.grade,s.name AS Salesman , s.city FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE grade < 300
ORDER BY c.customer_id ASC
```

**Output:**

<img width="1238" height="815" alt="image" src="https://github.com/user-attachments/assets/64f32241-03ca-46b9-b7ef-298a20adb12b" />

**Question 8**
```
Write the SQL query that achieves the selection of the "cust_name" and "city" columns from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for customers in the city 'London'.
```
Code
```sql
SELECT c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt FROM CUSTOMER c
LEFT JOIN ORDERS o
ON c.customer_id = o.customer_id
WHERE city = 'London';
```

**Output:**

<img width="1233" height="582" alt="image" src="https://github.com/user-attachments/assets/57e55c54-e886-4065-9ce6-4bb051b6b521" />

**Question 9**
```
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.
```

```sql
SELECT s.name AS salesman_name , c.cust_name AS customer_name FROM salesman s
LEFT JOIN customer c
ON s.salesman_id = c.salesman_id
```
Code
**Output:**

<img width="1238" height="944" alt="image" src="https://github.com/user-attachments/assets/766d85e2-b33f-46e5-afc2-193c75b082c2" />

**Question 10**
```
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE
```
Code
```sql
SELECT p.first_name,s.* FROM Patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE first_name = 'Alice';
```

**Output:**

<img width="1236" height="510" alt="image" src="https://github.com/user-attachments/assets/80486d15-2137-4268-bb63-e7d221b82bee" />

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
