# **Right Outer Join**

- Returns all records from the **right** table and matching records from the **left** table.

![[right-outer-join-venn-diagram.png|center|300]]

```sql
SELECT emp.e_no, emp.e_name, dept.d_name 
FROM Employee emp 
RIGHT OUTER JOIN Department dept 
ON emp.d_no = dept.dept_no;
```

**Output** includes all departments, even if no employee is assigned.

---

# **Full Outer Join**

- Combines the results of **left** and **right** outer joins.
- Returns all records from both tables, with `NULL`s where there's no match.    

```sql
SELECT emp.e_no, emp.e_name, dept.d_name 
FROM Employee emp 
FULL OUTER JOIN Department dept 
ON emp.d_no = dept.dept_no;
```

---

