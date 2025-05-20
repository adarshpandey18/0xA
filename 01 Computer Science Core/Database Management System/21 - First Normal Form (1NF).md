
According to **E.F. Codd** (the father of DBMS), a table is said to be in **First Normal Form** if:
- **All attributes (columns) must contain only atomic (indivisible) values.**
- **There should be no multivalued attributes.**

---

### **Example – Not in 1NF**

| RollNo | Name  | Course |
| ------ | ----- | ------ |
| 1      | Sai   | C/C++  |
| 2      | Harsh | Java   |
| 3      | Omkar | C/DBMS |

In this table:
- The `Course` column has **multiple values** in some rows (e.g., `C/C++`, `C/DBMS`).
- This **violates** the rule of atomic values, so the table is **not in 1NF**.

---

### **Converting to 1NF**
Split the multivalued `Course` column into **separate rows**:

| RollNo | Name  | Course |
| ------ | ----- | ------ |
| 1      | Sai   | C      |
| 1      | Sai   | C++    |
| 2      | Harsh | Java   |
| 3      | Omkar | C      |
| 3      | Omkar | DBMS   |

- Now each column has atomic values.    
- This is in **First Normal Form**.
- But now, the **primary key** becomes a **combination of `RollNo` and `Course`** to uniquely identify each row.

---

### **Alternative Method – Not Recommended**
You could try to store multiple courses in separate columns

| RollNo | Name   | Course1 | Course2 | Course3 |
| ------ | ------ | ------- | ------- | ------- |
| 3      | Adarsh | Java    | NULL    | NULL    |

- This method introduces **null values** for students with fewer courses.    
- This **wastes space** and leads to **poor design**.
- It's **not scalable** if a student takes more courses in the future.

---

### **Better Approach – Splitting into Two Tables**

To follow best practices, split the data into two related tables:
#### **1. Base Table (Student Information)**

| RollNo | Name  |
| ------ | ----- |
| 1      | Sai   |
| 2      | Harsh |
| 3      | Omkar |

- `RollNo` is the **Primary Key**.    

#### **2. Referencing Table (Courses Information)**

| RollNo | Course |
| ------ | ------ |
| 1      | C      |
| 1      | C++    |
| 2      | Java   |
| 3      | C      |
| 3      | DBMS   |

- `RollNo` is a **Foreign Key** (refers to the base table).    
- The **Primary Key** of this table is the **combination of `RollNo` and `Course`**.

---

### **Summary of 1NF**
- Eliminate multivalued attributes.
- Ensure atomic values in each field.
- Avoid nulls by not using multiple course columns.
- Use separate related tables for repeated data.
- Maintain data integrity using **primary** and **foreign keys**.

---