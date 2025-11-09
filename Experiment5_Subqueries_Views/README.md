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
<img width="1053" height="377" alt="438780616-bc4ca765-6c12-453c-af56-f0a8198394fe" src="https://github.com/user-attachments/assets/db9f6d12-a023-42c8-920e-a8c822254a0a" />


```sql
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi' AND AGE < 30
ORDER BY ID;
```

**Output:**
<img width="1200" height="291" alt="438780858-164afd13-3206-4254-9deb-93d55cd8b88b" src="https://github.com/user-attachments/assets/20e1f3db-91bf-4ab3-ac27-4f163735b9d8" />



**Question 2**
---
<img width="1258" height="412" alt="438780988-dec2ba69-7bfa-4b17-ba3d-0cd831375398" src="https://github.com/user-attachments/assets/a15a2caf-c7dd-498d-88a4-842b411f6028" />


```sql
SELECT g.student_name, g.grade
FROM GRADES g
JOIN (
    SELECT subject, MIN(grade) AS min_grade
    FROM GRADES
    GROUP BY subject
) AS min_grades ON g.subject = min_grades.subject AND g.grade = min_grades.min_grade;
```

**Output:**
<img width="754" height="371" alt="438781174-7ee610bf-6fc4-4082-a633-127d9c910ca2" src="https://github.com/user-attachments/assets/95677b29-4664-4019-a96c-2cf0838d689b" />



**Question 3**
---

<img width="1244" height="387" alt="438781270-5e256c61-584c-4a7b-967c-026c40be5020" src="https://github.com/user-attachments/assets/60aff18d-8193-4dd8-afb3-7c7ee9593e49" />

```sql
SELECT g.*
FROM GRADES g
JOIN (
    SELECT subject, MAX(grade) AS max_grade
    FROM GRADES
    GROUP BY subject
) AS max_grades ON g.subject = max_grades.subject AND g.grade = max_grades.max_grade;
```

**Output:**

<img width="1220" height="328" alt="438781793-befdcf19-4e1d-4428-b484-846c0c8a9135" src="https://github.com/user-attachments/assets/3f06695d-be15-46b7-88ed-b09d402a7e9b" />


**Question 4**
---

<img width="985" height="242" alt="438782079-e28348cd-68d4-4a59-8f37-e8eaa5f232e1" src="https://github.com/user-attachments/assets/2c797f36-60f0-40c5-bbb9-2d7f194759ed" />

```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**
<img width="596" height="396" alt="438782291-7d82ab61-0500-4b66-8b46-bd3e6d53c1d3" src="https://github.com/user-attachments/assets/a87361eb-d38b-42f7-86fd-a52f734f733c" />



**Question 5**
---
<img width="1008" height="359" alt="438782448-807faebf-2a81-4c43-bed0-c8c0e5b8f66a" src="https://github.com/user-attachments/assets/426c34c8-e7cd-40c1-bdb9-af373fb7f75c" />


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;
```

**Output:**

<img width="1194" height="368" alt="438783183-cfa4590b-c9cf-43bf-ad22-2af2cee2aeba" src="https://github.com/user-attachments/assets/0224fc18-d1b5-4f17-af10-0d410da011cf" />


**Question 6**
---
<img width="1208" height="503" alt="438783443-f2d8fbcc-acc2-4e5c-9445-e22e68ffbad5" src="https://github.com/user-attachments/assets/9739b116-e7fb-4bf3-aa5e-50d1c451e659" />


```sql
SELECT * FROM orders WHERE salesman_id IN (select salesman_id FROM salesman WHERE city ='London');
```

**Output:**

<img width="1227" height="348" alt="438783699-27a3e527-0a65-4509-98e2-3988bf6a79b3" src="https://github.com/user-attachments/assets/1699e71d-49b7-4f55-8584-4a99a43c7b5b" />


**Question 7**
---
<img width="1217" height="281" alt="438783844-bb7dbeaa-5a09-49d9-92da-0918d002c1c5" src="https://github.com/user-attachments/assets/420a5712-208a-4d35-a636-5f57876c6ea2" />


```sql
SELECT * FROM orders WHERE salesman_id IN (select salesman_id FROM salesman WHERE city ='New York');
```

**Output:**

<img width="1233" height="397" alt="438784090-82c8dc38-b695-4793-a71e-830d8f480fe6" src="https://github.com/user-attachments/assets/7e8d4386-ccef-412a-b5e5-1dc3b7e04ae9" />


**Question 8**
---
<img width="1031" height="276" alt="438784179-e916ed3d-47ea-4d5d-b855-3aa44329965e" src="https://github.com/user-attachments/assets/22072b33-a11e-4870-9035-33999555126a" />


```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**

<img width="1248" height="383" alt="438784377-f039ef9a-3a37-4ddd-a98d-89e78ef6626b" src="https://github.com/user-attachments/assets/32bfc122-668e-4fb5-a871-c611c434e41a" />

**Question 9**
---

<img width="1013" height="369" alt="438784521-90d07760-06b4-4ee4-9965-dd6c1d9a5128" src="https://github.com/user-attachments/assets/d297acdb-0e85-4a65-8fa8-e38253c1b2fb" />

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**
<img width="1192" height="540" alt="438784644-ddc741c3-ef05-4b06-8d11-a09d8874e583" src="https://github.com/user-attachments/assets/5db2a0cb-6f4b-4f24-85d4-6d6bb59d898f" />


**Question 10**
---
<img width="1260" height="388" alt="438784778-4667dcda-5d8e-4d32-ab12-73fdaa67a927" src="https://github.com/user-attachments/assets/1500ce19-9881-492e-abf6-8ebe921c7191" />


```sql
SELECT g.*
FROM GRADES g
JOIN (
    SELECT subject, MIN(grade) AS min_grade
    FROM GRADES
    GROUP BY subject
) AS min_grades ON g.subject = min_grades.subject AND g.grade = min_grades.min_grade;
```

**Output:**

<img width="1242" height="332" alt="438784938-6e44fe4a-6677-4d8b-a026-f713de5f75e2" src="https://github.com/user-attachments/assets/d192b4f3-63bf-4bf0-98ff-4f0c80a75f24" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
