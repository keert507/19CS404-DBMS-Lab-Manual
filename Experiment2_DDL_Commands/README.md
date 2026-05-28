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
--
-- Paste Question 1 here
<img width="784" height="164" alt="image" src="https://github.com/user-attachments/assets/6c162279-7307-427c-a4dd-7c59cce09390" />


```sql

create table Attendance(
 AttendanceID INTEGER PRIMARY KEY,
 EmployeeID INTEGER,
 AttendanceDate DATE,
 Status TEXT check(Status in ('Present','Absent','Leave')),
 foreign key(EmployeeID) references employees(EmployeeID));
 
```

**Output:**

<img width="1725" height="272" alt="image" src="https://github.com/user-attachments/assets/e73e33ed-16c6-417f-8310-2e1a2b807437" />

**Question 2**
---
<img width="1448" height="361" alt="image" src="https://github.com/user-attachments/assets/7eef9d16-7a9b-4564-aa9f-1b8d6e916d17" />

```sql

create table Department (
DepartmentID INTEGER primary key,
DepartmentName TEXT UNIQUE not null,
Location TEXT);



```

**Output:**

<img width="1839" height="265" alt="image" src="https://github.com/user-attachments/assets/c7356540-ab3e-42a6-8df2-a1be5498bfe7" />

**Question 3**
---
<img width="854" height="193" alt="image" src="https://github.com/user-attachments/assets/aeec70af-61a1-4496-be37-1706b8fc2e04" />

```sql

insert into Employee(EmployeeID,Name,Position,Department,Salary)
values(001,'Sarah Parker','Manager','HR',60000);


```

**Output:**

<img width="1838" height="313" alt="image" src="https://github.com/user-attachments/assets/86ddfbaa-8b9a-4050-b054-d9ea331cb1ae" />

**Question 4**
---
<img width="1215" height="660" alt="image" src="https://github.com/user-attachments/assets/a215f33a-feb0-40b7-a5bd-910bdd555de4" />

```sql

alter table Companies
add designation varchar(50);
alter table Companies
add net_salary  number;
alter table Companies
add dob date;


```

**Output:**

<img width="1716" height="434" alt="image" src="https://github.com/user-attachments/assets/2b19c8a6-7092-4323-a893-c9cd277e2851" />

**Question 5**
---
<img width="1590" height="365" alt="image" src="https://github.com/user-attachments/assets/f960e948-4b32-4c49-9324-7aef95fe49dc" />

```sql

create table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
Amount Real check(Amount>0),
DueDate DATE check(DueDate>InvoiceDate),
OrderID INTEGER,
foreign key(OrderID) references Orders(OrderID))


```

**Output:**

<img width="1890" height="272" alt="image" src="https://github.com/user-attachments/assets/6a72ce3a-dd6a-4fa3-907c-da467c1a0f61" />

**Question 6**
---
<img width="1398" height="433" alt="image" src="https://github.com/user-attachments/assets/4f46d53c-3027-47cb-bfee-39fce0f56c1b" />

```sql

ALTER TABLE Companies RENAME COLUMN name TO first_name;
ALTER TABLE Companies ADD COLUMN mobilenumber number;
ALTER TABLE Companies ADD COLUMN DOB Date;
ALTER TABLE Companies ADD COLUMN State varchar(30);



```

**Output:**

<img width="1781" height="474" alt="image" src="https://github.com/user-attachments/assets/ca9102d9-49a8-4666-8558-cfbd5b8792f5" />

**Question 7**
---
<img width="1705" height="438" alt="image" src="https://github.com/user-attachments/assets/2ea51568-125b-4b11-92e5-fe00d7d12167" />

```sql

INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-1234567890', 'Introduction to AI', 'John Doe', NULL, NULL);

INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-9876543210', 'Deep Learning', 'Jane Doe', 'TechPress', 2022);

INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-1122334455', 'Cybersecurity Essentials', 'Alice Smith', NULL, 2021);

```

**Output:**

<img width="1686" height="309" alt="image" src="https://github.com/user-attachments/assets/73e3ade0-539a-437f-9a05-3bf88d053bf6" />

**Question 8**
---

<img width="868" height="348" alt="image" src="https://github.com/user-attachments/assets/ce0dcdb1-cdd5-44b2-94e6-476679fdd364" />

```sql
CREATE TABLE Orders (
    OrderID INTEGER,
    OrderDate TEXT,
    CustomerID INTEGER
);


```

**Output:**

<img width="1620" height="374" alt="image" src="https://github.com/user-attachments/assets/5000f5d5-b74c-4d8c-8d35-f62c5049c54e" />

**Question 9**
---
<img width="1035" height="209" alt="image" src="https://github.com/user-attachments/assets/6a383ca3-a0ac-4d7e-a723-918384d3d8dc" />

```sql
INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES (101, 'Laptop', 'Electronics', 1500, 50);

```

**Output:**

<img width="1479" height="282" alt="image" src="https://github.com/user-attachments/assets/dedf3276-8a73-4bd9-bf7b-e86149de8849" />

**Question 10**
---
<img width="1790" height="400" alt="image" src="https://github.com/user-attachments/assets/b1257c26-e45d-4d51-b769-7e5b272584eb" />

```sql
CREATE TABLE contacts (
    contact_id INTEGER PRIMARY KEY,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT,
    phone TEXT NOT NULL CHECK(length(phone) >= 10)
);
```

**Output:**

<img width="1880" height="219" alt="image" src="https://github.com/user-attachments/assets/909bbdb1-5f8f-457f-874e-b58f4fbd1475" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
