## Salary by Education

**Problem ID:** 2100  
**Tags:** Google, Easy  

---

### Problem Summary

We have a table called `google_salaries`. It has information about different people who work at Google — including their salary and education level.

The goal is simple:
> Find the **average salary** for each **education level**.

---

### Table Schema: `google_salaries`

| Column      | Type   |
|-------------|--------|
| id          | bigint |
| first_name  | text   |
| last_name   | text   |
| department  | text   |
| education   | text   |
| salary      | bigint |

---

### My Thought Process

1. We want to group the data by the `education` column.
2. Then we just calculate the average of the `salary` for each group.

---

### SQL Solution

```sql
SELECT education, 
       AVG(salary) AS average_salary
FROM google_salaries
GROUP BY education;
```

---

### What I Learned

This is one of the most basic and common types of queries you'll see in analytics: calculating averages by category. It’s useful for understanding patterns or trends, like how salary differs across education levels.

---

### Tags
`#SQL` `#Easy` `#GoogleSalaries` `#GroupBy` `#AverageSalary` `#InterviewPrep`
