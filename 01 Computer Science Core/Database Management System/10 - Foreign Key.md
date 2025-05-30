# Foreign Key

A **foreign key** is an **attribute** or **set of attributes** in one table that **refers to the primary key** of the **same or another table**.

> **Purpose**: Maintains **referential integrity** between related tables.

---
### **Key Concepts**

| Term                  | Meaning                                                                |
| --------------------- | ---------------------------------------------------------------------- |
| **Foreign Key**       | An attribute that references the **primary key** of another table.     |
| **Referenced Table**  | The table **whose primary key is being referenced**. (e.g., `student`) |
| **Referencing Table** | The table that **contains the foreign key**. (e.g., `course`)          |

---

### **Example: Tables**

#### `Student` Table (Referenced Table)

|rollno|name|address|
|---|---|---|
|1|a|delhi|
|2|b|mumbai|
|3|a|chd|

> Here, `rollno` is the **Primary Key**.

#### `Course` Table (Referencing Table)

|courseId|courseName|rollNo|
|---|---|---|
|c1|dbms|1|
|c2|networks|2|

> Here, `rollNo` is a **Foreign Key**, referencing `student(rollno)`.

---

### **SQL Syntax**

**Creating table with foreign key:**

```sql
CREATE TABLE course (
  courseId VARCHAR(10),
  courseName VARCHAR(20),
  rollNo INT REFERENCES student(rollNo)
);
```

**Or using ALTER to add foreign key constraint later:**

```sql
ALTER TABLE course
ADD CONSTRAINT fk FOREIGN KEY (rollNo)
REFERENCES student(rollNo);
```

---

### **Important Points**

- You **cannot insert a value in `course.rollNo`** that doesn't exist in `student.rollno`.
    
- **Names of columns do NOT need to match**, but **data types should be compatible**.
    
- A table can have **multiple foreign keys** referencing different tables.
    
- Helps in maintaining **data consistency** by preventing orphan records.
    
---
