## Sum Of Transportation Numbers

**Problem ID:** 9819  
**Tags:** Uber, Tesla, Google, Medium  
 

---

### Problem Summary

We are given a table `transportation_numbers` that contains numeric entries. The task is:
> Find the **sum of all numbers**, excluding the **lowest** and **highest** values.

Return three columns:
- `min_num`: the lowest value
- `max_num`: the highest value
- `sum_numbers`: total sum excluding the lowest and highest values

---

### Table Schema: `transportation_numbers`

| Column | Type   |
|--------|--------|
| index  | bigint |
| number | bigint |

---

### My Thought Process

1. Use `MIN()` and `MAX()` to get the extreme values.
2. Use `SUM()` to calculate the total of all numbers.
3. Subtract both `MIN()` and `MAX()` from the total sum to get the desired result.

---

### SQL Solution

```sql
SELECT 
  MIN(number) AS min_num,
  MAX(number) AS max_num,
  SUM(number) - MIN(number) - MAX(number) AS sum_numbers
FROM transportation_numbers;
```

---

### What I Learned

This is a neat use of SQL aggregation functions to compute derived values with exclusions, often useful for robust summary statistics.

---

### Tags
`#SQL` `#Aggregation` `#MinMaxExclude` `#Summation` `#InterviewPrep
