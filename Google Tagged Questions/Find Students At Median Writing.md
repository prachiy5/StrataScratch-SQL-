## Find Students At Median Writing Score

**Problem ID:** 9610  
**Tags:** General Assembly, Kaplan, Google, Medium  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer  
**Last Updated:** March 2025  

---

### Problem Summary

We are working with a table called `sat_scores`. It contains student performance data including SAT section scores. Our goal is:
> Identify the **student IDs** of students who scored **exactly at the median** in the SAT **writing** section.

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

1. Rank all the writing scores using `ROW_NUMBER()`.
2. Find the **total number of rows** to identify the middle position(s).
3. Use the middle position(s) to identify the **median score(s)**.
   - If odd, there's one median.
   - If even, there are two middle values (we keep both).
4. Get student IDs for those with writing scores equal to the median(s).

---

### SQL Solution

```sql
WITH ordered_scores AS (
    SELECT student_id, sat_writing,
           ROW_NUMBER() OVER (ORDER BY sat_writing) AS rn,
           COUNT(*) OVER () AS total_count
    FROM sat_scores
),

median_values AS (
    SELECT sat_writing
    FROM ordered_scores
    WHERE rn IN (FLOOR((total_count + 1) / 2), CEIL((total_count + 1) / 2))
)

SELECT student_id 
FROM sat_scores
WHERE sat_writing IN (SELECT sat_writing FROM median_values);
```

---

### What I Learned

This problem is a solid example of how to calculate the **median in SQL** using ranking and filtering. It also shows how to handle both even and odd-sized datasets in one query.

---

### Tags
`#SQL` `#Median` `#SATData` `#WindowFunctions` `#InterviewPrep
