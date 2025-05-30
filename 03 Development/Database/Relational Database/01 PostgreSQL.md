# PostgreSQL 

---

## Why Use PostgreSQL?

- Fully adheres to SQL standards, ensuring compatibility and reliability.
    
- Excels at handling concurrent transactions with MVCC (Multi-Version Concurrency Control).
    
- Prevents data corruption by enforcing **ACID** (Atomicity, Consistency, Isolation, Durability) compliance.
    
- Supports custom data types, operators, index types, and functions, making it highly extensible.
    
- Scales efficiently for large datasets and high user loads.
    
- Provides secure, reliable, and robust data storage.
    

---

## Database Design Principles

- Each table represents a **single real-world entity** (e.g., Person, Product).
    
- Each column stores **atomic data** (indivisible units, like name, price).
    
- Use **foreign keys** to establish clear relationships between tables.
    
- Apply **normalization** to minimize data redundancy and improve integrity.
    
- Design for scalability, maintainability, and performance.
    

---

## Basic Database Commands

### Create Database

```sql
CREATE DATABASE db_name;
```

### Connect to Database

```sql
\c db_name
```

> Note: `\c` is the correct PostgreSQL command, unlike MySQL's `USE`.

### Drop Database

```sql
DROP DATABASE db_name;
```

---

## CRUD Operations

### Create Table

```sql
CREATE TABLE person (
    id INT,
    name VARCHAR(100),
    city VARCHAR(100)
);
```

### Insert Data

```sql
INSERT INTO person(id, name, city) VALUES (101, 'Raju', 'Heart');

-- Insert multiple rows
INSERT INTO person(id, name, city)
VALUES (102, 'Raju', 'Mumbai'), (103, 'Sham', 'Mumbai');
```

### Read Data

```sql
SELECT * FROM person;
```

### Update Data

```sql
UPDATE person
SET city = 'London'
WHERE id = 2;
```

### Delete Data

```sql
DELETE FROM person
WHERE id = 104;
```

---

## Data Types

- **Numeric:** `INT`, `FLOAT`, `DOUBLE PRECISION`, `DECIMAL` (exact precision)
    
- **Character:** `VARCHAR(n)` (variable-length), `CHAR(n)` (fixed-length)
    
- **Date/Time:** `DATE`, `TIMESTAMP`, `TIME`
    
- **Boolean:** `BOOLEAN` (`TRUE` / `FALSE`)
    
- **Serial:** `SERIAL` (auto-increment integer, usually for IDs)
    

---

## Constraints

- **PRIMARY KEY:** Uniquely identifies each row.
    
- **NOT NULL:** Column must have a value, cannot be NULL.
    
- **DEFAULT:** Provides a default value if none is supplied.
    
- **UNIQUE:** Ensures all values in the column are distinct.
    
- **CHECK:** Validates data against a condition.
    

Example:

```sql
CREATE TABLE person (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    clgName VARCHAR(50) NOT NULL DEFAULT 'AP',
    age INT CHECK (age >= 18)
);
```

To set the starting value of a serial:

```sql
SELECT setval('person_id_seq', 1000);
```

---

## Data Filtering and Query Clauses

### WHERE Clause

Filters rows based on a condition.

```sql
SELECT name FROM person WHERE city = 'Mumbai';
SELECT name FROM person WHERE dept IN ('HR', 'IT');
```

### BETWEEN

Selects values within a range.

```sql
SELECT * FROM orders WHERE amount BETWEEN 100 AND 500;
```

### DISTINCT

Returns unique values.

```sql
SELECT DISTINCT dept FROM employees;
```

### ORDER BY

Sorts results.

```sql
SELECT * FROM employee ORDER BY id ASC;
SELECT * FROM employee ORDER BY id DESC;
```

### LIMIT

Limits the number of rows returned.

```sql
SELECT * FROM employees LIMIT 5;
```

### LIKE (Pattern Matching)

```sql
SELECT * FROM employees WHERE name LIKE 'A%';  -- starts with A
SELECT * FROM employees WHERE name LIKE '%A';  -- ends with A
SELECT * FROM employees WHERE name LIKE '%i%'; -- contains 'i'
SELECT * FROM employees WHERE name LIKE '__';  -- exactly 2 characters
```

---

## Aggregation Functions

- `COUNT(column)`: Counts non-null entries.
    
- `SUM(column)`: Total sum.
    
- `AVG(column)`: Average value.
    
- `MIN(column)`: Minimum value.
    
- `MAX(column)`: Maximum value.
    

Example with GROUP BY:

```sql
SELECT dept, COUNT(emp_id) FROM employees GROUP BY dept;
```

---

## String Functions

- `CONCAT()`, `CONCAT_WS(separator, ...)` — Combine strings.
    
- `SUBSTRING(string, start, length)` — Extract substring.
    
- `LEFT(string, n)`, `RIGHT(string, n)` — Left or right characters.
    
- `LENGTH(string)` — Length of string.
    
- `UPPER(string)`, `LOWER(string)` — Convert case.
    
- `TRIM(string)`, `LTRIM(string)`, `RTRIM(string)` — Remove whitespace.
    
- `REPLACE(string, from, to)` — Replace substring.
    
- `REVERSE(string)` — Reverse string.
    
- `POSITION(substring IN string)` — Find substring position.
    
- `STRING_AGG(column, delimiter)` — Concatenate values with delimiter.
    

---

## Alter Table Commands

- Add column:
    

```sql
ALTER TABLE table_name ADD COLUMN new_column data_type;
```

