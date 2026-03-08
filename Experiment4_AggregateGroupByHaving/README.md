# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
```
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```
Code
```sql
SELECT avg(income) AS Average_Salary FROM employee
```

**Output:**

<img width="1237" height="398" alt="image" src="https://github.com/user-attachments/assets/d4d532ad-430d-4913-a0e7-adadd51ce39a" />

**Question 2**
```
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
```
Code
```sql
SELECT count(customer_id) AS COUNT FROM customer
```

**Output:**

<img width="1237" height="405" alt="image" src="https://github.com/user-attachments/assets/39dc4052-6465-47e3-8ea2-3e2f67f491cb" />

**Question 3**
```
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```
Code
```sql
SELECT COUNT(DISTINCT salesman_id) AS COUNT FROM orders
```

**Output:**

<img width="1240" height="400" alt="image" src="https://github.com/user-attachments/assets/a0e2f5e2-c10b-4809-bf06-8ea9193d552d" />

**Question 4**
```
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table
```
Code
```sql
SELECT PatientID , count(Medications) AS AvgMedications FROM MedicalRecords group by PatientID
```

**Output:**

<img width="1236" height="691" alt="image" src="https://github.com/user-attachments/assets/65126913-77c7-4eaf-8b87-08fa1cf38553" />

**Question 5**
```
What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE
```
Code
```sql
SELECT InsuranceCompany, AVG(EndDate - StartDate) AS AvgCoverageDurationDays FROM Insurance GROUP BY InsuranceCompany
```

**Output:**

<img width="1241" height="770" alt="image" src="https://github.com/user-attachments/assets/b35874c1-b203-4da2-ae27-0a0ee206eaac" />


**Question 6**
```
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```
Code
```sql
SELECT avg(income) AS avg_income FROM employee WHERE name LIKE ('A%');
```

**Output:**

<img width="1239" height="399" alt="image" src="https://github.com/user-attachments/assets/60199b3f-4cd0-4128-a2d4-6ad255cb12c5" />

**Question 7**
```
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```
Code
```sql
SELECT name AS Employee_Name , age AS Age FROM employee ORDER BY Age ASC LIMIT 1;
```

**Output:**

<img width="1231" height="401" alt="image" src="https://github.com/user-attachments/assets/9834c63c-caae-4dd3-8792-04c781e649cb" />

**Question 8**
```
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1
```
Code
```sql
SELECT address,AVG(salary) FROM customer1 GROUP BY address HAVING salary > 5000
```

**Output:**

<img width="1239" height="527" alt="image" src="https://github.com/user-attachments/assets/ec9c00cd-78ab-4dd0-8a9c-06b5c5e7ab9d" />

**Question 9**
```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the maximum work hours for each date, and excludes dates where the maximum work hour is not greater than 12.

Sample table: employee1
```
Code
```sql
SELECT jdate,MAX(workhour) FROM employee1 GROUP BY jdate HAVING workhour > 12
```

**Output:**

<img width="1239" height="470" alt="image" src="https://github.com/user-attachments/assets/4d88c4f1-1650-479a-891d-af7d37fe281a" />

**Question 10**
```
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee
```
Code
```sql
SELECT age,MIN(income) as Income FROM employee GROUP BY age HAVING income < 1000000
```

**Output:**

<img width="1236" height="525" alt="image" src="https://github.com/user-attachments/assets/502f47d0-60fc-4941-af8d-73323df0eadf" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
