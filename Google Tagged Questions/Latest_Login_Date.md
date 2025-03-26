## Latest Login Date

**Problem ID:** 2091  
**Tags:** Google, Amazon, Easy  

---

### Problem Summary

We have a table called `players_logins`.
Each row tells us:
- the player ID (`player_id`)
- and the date they logged in (`login_date`).

Our task is simple:
> For every player, find the **most recent date** they logged in.

---

### Table Schema: `players_logins`

| Column     | Type     |
|------------|----------|
| player_id  | bigint   |
| login_date | datetime |

---

### My Thought Process (in a simple way)

1. We want to look at each player.
2. And then just find the latest login date for that player.
3. This means we will group the table by `player_id`.
4. And then get the maximum value of `login_date`.

---

### SQL Solution

```sql
SELECT player_id,
       MAX(login_date) AS latest_login
FROM players_logins
GROUP BY player_id;
```

---

### What I Learned

Sometimes problems are really just about reading the question carefully.
This one is about using `GROUP BY` and `MAX()` to get the latest date per person.
Very simple, but a common real-world thing you’ll be asked to do in SQL.

---

### Tags
`#SQL` `#Easy` `#LoginTracking` `#MAXFunction` `#GroupBy` `#InterviewPrep
