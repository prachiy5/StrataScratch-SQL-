## Apple Product Counts by Language

**Problem ID:** 10141  
**Tags:** Apple, Google, Medium  

---

### Problem Summary

We want to measure the **popularity of Apple products** across languages.

Specifically:
- Count how many **distinct users** used any of the following Apple devices:
  - `macbook pro`
  - `iphone 5s`
  - `ipad air`
- Count the total number of distinct users per language (regardless of device)
- Sort by total number of users **descending**

Return:
- `language`
- `n_apple_user`
- `n_total_users`

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
  language, 
  COUNT(DISTINCT CASE 
    WHEN pe.device IN ('macbook pro','iphone 5s','ipad air') THEN pe.user_id
    ELSE NULL 
  END) AS n_apple_user,
  COUNT(DISTINCT pe.user_id) AS n_total_users
FROM playbook_events pe
INNER JOIN playbook_users pu
  ON pe.user_id = pu.user_id
GROUP BY language
ORDER BY n_total_users DESC;
```

---

### What I Learned

This question is a great exercise in combining filtering, aggregation, and conditional logic inside a single query. It also highlights how to break down user behavior by a demographic factor (language).

---

### Tags
`#SQL` `#AppleDevices` `#DeviceUsage` `#UserBehavior` `#LanguageAnalytics` `#InterviewPrep`
