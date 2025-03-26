## Find All Users That Have More Than 3 Friends

**Problem ID:** 9810  
**Tags:** Google, Medium  

---

### Problem Summary

We are working with a social network dataset that tracks friendships between users. The task is:
> Find all users who have **more than 3 friends**.

---

### Table Schema: `google_friends_network`

| Column    | Type   |
|-----------|--------|
| user_id   | bigint |
| friend_id | bigint |

---

### My Thought Process

1. Since friendships are **bidirectional**, we use a `UNION ALL` to create symmetric entries (so both A→B and B→A are considered).
2. Group by `user_id` and count how many friends they have.
3. Filter to return only those users who have more than 3 friends.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT user_id, friend_id FROM google_friends_network
    UNION ALL
    SELECT friend_id AS user_id, user_id AS friend_id FROM google_friends_network
)

SELECT user_id
FROM cte
GROUP BY user_id
HAVING COUNT(friend_id) > 3;
```

---

### What I Learned

This query demonstrates how to model **undirected relationships** in SQL and properly count mutual connections.

---

### Tags
`#SQL` `#SocialGraph` `#UserConnections` `#BidirectionalJoin` `#InterviewPrep
