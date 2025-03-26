## Count Users That Speak English, German, French, or Spanish

**Problem ID:** 9667  
**Tags:** Google, Easy  

---

### Problem Summary

We are given a table called `playbook_users`, which includes information about users and their preferred language. The task is:
> Count how many **unique users** speak **English, German, French, or Spanish**.

Important:
- If a user speaks more than one of these languages, they should be counted **only once**.

---

### Table Schema: `playbook_users`

| Column      | Type      |
|-------------|-----------|
| user_id     | bigint    |
| created_at  | timestamp |
| company_id  | bigint    |
| language    | text      |
| activated_at| datetime  |
| state       | text      |

---

### My Thought Process

1. Filter the data to only include users who speak one of the four specified languages.
2. Count the number of **distinct user IDs** that meet this condition.

---

### SQL Solution

```sql
SELECT COUNT(DISTINCT user_id)
FROM playbook_users
WHERE language IN ('english', 'german', 'french', 'spanish');
```

---

### What I Learned

This is a great example of how simple filtering and deduplication (`DISTINCT`) can be used to answer real-world business questions about user demographics.

---

### Tags
`#SQL` `#Filtering` `#UserLanguages` `#DistinctCount` `#InterviewPrep`
