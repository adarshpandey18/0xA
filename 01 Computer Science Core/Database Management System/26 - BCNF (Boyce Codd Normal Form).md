A relation is in **BCNF** if:
- It is in **Third Normal Form (3NF)**, **and**
- **For every functional dependency** (FD) **X → Y**,  
    **X must be a super key** (i.e., X is either a candidate key or contains a candidate key)

> **Stronger than 3NF**: Even if a dependency is between prime attributes, **BCNF requires the left-hand side (LHS) to be a super key**

---
### **Key Concept:**

- **BCNF removes all anomalies caused by functional dependencies where LHS is not a super key**

---
### **Example: Student Table**

| student_id | student_name | voter_id | age |
| ---------- | ------------ | -------- | --- |
| 1          | Ravi         | ko123    | 20  |
| 2          | Varun        | mo34     | 21  |
| 3          | Raj          | k786     | 22  |
| 4          | Raju         | 2012     | 23  |

**Functional Dependencies (FDs):**
- `rollNo → student_name`
- `rollNo → voter_id`
- `voter_id → age`
- `voter_id → rollNo`

**Candidate Key:**  
From the FDs, observe that `rollNo` and `voter_id` determine each other:
- `rollNo ↔ voter_id`  
    So, both `{rollNo}` and `{voter_id}` are **candidate keys**

**Now Analyze the FDs:**

| FD                      | Is LHS a Candidate Key? | BCNF-Compliant? |
| ----------------------- | ----------------------- | --------------- |
| `rollNo → student_name` | Yes                     | Yes             |
| `rollNo → voter_id`     | Yes                     | Yes             |
| `voter_id → age`        | Yes                     | Yes             |
| `voter_id → rollNo`     | Yes                     | Yes             |

 All FDs have LHS as candidate keys  
 Therefore, **the relation is in BCNF**

---
### Summary:
A relation is in **BCNF** if:
- It is in **3NF**
- **Every FD's LHS is a super key**

BCNF eliminates:
- Redundancy caused by dependencies on **non-superkey** attributes
    
---