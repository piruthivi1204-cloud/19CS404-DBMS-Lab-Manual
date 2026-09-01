# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**

![image](https://github.com/user-attachments/assets/27a2402a-b3f1-4d37-aea8-9cdcab8104f4)

```sql
UPDATE Products
SET sell_price =sell_price*1.10
WHERE category='Bakery'
```

**Output:**

![image](https://github.com/user-attachments/assets/6046fbd6-d8c4-42dd-a28d-c3a1e4845390)

**Question 2**

![image](https://github.com/user-attachments/assets/7d87e11d-78b1-4519-92ce-d21ca723ff69)

```sql
UPDATE PRODUCTS
SET reorder_lvl = reorder_lvl* 0.7
WHERE product_name LIKE '%cream%' AND quantity>reorder_lvl
```

**Output:**

![image](https://github.com/user-attachments/assets/56e21be8-4272-472d-add1-99beee9214ec)

**Question 3**

![image](https://github.com/user-attachments/assets/0ff8a38d-c2ce-4163-9614-58f51623d340)

```sql
UPDATE products
SET availability=availability*2
WHERE  product_id = 1
```

**Output:**

![image](https://github.com/user-attachments/assets/a2a7e014-d957-4cce-98e9-2ec9f9dae3dc)

**Question 4**

![image](https://github.com/user-attachments/assets/9c9ebea3-7931-4357-bb78-3cf2e003bb33)

```sql
UPDATE Employees
SET salary=8000
WHERE employee_id=105
```

**Output:**

![image](https://github.com/user-attachments/assets/3294f976-b436-43d9-a26d-edc7217a106b)

**Question 5**

![image](https://github.com/user-attachments/assets/1c9459c5-1ca9-4dc3-9c1a-27ca47a551f7)

```sql
DELETE FROM customer
WHERE GRADE != 3
```

**Output:**

![image](https://github.com/user-attachments/assets/46e42085-4299-4065-9714-872a9a648f64)

**Question 6**

![image](https://github.com/user-attachments/assets/12deeb76-bd5c-47f4-85cf-bc0bc55d22da)

```sql
DELETE FROM Doctors 
WHERE last_name IS NULL
```

**Output:**

![image](https://github.com/user-attachments/assets/208071c2-42ab-4e4e-8299-3eb766aa144e)

**Question 7**

![image](https://github.com/user-attachments/assets/4af5cc53-bee9-4de5-8d0c-80c40a08d3ce)

```sql
DELETE FROM customer 
WHERE CUST_COUNTRY NOT IN ('India', 'USA')
```

**Output:**

![image](https://github.com/user-attachments/assets/8adb8591-6f30-41f3-afd8-e302a2591a27)

**Question 8**

![image](https://github.com/user-attachments/assets/0d916e13-889b-4d70-9a24-4e7b1e9ebcba)

```sql
SELECT * FROM EmployeePosition
ORDER BY SALARY DESC LIMIT 3
```

**Output:**

![image](https://github.com/user-attachments/assets/0de0461d-1a42-4852-a93f-8de83ac1d407)

**Question 9**

![image](https://github.com/user-attachments/assets/e776eef3-049f-4210-9b58-3b10d713a5e2)

```sql
SELECT patient_id,first_name,admission_date,discharge_date FROM Patients
WHERE admission_date =  discharge_date
```

**Output:**

![image](https://github.com/user-attachments/assets/ab0de0da-30d1-45c1-84c7-9bab11ea1d25)

**Question 10**

![image](https://github.com/user-attachments/assets/45ac9bc3-d6ec-4394-ac29-1d5d5f431630)

```sql
SELECT * FROM orders
WHERE purch_amt BETWEEN 500 AND 4000 AND purch_amt NOT IN (948.50,1983.43)
```

**Output:**

![image](https://github.com/user-attachments/assets/b1b5742d-a4e5-4a41-af39-6b53c4e1ffb9)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
