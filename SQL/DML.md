### SQL Data Manipulation Language (DML) Tutorial

SQL (Structured Query Language) is a standard language for managing and manipulating databases. SQL statements are categorized into several types, including DML (Data Manipulation Language), DDL (Data Definition Language), DCL (Data Control Language), and TCL (Transaction Control Language).

DML is used for managing data within database objects. The primary DML statements are:
- `SELECT`: Retrieves data from a database.
- `INSERT`: Adds new rows of data to a table.
- `UPDATE`: Modifies existing data within a table.
- `DELETE`: Removes data from a table.

Let's dive into each of these DML statements with examples.

#### 1. SELECT

The `SELECT` statement retrieves data from one or more tables.

**Syntax:**
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Example:**
```sql
SELECT first_name, last_name
FROM employees
WHERE department = 'Sales';
```

This query retrieves the `first_name` and `last_name` of employees who work in the Sales department.

**Additional Features:**
- **`SELECT *`**: Selects all columns.
- **`WHERE`**: Filters records.
- **`ORDER BY`**: Sorts results.
- **`GROUP BY`**: Groups rows that have the same values in specified columns.
- **`HAVING`**: Filters groups.

**Example with Additional Features:**
```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 10
ORDER BY COUNT(*) DESC;
```

This query counts the number of employees in each department, includes only departments with more than 10 employees, and sorts the results in descending order.

#### 2. INSERT

The `INSERT` statement adds new rows to a table.

**Syntax:**
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

**Example:**
```sql
INSERT INTO employees (first_name, last_name, department, hire_date)
VALUES ('John', 'Doe', 'Engineering', '2024-05-27');
```

This query inserts a new employee into the `employees` table.

**Multiple Inserts:**
```sql
INSERT INTO employees (first_name, last_name, department, hire_date)
VALUES 
  ('Jane', 'Smith', 'HR', '2024-04-15'),
  ('Alice', 'Johnson', 'Finance', '2024-03-20');
```

#### 3. UPDATE

The `UPDATE` statement modifies existing data in a table.

**Syntax:**
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Example:**
```sql
UPDATE employees
SET department = 'Marketing'
WHERE last_name = 'Doe';
```

This query updates the department of all employees with the last name 'Doe' to 'Marketing'.

#### 4. DELETE

The `DELETE` statement removes rows from a table.

**Syntax:**
```sql
DELETE FROM table_name
WHERE condition;
```

**Example:**
```sql
DELETE FROM employees
WHERE last_name = 'Smith';
```

This query deletes all employees with the last name 'Smith'.

**Caution:**
Omitting the `WHERE` clause will delete all rows in the table:
```sql
DELETE FROM employees;
```

### Additional Concepts

#### Transactions

Transactions ensure data integrity by grouping multiple DML statements into a single unit of work.

**Syntax:**
```sql
BEGIN TRANSACTION;
-- DML statements
COMMIT;
```

**Example:**
```sql
BEGIN TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

COMMIT;
```

This transaction transfers $100 from account 1 to account 2. If any statement fails, no changes are made.

#### Rollback

You can undo changes made within a transaction using `ROLLBACK`.

**Example:**
```sql
BEGIN TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

-- Something goes wrong
ROLLBACK;
```
