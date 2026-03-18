# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

### CODE
```
DECLARE
   CURSOR cr1 IS 
      SELECT emp_name, designation FROM EMPLOYEE;

   name_var EMPLOYEE.emp_name%TYPE;
   des_var  EMPLOYEE.designation%TYPE;

BEGIN
   OPEN cr1;

   LOOP
      FETCH cr1 INTO name_var, des_var;
      EXIT WHEN cr1%NOTFOUND;

      DBMS_OUTPUT.PUT_LINE('Name: ' || name_var || ' Designation: ' || des_var);
   END LOOP;

   CLOSE cr1;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No data found.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Some error occurred.');
END;
/
```

### OUTPUT 

<img width="663" height="255" alt="image" src="https://github.com/user-attachments/assets/57e95c88-ed16-4096-94de-8c67d5bd4c59" />

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

### CODE 

```
DECLARE
   CURSOR cr1(p_min NUMBER, p_max NUMBER) IS
      SELECT emp_name, designation, salary 
      FROM EMPLOYEE
      WHERE salary BETWEEN p_min AND p_max;

   name_var EMPLOYEE.emp_name%TYPE;
   des_var  EMPLOYEE.designation%TYPE;
   sal_var  EMPLOYEE.salary%TYPE;

   v_min NUMBER := 20000;
   v_max NUMBER := 50000;

BEGIN
   OPEN cr1(v_min, v_max);

   LOOP
      FETCH cr1 INTO name_var, des_var, sal_var;
      EXIT WHEN cr1%NOTFOUND;

      DBMS_OUTPUT.PUT_LINE('Name: ' || name_var || 
                           ' Designation: ' || des_var || 
                           ' Salary: ' || sal_var);
   END LOOP;

   CLOSE cr1;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employees found in given salary range.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

### OUTPUT

<img width="662" height="256" alt="image" src="https://github.com/user-attachments/assets/cc79a7c9-8f43-4c09-8232-eba85db2a522" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

### CODE 

```
DECLARE
   CURSOR cr1 IS 
      SELECT emp_name, dept_no FROM EMPLOYEE;

   v_count NUMBER := 0;

BEGIN
   FOR rec IN cr1
   LOOP
      DBMS_OUTPUT.PUT_LINE('Name: ' || rec.emp_name || 
                           ' Department: ' || rec.dept_no);
      v_count := v_count + 1;
   END LOOP;

   IF v_count = 0 THEN
      RAISE NO_DATA_FOUND;
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employees found.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```
### OUTPUT

<img width="666" height="206" alt="image" src="https://github.com/user-attachments/assets/879d4ad0-e413-486c-86b0-c1090fc179ee" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

### CODE 

```
DECLARE
   CURSOR cr1 IS 
      SELECT * FROM EMPLOYEE;

   emp_rec EMPLOYEE%ROWTYPE;
   v_count NUMBER := 0;

BEGIN
   OPEN cr1;

   LOOP
      FETCH cr1 INTO emp_rec;
      EXIT WHEN cr1%NOTFOUND;

      DBMS_OUTPUT.PUT_LINE('ID: ' || emp_rec.emp_id || 
                           ' Name: ' || emp_rec.emp_name || 
                           ' Designation: ' || emp_rec.designation || 
                           ' Salary: ' || emp_rec.salary);

      v_count := v_count + 1;
   END LOOP;

   CLOSE cr1;

   IF v_count = 0 THEN
      RAISE NO_DATA_FOUND;
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employee records found.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

### OUTPUT

<img width="669" height="270" alt="image" src="https://github.com/user-attachments/assets/701e8a0f-4988-4f68-80ee-cbb5023d3bd3" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

### CODE 
```
DECLARE
   CURSOR cr1 IS 
      SELECT emp_id, salary 
      FROM EMPLOYEE
      WHERE dept_no = 10
      FOR UPDATE;

   v_emp_id EMPLOYEE.emp_id%TYPE;
   v_salary EMPLOYEE.salary%TYPE;
   v_count NUMBER := 0;

BEGIN
   OPEN cr1;

   LOOP
      FETCH cr1 INTO v_emp_id, v_salary;
      EXIT WHEN cr1%NOTFOUND;

      UPDATE EMPLOYEE
      SET salary = v_salary + 5000
      WHERE CURRENT OF cr1;

      v_count := v_count + 1;
   END LOOP;

   CLOSE cr1;

   IF v_count = 0 THEN
      RAISE NO_DATA_FOUND;
   ELSE
      DBMS_OUTPUT.PUT_LINE('Salary updated successfully.');
   END IF;

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employees found in given department.');

   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

### OUTPUT

<img width="669" height="220" alt="image" src="https://github.com/user-attachments/assets/28bb5811-456c-4b9e-ab57-b3d9159c525a" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

