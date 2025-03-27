## Find How Many Logins Spanish Speakers Made by Country

**Problem ID:** 9889  
**Tags:** Google, Medium  

---

### Problem Summary

Determine how many **logins** were made by **Spanish-speaking users**, grouped by **country (location)**.

Return:
- `location`
- number of login events

Exclude countries with zero logins. Sort results in descending order by number of logins.

---

### Table Schemas

**playbook_users**
| Column      | Type      |
|-------------|-----------|
| user_id     | bigint    |
| language    | text      |
| created_at  | timestamp |
| company_id  | bigint    |
| activated_at| datetime  |
| state       | text      |

**playbook_events**
| Column      | Type      |
|-------------|-----------|
| user_id     | bigint    |
| occurred_at | timestamp |
| event_type  | text      |
| event_name  | text      |
| location    | text      |
| device      | text      |

---

### SQL Solution

```sql
SELECT 
  location, 
  COUNT(event_name) AS n_logins 
FROM playbook_users pu
INNER JOIN playbook_events pe
  ON pu.user_id = pe.user_id
WHERE event_name = 'login' 
  AND language = 'spanish'
GROUP BY location
ORDER BY n_logins DESC;
```

---

### What I Learned

This is a good example of joining user profile data with event logs to extract usage patterns based on language and region.

---

### Tags
`#SQL` `#LoginAnalysis` `#UserBehavior` `#SpanishSpeakers` `#InterviewPrep
