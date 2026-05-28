# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
<img width="1174" height="656" alt="image" src="https://github.com/user-attachments/assets/1ebbe2d9-56cc-4aff-ae03-63cadd03edd9" />

```sql
select *
from GRADES
where(subject,grade) in(select subject,min(grade)
from GRADES
group by subject
);
```

**Output:**

<img width="1229" height="459" alt="image" src="https://github.com/user-attachments/assets/b1decf5d-fda8-4468-b6be-3d43915ae78f" />

**Question 2**
---
<img width="1182" height="479" alt="image" src="https://github.com/user-attachments/assets/a829b947-b44c-4f89-a94b-ebb72fc96c09" />

```sql
select *
from Orders
where salesman_id in (select distinct salesman_id
from Orders
where customer_id=3007
);
```

**Output:**

<img width="1140" height="458" alt="image" src="https://github.com/user-attachments/assets/5efcf0c3-1639-494a-b875-1045de58b2f7" />

**Question 3**
---
<img width="862" height="588" alt="image" src="https://github.com/user-attachments/assets/3f6ed53b-aa88-45d4-88c2-2bae1bdb5d80" />

```sql
select *
from CUSTOMERS
where SALARY<2500;
```

**Output:**

<img width="1096" height="465" alt="image" src="https://github.com/user-attachments/assets/63b20338-927b-45c3-b598-bdfb832c1336" />

**Question 4**
---
<img width="986" height="591" alt="image" src="https://github.com/user-attachments/assets/a1ce4f81-f22a-43e0-9325-066855c558dc" />

```sql
select *
from Employee
where age<(
select AVG(age)
from employee
where income>250000);
```

**Output:**

<img width="1244" height="521" alt="image" src="https://github.com/user-attachments/assets/a7d5ea4d-0785-4805-99c3-f9fcea5b2537" />

**Question 5**
---
<img width="870" height="567" alt="image" src="https://github.com/user-attachments/assets/42838cd1-fb41-491d-a129-6a7c8a658404" />

```sql
select *
from CUSTOMERS
where SALARY=1500;
```

**Output:**

<img width="1095" height="355" alt="image" src="https://github.com/user-attachments/assets/8f307560-0c1c-4665-bd36-eae19b921320" />

**Question 6**
---
<img width="1184" height="568" alt="image" src="https://github.com/user-attachments/assets/caa39734-ab81-49f3-ad31-beb19c9524f1" />

```sql
select
ord_no,
purch_amt,
ord_date,
customer_id,
salesman_id
from Orders
where salesman_id=(
select salesman_id
from salesman
where name='Paul Adam'
);
```

**Output:**

<img width="1162" height="418" alt="image" src="https://github.com/user-attachments/assets/325e0c4b-bbac-4424-9eb6-57317ea781cc" />

**Question 7**
---
<img width="894" height="673" alt="image" src="https://github.com/user-attachments/assets/d4e4a61f-6d76-4d32-a4b6-213b93018061" />

```sql
select*
from CUSTOMERS
where SALARY>1500;
```

**Output:**

<img width="1140" height="605" alt="image" src="https://github.com/user-attachments/assets/8b917110-f6e4-49a4-8340-992640cf8258" />

**Question 8**
---
<img width="1182" height="426" alt="image" src="https://github.com/user-attachments/assets/4cdd3fe7-4db7-41da-9f22-c845d1fea54a" />

```sql
select grade,COUNT(*)
from customer
where grade>(
select AVG(grade)
from customer
where city='New York'
)
group by grade;
```

**Output:**

<img width="571" height="358" alt="image" src="https://github.com/user-attachments/assets/a1c05ef6-05f1-4784-8584-b4ee90c83838" />

**Question 9**
---
<img width="1189" height="714" alt="image" src="https://github.com/user-attachments/assets/c276addc-89f3-4314-9132-60556df7b8a2" />

```sql
select 
ord_no,
purch_amt,
ord_date,
customer_id,
salesman_id
from ORDERS
where salesman_id in(select salesman_id
from salesman
where city='New York');
```

**Output:**

<img width="1126" height="509" alt="image" src="https://github.com/user-attachments/assets/2a8dcc3b-c5a9-4068-b97c-786b3226f900" />

**Question 10**
---
<img width="747" height="293" alt="image" src="https://github.com/user-attachments/assets/bc440743-8596-45fb-81a0-e908a663bab0" />

```sql
select *
from Departments
where LENGTH(department_name)>(
select AVG(LENGTH(department_name))
from Departments
);
```

**Output:**

<img width="591" height="420" alt="image" src="https://github.com/user-attachments/assets/0f6c3f3b-4aaa-4679-8722-d6bc819ad49b" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
