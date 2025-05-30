# Integrity Constraints

---
## **What are Integrity Constraints?**
- **Rules** enforced in a database to ensure:
    - **Accuracy**
    - **Consistency**
    - **Reliability** of the data
- They ensure that all data entered follows **predefined conditions** and **logical correctness**.

---
##  **Types of Integrity Constraints**

### **Domain Constraints**
- Define the **valid data types** or **ranges** for a column.
- Enforce that each attribute value **falls within an acceptable domain**.
**Example:**
```sql
Age INT CHECK (Age > 0)
```
- Ensures age is always a positive number.
 
---
###  **Entity Integrity Constraints**
- Ensure that **every table has a Primary Key**.
- **Primary Key** values must be:
    - **Unique**        
    - **Not NULL**
**Example:**
```sql
PRIMARY KEY (StudentID)
```
- Ensures each student has a unique ID and it cannot be null.

---
###  **Referential Integrity Constraints**
- Concerned with **Foreign Keys**.
- Ensures that a value in one table **must match** a primary key value in another table (or be NULL if allowed).
**Example:**
```sql
FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
```
- Prevents inserting a `CourseID` in the Enrollments table that doesn't exist in the Courses table.

---
###  **Key Constraints**
- Ensure that there is **at least one unique attribute** (a **Candidate Key**) in a table.
- **Candidate Key**: An attribute (or set) that can uniquely identify tuples.
- One candidate key is chosen as the **Primary Key**.

---

##  Summary 

| Constraint Type           | Purpose                          | Example                     |
| ------------------------- | -------------------------------- | --------------------------- |
| **Domain Constraint**     | Validates data type or range     | `Age > 0`                   |
| **Entity Integrity**      | Enforces Primary Key is not NULL | `PRIMARY KEY (ID)`          |
| **Referential Integrity** | Validates Foreign Key references | `FOREIGN KEY (DeptID)`      |
| **Key Constraint**        | Ensures uniqueness in records    | `Candidate Keys: ID, Email` |

---
