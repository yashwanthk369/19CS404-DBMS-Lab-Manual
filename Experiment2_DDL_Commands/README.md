# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
```
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
```
Code
```sql
CREATE TABLE Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary INTEGER CHECK(Salary > 0),
DepartmentID INTEGER REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1236" height="518" alt="image" src="https://github.com/user-attachments/assets/c96230bd-8883-43b9-852f-db7b92ea00f3" />


**Question 2**
```
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.
```
Code
```sql
INSERT INTO Student_details(RollNo,Name,Gender) VALUES(204,"Samuel Black","M");
```

**Output:**

<img width="1236" height="400" alt="image" src="https://github.com/user-attachments/assets/79e8aa98-0216-4498-bfb5-a5a416d9471c" />

**Question 3**
```
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
```
Code
```sql
CREATE TABLE Orders(
OrderID INTEGER PRIMARY KEY,
OrderDate DATE NOT NULL,
CustomerID INTEGER REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1236" height="376" alt="image" src="https://github.com/user-attachments/assets/9bb5d39f-d83e-4b2c-8d14-893ddf375b44" />

**Question 4**
```
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
```
Code
```sql
CREATE TABLE Bonuses(
BonusID INTEGER PRIMARY KEY,
EmployeeID INTEGER REFERENCES Employees(EmployeeID),
BonusAmount REAL check(BonusAmount > 0),
BonusDate DATE,
Reason TEXT NOT NULL
);
```

**Output:**

<img width="1241" height="375" alt="image" src="https://github.com/user-attachments/assets/25b60019-14e2-4eed-a57e-f9105824f342" />

**Question 5**
```
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.
```
Code
```sql
INSERT INTO Employee VALUES(001,"Sarah Parker","Manager","HR",60000);
```

**Output:**

<img width="1234" height="326" alt="image" src="https://github.com/user-attachments/assets/0dc5c899-58c4-47e4-8bc9-5628820719ef" />

**Question 6**
```
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
```
Code
```sql
CREATE TABLE Attendance(
AttendanceID INTEGER PRIMARY KEY,
EmployeeID INTEGER REFERENCES Employees(EmployeeID),
AttendanceDate DATE,
Status TEXT check(Status IN("Present","Absent","Leave"))
);
```

**Output:**

<img width="1238" height="374" alt="image" src="https://github.com/user-attachments/assets/e1dde314-9ad1-4ea1-9886-20332e77975a" />

**Question 7**
```
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
```
Code
```sql
INSERT INTO Books(ISBN,Title,Author) VALUES
("978-6655443321","Big Data Analytics","Karen Adams");
```

**Output:**

<img width="1238" height="419" alt="image" src="https://github.com/user-attachments/assets/f8fb5b15-317f-4388-8223-ceed53fceaae" />

**Question 8**
```
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```
Code
```sql
ALTER TABLE Student_details ADD COLUMN mobilenumb number;
```

**Output:**

<img width="1237" height="450" alt="image" src="https://github.com/user-attachments/assets/8e4ee11b-601c-456e-b52b-2cb1617593f2" />

**Question 9**
```
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
```

```sql
NSERT INTO Products(ProductID,Name,Category) VALUES(106,"Fitness Tracker","Wearables");
INSERT INTO Products(ProductID,Name,Category,Price,Stock) VALUES(107,"Laptop","Electronics",999.99,50);
INSERT INTO Products(ProductID,Name,Category,Stock) VALUES(108,"Wireless Earbud","Accessorie",100);
```

**Output:**

<img width="1238" height="380" alt="image" src="https://github.com/user-attachments/assets/d1b8fa9a-5649-40b4-8b72-83d9f9dae8ec" />

**Question 10**
```
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE
```

```sql
CREATE TABLE Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE
);
```

**Output:**

<img width="1238" height="468" alt="image" src="https://github.com/user-attachments/assets/3ccb450d-ca89-4d93-bd09-6c3b10700972" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
