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
--
<img width="1196" height="185" alt="image" src="https://github.com/user-attachments/assets/50b0aa00-1b16-42a8-a0c7-ea34728166e7" />

```sql
DELETE FROM Doctors
WHERE specialization = 'Pediatrics'
AND first_name = 'Michael';
```

**Output:**

<img width="1342" height="458" alt="image" src="https://github.com/user-attachments/assets/57c9665d-92bb-445b-a62a-7e8375f72003" />

**Question 2**
---
<img width="930" height="604" alt="image" src="https://github.com/user-attachments/assets/00a01e47-0674-4823-842f-a81c8b85f960" />

```sql
SELECT id, value1, ABS(value1) AS absolute_value
FROM Calculations;

```

**Output:**

<img width="1059" height="376" alt="image" src="https://github.com/user-attachments/assets/cbd441bd-da70-490a-8981-7a724b438b0b" />

**Question 3**
---
<img width="1380" height="651" alt="image" src="https://github.com/user-attachments/assets/fcecd808-bf32-4efa-a1d1-0bc3d83afa05" />

```sql
SELECT 
    product_id,
    original_price,
    discount_percentage,
    original_price - (original_price * discount_percentage) AS discounted_price
FROM Products
WHERE (original_price - (original_price * discount_percentage)) > 100;

```

**Output:**

<img width="1452" height="365" alt="image" src="https://github.com/user-attachments/assets/b2e71a34-ac38-40bb-9886-4b0b82249744" />

**Question 4**
---
<img width="1043" height="708" alt="image" src="https://github.com/user-attachments/assets/0e4867d1-8860-4f50-a83d-15bd9444f798" />

```sql
SELECT 
    ename,
    hiredate,
    CASE strftime('%w', hiredate)
        WHEN '0' THEN 'Sunday'
        WHEN '1' THEN 'Monday'
        WHEN '2' THEN 'Tuesday'
        WHEN '3' THEN 'Wednesday'
        WHEN '4' THEN 'Thursday'
        WHEN '5' THEN 'Friday'
        WHEN '6' THEN 'Saturday'
    END AS day_of_week
FROM emp;

```

**Output:**

<img width="854" height="460" alt="image" src="https://github.com/user-attachments/assets/cf8c2b80-1776-4bf6-80d5-c2f1d58d8682" />

**Question 5**
---
<img width="951" height="673" alt="image" src="https://github.com/user-attachments/assets/684a2f69-3bea-47e3-8936-c8afffd07cfc" />

```sql
UPDATE Employees
SET hire_date = '2024-01-24'
WHERE department_id = 50;

```

**Output:**

<img width="1392" height="343" alt="image" src="https://github.com/user-attachments/assets/52fa930b-5103-4bd9-a1c8-b2a5e4c86cdd" />

**Question 6**
---
<img width="1445" height="607" alt="image" src="https://github.com/user-attachments/assets/d7351c3e-b28b-422a-8dca-04ab1997db75" />

```sql
UPDATE purchases
SET 
    per_unit_price = 25,
    total_price = quantity * 25
WHERE purchase_date = '2022-08-15'
AND product_id = 12;
```

**Output:**

<img width="1676" height="382" alt="image" src="https://github.com/user-attachments/assets/a559f798-16fd-42b8-b434-9a59931277f1" />

**Question 7**
---
<img width="1508" height="579" alt="image" src="https://github.com/user-attachments/assets/ebe79ffa-be89-4f9d-9c2a-86639de52d3c" />

```sql

DELETE FROM customer
WHERE OPENING_AMT BETWEEN 4000 AND 6000;


```

**Output:**

<img width="1874" height="393" alt="image" src="https://github.com/user-attachments/assets/e2f6174b-2808-4cea-bc1c-bde44abdbaa3" />

**Question 8**
---
<img width="926" height="430" alt="image" src="https://github.com/user-attachments/assets/d01928a4-bf45-4427-96ad-ae56d93c380a" />

```sql
SELECT 
    strftime('%Y', hiredate) AS Year,
    strftime('%m', hiredate) AS Month,
    strftime('%d', hiredate) AS Day
FROM emp;


```

**Output:**

<img width="978" height="516" alt="image" src="https://github.com/user-attachments/assets/56cc16f2-6392-4d2c-b73f-d81a14c992b7" />

**Question 9**
---
<img width="1755" height="589" alt="image" src="https://github.com/user-attachments/assets/cbfcb37e-4f32-4988-8baf-4ed02be66f4f" />

```sql

DELETE FROM Customer
WHERE CUST_COUNTRY NOT IN ('UK', 'USA', 'Canada')
AND GRADE >= 3;

```

**Output:**

<img width="1888" height="295" alt="image" src="https://github.com/user-attachments/assets/14372828-92cc-43ce-8f46-99a6354082d6" />

**Question 10**
---
<img width="1821" height="692" alt="image" src="https://github.com/user-attachments/assets/25376624-1959-4632-8d03-4d3ea60f4b21" />

```sql
SELECT
    product_id,
    original_price,
    discount_percentage,
    original_price - (original_price * discount_percentage) AS discounted_price
FROM Products
WHERE original_price BETWEEN 50 AND 150;
```

**Output:**

<img width="1572" height="381" alt="image" src="https://github.com/user-attachments/assets/d05e839d-584c-41c0-b51e-62f7430234d2" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
