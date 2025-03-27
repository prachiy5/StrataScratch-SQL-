## Total Employees in Each Department

**Problem ID:** 9861  
**Tags:** Apple, Google, Amazon, Easy  

---

### Problem Summary

We are working with the `worker` table which contains employee information. The task is:
> Count the number of employees in each department.

Return:
- `department`
- number of employees in each

---

### Table Schema: `worker`

| Column        | Type      |
|---------------|-----------|
| department    | varchar   |
| first_name    | varchar   |
| last_name     | varchar   |
| joining_date  | datetime2 |
| salary        | bigint    |
| worker_id     | bigint    |

---

### My Thought Process

1. Count each unique `worker_id` grouped by the `department` column.
2. Use `GROUP BY` and `COUNT()` to compute the result.

---

### SQL Solution

```sql
SELECT department, COUNT(worker_id) AS total_employees
FROM worker
GROUP BY department;
```

---

### What I Learned

This is a basic SQL aggregation task — useful for HR analytics and departmental staffing summaries.

---

### Tags
`#SQL` `#EmployeeCount` `#GroupBy` `#HRAnalytics` `#InterviewPrep`
