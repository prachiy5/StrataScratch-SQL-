## User with Most Approved Flags

**Problem ID:** 2104  
**Tags:** Google, Medium  

---

### Problem Summary

We are given two tables:

- `user_flags`: tells us which user flagged which video
- `flag_review`: tells us whether those flags were reviewed and what the outcome was

Our goal:
> Find the user(s) who flagged the most **distinct videos** that were **approved** by YouTube.
> Show the user’s full name (first + last with a space).
> If there’s a tie, show all such users.

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

1. Join the two tables on `flag_id`.
2. Filter to only keep rows where `reviewed_outcome = 'APPROVED'`.
3. Create a full name for the user by combining first and last names.
4. For each user, count how many **different videos** they flagged that were approved.
5. Use `DENSE_RANK()` to get the user(s) with the highest count.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT COALESCE(CONCAT(user_firstname, ' ', user_lastname), 'unknown') AS full_name,
           video_id,
           uf.flag_id,
           reviewed_by_yt,
           reviewed_outcome
    FROM user_flags uf
    INNER JOIN flag_review fr
        ON uf.flag_id = fr.flag_id
    WHERE reviewed_outcome = 'APPROVED'
),

cte2 AS (
    SELECT full_name,
           COUNT(DISTINCT video_id) AS distinct_video_count,
           DENSE_RANK() OVER(ORDER BY COUNT(DISTINCT video_id) DESC) AS dr
    FROM cte
    GROUP BY full_name
)

SELECT full_name
FROM cte2
WHERE dr = 1;
```

---

### What I Learned

This problem is great for practicing how to:
- Join two datasets
- Work with review outcomes
- Aggregate based on distinct values
- Rank results and handle ties

It also shows how to cleanly format names and handle missing data using `COALESCE()`.

---

### Tags
`#SQL` `#Joins` `#Filtering` `#GroupBy` `#ReviewAnalysis` `#ApprovedFlags` `#InterviewPrep
