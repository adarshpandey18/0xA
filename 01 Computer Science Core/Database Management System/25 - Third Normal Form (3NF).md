A relation is in **Third Normal Form (3NF)** if
1. It is in **Second Normal Form (2NF)**
2. It has **no transitive dependencies**, i.e.:
    - **No non-prime attribute should determine another non-prime attribute**

> A transitive dependency exists if:> 
> - `X → Y` and `Y → Z`, then `X → Z`
> - Where `Z` is **transitively dependent** on `X` through `Y`

---
### **Example 1:**
**Relation:**  
`RollNo | State | City`

**Functional Dependencies:**
- `RollNo → State`
- `State → City`

**Candidate Key:** `RollNo`  
**Prime Attribute:** `RollNo`  
**Non-Prime Attributes:** `State`, `City`

**Issue:**
- `RollNo → State` → valid
- But `State → City` → **City** is transitively dependent on **RollNo** via **State**
- Both `State` and `City` are **non-prime attributes**

**This violates 3NF** due to transitive dependency between non-prime attributes.
**Fix (Decompose into 3NF):**
1. **Student Table:** `(RollNo, State)`
2. **State Table:** `(State, City)`    

---
### **Example 2:**

**Relation:** `R(A, B, C, D)`  
**Functional Dependencies:**
- `AB → C`
- `C → D`

**Candidate Key:** `AB`  
**Prime Attributes:** `A`, `B`  
**Non-Prime Attributes:** `C`, `D`

**Problem:**
- `C` (non-prime) → `D` (non-prime)
- So, `AB → C` and `C → D` ⇒ `AB → D` (via transitive dependency)
 Violates 3NF due to **non-prime → non-prime**

**Fix (Decompose into 3NF):**
1. **R1(AB, C)**
2. **R2(C, D)**


---

### Summary:
To ensure **3NF**:
- Eliminate **transitive dependencies**
- Only **candidate keys** or **prime attributes** should determine other attributes

---