### Question : 
![[minimize-table-question.png]]
### Answer: b) 3
##  **Step-by-Step Analysis**

###  **Entities:**

1. `E₁(A)` → Entity table
    
2. `E₂(B)` → Entity table
    

These **must be converted** to two separate tables.

---

###  **Relationships:**

#### 🔹 **R₁: 1 to M (E₁ → E₂)**

- One-to-Many → can be **implemented by adding a foreign key**
    
- Add **E₁'s key** as a **foreign key** in the **E₂ table** (since many E₂ instances refer to one E₁)
    

 **No separate table** needed for this relationship.

#### 🔹 **R₂: M to N (E₁ ↔ E₂)**

- Many-to-Many → **requires a separate table**
    
- Create a new table with **foreign keys** from both **E₁** and **E₂**
    

 **One additional table** required

---

###  **Final Tables Required:**

| Table Type             | Count  |
| ---------------------- | ------ |
| Entity Tables (E₁, E₂) | 2      |
| R₁ (1:M)               | 0      |
| R₂ (M:N)               | 1      |
| **Total**              | **3**  |