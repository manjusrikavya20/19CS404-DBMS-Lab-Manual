# Experiment 2: DDL Commands
# NAME: MANJUSRI KAVYA R
# REG.NO: 212224040186

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

Create a new table named products with the following specifications:
* product_id as INTEGER and primary key.
* product_name as TEXT and not NULL.
* list_price as DECIMAL (10, 2) and not NULL.
* discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
* A CHECK constraint at the table level to ensure:
  * list_price is greater than or equal to discount
  * discount is greater than or equal to 0
  * list_price is greater than or equal to 0

```
CREATE TABLE products(product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL (10, 2),
discount DECIMAL (10, 2) DEFAULT 0 NOT NULL,
CHECK(list_price>=discount AND discount>=0 AND list_price>=0)
);
```

**Output:**

<img width="1105" height="113" alt="image" src="https://github.com/user-attachments/assets/588763ab-82f5-4357-9adf-5b9511053592" />

**Question 2**

Create a new table named contacts with the following specifications:
* contact_id as INTEGER and primary key.
* first_name as TEXT and not NULL.
* last_name as TEXT and not NULL.
* email as TEXT.
* phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```
CREATE TABLE contacts(contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK(LENGTH(phone)>=10)
);
```

**Output:**

<img width="959" height="91" alt="image" src="https://github.com/user-attachments/assets/72aeead6-f7ec-47f5-b1bc-5bf0da0424cd" />

**Question 3**

Create a table named Locations with the following columns:

* LocationID as INTEGER
* LocationName as TEXT
* Address as TEXT

```
CREATE TABLE Locations(LocationID INTEGER,
LocationName TEXT,
Address TEXT);
```

**Output:**

<img width="1097" height="160" alt="image" src="https://github.com/user-attachments/assets/bb6806e1-4a0b-4a8c-80d8-8718aaba9496" />

**Question 4**

In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

```
INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)VALUES
(5,'George Clark','Consultant',NULL,NULL),
(7,'Noah Davis','Manager','HR',60000),
(8,'Ava Miller','Consultant','IT',NULL);
```

**Output:**

<img width="1196" height="165" alt="image" src="https://github.com/user-attachments/assets/ee92ace2-63fa-4216-bb88-d01ca1f0d594" />

**Question 5**

Insert all customers from Old_customers into Customers
Table attributes are CustomerID, Name, Address, Email

```
INSERT INTO Customers(CustomerID,Name,Address,Email)
SELECT CustomerID,Name,Address,Email 
FROM Old_customers;
```

**Output:**

<img width="1149" height="147" alt="image" src="https://github.com/user-attachments/assets/926862f0-b5a2-42cb-9379-7d3d4270e957" />

**Question 6**

Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 
Sample table: customer

```
ALTER TABLE customer ADD birth_date timestamp;
```

**Output:**

<img width="1173" height="151" alt="image" src="https://github.com/user-attachments/assets/7234d5ed-c910-4ef9-8eb8-8e108b785dff" />

**Question 7**

Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

```
INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)VALUES
(001,'Sarah Parker','Manager','HR',60000);
```

**Output:**

<img width="1217" height="112" alt="image" src="https://github.com/user-attachments/assets/dd7f1ffb-a736-4ff4-a5c0-0b1623db8a78" />

**Question 8**

Create a table named Invoices with the following constraints:
* InvoiceID as INTEGER should be the primary key.
* InvoiceDate as DATE.
* Amount as REAL should be greater than 0.
* DueDate as DATE should be greater than the InvoiceDate.
* OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```
CREATE TABLE Invoices(InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK(Amount>0),
DueDate DATE CHECK(DueDate>InvoiceDate),
OrderID INTEGER,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1281" height="115" alt="image" src="https://github.com/user-attachments/assets/36e54ad1-a807-41f4-8e11-40752b75e874" />

**Question 9**

Create a new table named item with the following specifications and constraints:
1. item_id as TEXT and as primary key.
2. item_desc as TEXT.
3. rate as INTEGER.
4. icom_id as TEXT with a length of 4.
5. icom_id is a foreign key referencing com_id in the company table.
6. The foreign key should cascade updates and deletes.
7. item_desc and rate should not accept NULL.

```
CREATE TABLE item(item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT CHECK(LENGTH(icom_id)=4),
FOREIGN KEY(icom_id) REFERENCES company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE
);
```

**Output:**

<img width="1134" height="196" alt="image" src="https://github.com/user-attachments/assets/03c84460-205b-4dda-a589-ee2be86e08c5" />

**Question 10**

Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

```
ALTER TABLE employees ADD salary INTEGER CHECK(salary>0);
```

**Output:**

<img width="1248" height="149" alt="image" src="https://github.com/user-attachments/assets/75064901-3bdd-4d67-a23b-9e147f8aad93" />

**Module 1 SEB Completion Grade:**

<img width="992" height="78" alt="image" src="https://github.com/user-attachments/assets/90adbb4e-b7d7-41d1-94dc-e46f2bb7fb2f" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
