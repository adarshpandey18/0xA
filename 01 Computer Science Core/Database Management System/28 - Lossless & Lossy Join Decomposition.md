###  Normalization & Decomposition Basics:

- **Normalization** is the process of organizing data to minimize redundancy and improve data integrity.
- It usually involves **decomposition**, i.e., breaking one table into two or more tables.
- The goal is to preserve all information **without loss** (ideally).

---

###  Lossless vs. Lossy Join Decomposition

#### 1. **Lossless Join Decomposition:**
- **Definition:** No information is lost when decomposed tables are joined back.
- **Condition:** At least one of the decomposed tables must contain a **candidate key** of the original relation.

> _This is the **goal** in normalization._

#### 2. **Lossy Join Decomposition:**
- **Definition:** Some information is lost or incorrect rows are added when joining decomposed tables.
- Happens when the common attribute is **not enough to reconstruct the original table correctly**.

> _This is **not desirable**_.

---

###  Example
Original Table `R(a, b, c)`:

| a   | b   | c   |
| --- | --- | --- |
| 1   | 2   | 1   |
| 2   | 2   | 2   |
| 3   | 3   | 2   |

**Decomposition:**
- `R1(a, b)`

| a   | b   |
| --- | --- |
| 1   | 2   |
| 2   | 2   |
| 3   | 3   |

- `R2(b, c)`    

| b   | c   |
| --- | --- |
| 2   | 1   |
| 2   | 2   |
| 3   | 2   |

Now let's **join R1 and R2** on the common attribute `b`:

```sql
SELECT * FROM R1 NATURAL JOIN R2;
```

This will result in:

| a   | b   | c   |
| --- | --- | --- |
| 1   | 2   | 1   |
| 1   | 2   | 2   |
| 2   | 2   | 1   |
| 2   | 2   | 2   |
| 3   | 3   | 2   |

This contains **more rows than original R**, meaning it is a **lossy decomposition**.

---

###  Why Did Loss Occur?

- `b` is not a **key** in either `R1` or `R2`, so it cannot uniquely identify a tuple.
- Therefore, the join introduces **extra combinations** — this is a **lossy join**.

---

###  Query to Find `c` Where `a = 1`

We need to **rejoin** the decomposed tables:

```sql
SELECT r2.c
FROM r1
NATURAL JOIN r2
WHERE r1.a = '1';
```

Explanation:
- `NATURAL JOIN` joins on common column `b`.
- We filter by `a = 1` from `r1`, and get corresponding `c` values from `r2`.

---

###  Important Rule (Your Note):

> When decomposing, **at least one common attribute is required** between tables if they are related. If not, they don’t need to be joined.

True. This ensures that you can rejoin the tables logically.

---
###  Summary

| Term               | Meaning                                                               |
| ------------------ | --------------------------------------------------------------------- |
| **Lossless Join**  | Original table is fully reconstructible from decomposed tables        |
| **Lossy Join**     | Reconstructed table has missing or extra rows                         |
| **Join Condition** | Common attribute (preferably a key) is required to ensure proper join |

---