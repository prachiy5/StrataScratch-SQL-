## Find the Student with the Highest Efficiency for Mathematics

**Problem ID:** 9661  
**Tags:** General Assembly, Kaplan, Google, Medium  


---

### Problem Summary

We’re working with the `sat_scores` table, which contains student SAT performance and study time. We need to:
> Find the student with the **highest efficiency in math**, defined as:
> 
> `efficiency = sat_math / hrs_studied`

Only include students who studied **at least 1 hour**.

Return:
- `student_id`
- `hrs_studied`
- `sat_math`
- `points_per_hour` (i.e., efficiency)

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

1. Filter out students who studied less than 1 hour.
2. Calculate their math efficiency as `sat_math / hrs_studied`.
3. Rank them by efficiency in descending order using `DENSE_RANK()`.
4. Pick the student(s) with the highest efficiency (rank = 1).

---

### SQL Solution

```sql
WITH cte AS (
    SELECT student_id,
           hrs_studied,
           sat_math,
           sat_math / hrs_studied AS points_per_hour,
           DENSE_RANK() OVER(ORDER BY sat_math / hrs_studied DESC) AS rn
    FROM sat_scores
    WHERE hrs_studied >= 1
)

SELECT student_id, hrs_studied, sat_math, points_per_hour
FROM cte
WHERE rn = 1;
```

---

### What I Learned

This problem is a great example of combining filtering, calculated fields, and ranking functions to pull out top performers based on custom metrics.

---

### Tags
`#SQL` `#Efficiency` `#MathScore` `#WindowFunctions` `#InterviewPrep`
