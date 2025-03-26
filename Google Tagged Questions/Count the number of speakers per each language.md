## Count the Number of Speakers Per Each Language

**Problem ID:** 9669  
**Tags:** Google, Easy  

---

### Problem Summary

We’re given a table `playbook_users` that contains user data, including the language each user speaks.

The task is:
> Count how many **unique users** speak each language, and then **sort** the results by the number of users in **descending order**.

---

### Table Schema: `playbook_users`

| Column        | Type      |
|----------------|-----------|
| user_id        | bigint    |
| created_at     | timestamp |
| company_id     | bigint    |
| language       | text      |
| activated_at   | datetime  |
| state          | text      |

---

### My Thought Process

1. Group the data by `language`.
2. Count the number of **distinct** `user_id`s for each language.
3. Order the result by the count in descending order.

---

### SQL Solution

```sql
SELECT language,
       COUNT(DISTINCT user_id) AS num_speakers
FROM playbook_users
GROUP BY language
ORDER BY num_speakers DESC;
```

---

### What I Learned

This query shows a standard way to summarize categorical data and rank it by volume — something very useful for reporting and dashboards.

---

### Tags
`#SQL` `#LanguageStats` `#GroupBy` `#OrderBy` `#InterviewPrep
