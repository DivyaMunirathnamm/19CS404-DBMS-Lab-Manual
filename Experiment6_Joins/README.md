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

![image](https://github.com/user-attachments/assets/49b29802-c810-445f-9e7f-eec32e3797bd)

```sql
select
 n.nurse_id,
 n.first_name,
 n.last_name,
 n.department_id,
 d.department_name
from
  nurses n
inner join
 departments d
on
 n.department_id=d.department_id

```

**Output:**

![image](https://github.com/user-attachments/assets/fc169cfd-8d27-4cfc-8d92-dd34293462ef)

**Question 2**

![image](https://github.com/user-attachments/assets/a46a4eb5-2ccd-4c46-81a5-1e6998c44f58)

```sql
select c.cust_name,c.city,c.grade,s.name as Salesman,s.city from customer c
inner join salesman s on c.salesman_id=s.salesman_id
where c.grade<300
order by c.customer_id asc;
```

**Output:**

![image](https://github.com/user-attachments/assets/dad3fbc1-b23f-4ab1-a0c8-ea7f28bade28)

**Question 3**

![image](https://github.com/user-attachments/assets/4d2b264a-a818-48f1-a91c-f66b74b2d8a5)

```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM 
    salesman s
LEFT JOIN 
    customer c ON s.salesman_id = c.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/a1214911-c053-422e-ba06-4c184b5d7ff5)

**Question 4**

![image](https://github.com/user-attachments/assets/62fe53ff-0d4a-4cbe-a808-ab5214598703)

```sql
select s.* from salesman s
left join customer c on s.salesman_id=c.salesman_id
where c.cust_name ='Fabian Johns';
```

**Output:**

![image](https://github.com/user-attachments/assets/747bc7a0-1c51-4ae9-86f5-cfc95cdc02ea)

**Question 5**

![image](https://github.com/user-attachments/assets/b4d51d48-3104-4e27-8d13-5fe6916699b8)

```sql
SELECT p.first_name AS patient_name
FROM patients p
INNER JOIN test_results tr ON p.patient_id = tr.patient_id
WHERE tr.test_name = 'Blood Pressure';
```

**Output:**

![image](https://github.com/user-attachments/assets/ae041fd9-72eb-4252-8072-697584ebf4a2)

**Question 6**

![image](https://github.com/user-attachments/assets/6ad9027d-b8fa-44b3-9bc0-629418a7ae56)

```sql
select c.cust_name as "Customer Name",c.city,s.name as Salesman,s.commission from customer c
join salesman s on c.salesman_id=s.salesman_id
where s.commission>0.12;
```

**Output:**

![image](https://github.com/user-attachments/assets/02728cab-49ed-45c9-9f3c-ce89dd14376f)

**Question 7**

![image](https://github.com/user-attachments/assets/7a3003aa-8273-4941-93d3-bf5d39544b8d)

```sql
select
  c.cust_name as "Customer Name",
  c.city,
  s.name as "Salesman",
  s.city,
  s.commission
from
  customer c
inner join
   salesman s
on
  c.salesman_id=s.salesman_id
where
  c.city!=s.city
  and s.commission>0.12;
```

**Output:**

![image](https://github.com/user-attachments/assets/3ab593b5-e46e-4098-a762-1efdc15f9d13)

**Question 8**

![image](https://github.com/user-attachments/assets/193a3a8b-1335-4b07-8ad7-93c95854bbf3)

```sql
select
  c.cust_name,
  c.city,
  o.ord_no,
  o.ord_date,
  o.purch_amt as "Order Amount",
  s.name,
  s.commission
from
  customer c
left join 
   orders o
on
  c.customer_id=o.customer_id
left  join
   salesman s
on
   c.salesman_id=s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/6622abed-4475-44db-9426-5b3363365adc)

**Question 9**

![image](https://github.com/user-attachments/assets/611af145-2254-4cd0-84de-c727550f267e)

```sql
select p.* ,d.specialization as doctor_specialization from patients p
inner join doctors d on p.doctor_id=d.doctor_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/1f909086-a729-4f7a-9793-c0080fef8a92)

**Question 10**

![image](https://github.com/user-attachments/assets/4065b691-a6e8-4ea4-aa04-f0b61c001dad)

```sql
select 
 s.name as "Salesman",
 c.cust_name,
 c.city
from
 salesman s
inner join 
  customer c
on
  s.city=c.city;
```

**Output:**

![image](https://github.com/user-attachments/assets/9e1448a1-2e36-47e6-8118-3326a866fd80)

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
