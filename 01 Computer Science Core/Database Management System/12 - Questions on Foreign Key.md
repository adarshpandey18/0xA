1. Let R1 (a, b,c) and R2(x,y,x) be two relations in which 'a ' is foreing key in R1 that refers to primary key of r2 consider fours options 
	 1. Insert into R1
	 2. Insert into R2
	 3. Delete from R1
	 4. Delete from R2
Which is correct referring referential integrity ?
	5. option a and b case viaolation
	6. option b and c willl cause vialation
	7. option c and d will cause violation
	8. option c and d will cause violation
	9. option d and a will cause violation

---

## **Referential Integrity Notes with Foreign Key**

### **Given:**

- **R1(a, b, c)** and **R2(x, y, z)**
    
- Attribute **`a` in R1** is a **foreign key** that references **primary key `x` in R2**
    

---

### **Understanding Referential Integrity:**

Referential integrity ensures that:

1. You **cannot insert a value in the foreign key column** (`a` in R1) **unless it exists in the referenced primary key column** (`x` in R2).
    
2. You **cannot delete a row in the referenced table** (`R2`) **if it is being referenced** by a foreign key in another table (`R1`).
    

---

### **Operations and Effects on Integrity:**

|Operation|Effect on Referential Integrity|
|---|---|
|**Insert into R1**|May violate integrity if value in `a` doesn't exist in `R2(x)`|
|**Insert into R2**|Safe. You are adding values to the referenced table, no violation|
|**Delete from R1**|Safe. Removing a referencing row doesn't affect integrity|
|**Delete from R2**|May violate integrity if a value in `x` is referenced by any value in `R1(a)`|

---

### **Answer Options Analysis:**

- **Option A (Insert into R1)** — Can **violate** integrity if `a` does not match an existing `x` in R2.
    
- **Option B (Insert into R2)** — **Safe**
    
- **Option C (Delete from R1)** — **Safe**
    
- **Option D (Delete from R2)** — Can **violate** integrity if `x` is being referenced in R1.
    

---

### **Correct Answer Based on Violations:**

#### Option **9**: **Delete from R2** and **Insert into R1** can cause referential integrity **violations**

> So, **Correct Answer: Option 9 — option d and a will cause violation**
	