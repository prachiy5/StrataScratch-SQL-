## Unique Users Who Flagged Each Video

**Problem ID:** Custom  
**Tags:** Group By, String Manipulation, Filtering  
**Roles:** Data Analyst, BI Analyst, Data Scientist  
**Last Updated:** March 2025  

---

### Problem Summary

We are given a table called `user_flags`. Each row shows who flagged a video, and includes:
- the user's first name
- the user's last name
- the video ID
- the flag ID (which may be blank if no flag was made)

We want to:
> Find out how many **unique users** flagged each video.

We identify a unique user by combining their **first and last names**. We **ignore** any rows that don’t have a `flag_id`.

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

1. First, we remove rows where `flag_id` is empty, since those users didn’t flag anything.
2. Then we combine `user_firstname` and `user_lastname` into one name to identify unique users.
3. After that, we count how many **distinct users** flagged each `video_id`.
4. Finally, we sort the results by number of users.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT COALESCE(CONCAT(user_firstname, ' ', user_lastname), 'unknown') AS full_name,
           video_id,
           flag_id
    FROM user_flags
    WHERE flag_id != ''
)

SELECT video_id,
       COUNT(DISTINCT full_name) AS num_users
FROM cte
GROUP BY video_id
ORDER BY num_users;
```

---

### What I Learned

This problem is about combining basic SQL skills:
- Filtering out rows using `WHERE`
- Creating unique identifiers by concatenating strings
- Grouping and counting distinct values

---

### Tags
`#SQL` `#GroupBy` `#DistinctCount` `#Filtering` `#UserEngagement` `#InterviewPrep`
