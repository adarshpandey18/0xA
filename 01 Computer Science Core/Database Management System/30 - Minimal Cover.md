### What is **Minimal Cover**?
A **minimal cover** (also called **canonical cover**) of a set of functional dependencies (FDs) is an equivalent set of dependencies that is:
1. **Logically equivalent** to the original set.    
2. **Minimal**, meaning:
    - Each functional dependency has a **single attribute** on the right-hand side.
    - The left-hand side of each FD has **no extraneous attributes**.
    - The set contains **no redundant dependencies**.

---
### Why Use Minimal Cover?
- Used in **normalization**.
- Helps to find **candidate keys**.
- Useful for minimizing **redundancy** and simplifying **FD analysis**.

---

### Example
Given Functional Dependencies:
```
F = {
  A → B,
  C → B,
  D → ABC,
  AC → D
}
```

---

### Step-by-step Process to Find Minimal Cover

---

#### **Step 1: Split RHS to Singleton Attributes**

Split dependencies where RHS has multiple attributes:

```
D → ABC  becomes:
D → A  
D → B  
D → C
```

Now the full set becomes:

```
A → B  
C → B  
D → A  
D → B  
D → C  
AC → D
```

---

#### **Step 2: Remove Redundant Dependencies**

Check if any FD is **redundant** by removing it and checking if the same dependency can be **inferred** from the remaining ones.

Let’s evaluate one by one:

1. Try removing `D → B`  
    Check if `D → B` is implied by:
    
    ```
    A → B  
    C → B  
    D → A  
    D → C  
    AC → D
    ```
    
    - D → A and A → B ⇒ D → B  
        ✅ So, **D → B is redundant**.
        
2. Try removing `D → C`
    
    - D → C is **not implied** by remaining FDs.  
        ❌ Keep it.
        

Now F becomes:

```
A → B  
C → B  
D → A  
D → C  
AC → D
```

---

#### **Step 3: Minimize LHS (remove extraneous attributes)**

Only one FD has a **composite LHS**: `AC → D`

Check if either `A` or `C` is extraneous.

- Try removing `A` from `AC → D`:  
    Check if `C → D` holds.
    
    - From `C → B`, `C → D` can't be derived.  
        ❌ `C` alone doesn't determine `D`.
        
- Try removing `C` from `AC → D`:  
    Check if `A → D` holds.
    
    - From `A → B`, `A → D` can't be derived.  
        ❌ `A` alone doesn't determine `D`.
        

So `AC → D` is already minimal.

---

### Final Minimal Cover

```
A → B  
C → B  
D → A  
D → C  
AC → D
```

This is the **minimal cover** for the given set of FDs.

---