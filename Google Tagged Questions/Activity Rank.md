## Email Activity Rank by User

**Problem ID:** 10351  
**Tags:** Google, Medium  

---

### Problem Summary

Find the **email activity rank** for each user, based on the total number of emails **sent**.

Rules:
- Rank 1 is for the user who sent the most emails.
- If multiple users sent the same number, rank by username alphabetically.
- **Ranks must be unique** (use `ROW_NUMBER`, not `RANK` or `DENSE_RANK`).

Return:
- `from_user`
- `total_email`
- `rn` (activity rank)

---

### Table Schema: `google_gmail_emails`

| Column   | Type   |
|----------|--------|
| id       | bigint |
| from_user | text  |
| to_user   | text  |
| day       | bigint |

---

### SQL Solution

```sql
SELECT 
  from_user, 
  COUNT(*) AS total_email, 
  ROW_NUMBER() OVER(ORDER BY COUNT(*) DESC, from_user ASC) AS rn 
FROM google_gmail_emails
GROUP BY from_user
ORDER BY total_email DESC, from_user;
```

---

### What I Learned

This is a great example of using `R
