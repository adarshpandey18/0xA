## **One-to-One (1:1) Relationship**
A **one-to-one relationship** exists when **one entity** in a table is **associated with exactly one entity** in another table, and **vice versa**.

---

### **Example:**

![[one-to-one-relationship-example.png|center]]

#### **Employee Table** (Primary Key: `employee_id`)

| employee_id | employee_name | age |
| ----------- | ------------- | --- |
| e001        | Alice         | 30  |
| e002        | Bob           | 25  |
| e003        | Carol         | 28  |
| e004        | Dave          | 35  |
| e005        | Eve           | 32  |

#### **Department Table** (Primary Key: `department_id`)

| department_id | department_name | location  |
| ------------- | --------------- | --------- |
| d001          | IT              | Bangalore |
| d002          | Production      | Delhi     |
| d003          | HR              | Mumbai    |

#### **Work Table** (1:1 Relationship: Employee works in exactly one Department)

| employee_id | department_id |
| ----------- | ------------- |
| e001        | d001          |
| e003        | d002          |
| e002        | d003          |

- **`employee_id`** → foreign key referencing `Employee(employee_id)`    
- **`department_id`** → foreign key referencing `Department(department_id)`
- Each `employee_id` and `department_id` appears **only once** to preserve the **1:1 constraint**
- No `employee_id` or `department_id` is duplicated
- Either `employee_id` or `department_id` can serve as the **primary key** of `Work` table

---

### **Key Points for 1:1 Relationships**
- One record in **Entity A** (Employee) is associated with **one and only one** record in **Entity B** (Department)
- Enforced by:
    - **Unique** constraints on foreign keys
    - Or by setting either attribute as the **primary key**
- Useful when splitting large entities or when certain attributes are optional/rarely used

---

## **Can Tables Be Reduced?**

### **Yes – Table Reduction is Possible**

Since it's a **1:1 relationship**, the `Work` table can be **merged** with either the `Employee` or `Department` table.

> Usually, the merging is done into the table where the foreign key **is optional** or where the relationship **logically belongs**.

### **Merging into Employee Table:**

Add the `department_id` column (foreign key) into the `Employee` table:

#### **New Employee Table:**

|employee_id|employee_name|age|department_id|
|---|---|---|---|
|e001|Alice|30|d001|
|e002|Bob|25|d003|
|e003|Carol|28|d002|
|e004|Dave|35|NULL|
|e005|Eve|32|NULL|

- Here, `department_id` is a **foreign key** referencing `Department(department_id)`
    
- Rows without department assignments (like e004, e005) can have **NULL** in `department_id`
    

---

## **Summary Table: One-to-One Relationship**

|Aspect|One-to-One Relationship|
|---|---|
|**Definition**|One entity from A (Employee) maps to only one entity in B (Department)|
|**Notation (ERD)**|Line with **1:1** on both ends|
|**Implementation**|Use of foreign key with **UNIQUE** constraint|
|**Can be reduced?**|Yes, by merging into one table if the relationship is optional|
|**When to use?**|When logically separating optional attributes, or to optimize schema|

---

