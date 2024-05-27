### SQL Data Definition Language (DDL) Tutorial

SQL (Structured Query Language) is used to communicate with databases. It is the standard language for relational database management systems. SQL statements are used to perform tasks such as update data on a database, or retrieve data from a database. DDL (Data Definition Language) is a subset of SQL and is used to define the database schema.

In this tutorial, we'll cover the key DDL commands: `CREATE`, `ALTER`, `DROP`, and `TRUNCATE`.

#### 1. CREATE
The `CREATE` command is used to create a new database, table, index, or view.

**Create Database:**
```sql
CREATE DATABASE database_name;
```

**Create Table:**
```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ...
);
```
Example:
```sql
CREATE TABLE Employees (
    EmployeeID int PRIMARY KEY,
    FirstName varchar(255) NOT NULL,
    LastName varchar(255) NOT NULL,
    BirthDate date,
    HireDate date,
    Salary decimal(10, 2)
);
```

#### 2. ALTER
The `ALTER` command is used to modify an existing database object, like a table.

**Add Column:**
```sql
ALTER TABLE table_name
ADD column_name datatype constraint;
```

**Modify Column:**
```sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype constraint;
```

**Drop Column:**
```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

Example:
```sql
ALTER TABLE Employees
ADD Email varchar(255);

ALTER TABLE Employees
MODIFY COLUMN Salary decimal(12, 2);

ALTER TABLE Employees
DROP COLUMN BirthDate;
```

#### 3. DROP
The `DROP` command is used to delete an entire database or table.

**Drop Database:**
```sql
DROP DATABASE database_name;
```

**Drop Table:**
```sql
DROP TABLE table_name;
```
Example:
```sql
DROP DATABASE CompanyDB;

DROP TABLE Employees;
```

#### 4. TRUNCATE
The `TRUNCATE` command is used to delete all the rows from a table, but the table structure remains.

```sql
TRUNCATE TABLE table_name;
```
Example:
```sql
TRUNCATE TABLE Employees;
```

### Example Scenario

Let's walk through a simple scenario where we create a database, add a table, modify the table, and then clean up.

1. **Create a Database:**
```sql
CREATE DATABASE CompanyDB;
```

2. **Use the Database:**
```sql
USE CompanyDB;
```

3. **Create a Table:**
```sql
CREATE TABLE Departments (
    DepartmentID int PRIMARY KEY,
    DepartmentName varchar(255) NOT NULL
);
```

4. **Create another Table:**
```sql
CREATE TABLE Employees (
    EmployeeID int PRIMARY KEY,
    FirstName varchar(255) NOT NULL,
    LastName varchar(255) NOT NULL,
    DepartmentID int,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

5. **Add a Column to Employees:**
```sql
ALTER TABLE Employees
ADD Email varchar(255);
```

6. **Modify a Column in Employees:**
```sql
ALTER TABLE Employees
MODIFY COLUMN LastName varchar(100);
```

7. **Drop a Column from Employees:**
```sql
ALTER TABLE Employees
DROP COLUMN Email;
```

8. **Truncate the Employees Table:**
```sql
TRUNCATE TABLE Employees;
```

9. **Drop the Employees Table:**
```sql
DROP TABLE Employees;
```

10. **Drop the Departments Table:**
```sql
DROP TABLE Departments;
```

11. **Drop the Database:**
```sql
DROP DATABASE CompanyDB;
```

### Summary
- **`CREATE`**: Defines new databases, tables, and other objects.
- **`ALTER`**: Modifies existing database objects.
- **`DROP`**: Deletes databases or tables.
- **`TRUNCATE`**: Empties all rows from a table but keeps the table structure.
