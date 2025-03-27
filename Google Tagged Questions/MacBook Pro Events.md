## MacBook Pro Events by Non-Spanish Speakers in Argentina

**Problem ID:** 10140  
**Tags:** Apple, Google, Medium  

---

### Problem Summary

We want to count how many **events** were performed **on MacBook Pro** devices **in Argentina** by users who **do not speak Spanish**.

Return:
- `company_id`
- `language` (non-Spanish only)
- number of events performed by those users

---

### Table Schemas

**playbook_events**
| Column       | Type      |
|--------------|-----------|
| user_id      | bigint    |
| occurred_at  | timestamp |
| event_type   | text      |
| event_name   | text      |
| location     | text      |
| device       | text      |

**playbook_users**
| Column       | Type      |
|--------------|-----------|
| user_id      | bigint    |
| created_at   | timestamp |
| company_id   | bigint    |
| language     | text      |
| activated_at | datetime  |
| state        | text      |

---

### SQL Solution

```sql
SELECT 
  company_id, 
  language, 
  COUNT(event_name) AS num_events
FROM playbook_events pe
INNER JOIN playbook_users pu
  ON pe.user_id = pu.user_id
WHERE language != 'spanish'
  AND location = 'Argentina'
  AND device = 'macbook pro'
GROUP BY company_id, language;
```

---

### What I Learned

This query combines multiple filtering conditions across two datasets to pinpoint highly specific user activity segments. Great for device- or region-specific behavioral analytics.

---

### Tags
`#SQL` `#DeviceAnalytics` `#MacBookPro` `#Argentina` `#NonSpanishSpeakers` `#EventTracking` `#InterviewPrep`
