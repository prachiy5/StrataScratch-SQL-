## LeetCode SQL Easy – Active Users Per Platform

**Problem ID:** 2072  
**Tags:** Google, Apple, Easy  


---

### Problem Summary

We have a table called `user_sessions` that keeps track of when users open the app. Each row in the table tells us:

- Which session it was (`session_id`)
- Who the user was (`user_id`)
- When they started and ended the session
- Which device or platform they were using (like iPhone, Windows, iPad, etc.)

Now we want to answer a simple question:
> For each platform, how many **different users** used the app?

We don’t care how many sessions they had — we just want to count each user **once per platform**.

---

###  Table Schema: `user_sessions`

| Column            | Type      |
|-------------------|-----------|
| session_id        | bigint    |
| user_id           | text      |
| session_starttime | timestamp |
| session_endtime   | timestamp |
| platform          | text      |

---

###  My Thought Process (Explained Simply)

This one is super easy:

1. We want to know the number of **unique users** per platform.
2. So, we group the data by `platform`.
3. And then we just count how many **distinct `user_id`s** there are for each platform.

---

###  SQL Solution

```sql
SELECT platform, 
       COUNT(DISTINCT user_id) AS user_count
FROM user_sessions
GROUP BY platform;
```

---

### What I Learned

Even basic SQL queries like this are super useful. A lot of real-world questions are just about counting things the right way. In this case, we made sure not to count repeat sessions — just the number of real users per device.

---

###  Tags
`#SQL` `#Easy` `#UserAnalytics` `#UniqueUsers` `#PlatformAnalysis` `#InterviewPrep`
