## First Record Without LIMIT or ORDER BY

**Problem ID:** 9863  
**Tags:** Google, Amazon, Easy  


---

### Problem Summary

We are working with the `worker` table. The task is:
> Return the **first record** based on `worker_id`, **without using LIMIT or ORDER BY**.

This assumes that **lower `worker_id`s are earlier employees**.

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

1. Since `worker_id` increases over time, the first record is the one with the **minimum `worker_id`**.
2. Use a `WHERE` clause to filter for that minimum value.

---

### SQL Solution

```sql
SELECT *
FROM worker
WHERE worker_id = (
    SELECT MIN(worker_id)
    FROM worker
);
```

---

### What I Learned

This mirrors the approach for finding the last record, using `MIN()` instead of `MAX()`. Useful when `ORDER BY` or `LIMIT` is restricted.

---

### Tags
`#SQL` `#MinFunction` `#RowSelection` `#FirstRecord` `#InterviewPrep`
