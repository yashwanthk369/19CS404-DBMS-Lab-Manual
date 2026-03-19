# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

### CODE 
```
CREATE OR REPLACE PROCEDURE cal_square(n NUMBER) IS
  v_square NUMBER;
BEGIN
  v_square := n * n;
  DBMS_OUTPUT.PUT_LINE('Square of ' || n || ' is ' || v_square);
END;
/

BEGIN
  cal_square(6);
END;
/
```

### OUTPUT

<img width="1000" height="233" alt="image" src="https://github.com/user-attachments/assets/1c1ddf91-68da-48ab-a09a-56a2d686de6f" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

### CODE
```
CREATE OR REPLACE FUNCTION get_factorial(n NUMBER)
RETURN NUMBER IS
  fact NUMBER := 1;
BEGIN
  FOR i IN 1..n LOOP
    fact := fact * i;
  END LOOP;

  RETURN fact;
END;
DECLARE
  result NUMBER;
BEGIN
  result := get_factorial(5);
  DBMS_OUTPUT.PUT_LINE('Factorial is ' || result);
END;
/
```
### OUTPUT

<img width="677" height="224" alt="image" src="https://github.com/user-attachments/assets/6a397d36-51ac-4348-96cd-298e8cf127cc" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

### CODE 
```
CREATE OR REPLACE PROCEDURE cal_even(n NUMBER) IS
BEGIN
  if (n MOD 2 = 0) THEN
  DBMS_OUTPUT.PUT_LINE(n||' is even');
  ELSE
  DBMS_OUTPUT.PUT_LINE(n||' is odd');
  END IF;
  END cal_even;
/

BEGIN
  cal_even(12);
END;
/
```
### OUTPUT

<img width="982" height="331" alt="image" src="https://github.com/user-attachments/assets/138d7ffd-3493-446c-929f-263a20bb37fd" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

### CODE
```
CREATE OR REPLACE FUNCTION reverse_number(n NUMBER)
RETURN NUMBER IS
  rev NUMBER := 0;
  temp NUMBER := n;
  digit NUMBER;
BEGIN
  WHILE temp > 0 LOOP
    digit := MOD(temp, 10);
    rev := rev * 10 + digit;
    temp := TRUNC(temp / 10);
  END LOOP;

  RETURN rev;
END;
/
DECLARE
  result NUMBER;
BEGIN
  result := reverse_number(1234);
  DBMS_OUTPUT.PUT_LINE('Reversed number is ' || result);
END;
/
```
### OUTPUT

<img width="979" height="192" alt="image" src="https://github.com/user-attachments/assets/25250918-8902-42c9-9596-74cb9f56158e" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

### CODE 
```
CREATE OR REPLACE PROCEDURE print_table(n NUMBER) IS
BEGIN
  DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || n || ':');

  FOR i IN 1..10 LOOP
    DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
  END LOOP;

END print_table;
/
BEGIN
  print_table(5);
END;
/
```
### OUTPUT 

<img width="992" height="348" alt="image" src="https://github.com/user-attachments/assets/cea1a0e3-91a7-46af-9134-686f6a9bedec" />

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
