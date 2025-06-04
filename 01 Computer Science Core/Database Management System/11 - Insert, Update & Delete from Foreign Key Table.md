# Insert, Update & Delete from Foreign Key Table

###  Table Setup

```sql
CREATE TABLE Department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Department(dept_id)
);
```

---

###  INSERT into FK Table (Child Table)

- FK value **must exist** in parent table.
    

```sql
-- Valid: dept_id = 1 exists
INSERT INTO Employee (emp_id, emp_name, dept_id)
VALUES (101, 'Alice', 1);

-- Invalid: dept_id = 99 doesn’t exist → Error
INSERT INTO Employee (emp_id, emp_name, dept_id)
VALUES (102, 'Bob', 99);
```

---

###  UPDATE FK in Child Table

- You can **update** FK only if the **new value exists** in parent table.
    

```sql
-- Valid update
UPDATE Employee
SET dept_id = 2
WHERE emp_id = 101;

-- Invalid update: new FK doesn't exist → Error
UPDATE Employee
SET dept_id = 99
WHERE emp_id = 101;
```

---

###  DELETE from FK Table (Child Table)

- No issue, delete freely.
    

```sql
DELETE FROM Employee
WHERE emp_id = 101;
```

---

###  DELETE from Parent Table (with existing child rows)

- **Without ON DELETE CASCADE** → Error
    
- **With ON DELETE CASCADE** → Child rows auto-deleted
    

```sql
-- Without cascade
DELETE FROM Department WHERE dept_id = 1;
-- → Fails if employees exist with dept_id = 1

-- With cascade
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Department(dept_id) ON DELETE CASCADE
);
```

---

###  UPDATE Parent Table’s PK (Referencing FK)

- Same rules as delete:
    
    - **ON UPDATE CASCADE** → FK auto-updates
        
    - **No cascade** → Error if child exists
        

```sql
-- With cascade
FOREIGN KEY (dept_id) REFERENCES Department(dept_id) ON UPDATE CASCADE
```

---

TL;DR:

- Insert → FK must exist
    
- Update → New FK must exist
    
- Delete child → Allowed
    
- Delete parent → Use `ON DELETE CASCADE` or suffer
    
- Update parent PK → Use `ON UPDATE CASCADE` or suffer
    