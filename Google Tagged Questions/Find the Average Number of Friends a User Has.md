## Find the Average Number of Friends a User Has

**Problem ID:** 9822  
**Tags:** Google, Hard  

---

### Problem Summary

We are working with a table that contains pairs of users and their friends. The task is:
> Calculate the **average number of friends** per user.

---

### Table Schema: `google_friends_network`

| Column    | Type   |
|-----------|--------|
| user_id   | bigint |
| friend_id | bigint |

---

### My Thought Process

1. Friendships are bidirectional, but the table might only store one direction (e.g., A→B).
2. Use a `UNION ALL` to ensure both directions are included.
3. Count the number of friends each user has.
4. Take the average of those friend counts.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT * FROM google_friends_network
    UNION ALL
    SELECT friend_id, user_id FROM google_friends_network
),

cte2 AS (
    SELECT user_id, COUNT(friend_id) AS total_friends
    FROM cte
    GROUP BY user_id
)

SELECT 1.0 * SUM(total_friends) / COUNT(total_friends) AS avg_friends
FROM cte2;
```

---

### What I Learned

This query is a great example of using symmetric relationships and aggregate functions to get meaningful network-level insights.

---

### Tags
`#SQL` `#AverageFriends` `#SocialNetwork` `#Aggregation` `#InterviewPrep
