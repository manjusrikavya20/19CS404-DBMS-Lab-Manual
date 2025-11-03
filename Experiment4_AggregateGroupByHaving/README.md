# Experiment 4: Aggregate Functions, Group By and Having Clause

## NAME: MANJUSRI KAVYA R
## REG NO: 212224040186

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
How many patients are covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT

```sql
select InsuranceCompany,count(distinct patientid) as TotalPatients from insurance group by InsuranceCompany;
```

**Output:**

<img width="1220" height="768" alt="image" src="https://github.com/user-attachments/assets/f39212f2-6de6-4b21-8df9-2054ec2ea15c" />


**Question 2**
---
How many prescriptions were written for each medication?

Sample tablePrescriptions Table



For example:

Result
Medication     TotalPrescriptions
-------------  ------------------
Ciprofloxacin  1
Doxorubicin    1
Ibuprofen      1
Levothyroxine  1
Lisinopril     1
MMR            1
Pending        1
Prenatal vita  1
Sertraline     1
Topiramate     1


```sql
select Medication,count(distinct prescriptionid) as TotalPrescriptions from Prescriptions group by medication;
```

**Output:**

<img width="1230" height="845" alt="image" src="https://github.com/user-attachments/assets/dd944b04-54ee-45d9-baed-c8980a2575a7" />


**Question 3**
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3


```sql
select Patientid,count(distinct appointmentid) as TotalAppointments from Appointments group by patientid;
```

**Output:**

<img width="1226" height="700" alt="image" src="https://github.com/user-attachments/assets/04d2da67-6ae6-4e43-aeb8-4598baedf0e4" />


**Question 4**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
```sql
select name as fruit_name,inventory as lowest_quantity from fruits where inventory=(select min(inventory) from fruits);
```

**Output:**

<img width="1240" height="403" alt="image" src="https://github.com/user-attachments/assets/8cf122e5-b3c3-4de3-9aab-7f08249a6f50" />


**Question 5**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
total_income
------------
1800000


```sql
select sum(income) as total_income from employee where age>= 40;
```

**Output:**

<img width="1233" height="396" alt="image" src="https://github.com/user-attachments/assets/dea728c9-4271-461b-a5f7-115c2c5daf6e" />


**Question 6**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```sql
select avg(income) as Average_Salary from employee;
```

**Output:**

<img width="1228" height="406" alt="image" src="https://github.com/user-attachments/assets/3bef5955-145a-476e-b043-372af773528a" />


**Question 7**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select min(purch_amt) as MINIMUM from orders;
```

**Output:**

<img width="1244" height="405" alt="image" src="https://github.com/user-attachments/assets/cfa463db-851f-4622-b6fe-38f7b12108f1" />


**Question 8**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products


```sql
select category_id,count(product_name) from products where category_id<3 group by category_id ;
```

**Output:**

<img width="1228" height="444" alt="image" src="https://github.com/user-attachments/assets/32376ce7-fb20-4683-842a-de062c46dab5" />


**Question 9**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000

Sample table: customer1

```sql
select address, AVG(salary) from customer1 group by address having avg(salary)<15000;
```

**Output:**

<img width="1225" height="698" alt="image" src="https://github.com/user-attachments/assets/14653062-533f-4dd8-87f9-8509a6d5590e" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1

```sql
select (age/5)*5 as age_group,AVG(age) from customer1 group by (age/5)*5 having avg(age)<24;
```

**Output:**

<img width="1238" height="423" alt="image" src="https://github.com/user-attachments/assets/05f856b9-7746-4b9b-a91c-55dc5fd01bfe" />

## MODULE 3 SEB GRADE:

<img width="983" height="102" alt="image" src="https://github.com/user-attachments/assets/caf04e1e-b1e5-47de-9caa-4090e1787a8e" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
