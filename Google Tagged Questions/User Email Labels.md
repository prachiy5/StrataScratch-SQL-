## User Email Labels

**Problem ID:** 10068  
**Tags:** Google, Medium  

---

### Problem Summary

We need to count how many emails each user received under the **built-in email labels**:
- `Promotion`
- `Social`
- `Shopping`

Return:
- The `to_user` (receiver of email)
- Number of emails received under each of the 3 labels

---

### Tables Used

**google_gmail_emails**
| Column    | Type   |
|-----------|--------|
| id        | bigint |
| from_user | text   |
| to_user   | text   |
| day       | bigint |

**google_gmail_labels**
| Column   | Type   |
|----------|--------|
| email_id | bigint |
| label    | text   |

---

### SQL Solution

```sql
WITH cte AS (
  SELECT *
  FROM google_gmail_emails ge
  INNER JOIN google_gmail_labels gl
    ON gl.email_id = ge.id
)

SELECT 
  to_user,
  SUM(CASE WHEN label = 'Promotion' THEN 1 ELSE 0 END) AS promotion_count,
  SUM(CASE WHEN label = 'Social' THEN 1 ELSE 0 END) AS social_count,
  SUM(CASE WHEN label = 'Shopping' THEN 1 ELSE 0 END) AS shopping_count
FROM cte
GROUP BY to_user;
```

---

### What I Learned

This problem tests your ability to join datasets and apply conditional aggregation using `CASE WHEN`. It’s great practice for reporting and label-based email analytics.

---

### Tags
`#SQL` `#EmailAnalysis` `#GmailLabels` `#ConditionalAggregation` `#UserEngagement` `#InterviewPrep
