## Email Details Based on Sends vs Receives

**Problem ID:** 10086  
**Tags:** Google, Medium  


---

### Problem Summary

We want to find email records from the days where **more distinct users received emails** than those who sent them.

Return:
- All columns from `google_gmail_emails` for qualifying days.

---

### Table Schema: `google_gmail_emails`

| Column    | Type   |
|-----------|--------|
| id        | bigint |
| from_user | text   |
| to_user   | text   |
| day       | bigint |

---

### SQL Solution

```sql
WITH cte AS (
  SELECT 
    day,
    COUNT(DISTINCT from_user) AS sender_cnt, 
    COUNT(DISTINCT to_user) AS receipent_cnt 
  FROM google_gmail_emails
  GROUP BY day
  HAVING COUNT(DISTINCT to_user) > COUNT(DISTINCT from_user)
)

SELECT *
FROM google_gmail_emails
WHERE day IN (SELECT day FROM cte);
```

---

### What I Learned

This is a good example of grouping data by a dimension (day), applying `HAVING` conditions on aggregates, and using that filtered set to retrieve full records. Useful for engagement or anomaly analysis in communication datasets.

---

### Tags
`#SQL` `#EmailAnalysis` `#Engagement` `#FromVsTo` `#IntermediateSQL` `#InterviewPrep`
