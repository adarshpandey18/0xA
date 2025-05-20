### **Why is Closure Important?**

- Closure helps to find **all attributes that a set of attributes can determine** using a given set of functional dependencies.    
- It is used to **identify candidate keys**, which are minimal sets of attributes that can determine all attributes in a relation.

---
### **Definition: Closure**
The **closure** of an attribute or set of attributes `X` (written as `X⁺`) is the **set of all attributes** that can be functionally determined by `X`, using the given set of functional dependencies.

---

### **Example 1:**

Let  
**Relation R(ABCD)**  
**Functional Dependencies (F):**
- A → B
- B → C
- C → D

#### **Finding A⁺:**
Start with A
- A → B ⇒ Add B
- B → C ⇒ Add C
- C → D ⇒ Add D

**A⁺ = {A, B, C, D}**

Since A⁺ contains **all attributes of R**,  
**A is a Candidate Key (CK)**

Other closures:
- B⁺ = {B, C, D} (Missing A → Not a CK)
- C⁺ = {C, D}
- D⁺ = {D}

#### **Summary:**

- **Candidate Key (CK):** {A}
- **Prime Attribute:** A
- **Non-Prime Attributes:** B, C, D
    

---

### **Example 2:**

Let  
**Relation R(ABCD)**  
**Functional Dependencies (F):**
- A → B
- B → C
- C → D
- D → A
This creates a **cycle** where each attribute can reach the others.

#### **Finding Closures:**
- A⁺ = {A, B, C, D}
- B⁺ = {B, C, D, A}
- C⁺ = {C, D, A, B}
- D⁺ = {D, A, B, C}
Each of these attribute closures includes **all attributes of R**, so **each is a Candidate Key**.

#### **Summary:**

- **Candidate Keys (CK):** {A}, {B}, {C}, {D}
- **Prime Attributes:** A, B, C, D
- **Non-Prime Attributes:** None

---

### **Steps to Find Closure of X⁺:**

1. Start with X⁺ = X
2. Apply all functional dependencies where the **left side is a subset of X⁺**
3. Add the right side to X⁺
4. Repeat until no more attributes can be added
    

---