- Drop column:
    

```sql
ALTER TABLE table_name DROP COLUMN column_name;
```

- Rename column:
    

```sql
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;
```

- Rename table:
    

```sql
ALTER TABLE old_table_name RENAME TO new_table_name;
```

- Change data type:
    

```sql
ALTER TABLE table_name ALTER COLUMN column_name SET DATA TYPE new_data_type;
```

---

## Check Constraint

Ensure column values meet a condition.

```sql
CREATE TABLE contact (
    mobile VARCHAR(15) CHECK (LENGTH(mobile) >= 10)
);
```

Remove constraint:

```sql
ALTER TABLE contact DROP CONSTRAINT contact_mobile_check;
```

---

## CASE Statement

Conditional expressions inside queries.

```sql
SELECT fname, salary,
    CASE
        WHEN salary >= 5000 THEN 'High'
        ELSE 'Low'
    END AS salary_level
FROM employees;
```

---

## Foreign Keys and Relationships

- Define related tables with foreign keys:
    

```sql
CREATE TABLE department (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE employee (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES department(id)
);
```

- Example Insert:
    

```sql
INSERT INTO department(name) VALUES ('HR'), ('IT');
INSERT INTO employee(name, dept_id) VALUES ('Alice', 1), ('Bob', 2);
```

- Join to read related data:
    

```sql
SELECT e.name, d.name AS department
FROM employee e
JOIN department d ON e.dept_id = d.id;
```

---

## JOIN Types

- **INNER JOIN**: Matches rows in both tables.
    
- **LEFT JOIN**: All rows from left table + matched rows from right.
    
- **RIGHT JOIN**: All rows from right table + matched rows from left.
    
- **FULL OUTER JOIN**: All rows from both tables, matched or not.
    
- **CROSS JOIN**: Cartesian product of both tables.
    
- **SELF JOIN**: Join table to itself.
    

Example INNER JOIN:

```sql
SELECT e.name, d.name AS department
FROM employee e
INNER JOIN department d ON e.dept_id = d.id;
```

---

## Views

- A **view** is a virtual table representing the result of a stored query.
    
- Simplifies complex queries and improves security by restricting access.
    

```sql
CREATE VIEW employee_view AS
SELECT e.name, d.name AS department
FROM employee e
JOIN department d ON e.dept_id = d.id;
```

---

## HAVING Clause

- Filters groups created by `GROUP BY`.
    
- Used to apply conditions on aggregated data.
    

```sql
SELECT dept, COUNT(emp_id)
FROM employees
GROUP BY dept
HAVING COUNT(emp_id) > 5;
```

---

## Stored Routines

### Stored Procedures

- A set of SQL statements stored in the database, executed via a single call.
    
- Can include control flow, variables, and error handling.
    
- Does **not** return a value.

Example : 
```postgresql
CREATE OR REPLACE PROCEDURE add_employee(
    emp_name VARCHAR,
    emp_dept VARCHAR,
    emp_salary NUMERIC
)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO employee (name, department, salary)
    VALUES (emp_name, emp_dept, emp_salary);
END;
$$;

-- using procedure
CALL add_employee('John Doe', 'IT', 55000);

```

### User-Defined Functions (UDFs)

- Similar to procedures but return a value.
    
- Used inside SQL queries.
    

Example:

```sql
CREATE FUNCTION add_numbers(a INT, b INT) RETURNS INT AS $$
BEGIN
    RETURN a + b;
END;
$$ LANGUAGE plpgsql;
```

---

## Window Functions

- Perform calculations across a set of rows related to the current row.
    
- Allow running totals, ranking, moving averages, etc.
    

Common Window Functions:

- `ROW_NUMBER() OVER (ORDER BY column)`
    
- `RANK() OVER (ORDER BY column)`
    
- `DENSE_RANK() OVER (ORDER BY column)`
    
- `LEAD(column, offset) OVER (ORDER BY column)`
    
- `LAG(column, offset) OVER (ORDER BY column)`
    

Example:

```sql
SELECT
    employee,
    salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

---

## Common Table Expressions (CTE)

- Temporary result sets that can be referenced within a query.
    
- Use `WITH` clause.
    
- Useful for breaking complex queries into simpler parts.
    

Example:

```sql
WITH dept_count AS (
    SELECT dept_id, COUNT(*) AS emp_count
    FROM employee
    GROUP BY dept_id
)
SELECT d.name, dc.emp_count
FROM department d
JOIN dept_count dc ON d.id = dc.dept_id;
```

---

## Triggers

- Automatically execute a function/procedure on certain events like `INSERT`, `UPDATE`, or `DELETE`.
    
- Used for enforcing complex constraints, auditing, etc.
    

Example:

```sql
CREATE FUNCTION audit_log() RETURNS trigger AS $$
BEGIN
    INSERT INTO audit_table(table_name, action, action_time)
    VALUES (TG_TABLE_NAME, TG_OP, NOW());
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER audit_trigger
AFTER INSERT OR UPDATE OR DELETE ON employee
FOR EACH ROW EXECUTE FUNCTION audit_log();
```

---

## Cursors

- Allow row-by-row processing of query results.
    
- Useful for procedural logic where you need to process each row individually.
    

Example:

```sql
DECLARE cursor_name CURSOR FOR
SELECT id, name FROM employee;

OPEN cursor_name;

FETCH NEXT FROM cursor_name INTO var_id, var_name;

-- Process each row here

CLOSE cursor_name;
```

---
