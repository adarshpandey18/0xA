
#  Equi Join

- A specific type of conditional join using equality (`=`) between columns.

### Example:
Find employee names where employee and department locations match.

```sql
SELECT employee_name 
FROM Employee 
JOIN Department 
ON Employee.employee_id = Department.employee_id 
AND Employee.employee_address = Department.location;
```

(Note: For this query to work, `Department` table must have a `location` column.)

---


