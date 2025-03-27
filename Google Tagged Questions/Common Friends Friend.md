## Common Friends Friend

**Problem ID:** 9821  
**Tags:** Google, Hard  

---

### Problem Summary

We're working with the `google_friends_network` table. Each row indicates a friendship between two users. The task is:
> For each user, count how many of their **friends-of-friends** are **also their direct friends**.

Return:
- `user_id`
- `n_direct`: number of friends' friends who are also the user’s direct friends

---

### Table Schema: `google_friends_network`

| Column    | Type   |
|-----------|--------|
| user_id   | bigint |
| friend_id | bigint |

---

### My Thought Process

1. Make the friendship bidirectional using `UNION ALL`.
2. For each user, find their **friends' friends**.
3. Join the result again with the original network to check if those friends-of-friends are also direct friends.
4. Count the number of such overlaps per user.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT user_id, friend_id FROM google_friends_network
    UNION ALL
    SELECT friend_id, user_id FROM google_friends_network
),

friends_of_friends AS (
    SELECT c1.user_id, c2.friend_id AS fof
    FROM cte c1
    INNER JOIN cte c2
        ON c1.friend_id = c2.user_id
       AND c1.user_id != c2.friend_id
)

SELECT c.user_id, COUNT(DISTINCT fof) AS n_direct
FROM friends_of_friends fof
INNER JOIN cte c
    ON fof.user_id = c.user_id AND fof.fof = c.friend_id
GROUP BY c.user_id;
```

---

### What I Learned

This query is a perfect example of social network analysis using self-joins. It identifies shared connections between users and their broader friend networks.

---

### Tags
`#SQL` `#GraphAnalysis` `#FriendsOfFriends` `#SelfJoin` `#SocialNetwork` `#InterviewPrep`
