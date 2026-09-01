# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.
**Program:**
```
SET SERVEROUTPUT ON;

CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    action VARCHAR2(20)
);

CREATE OR REPLACE TRIGGER emp_insert_log
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (:NEW.emp_id, :NEW.emp_name, 'INSERT');
END;
/

INSERT INTO employees VALUES (1, 'Ajay', 5000);

SELECT * FROM employee_log;
```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

**Output:**
<img width="837" height="258" alt="Screenshot 2026-08-28 171638" src="https://github.com/user-attachments/assets/cb6807d5-d8dd-4f2e-a2fc-f650d2358a7a" />
---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Program:**
```
CREATE TABLE sensitive_data (
    id NUMBER,
    data VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Confidential Data');

CREATE OR REPLACE TRIGGER prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001,
        'Deletion not allowed on this table.');
END;
/

DELETE FROM sensitive_data WHERE id = 1;

```

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

**Output:**
  <img width="807" height="355" alt="image" src="https://github.com/user-attachments/assets/c76de68a-baa8-475f-a446-429a69a01314" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program:**
```
CREATE TABLE products (
    product_id NUMBER,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);

INSERT INTO products
VALUES (1, 'Laptop', 50000, SYSTIMESTAMP);

CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/

UPDATE products
SET price = 55000
WHERE product_id = 1;

SELECT * FROM products;
```
**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
  
**Output:**
  <img width="902" height="255" alt="image" src="https://github.com/user-attachments/assets/2956f8bc-a7ad-43c4-8d77-e6c892e7dd3e" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program:**
```
CREATE TABLE customer_orders (
    order_id NUMBER,
    customer_name VARCHAR2(50),
    amount NUMBER
);

CREATE TABLE audit_log (
    update_count NUMBER
);

INSERT INTO audit_log VALUES (0);

INSERT INTO customer_orders
VALUES (1, 'Ajay', 5000);

CREATE OR REPLACE TRIGGER count_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/

UPDATE customer_orders
SET amount = 6000
WHERE order_id = 1;

SELECT * FROM audit_log;
```

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
  
**Output:**
<img width="856" height="242" alt="image" src="https://github.com/user-attachments/assets/45b223d6-4ec3-487f-8525-546eff314c34" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program:**
```
-- Create the employees table
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

-- Create the trigger
CREATE OR REPLACE TRIGGER check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20002,
            'Salary below minimum threshold.'
        );
    END IF;
END;
/

#Test Case:

INSERT INTO employees
VALUES (101, 'Aman', 5000);

SELECT * FROM employees;

```

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`
**Output:**
  <img width="1058" height="333" alt="image" src="https://github.com/user-attachments/assets/cb78d761-e5bc-42b0-90ec-621796483eac" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
