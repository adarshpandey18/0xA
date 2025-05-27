# Self Join
- A table joins with itself.
- Useful for comparing rows within the same table.

### Example:
Find students enrolled in at least two different courses.

**Study Table:**

| s_id | c_id | since |
| ---- | ---- | ----- |
| s1   | c1   | 2016  |
| s2   | c2   | 2017  |
| s1   | c2   | 2017  |

```sql
SELECT DISTINCT t1.s_id 
FROM Study t1 
JOIN Study t2 
ON t1.s_id = t2.s_id AND t1.c_id <> t2.c_id;
```

---
