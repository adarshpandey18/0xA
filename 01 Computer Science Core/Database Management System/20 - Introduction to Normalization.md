**Normalization** is a database design technique used to minimize redundancy and dependency by organizing fields and tables in a relational database. It ensures that the data is stored efficiently and eliminates data anomalies.

There are two types of duplicacy (redundancy) that normalization helps to remove:

---

### **1. Row-Level Redundancy**

Occurs when **entire rows are repeated** in a table.

**Example:**

| Student_id | Student_name | Student_age |
| ---------- | ------------ | ----------- |
| 1          | Adarsh       | 21          |
| 2          | Riddhi       | 23          |
| 1          | Adarsh       | 21          |

In this case, the **first** and **third** rows are identical. This is a violation of data integrity.

**Solution:**  
Introduce a **Primary Key**, such as `Student_id`, which ensures:
- Uniqueness (no two rows can have the same value)
- Non-null values

By setting `Student_id` as the primary key, we prevent the duplication of rows.

---

### **2. Column-Level Redundancy**

Occurs when **sets of columns** repeat the same information across different rows.

**Example:**

| Student_id | Student_name | Course_id | Course_Name | F_id | F_name | Salary |
| ---------- | ------------ | --------- | ----------- | ---- | ------ | ------ |
| 1          | Ram          | C1        | DBMS        | F1   | John   | 30000  |
| 2          | Ravi         | C2        | Java        | F2   | Bob    | 40000  |
| 3          | Nitin        | C1        | DBMS        | F1   | John   | 30000  |
| 4          | Amrit        | C1        | DBMS        | F1   | John   | 30000  |

In this table:
- Course ID `C1` with course name `DBMS` is repeated multiple times.
- Faculty ID `F1` with name `John` and salary `30000` is repeated.

This leads to **data anomalies**:

---

#### **Anomalies Caused by Column-Level Redundancy**

1. **Insertion Anomaly:**    
    - If we want to add a **new course (C10)** and **new faculty**, but no student has registered for it yet, we can't add this information because `Student_id` (which might be the primary key) cannot be null.
    - As a result, we **cannot insert** the new course/faculty without student data.

2. **Deletion Anomaly:**    
    - If we delete a row containing the only instance of a course or faculty, we **lose all information** about that course/faculty.
    - For example, if we delete the second row, we lose all information about `Course C2` and `Faculty F2`.
        
3. **Update Anomaly:**
    - If we need to update the **salary of Faculty F1**, we must update it **in every row** where F1 appears.
    - If any instance is missed, the data becomes inconsistent.
        
---

### **Summary**

- **Row-level redundancy** is handled by using **primary keys**.
- **Column-level redundancy** is removed by **splitting the data into multiple related tables** (normal forms).
- Normalization helps eliminate **insertion, deletion, and update anomalies** and promotes **data integrity and consistency**.
    
---