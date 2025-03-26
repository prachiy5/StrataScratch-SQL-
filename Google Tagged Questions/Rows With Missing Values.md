## Rows With Missing Values

**Problem ID:** 2106  
**Tags:** Google, Medium  


---

### Problem Summary

We’re working with a table called `user_flags`, and our goal is simple:
> Find all the rows where **more than one column is missing** (i.e. has a NULL value).

This is part of a data cleaning task.

---

### Table Schema: `user_flags`

| Column          | Type |
|------------------|------|
| user_firstname   | text |
| user_lastname    | text |
| video_id         | text |
| flag_id          | text |

---

### My Thought Process

1. For each row, check each column to see if it’s NULL.
2. Add up how many NULLs are in that row.
3. Only keep the rows where more than one column has missing values.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT *,
           (CASE WHEN user_firstname IS NULL THEN 1 ELSE 0 END +
            CASE WHEN user_lastname IS NULL THEN 1 ELSE 0 END +
            CASE WHEN video_id IS NULL THEN 1 ELSE 0 END +
            CASE WHEN flag_id IS NULL THEN 1 ELSE 0 END) AS missing_values
    FROM user_flags
)

SELECT user_firstname, user_lastname, video_id, flag_id
FROM cte
WHERE missing_values > 1;
```

---

### What I Learned

This is a helpful example of how to scan for data quality issues in a dataset. Summing up boolean checks for NULLs is a simple but powerful way to identify rows with lots of missing data.

---

### Tags
`#SQL` `#DataCleaning` `#NullCheck` `#DataQuality` `#YouTubeFlags` `#InterviewPrep
