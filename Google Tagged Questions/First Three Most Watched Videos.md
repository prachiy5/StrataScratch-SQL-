## Top 3 Videos Watched First by Users

**Problem ID:** Custom  
**Tags:** Ranking, Window Functions, Watch Behavior  

---

### Problem Summary

We’re given a table called `videos_watched` that logs which videos users watched and when. Each row contains:
- `user_id`: who watched the video
- `video_id`: what video was watched
- `watched_at`: when it was watched

We want to:
> Find the top 3 videos that appeared most often in users’ **first 3 watched videos**.
> If there’s a tie in counts, include all videos tied within the top 3 ranks.

---

### Table Schema: `videos_watched`

| Column     | Type      |
|------------|-----------|
| user_id    | text      |
| video_id   | text      |
| watched_at | timestamp |

---

### My Thought Process

1. First, for each user, rank the videos they watched by `watched_at`.
2. Keep only the videos ranked in the first 3 (these are the first 3 videos a user watched).
3. Count how many users had each video in their first 3.
4. Use `DENSE_RANK()` to rank videos by how many times they appeared in first 3.
5. Return all videos that are within the top 3 ranks.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT *,
           DENSE_RANK() OVER(PARTITION BY user_id ORDER BY watched_at) AS first_video
    FROM videos_watched
),

cte2 AS (
    SELECT video_id,
           COUNT(user_id) AS n_in_first_3,
           DENSE_RANK() OVER(ORDER BY COUNT(user_id) DESC) AS dr
    FROM cte
    WHERE first_video <= 3
    GROUP BY video_id
)

SELECT video_id, n_in_first_3
FROM cte2
WHERE dr <= 3;
```

---

### What I Learned

This problem is a great example of how to use window functions to look at user behavior and identify popular trends based on watch order. It’s a good mix of ranking, grouping, and counting across partitions.

---

### Tags
`#SQL` `#WindowFunctions` `#DenseRank` `#VideoWatchData` `#UserBehavior` `#TopK` `#InterviewPrep`
