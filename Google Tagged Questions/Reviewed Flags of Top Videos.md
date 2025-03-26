## Reviewed Flags of Top Videos

**Problem ID:** 2103  
**Tags:** Google, Hard  


---

### Problem Summary

We’re given two tables:

- `user_flags`: shows which user flagged which video
- `flag_review`: shows which flags were reviewed by YouTube

We need to:
> Find the video (or videos) that got the **most user flags**, and then count how many of those flags were **reviewed by YouTube**.

The output should be:
- `video_id`
- Number of reviewed flags for that video

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

1. First, count how many flags each video got.
2. Use `DENSE_RANK()` to find the video(s) with the highest number of flags.
3. Filter out just those top-ranked video(s).
4. Join with the `flag_review` table to check which flags were reviewed.
5. Only count flags that were reviewed by YouTube (`reviewed_by_yt = 1`).

---

### SQL Solution

```sql
WITH cte AS (
    SELECT video_id,
           COUNT(flag_id) AS total_flags,
           DENSE_RANK() OVER(ORDER BY COUNT(flag_id) DESC) AS rn
    FROM user_flags
    WHERE video_id IS NOT NULL
    GROUP BY video_id
),

cte2 AS (
    SELECT *
    FROM cte
    WHERE rn = 1
)

SELECT uf.video_id,
       COUNT(uf.flag_id) AS reviewed_flags
FROM user_flags uf
INNER JOIN flag_review fr
    ON fr.flag_id = uf.flag_id
WHERE uf.video_id IN (SELECT video_id FROM cte2)
  AND fr.reviewed_by_yt = 1
GROUP BY uf.video_id;
```

---

### What I Learned

This problem is a good example of combining **ranking**, **joins**, and **filters**. It shows how we can find top performers (in this case, most flagged videos), then filter and analyze them further using another table.

---

### Tags
`#SQL` `#Ranking` `#Joins` `#Filters` `#YouTubeReview` `#InterviewPrep`
