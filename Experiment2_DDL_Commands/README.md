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

![image](https://github.com/user-attachments/assets/942d6a0b-7606-402b-8f11-44f10198b37d)

```sql
CREATE TABLE Bonuses(
BonusID INT PRIMARY KEY,
EmployeeID INT,
BonusAmount REAL CHECK(BonusAmount>0),
BonusDate DATE,
Reason TEXT NOT NULL
);

```
**Output:**

![image](https://github.com/user-attachments/assets/ea63e41a-09d4-4288-b139-43ea519825ed)


**Question 2**

![image](https://github.com/user-attachments/assets/560ebfe7-6a54-41b1-a177-84d9a5353047)

```sql
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(101,'Laptop','Electronics',1500,50);
```

**Output:**

![image](https://github.com/user-attachments/assets/c341e460-a000-4de8-8a82-fdd131941394)


**Question 3**

![image](https://github.com/user-attachments/assets/7078b380-4e06-425d-8f7c-1471402da45d)



```sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INT NOT NULL,
icom_id TEXT(4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/d9a11b44-58b4-4218-8148-f08af352f7c4)


**Question 4**

![image](https://github.com/user-attachments/assets/d901433e-5f0c-4ef6-ba8f-37000fd2dde5)


```sql
CREATE TABLE ProjectAssignments(
AssignmentID INT PRIMARY KEY,
EmployeeID INT,
ProjectID INT,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/7dc2bdd2-ad69-4dbe-9114-0626ef3c0db1)

**Question 5**

![image](https://github.com/user-attachments/assets/52b89195-caf0-4ae9-a86f-68b5c64e1e4c)


```sql
INSERT INTO Books(ISBN,Title,Author,Publisher,YearPublished)
SELECT  ISBN, Title, Author, Publisher, YearPublished
FROM  Out_of_print_books;
```

**Output:**

![image](https://github.com/user-attachments/assets/22d0beef-7ccb-4f8a-8b2c-dc4afea77986)

**Question 6**

![image](https://github.com/user-attachments/assets/52060e56-080f-468c-b8de-a8312006f748)

```sql
CREATE TABLE Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/b22c3171-def9-4d72-97fc-140a0daa0dee)

**Question 7**

![image](https://github.com/user-attachments/assets/4ddf8d63-e95b-4542-bead-dee188ba99b1)

```sql
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(106,'Fitness Tracker','Wearables',NULL,NULL);
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(107,'Laptop','Electronics',999.99,50);
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(108,'Wireless Earbuds','Accessories',NULL,100);
```

**Output:**

![image](https://github.com/user-attachments/assets/591defed-3658-4976-a479-3704104d7909)

**Question 8**

![image](https://github.com/user-attachments/assets/db29c91b-9692-462e-ac58-ad7c8a035391)

```sql
ALTER TABLE Companies ADD COLUMN designation varchar(50);
ALTER TABLE Companies ADD COLUMN net_salary number;
ALTER TABLE Companies ADD COLUMN dob date;
```

**Output:**

![image](https://github.com/user-attachments/assets/36f6e886-cdbc-40c1-937c-7d2559a0e7b3)

**Question 9**

![image](https://github.com/user-attachments/assets/04c55e88-d808-4cce-9f43-0a4b2daa2943)

```sql
CREATE TABLE jobs(
job_id INT,
job_title TEXT DEFAULT '',
min_salary INT DEFAULT 8000,
max_salary INT DEFAULT NULL);
```

**Output:**

![image](https://github.com/user-attachments/assets/4d67b31f-2b95-4c12-add8-b3054eb0448f)

**Question 10**

![image](https://github.com/user-attachments/assets/baedcb9b-7706-43c1-afd3-a0ca26f7c903)

```sql
ALTER TABLE Student_details ADD COLUMN Email VARCHAR(50);
ALTER TABLE Student_details ADD COLUMN MARKS INT DEFAULT 0;
```

**Output:**

![image](https://github.com/user-attachments/assets/e2dcd365-c733-4639-9d0d-e9db05b3eda1)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
