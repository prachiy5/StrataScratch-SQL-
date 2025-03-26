## Videos Removed on Latest Date

**Problem ID:** 2105  
**Tags:** Google, Hard  


---

### Problem Summary

We’re given two tables:
- `user_flags`: which user flagged which video
- `flag_review`: when a flag was reviewed and what the outcome was

We want to:
> For each user, find the latest date when one of their flags got reviewed.
> Then, check how many **distinct videos** were removed on that same date (by any user).
> Show the user's first name, last name, the date, and the number of removed videos.
> Only include users who had **at least one** of their flags reviewed by YouTube.
> If **no videos** were removed on that date, show **0**.

---

### Table Schemas

**user_flags**

| Column          | Type |
|------------------|------|
| user_firstname   | text |
| user_lastname    | text |
| video_id         | text |
| flag_id          | text |

**flag_review**

| Column          | Type     |
|------------------|----------|
| flag_id          | text     |
| reviewed_by_yt   | tinyint  |
| reviewed_date    | datetime |
| reviewed_outcome | text     |

---

### My Thought Process

1. First, for each user, find the **latest review date** of any of their flags.
2. Next, find how many **distinct videos were removed** on each review date.
3. Join both results on the date.
4. Use `COALESCE()` to show 0 if no videos were removed on a date.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT user_firstname, 
           user_lastname,
           uf.flag_id,
           MAX(reviewed_date) AS latest_date
    FROM user_flags uf
    INNER JOIN flag_review fr
        ON uf.flag_id = fr.flag_id
    WHERE reviewed_date IS NOT NULL
    GROUP BY user_firstname, user_lastname
),

cte2 AS (
    SELECT reviewed_date,
           COUNT(DISTINCT video_id) AS n_removed
    FROM user_flags uf
    INNER JOIN flag_review fr 
        ON uf.flag_id = fr.flag_id
    WHERE reviewed_outcome = 'REMOVED'
    GROUP BY reviewed_date
)

SELECT c1.user_firstname, 
       c1.user_lastname, 
       c1.latest_date, 
       COALESCE(c2.n_removed, 0) AS n_removed
FROM cte c1
LEFT JOIN cte2 c2
    ON c1.latest_date = c2.reviewed_date;
```

---

### What I Learned

This problem mixes several concepts:
- `MAX()` to get the latest value
- `LEFT JOIN` to keep all users even if no videos were removed on their date
- `COALESCE()` to handle missing data cleanly

