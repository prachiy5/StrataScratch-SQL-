## Count the Number of Students Lectured by Each Teacher

**Problem ID:** 9660  
**Tags:** General Assembly, Kaplan, Google, Easy  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer  
**Last Updated:** January 2025  

---

### Problem Summary

We are given a table called `sat_scores`, which contains student information including which teacher taught them. We want to:
> Count how many **unique students** each teacher has lectured.

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

1. Group the data by `teacher`.
2. Use `COUNT(DISTINCT student_id)` to make sure we only count each student once per teacher.

---

### SQL Solution

```sql
SELECT teacher,
       COUNT(DISTINCT student_id) AS num_students
FROM sat_scores
GROUP BY teacher;
```

---

### What I Learned

This kind of problem is useful for practicing how to group and count unique values. It’s very common in educational, sales, and HR datasets.

---

### Tags
`#SQL` `#GroupBy` `#EducationData` `#StudentCounts` `#InterviewPrep
