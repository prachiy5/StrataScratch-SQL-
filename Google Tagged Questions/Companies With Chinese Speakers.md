## Companies With Chinese Speakers

**Problem ID:** 9685  
**Tags:** Google, Easy  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer  
**Last Updated:** August 2024  

---

### Problem Summary

We’re working with the `playbook_users` table. The goal is:
> Find all companies that have **at least 2 users** who speak **Chinese**.

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

1. Filter for users who speak Chinese.
2. Group the result by `company_id`.
3. Count unique users per company.
4. Only return companies where the count is 2 or more.

---

### SQL Solution

```sql
SELECT company_id
FROM playbook_users
WHERE language = 'chinese'
GROUP BY company_id
HAVING COUNT(DISTINCT user_id) >= 2;
```

---

### What I Learned

This type of query is useful when determining thresholds or usage levels per group. It's especially relevant in multi-tenant applications where usage per client/company is tracked.

---

### Tags
`#SQL` `#ChineseLanguage` `#UserGrouping` `#CompanyFilter` `#InterviewPrep`
