## Find Non-HS SAT Scores

**Problem ID:** 9598  
**Tags:** General Assembly, Kaplan, Google, Easy  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer, Software Engineer  
**Last Updated:** March 2025  

---

### Problem Summary

We’re given a table called `sat_scores`, which has SAT score information for students from different schools.
Each row contains things like:
- the name of the school
- student ID
- SAT scores (math, verbal, writing)
- study hours and more

The goal is:
> Find all the SAT score records where the **school name does not end with 'HS'** (case-insensitive).

---

### Table Schema: `sat_scores`

| Column        | Type    |
|---------------|---------|
| school        | text    |
| teacher       | text    |
| student_id    | double  |
| sat_writing   | double  |
| sat_verbal    | double  |
| sat_math      | double  |
| hrs_studied   | double  |
| id            | bigint  |
| average_sat   | double  |
| love          | datetime |

---

### My Thought Process

1. We’re looking at the `school` column.
2. We want to filter out rows where the school name ends with 'HS'.
3. We use the `NOT LIKE '%HS'` pattern to do this.
4. To be safe, we should make it case-insensitive by converting to lowercase (or uppercase).

---

### SQL Solution

```sql
SELECT *
FROM sat_scores
WHERE LOWER(school) NOT LIKE '%hs';
```

---

### What I Learned

This kind of question teaches you how to filter string values using `LIKE` and how to ensure case insensitivity using functions like `LOWER()` or `UPPER()`.

---

### Tags
`#SQL` `#Filtering` `#StringFunctions` `#SATData` `#InterviewPrep`
