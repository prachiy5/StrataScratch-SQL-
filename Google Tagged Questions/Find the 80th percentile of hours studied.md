## Find the 80th Percentile of Hours Studied

**Problem ID:** 9611  
**Tags:** General Assembly, Kaplan, Google, Medium  

---

### Problem Summary

We are working with the `sat_scores` table that includes student data such as SAT scores and hours studied. Our task is:
> Find the **80th percentile** of `hrs_studied`. Output just the value of `hrs_studied` that corresponds to the 80th percentile.

---

### Table Schema: `sat_scores`

| Column        | Type     |
|---------------|----------|
| school        | text     |
| teacher       | text     |
| student_id    | double   |
| sat_writing   | double   |
| sat_verbal    | double   |
| sat_math      | double   |
| hrs_studied   | double   |
| id            | bigint   |
| average_sat   | double   |
| love          | datetime |

---

### My Thought Process

1. Use the `PERCENT_RANK()` window function to calculate the percentile rank for each `hrs_studied` value.
2. Filter only rows where the percentile rank rounds to **80**.
3. Use `DISTINCT` to ensure we return only unique values in case of ties.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT hrs_studied,
           PERCENT_RANK() OVER(ORDER BY hrs_studied) AS percentile_hrs
    FROM sat_scores
    WHERE hrs_studied IS NOT NULL
)

SELECT DISTINCT hrs_studied
FROM cte
WHERE ROUND(percentile_hrs * 100) = 80;
```

---

### What I Learned

This problem shows how useful `PERCENT_RANK()` is when trying to calculate percentiles in SQL, especially for datasets where built-in percentile functions aren't available.

---

### Tags
`#SQL` `#Percentiles` `#HoursStudied` `#WindowFunctions` `#InterviewPrep`
