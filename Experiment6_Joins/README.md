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
--
<img width="1210" height="860" alt="image" src="https://github.com/user-attachments/assets/efff2e97-4f87-4abf-92c8-bc7ccc7ca42b" />

```sql
select
c.cust_name as "Customer Name",
c.city as "city",
s.name as "Salesman",
s.commission
from customer c
join salesman s
on c.salesman_id=s.salesman_id
where s.commission>0.12;
```

**Output:**

<img width="1238" height="683" alt="image" src="https://github.com/user-attachments/assets/c33c9cad-af5b-47f3-96b4-c58f8d8eb955" />

**Question 2**
---
<img width="1256" height="908" alt="image" src="https://github.com/user-attachments/assets/c3360f83-01b3-47a4-a36b-979dd0e1eb31" />

```sql
select
c.cust_name,
c.city,
o.ord_no,
o.ord_date,
o.purch_amt as "Order Amount"
from customer c
left join orders o
on c.customer_id=o.customer_id
order by o.ord_date ASC;
```

**Output:**

<img width="1230" height="911" alt="image" src="https://github.com/user-attachments/assets/1014469f-ef79-4ba9-916a-3aeb3b3859f3" />

**Question 3**
---
<img width="1556" height="585" alt="image" src="https://github.com/user-attachments/assets/8ad65292-1241-41bb-a7d8-9dd2b7d8d617" />

```sql
select
p.first_name as patient_name
from
PATIENTS p
inner join
doctors d on p.doctor_id=d.doctor_id
where
d.first_name="Emily"
and d.last_name="Johnson"
and p.discharge_date is not null;
```

**Output:**

<img width="475" height="451" alt="image" src="https://github.com/user-attachments/assets/7f9ec906-9a80-4fdc-bdb6-61c4b412de97" />

**Question 4**
---
<img width="1593" height="783" alt="image" src="https://github.com/user-attachments/assets/78d7b39f-487d-4257-82ec-0041dba6a1cf" />

```sql
select 
s.name as salesman_name,
c.cust_name as customer_name
from
salesman s
left join
customer c on s.salesman_id=c.salesman_id;
```

**Output:**

<img width="755" height="936" alt="image" src="https://github.com/user-attachments/assets/c1a005ca-05c2-4b53-92c5-3d1721cdd413" />

**Question 5**
---
<img width="1600" height="566" alt="image" src="https://github.com/user-attachments/assets/363df3ee-570f-4604-949b-7278e292b6af" />

```sql
select
p.date_of_birth,
a.*
from 
patients p
inner join 
appointments a on p.patient_id=a.patient_id
where
p.first_name="Alice";
```

**Output:**

<img width="1610" height="435" alt="image" src="https://github.com/user-attachments/assets/52205770-4a25-42db-a4cc-6d203c83d46d" />

**Question 6**
---
<img width="1580" height="759" alt="image" src="https://github.com/user-attachments/assets/08f3d8e4-eb4c-48f1-b123-8e989ae40d50" />

```sql
select
p.*,
d.specialization as doctor_specialization
from
PATIENTS p
inner join
doctors d on p.doctor_id=d.doctor_id;
```

**Output:**

<img width="1604" height="606" alt="image" src="https://github.com/user-attachments/assets/c15f1855-308e-491c-b71f-9168c06a3ec0" />

**Question 7**
---
<img width="998" height="852" alt="image" src="https://github.com/user-attachments/assets/e5fc4f67-6e40-4a36-b468-1001779d886c" />

```sql
select 
s.name as Salesman,
c.cust_name,
s.city
from
salesman s
join
customer c on s.city=c.city;
```

**Output:**

<img width="1017" height="654" alt="image" src="https://github.com/user-attachments/assets/bb83ca24-cd6e-472f-ad08-1033d9aca44f" />

**Question 8**
---
<img width="1579" height="823" alt="image" src="https://github.com/user-attachments/assets/5550d06a-1fcf-40bd-8e95-d3eb8396a3d8" />

```sql
select
c.cust_name as "Customer Name",
c.city as "city",
s.name as "Salesman",
s.city as "city",
s.commission
from
customer c
join salesman s on c.salesman_id=s.salesman_id
where
c.city<>s.city
and s.commission >0.12;
```

**Output:**

<img width="1557" height="616" alt="image" src="https://github.com/user-attachments/assets/4e212feb-d0f0-46d0-ac62-750f872c7a10" />

**Question 9**
---
<img width="1592" height="607" alt="image" src="https://github.com/user-attachments/assets/e7ef7481-4263-4705-b6fd-64ca6daa789e" />

```sql
select
p.first_name as patient_name,
t.test_name
from
PATIENTS  p
inner join
test_results t on p.patient_id=t.patient_id;
```

**Output:**

<img width="778" height="572" alt="image" src="https://github.com/user-attachments/assets/d090a13d-6cdd-4c0a-bacb-3b21640af7bd" />

**Question 10**
---
<img width="1394" height="888" alt="image" src="https://github.com/user-attachments/assets/00229e31-c679-4f90-9ab1-2faab098af36" />

```sql
select
c.cust_name,
c.city,
c.grade,
s.name as Salesman,
s.city as city
from customer c
inner join salesman s
on c.salesman_id=s.salesman_id
order by c.customer_id ASC;
```

**Output:**

<img width="1508" height="880" alt="image" src="https://github.com/user-attachments/assets/e9dfe836-376b-4f02-bba2-d6044d739e3e" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
