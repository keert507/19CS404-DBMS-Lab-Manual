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

**Output:**  
The program should display the employee details or an error message.

```
-- Create employees table
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'Zayn', 'Manager');
INSERT INTO employees VALUES (2, 'Tara', 'Developer');
INSERT INTO employees VALUES (3, 'Amit', 'Tester');

COMMIT;

-- PL/SQL Program using Simple Cursor with Exception Handling
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_name);
        DBMS_OUTPUT.PUT_LINE('Designation : ' || v_designation);
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

<img width="818" height="799" alt="image" src="https://github.com/user-attachments/assets/833d3178-9187-43be-8a19-e73e59f1c9ee" />


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

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

```
-- Add salary column
ALTER TABLE employees
ADD salary NUMBER;

-- Insert sample salary values
UPDATE employees SET salary = 50000 WHERE emp_id = 1;
UPDATE employees SET salary = 35000 WHERE emp_id = 2;
UPDATE employees SET salary = 25000 WHERE emp_id = 3;

COMMIT;

-- PL/SQL Program using Parameterized Cursor
DECLARE
    CURSOR emp_cursor(p_min NUMBER, p_max NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN p_min AND p_max;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_salary employees.salary%TYPE;

    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor(30000, 60000);

    LOOP
        FETCH emp_cursor INTO v_name, v_designation, v_salary;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Name: ' || v_name ||
            ', Designation: ' || v_designation ||
            ', Salary: ' || v_salary
        );
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the given salary range.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

<img width="784" height="733" alt="image" src="https://github.com/user-attachments/assets/137da905-8b5e-4a40-867f-f329a7827f2a" />

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

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

```
-- Add dept_no column
ALTER TABLE employees
ADD dept_no NUMBER;

-- Insert sample department numbers
UPDATE employees SET dept_no = 101 WHERE emp_id = 1;
UPDATE employees SET dept_no = 102 WHERE emp_id = 2;
UPDATE employees SET dept_no = 103 WHERE emp_id = 3;

COMMIT;

-- PL/SQL Program using Cursor FOR Loop
DECLARE
    v_count NUMBER := 0;

BEGIN
    FOR emp_rec IN (
        SELECT emp_name, dept_no
        FROM employees
    )
    LOOP
        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || emp_rec.emp_name ||
            ', Department No: ' || emp_rec.dept_no
        );
    END LOOP;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

<img width="800" height="830" alt="image" src="https://github.com/user-attachments/assets/e6ceb987-caca-441e-be0b-a659fc8156a4" />

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

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

```
-- Create employees table
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'Zayn', 'Manager', 50000);
INSERT INTO employees VALUES (2, 'Tara', 'Developer', 35000);
INSERT INTO employees VALUES (3, 'Amit', 'Tester', 25000);

COMMIT;

-- PL/SQL Program using Cursor with %ROWTYPE
DECLARE
    CURSOR emp_cursor IS
        SELECT * FROM employees;

    emp_record emp_cursor%ROWTYPE;

    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_record;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || emp_record.emp_id ||
            ', Name: ' || emp_record.emp_name ||
            ', Designation: ' || emp_record.designation ||
            ', Salary: ' || emp_record.salary
        );
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

<img width="806" height="842" alt="image" src="https://github.com/user-attachments/assets/09210e14-e5c3-45ee-9e92-85c143e2e544" />

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

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

```
-- Create employees table
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    dept_no NUMBER,
    salary NUMBER
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'Zayn', 101, 50000);
INSERT INTO employees VALUES (2, 'Tara', 102, 35000);
INSERT INTO employees VALUES (3, 'Amit', 101, 25000);

COMMIT;

-- PL/SQL Program using FOR UPDATE Cursor
DECLARE
    CURSOR emp_cursor IS
        SELECT *
        FROM employees
        WHERE dept_no = 101
        FOR UPDATE;

    v_emp employees%ROWTYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp;
        EXIT WHEN emp_cursor%NOTFOUND;

        UPDATE employees
        SET salary = salary + 5000
        WHERE CURRENT OF emp_cursor;

        v_count := v_count + 1;
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    ELSE
        DBMS_OUTPUT.PUT_LINE('Employee salaries updated successfully.');
    END IF;

    COMMIT;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the department.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```

<img width="814" height="780" alt="image" src="https://github.com/user-attachments/assets/0f7f461e-78d6-4418-b411-c7d41a7494a0" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

