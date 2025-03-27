## Number of Custom Email Labels per User

**Problem ID:** 10120  
**Tags:** Google, Medium  

---

### Problem Summary

Find the **number of occurrences** of **custom email labels** for each user who received an email.

Return:
- `to_user` (recipient)
- `label` (must include the word 'Custom')
- `n_occurrences` (number of emails with that label received by that user)

---

### Tables

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
SELECT 
  to_user, 
  label, 
  COUNT(*) AS n_occurences
FROM google_gmail_emails ge
INNER JOIN google_gmail_labels gl
  ON ge.id = gl.email_id
WHERE label LIKE '%Custom%'
GROUP BY to_user, label;
```

---

### What I Learned

This problem demonstrates how to combine filtering and aggregation across joined datasets — a common scenario in product analytics and email systems.

---

### Tags
`#SQL` `#CustomLabels` `#Gmail` `#LabelTracking` `#JoinAndGroup` `#InterviewPrep`
