## **Third Normal Form (3NF)**

- A relation is in **3NF** if:    
    - It is in **2NF**
    - For every functional dependency **X → Y**, one of the following holds:
        - **X is a super key**
        - **Y is a prime attribute** (i.e., part of some candidate key)
- **Dependency preserving decomposition** is always possible in 3NF.
- **Lossless decomposition** is also guaranteed in 3NF.

> 3NF is often used in practice when maintaining functional dependencies directly in the schema is important.

---
### Example:

**Relation:** R(A, B, C, D)  
**Functional Dependencies:**
- AB → CD
- D → A
    
**Candidate Key:** AB
- In D → A:
    - D is **not** a super key
    - A is a **prime attribute** (since AB is a candidate key)

This satisfies 3NF.  
All dependencies can be preserved after decomposition.  
Decomposition is both **lossless** and **dependency-preserving**.

---

## **Boyce-Codd Normal Form (BCNF)**
- A relation is in **BCNF** if:
    - For every functional dependency **X → Y**, **X is a super key**
- **Dependency preserving decomposition is not guaranteed** in BCNF.
- **Lossless decomposition is guaranteed**
    
> BCNF eliminates all redundancy caused by functional dependencies, but may result in losing the ability to enforce some dependencies directly in the schema.

---

### Dependency Preservation in BCNF:
- During BCNF decomposition, some functional dependencies may not be represented in the resulting relations.
- Those dependencies may need to be enforced through joins or additional logic, rather than through schema constraints.

---

### Summary Table:

| Feature                 | 3NF             | BCNF                |
| ----------------------- | --------------- | ------------------- |
| Lossless Decomposition  | Yes             | Yes                 |
| Dependency Preservation | Always possible | Not always possible |
| Eliminates Redundancy   | Mostly          | Completely          |
| Condition Strictness    | Less strict     | More strict         |

---
