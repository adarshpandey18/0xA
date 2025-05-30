# Super Key

A **super key** is a **set of one or more attributes** that can **uniquely identify** a tuple (row) in a table.
- Any **super set of a candidate key** is a **super key**.
- A **candidate key** is a **minimal super key** (i.e., removing any attribute from it will cause it to stop being a key).

---
### **Example:**
**Student Table:**

| rollNo | name | age |
| ------ | ---- | --- |

Let `rollNo` be a **candidate key** (unique and minimal).
Then, possible **super keys** include:
- `{rollNo}`
- `{rollNo, name}`
- `{rollNo, age}`
- `{rollNo, name, age}`

> All of the above can uniquely identify each student, so they are super keys.

---
## **How Many Super Keys Are Possible?**
Let relation **R(A₁, A₂, ..., Aₙ)** have **n attributes**.
Let’s assume the **candidate keys** are known.

---

### **Case 1: A₁ is the only candidate key**

We can create a super key by taking **A₁** and **any combination of remaining attributes**.
- Number of attributes excluding $A₁ = n − 1$
- For each attribute, there are 2 choices: **include** or **exclude**
- So, number of combinations with $A₁ = 2^{n-1}$

$$\text{Total super keys} = 2 ^ {n-1}$$

---

### **Case 2: A₁ and A₂ are both candidate keys**

Now, you must include **either A₁ or A₂** (or both) in every super key.
- For each candidate key, the number of super keys that include it = $2{n-1}$
So, total:

$$\text{Total super keys} = 2^{n−1} + 2^{n−1} = 2× 2^{n−1} = 2^{n}$$

> But you must be cautious: if A₁ and A₂ **overlap in super sets**, some super keys may be **counted twice**. So the actual number may be **less than** 2n2^n in practice unless they are completely disjoint.

---
