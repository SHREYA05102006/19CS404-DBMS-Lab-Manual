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
```
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```
```sql
CREATE TABLE Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary REAL CHECK(Salary>0),
DepartmentID INTEGER,
FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**
<img width="1306" height="275" alt="image" src="https://github.com/user-attachments/assets/6d80bd0e-6d29-4fc2-adc9-d2d787279dde" />


**Question 2**
---
```
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
```

```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER ,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY(employeeID) REFERENCES Employees (EmployeeID),
FOREIGN KEY(ProjectID) REFERENCES Projects (ProjectID)

);
```

**Output:**

<img width="1096" height="151" alt="image" src="https://github.com/user-attachments/assets/81dead55-4413-4137-a1c2-d41af3cb1341" />

**Question 3**
---
```
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```

```sql
ALTER TABLE customer
ADD discount DECIMAL(5,2);
```

**Output:**

<img width="1763" height="297" alt="image" src="https://github.com/user-attachments/assets/633b1caa-630b-4c4d-a755-8447977dd762" />


**Question 4**
---
```
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email
```

```sql
INSERT INTO customers(CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email
FROM  Old_customers;
```

**Output:**

<img width="1852" height="355" alt="image" src="https://github.com/user-attachments/assets/f30c5ee8-b32d-4f2f-bd79-efe7aa3adc17" />


**Question 5**
---
```
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.
```

```sql
INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES(1,'Sarah Parker','Manager','HR',60000);
```

**Output:**

<img width="1755" height="261" alt="image" src="https://github.com/user-attachments/assets/dac2e375-a105-47d5-b064-1e83dd13cee1" />


**Question 6**
---
```
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
```

```sql
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**

<img width="1742" height="318" alt="image" src="https://github.com/user-attachments/assets/3ff29409-4d81-43a3-8366-2e18492c987b" />


**Question 7**
---
```
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

 
```

```sql
INSERT INTO  Student_details(RollNo,Name,Gender,Subject, MARKS)
VALUES
(202,'Ella King','F','Chemistry',87),
(203,'James Bond','M','Literature',78);

```

**Output:**

<img width="1329" height="214" alt="image" src="https://github.com/user-attachments/assets/d74c8f1c-e41f-46dc-90eb-6d9e98cfe62a" />


**Question 8**
---
```
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 
```

```sql
ALTER TABLE customer
ADD birth_date timestamp;
```

**Output:**

<img width="1865" height="294" alt="image" src="https://github.com/user-attachments/assets/0d88f964-3532-47e1-971f-a4d2a3f2465a" />


**Question 9**
---
```
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
```
```sql
CREATE TABLE products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL,
discount DECIMAL(10,2) NOT NULL DEFAULT 0,
CHECK (list_price>=discount),
CHECK (discount>=0),
CHECK (list_price>=0)
);

```

**Output:**

<img width="1895" height="228" alt="image" src="https://github.com/user-attachments/assets/51d65597-037e-443d-8d57-87a3cf5c562d" />


**Question 10**
---
```
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
```

```sql
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT
);
```

**Output:**

<img width="1636" height="142" alt="image" src="https://github.com/user-attachments/assets/cb734d58-badf-4fef-9f09-d258c777ed07" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
