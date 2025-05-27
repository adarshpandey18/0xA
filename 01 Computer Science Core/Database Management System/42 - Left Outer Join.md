
# Left Outer Join

- Returns all records from the **left** table and matching records from the **right** table.
- Fills with `NULL` if there’s no match.

![[left-outer-join-venn-diagram.png|center|300]]

```sql
SELECT emp.emp_no, emp.e_name, dept.d_name, dept.loc 
FROM Employee emp 
LEFT OUTER JOIN Department dept 
ON emp.dept_no = dept.dept_no;
```

**Output Example**:

|emp_no|e_name|d_name|loc|
|---|---|---|---|
|e1|Varun|IT|Delhi|
|e2|Amrit|HR|Hyd|
|e3|Ravi|IT|Delhi|
|e4|Nitin|NULL|NULL|

---

