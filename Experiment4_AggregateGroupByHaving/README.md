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
--
<img width="1028" height="457" alt="image" src="https://github.com/user-attachments/assets/61c022de-bc6c-4212-b431-b70952d774b9" />

```sql
select max(age)-min(age) as age_difference
from employee;
```

**Output:**
<img width="619" height="396" alt="image" src="https://github.com/user-attachments/assets/819bad7c-d102-4e53-b7cc-49e4b5ea162d" />


**Question 2**
---
<img width="637" height="494" alt="image" src="https://github.com/user-attachments/assets/8d51462b-9e9f-4498-be4a-1fdecb0c8a3b" />

```sql

select min(purch_amt) as MINIMUM
from orders;
```

**Output:**

<img width="440" height="376" alt="image" src="https://github.com/user-attachments/assets/a2a310f6-3159-4b16-ab0a-3c954c787795" />

**Question 3**
---
<img width="891" height="466" alt="image" src="https://github.com/user-attachments/assets/a1da6165-22f2-45db-aaf7-fa6447d50de3" />

```sql
select sum(purch_amt) as TOTAL
from orders;
```

**Output:**

<img width="525" height="385" alt="image" src="https://github.com/user-attachments/assets/1f718c78-ce3a-48a8-af1a-fe5ae9d46bcc" />

**Question 4**
---
<img width="1035" height="648" alt="image" src="https://github.com/user-attachments/assets/c2f155f6-c33e-4a6c-a44d-f0c99752fa0f" />

```sql
select DoctorID,count (PrescriptionID) as TotalPrescriptions
from Prescriptions
group by DoctorID;
```

**Output:**

<img width="769" height="824" alt="image" src="https://github.com/user-attachments/assets/a96e3d1c-ebfb-492c-942f-d3e31c0247cf" />

**Question 5**
---
<img width="756" height="501" alt="image" src="https://github.com/user-attachments/assets/0ef281cb-4c46-42d7-8b40-a75b1e066f43" />


```sql
select PatientID,count(Medications) as AvgMedications
from MedicalRecords
group by PatientID;
```

**Output:**

<img width="758" height="677" alt="image" src="https://github.com/user-attachments/assets/193ca961-e70c-4386-b422-ef43394cf5d9" />

**Question 6**
---
<img width="712" height="643" alt="image" src="https://github.com/user-attachments/assets/726adf35-2218-4155-8acd-adda3a0c7999" />

```sql
select PatientID,count(Medication) as TotalMedications
from Prescriptions
group by PatientID;
```

**Output:**

<img width="782" height="758" alt="image" src="https://github.com/user-attachments/assets/54e6bcc1-e2ec-4cbe-b4e9-7da9c6675746" />

**Question 7**
---
<img width="1185" height="480" alt="image" src="https://github.com/user-attachments/assets/90965ff5-d30a-4ecf-b550-79419c2ce039" />

```sql
select category_id,AVG(Price)
from products
group by category_id 
having AVG(price) between 10 and 15;
```

**Output:**

<img width="644" height="398" alt="image" src="https://github.com/user-attachments/assets/40982ebd-f1c4-4bf3-bf85-594d40864f8a" />

**Question 8**
---
<img width="1172" height="493" alt="image" src="https://github.com/user-attachments/assets/6cc618fc-3d74-4500-942a-241a60519881" />

```sql
select category_id, product_name,max(price) as Price
from products
group by category_id 
having max(price) > 15
```

**Output:**

<img width="864" height="458" alt="image" src="https://github.com/user-attachments/assets/e37d6931-2eac-4da0-90c1-fb8287731c64" />

**Question 9**
---
<img width="1170" height="511" alt="image" src="https://github.com/user-attachments/assets/a760641d-b8ac-4e1b-9c74-facc023626ba" />

```sql
select category_id,count(product_name)
from products
group by category_id
having category_id<3;
```

**Output:**

<img width="728" height="429" alt="image" src="https://github.com/user-attachments/assets/099fa0ed-2a9b-4004-b644-68c3613c32b5" />

**Question 10**
---
<img width="1188" height="467" alt="image" src="https://github.com/user-attachments/assets/9725aa2e-8640-4933-83d7-537234902d35" />

```sql
select age,AVG(income)
from employee
group by age
having AVG(income) between 300000 and 500000;
```

**Output:**

<img width="695" height="400" alt="image" src="https://github.com/user-attachments/assets/c3ef23fc-467f-41d7-8280-16e48c992211" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
