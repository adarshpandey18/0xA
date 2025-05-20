## **One-to-Many (1:M) / Many-to-One (M:1) Relationship**

- A **One-to-Many (1:M)** relationship exists when **a single record** in one table (**Parent**) is associated with **multiple records** in another table (**Child**).    
- The reverse is called **Many-to-One (M:1)** — many child records point to **one parent**.

---
### **Real-Life Example:**
**Scenario**: A customer can place multiple orders, but each order belongs to only **one customer**.
![[one-to-many-relationship-example.png|center]]

---

### **Entity Tables:**

#### **Customer Table** (Primary Key: `customer_id`)

| customer_id | customer_name | customer_city |
| ----------- | ------------- | ------------- |
| c1          | Alice         | Mumbai        |
| c2          | Bob           | Delhi         |

#### **Order Table** (Primary Key: `order_id`)

| order_id | order_item | order_cost |
| -------- | ---------- | ---------- |
| o1       | Shoes      | 200        |
| o2       | Books      | 300        |
| o3       | Shirt      | 400        |
| o4       | Jeans      | 600        |

---

### **Relationship Table: Gives**

(Describes the relationship between customer and orders, includes a descriptive attribute `date`)

| customer_id | order_id | date      |
| ----------- | -------- | --------- |
| c1          | o1       | 1st March |
| c1          | o2       | 1st March |
| c2          | o3       | 2nd March |
| c3          | o4       | 4th March |

- `customer_id` → foreign key referencing `Customer(customer_id)`    
- `order_id` → foreign key referencing `Order(order_id)`
- `order_id` is **unique** (one order per row) → **primary key** of this relationship
- `customer_id` is **repeated** (a customer gives multiple orders)

---
## **Can Tables Be Reduced?**

###  Yes – Table Reduction Is Possible

Since `order_id` is a **primary key** in both the `Order` table and the `Gives` relationship table, and we need all info per order, we can **merge** them into a single table.

### **New Merged Order Table:**

| order_id | order_item | order_cost | customer_id | date      |
| -------- | ---------- | ---------- | ----------- | --------- |
| o1       | Shoes      | 200        | c1          | 1st March |
| o2       | Books      | 300        | c1          | 1st March |
| o3       | Shirt      | 400        | c2          | 2nd March |
| o4       | Jeans      | 600        | c3          | 4th March |

- Now `customer_id` acts as a **foreign key** in the `Order` table    
- Relationship is still **1:M** (one customer → many 

---

## **Summary Table: One-to-Many Relationship**

| Aspect                     | One-to-Many (1:M) Relationship                                 |
| -------------------------- | -------------------------------------------------------------- |
| **Definition**             | One record in Table A is linked to multiple records in Table B |
| **Example**                | One customer gives many orders                                 |
| **Foreign Key Location**   | On the **many** side (Order table)                             |
| **Reduction Possible?**    | ✅ Yes, by merging if primary key overlaps                      |
| **Descriptive Attributes** | Can exist in the relationship (e.g., `date`)                   |
| **ER Diagram Notation**    | One line from Customer to many lines to Order (crow’s foot)    |

---
