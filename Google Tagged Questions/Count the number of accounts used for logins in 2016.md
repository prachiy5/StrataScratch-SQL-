## Count the Number of Accounts Used for Logins in 2016

**Problem ID:** 9649  
**Tags:** Apple, Google, Easy  


---

### Problem Summary

We’re given a table called `product_logins`, which tracks user login activity. It includes:
- `account_id`: the ID of the account that logged in
- `employer_key`: some identifier for the employer
- `login_date`: the timestamp of when the login happened

The question is:
> How many accounts **performed a login in 2016**?

---

### Table Schema: `product_logins`

| Column        | Type     |
|----------------|----------|
| account_id     | bigint   |
| employer_key   | text     |
| login_date     | datetime |

---

### My Thought Process

1. Filter rows where `login_date` is in the year 2016.
2. Count the number of matching `account_id`s.
3. Depending on the question intent, you could count distinct accounts — but since that’s not specified, we assume simple count.

---

### SQL Solution

```sql
SELECT COUNT(account_id)
FROM product_logins
WHERE YEAR(login_date) = 2016;
```

---

### What I Learned

This question helps reinforce how to filter by date using the `YEAR()` function. It’s a common use case in time-based reporting.

---

### Tags
`#SQL` `#LoginData` `#DateFiltering` `#YearFunction` `#InterviewPrep
