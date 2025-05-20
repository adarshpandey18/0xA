A relation is in **Second Normal Form (2NF)** if:
1. It is already in **First Normal Form (1NF)**.
2. **Every non-prime attribute** is **fully functionally dependent** on the **entire candidate key**.
    - That means **no partial dependency** should exist.

> **Partial Dependency** occurs when a non-prime attribute is dependent on **part of a candidate key**, rather than the **whole key**.

---
### **Example 1:**
**Relation:**  
`Customer_ID | Store_ID | Location`

**Data:**
```
Customer_ID | Store_ID | Location
------------|----------|---------
     1      |     1    | Delhi
     1      |     3    | Mumbai
     2      |     1    | Delhi
     2      |     2    | Bangalore
     4      |     3    | Mumbai
```

- **Candidate Key:** `{Customer_ID, Store_ID}`    
- **Prime Attributes:** `Customer_ID`, `Store_ID`
- **Non-Prime Attribute:** `Location`

**Problem:**  
`Location` depends **only on `Store_ID`**, not on the entire candidate key.

 This is a **partial dependency**  
 Therefore, **not in 2NF**

**Fix (Decompose):**
1. **Customer_Store Table**  
    `(Customer_ID, Store_ID)`
    
2. **Store Table**  
    `(Store_ID, Location)`
    
---
### **Example 2:**

**Relation:** `R(A, B, C, D, E, F)`  
**Functional Dependencies:**
- `C → F`
- `E → A`
- `EC → D`
- `A → B`

**Step 1: Identify Candidate Key**
- `{E, C}` is a candidate key
- Closure of `EC`:
    - `EC → D`
    - `E → A`, then `A → B` ⇒ `E → B`
    - `C → F`
    - Therefore, `EC⁺ = {E, C, D, A, B, F}`

 So, `EC` is the **candidate key**

**Step 2: Identify Prime Attributes**
- `E`, `C` (part of candidate key)

**Step 3: Identify Non-Prime Attributes**
- `A`, `B`, `D`, `F`

**Check for Partial Dependencies:**
- `E → A` → `A` is dependent on part of CK →  Partial dependency
- `C → F` → `F` is dependent on part of CK → Partial dependency
    

Hence, this relation is **not in 2NF**

---
