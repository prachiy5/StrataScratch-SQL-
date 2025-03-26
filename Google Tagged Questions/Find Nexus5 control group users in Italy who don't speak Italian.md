## Find Nexus 5 Control Group Users in Italy Who Don't Speak Italian

**Problem ID:** 9609  
**Tags:** Google, Medium  


---

### Problem Summary

We are given two tables:
- `playbook_experiments`: contains experiment data with device, group, location, and time.
- `playbook_users`: contains user info including language.

We need to:
> Find users who:
> - Are in **Italy**
> - Are in the **control group**
> - Use a **Nexus 5**
> - **Do not speak Italian**

Then, we return:
- `user_id`
- `language`
- `location`

Sort the results by the `occurred_at` timestamp (from the experiment table).

---

### Table Schemas

**playbook_experiments**

| Column          | Type     |
|------------------|----------|
| user_id          | text     |
| occurred_at      | datetime |
| location         | text     |
| experiment_group | text     |
| device           | text     |

**playbook_users**

| Column   | Type |
|-----------|------|
| user_id   | text |
| language  | text |

---

### My Thought Process

1. Filter the `playbook_experiments` table for rows where:
   - location is Italy
   - group is control
   - device is Nexus 5
2. Join this filtered list with `playbook_users` on `user_id`.
3. Filter out users whose language is Italian.
4. Return user_id, language, location and sort by `occurred_at`.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT user_id, occurred_at, location
    FROM playbook_experiments
    WHERE location = 'Italy'
      AND experiment_group = 'control_group'
      AND device = 'nexus 5'
)

SELECT pu.user_id, pu.language, c.location
FROM playbook_users pu
JOIN cte c ON c.user_id = pu.user_id
WHERE LOWER(pu.language) != 'italian'
ORDER BY c.occurred_at;
```

---

### What I Learned

This type of task is great for practicing multi-condition filtering, using CTEs for clarity, and ensuring correct joins and sorting.

---

### Tags
`#SQL` `#Filtering` `#Joins` `#ExperimentData` `#Nexus5` `#InterviewPrep`
