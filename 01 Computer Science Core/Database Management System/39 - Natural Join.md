# Natural Join
- Automatically joins tables on all columns with the same name and compatible data types.

### Example:

```sql
SELECT employee_name 
FROM Employee NATURAL JOIN Department;
```

Assumes `employee_id` is the common column.

---

# Conditional Join
- A join with a condition in the `ON` or `WHERE` clause.
### Example:

```sql
SELECT employee_name 
FROM Employee 
JOIN Department 
ON Employee.employee_id = Department.employee_id;
```

---
