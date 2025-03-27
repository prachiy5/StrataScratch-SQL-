## Last Record Without LIMIT or ORDER BY

**Problem ID:** 9862  
**Tags:** Google, Amazon, Easy  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer  


---

### Problem Summary

We are working with the `worker` table. The task is:
> Return the **last record** based on `worker_id`, **without using LIMIT or ORDER BY**.

This assumes that **higher `worker_id`s are newer employees**.

---

### Table Schema: `worker`

| Column       | Type     |
|--------------|----------|
| worker_id    | bigint   |
| first_name   | text     |
| last_name    | text     |
| salary       | bigint   |
| joining_date | datetime |
| department   | text     |

---

### My Thought Process

1. Since `worker_id` increases over time, the last record is the one with the **maximum `worker_id`**.
2. Use a `WHERE` clause to filter for that maximum value.

---

### SQL Solution

```sql
SELECT *
FROM worker
WHERE worker_id = (
    SELECT MAX(worker_id)
    FROM worker
);
```

---

### What I Learned

This is a helpful way to retrieve the most recent record when you're not allowed to use `ORDER BY` or `LIMIT`.

---

### Tags
`#SQL` `#MaxFunction` `#RowSelection` `#LatestRecord` `#InterviewPrep`
