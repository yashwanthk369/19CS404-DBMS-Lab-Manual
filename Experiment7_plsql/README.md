# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

### CODE 

```
DECLARE
   a NUMBER := 10;
   b NUMBER := 20;
BEGIN
   IF a > b THEN
      DBMS_OUTPUT.PUT_LINE('A is greatest');
   ELSE
      DBMS_OUTPUT.PUT_LINE('B is greatest');
   END IF;
END;
/
```

**Expected Output:**  
Greater number is: 80

### OUTPUT

<img width="680" height="223" alt="image" src="https://github.com/user-attachments/assets/f3dd2320-b34a-4b1e-b6f8-737dfb19f103" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

### CODE

```
DECLARE
   n NUMBER := &n;
   sum NUMBER := 0;
BEGIN
    FOR i IN 1..n LOOP
    sum := sum + i;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Sum of first '||n|| 'natural numbers is: ' || sum);
END;
/
```

**Expected Output:**  
Sum of first 10 natural numbers is: 55

### OUTPUT 

<img width="674" height="219" alt="image" src="https://github.com/user-attachments/assets/ce017ebe-2102-4af9-9e6d-43779ed6b0b7" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

### CODE
```
DECLARE
   n NUMBER := &n;
   a NUMBER := 0;
   b NUMBER := 1;
   c NUMBER;
BEGIN
    FOR i IN 3..n LOOP
    c := a + b;
    DBMS_OUTPUT.PUT_LINE(c);
    a := b;
    b := c;
    END LOOP;
END;
```

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

### OUTPUT 

<img width="674" height="292" alt="image" src="https://github.com/user-attachments/assets/22033f0e-6496-4685-8982-34198bb5ab1e" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

### CODE 

```
DECLARE
   n NUMBER := &n;
   rev NUMBER := 0;
   digit NUMBER;
BEGIN
   WHILE n > 0 LOOP
   digit := n MOD 10;
   rev := rev * 10 + digit;
   n := TRUNC(n / 10);
   END LOOP;
   DBMS_OUTPUT.PUT_LINE(rev);
END;
```

**Expected Output:**  
n = 1535  
Reversed number is 5351

### OUTPUT

<img width="678" height="223" alt="image" src="https://github.com/user-attachments/assets/d983d53c-1fb5-4427-bb38-aca451455a94" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

### CODE 
```
DECLARE
   a NUMBER := &a;
   b NUMBER := &b;
   c NUMBER := &c;
BEGIN
   IF a > b AND a > c THEN
      DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || a);
   ELSIF b > a AND b > c THEN
      DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || b);
   ELSE
      DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || c);
   END IF;
END;
/
```

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

### OUTPUT

<img width="677" height="221" alt="image" src="https://github.com/user-attachments/assets/c36ff035-acc1-4938-89ff-a4edffe66309" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
