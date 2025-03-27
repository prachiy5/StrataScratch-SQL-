## Number of Speakers by Language and Country

**Problem ID:** 10139  
**Tags:** Apple, Google, Medium  

---

### Problem Summary

Find how many **distinct users** speak each language **in each country** (represented by location).

Return:
- `location`
- `language`
- number of distinct users per (location, language) pair

Sort the result by location in ascending order.

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
  location, 
  language, 
  COUNT(DISTINCT pe.user_id) AS num_speakers
FROM playbook_events pe
INNER JOIN playbook_users pu
  ON pe.user_id = pu.user_id
GROUP BY location, language
ORDER BY location;
```

---

### What I Learned

This is a common pattern for user demographic analysis across regions. It's also a good exercise in combining user metadata with interaction data to form insights.

---

### Tags
`#SQL` `#UserDemographics` `#SpeakersByCountry` `#JoinAndGroup` `#InterviewPrep
