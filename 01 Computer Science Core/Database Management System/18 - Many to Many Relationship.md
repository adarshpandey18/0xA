
## **Many-to-Many (M:N) Relationship**
A **many-to-many relationship** exists when:
- **One record** in **Table A** can be associated with **multiple records** in **Table B**,
- And **one record** in **Table B** can also be associated with **multiple records** in **Table A**.

---
### **Real-Life Example:**
**Scenario**: Many students can enroll in many courses, and each course can have many students.
![[many-to-many-realtionship-example.png]]

---
### **Entity Tables:**

#### **Student Table** (Primary Key: `roll_no`)

| roll_no | name | age |
| ------- | ---- | --- |
| 1       | A    | 16  |
| 2       | B    | 18  |
| 3       | C    | 17  |
| 4       | D    | 18  |

#### **Course Table** (Primary Key: `course_id`)

| course_id | course_name | course_credit |
| --------- | ----------- | ------------- |
| c1        | Maths       | 4             |
| c2        | Physics     | 4             |
| c3        | Chemistry   | 4             |
| c4        | Hindi       | 4             |

---

### **Relationship Table: `Study`**

Used to represent the **M:N relationship** between students and courses.
	
| roll_no | course_id |
| ------- | --------- |
| 1       | c1        |
| 2       | c2        |
| 1       | c2        |
| 2       | c1        |

- `roll_no` → foreign key referencing `Student(roll_no)`    
- `course_id` → foreign key referencing `Course(course_id)`
- Together, `roll_no + course_id` form a **composite primary key**
- No duplicate `(roll_no, course_id)` pairs allowed

---

### **Why a Composite Key?**
- Neither `roll_no` nor `course_id` alone can uniquely identify a record.
- The combination (`roll_no`, `course_id`) ensures each enrollment is unique.

---

### **Can the Tables Be Reduced?**
**No, reduction is not possible.**
- You **cannot merge** student and course tables directly because:
    - One student can have multiple courses.
    - One course can have multiple students.
- The `Study` table is **essential** to properly model the M:N relationship.

---

## **Summary Table: Many-to-Many Relationship**

| Aspect                     | Many-to-Many (M:N) Relationship                             |
| -------------------------- | ----------------------------------------------------------- |
| **Definition**             | Many records in A relate to many records in B               |
| **Example**                | Students enroll in many courses; courses have many students |
| **Intermediate Table**     | Required (e.g., `Study`)                                    |
| **Primary Key**            | Composite (e.g., `roll_no + course_id`)                     |
| **Foreign Keys**           | `roll_no` → Student, `course_id` → Course                   |
| **Table Reduction?**       | Not possible                                                |
| **Descriptive Attributes** | Can be added to `Study` (e.g., `enrollment_date`, `grade`)  |
| **ER Diagram Notation**    | Line with crow’s foot on both sides (many-to-many)          |

---
