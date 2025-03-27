## Make the Friends Network Symmetric

**Problem ID:** 9813  
**Tags:** Google, Medium  

---

### Problem Summary

We are working with the `google_friends_network` table, which records friendships between users. Each row indicates a one-way relationship from `user_id` to `friend_id`.

Our task is:
> Make the **friends network symmetric** — meaning, for every friendship from A to B, we should also include B to A.

---

### Table Schema: `google_friends_network`

| Column    | Type   |
|-----------|--------|
| user_id   | bigint |
| friend_id | bigint |

---

### My Thought Process

1. Use a `UNION` to combine:
   - The original friendships
   - A reversed version of the same data (friend_id becomes user_id and vice versa)
2. `UNION` (not `UNION ALL`) ensures duplicates are automatically removed.

---

### SQL Solution

```sql
SELECT user_id, friend_id
FROM google_friends_network
UNION
SELECT friend_id, user_id
FROM google_friends_network;
```

---

### What I Learned

This approach ensures that each friendship is treated as bidirectional, which is critical in graph-based social network analyses.

---

### Tags
`#SQL` `#GraphData` `#SymmetricRelations` `#Union` `#InterviewPrep
