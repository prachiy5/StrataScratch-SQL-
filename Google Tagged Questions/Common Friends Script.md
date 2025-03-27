## Common Friends Between Karl and Hans

**Problem ID:** 10365  
**Tags:** Google, Medium  

---

### Problem Summary

Find **mutual friends** between **Karl** and **Hans** in a social network dataset. 

Return:
- `user_id`
- `user_name` (of the mutual friends)

Assumption: There is only **one Karl** and **one Hans** in the `users` table.

---

### Table Schemas

**users**
| Column     | Type   |
|------------|--------|
| user_id    | bigint |
| user_name  | text   |

**friends**
| Column     | Type   |
|------------|--------|
| user_id    | bigint |
| friend_id  | bigint |

---

### SQL Solution

```sql
WITH karl_friends AS (
  SELECT friend_id 
  FROM friends
  WHERE user_id IN (
    SELECT user_id FROM users WHERE user_name = 'Karl')
),

hans_friends AS (
  SELECT friend_id 
  FROM friends
  WHERE user_id
