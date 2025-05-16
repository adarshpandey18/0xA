![[3-schema-architecture.png|center|500]]
## **Main Goal: Data Independence**
- Users should **not interact directly with the data**.
- **Data Abstraction** hides implementation details such as:
    - Where data is stored
    - How it is structured or indexed
- Allows changes at one level without affecting others.

---
##  **Levels of Data Abstraction**

### 1. **View Level** (External Schema)
- Defines **how data is presented** to individual users.
- **User-specific views** based on roles, permissions, and needs.
-  _Example:_  
    In a University Management System:
    - Students see grades and courses
    - Teachers see class lists and schedules
    - Admins manage users and academic records    

---
### 2. **Logical Level** (Conceptual Schema)
- Describes **what data is stored** and the **relationships** among the data.
- Focuses on the **structure** of the entire database.
- Includes:
    - Tables
    - Attributes
    - Relationships
    - Constraints
- _Example:_  
    ER Diagrams or Relational Models defining entities like Students, Courses, and Enrollments.

---
### 3. **Physical Level** (Physical Schema)
- Deals with **how data is stored** in the system.
- Specifies:
    - File structures
    - Indexing methods
    - Storage paths
-  _Example:_  
    Data stored in B-trees, hash indexes, or SSDs in a specific directory path.

---
