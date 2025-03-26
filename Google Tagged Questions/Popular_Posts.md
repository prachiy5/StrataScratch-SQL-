## Popular Posts

**Problem ID:** 2073  
**Tags:** Google, Amazon, Meta, Hard  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer  
**Last Updated:** June 2024  

---

### Problem Summary

We’re given two tables:

- `user_sessions` – This tells us how long each session lasted.
- `post_views` – This shows which post was viewed during which session, and what percentage of the session time was spent viewing that post (called `perc_viewed`).

We want to find out how much total time each post was actually viewed by users, **in seconds**.

But there’s a condition:
> Only show posts where the total viewing time is **more than 5 seconds**.

---

### Table Schemas

**user_sessions**

| Column            | Type      |
|-------------------|-----------|
| session_id        | bigint    |
| user_id           | text      |
| session_starttime | timestamp |
| session_endtime   | timestamp |
| platform          | text      |

**post_views**

| Column     | Type   |
|------------|--------|
| session_id | bigint |
| post_id    | bigint |
| perc_viewed| double |

---

### My Thought Process (Explained Simply)

1. First, we want to find the duration of each session in seconds. We can do this by subtracting `session_starttime` from `session_endtime`.
2. Then, we join that session info with the `post_views` table so we know which post was viewed during that session.
3. Next, we use `perc_viewed` to figure out how much of the session time was spent viewing the post. For example, if the session was 60 seconds long and `perc_viewed` was 50, then the user viewed the post for 30 seconds.
4. Finally, we group everything by `post_id` and sum up all the viewing time.
5. We only keep the posts that were viewed for more than 5 seconds in total.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT post_id, perc_viewed,
           TIMESTAMPDIFF(SECOND, session_starttime, session_endtime) AS duration_sec
    FROM user_sessions us
    INNER JOIN post_views pv
        ON us.session_id = pv.session_id
)

SELECT post_id, 
       SUM((perc_viewed / 100) * duration_sec) AS total_view_time
FROM cte
GROUP BY post_id
HAVING SUM((perc_viewed / 100) * duration_sec) > 5;
```

---



### What I Learned

This problem is a nice mix of basic SQL skills:
- Doing a join between tables.
- Calculating time differences.
- Working with percentages.
- Using `HAVING` to filter aggregated results.

Even though it's a harder problem, the logic is pretty straightforward if you take it step by step.

---

### Tags
`#SQL` `#ViewTime` `#PercentTime` `#SessionData` `#PostEngagement` `#InterviewPrep`
