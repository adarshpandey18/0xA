# Joins

---
## **What is a Join?**
**Joins** are used when we want to retrieve data by combining rows from two or more tables based on a related column between them.

**Join = Cross Product + Some Condition**

To apply a join:
- There must be **at least one common attribute** between the tables.

---
## **Tables Example**
### `Employee` Table

| employee_id | employee_name | employee_address |
| ----------- | ------------- | ---------------- |
| 1           | Ram           | Delhi            |
| 2           | Varun         | Chd              |
| 3           | Ravi          | Chd              |
| 4           | Amrit         | Delhi            |
| 5           | Nitin         | Noida            |

### `Department` Table

| department_id | department_name | employee_id |
| ------------- | --------------- | ----------- |
| D1            | HR              | 1           |
| D2            | IT              | 2           |
| D3            | MRKT            | 4           |
| D4            | Finance         | 5           |

**Query**: Find the employee names of employees who work in the HR department.

```sql
SELECT employee_name 
FROM Employee 
JOIN Department ON Employee.employee_id = Department.employee_id 
WHERE Department.department_name = 'HR';
```

**Output**:

```
Ram
```

---

## **Types of Joins**

1. **Cross Join**

2. **Natural Join**
    
3. **Conditional Join**
    
4. **Equi Join**
    
5. **Self Join**
    
6. **Outer Join**
    
    - Left Outer Join
        
    - Right Outer Join
        
    - Full Outer Join
        
---

##  Cross Join

- Produces a **Cartesian product**.
- If one table has `m` rows and another has `n`, the result has `m × n` rows.
- No condition is applied.

---
