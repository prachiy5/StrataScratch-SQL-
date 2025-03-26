##  StrataScratch SQL Hard – Player with Longest Streak

**Problem ID:** 2059  
**Tags:** Google, Amazon, Hard    
---

###  Problem Summary

We’re given a table `players_results` that tracks tennis matches for players. Each row contains:

- `player_id`: ID of the player  
- `match_date`: Date of the match  
- `match_result`: Either `'W'` (win) or `'L'` (loss)  

Our goal is to find the **longest consecutive winning streak** for each player. A streak ends when the player **loses** a match. The output should be the **player(s)** with the **longest streak** and the corresponding **streak length**.

---

### 📊 Table Schema: `players_results`

| Column       | Type     |
|--------------|----------|
| player_id    | bigint   |
| match_date   | datetime |
| match_result | text     |

---

###  My Thought Process

To solve this, I approached it like a typical **"group consecutive values"** problem using the **difference of row numbers** trick.

####  Step-by-step logic:

1. **Sort matches** for each player by date and assign two row numbers:
   - `rn`: Incrementing row number by date for each player.
   - `rn2`: Incrementing row number by date **only for wins** (`'W'`).

2. **Subtracting `rn - rn2`**:
   - For a sequence of consecutive wins, this difference will be constant.  
   - This helps us **group the streaks** together.

3. **Filter for only `'W'` matches**, compute the streak group (`anchor`) as `rn - rn2`.

4. **Group by player and streak group**, and **count the wins** to get streak length.

5. **Use `DENSE_RANK()`** to find the **maximum streak(s)** across all players.

---

###  SQL Solution

```sql
WITH cte AS (
    SELECT *, 
           ROW_NUMBER() OVER(PARTITION BY player_id ORDER BY match_date) AS rn,
           ROW_NUMBER() OVER(PARTITION BY player_id, match_result ORDER BY match_date) AS rn2
    FROM players_results
),

cte2 AS (
    SELECT *, 
           rn - rn2 AS anchor
    FROM cte
    WHERE match_result = 'W'
),

cte3 AS (
    SELECT player_id, 
           COUNT(*) AS num_wins,
           DENSE_RANK() OVER(ORDER BY COUNT(*) DESC) AS dr
    FROM cte2
    GROUP BY player_id, anchor
)

SELECT player_id, num_wins
FROM cte3
WHERE dr = 1;
```

---

###  Explanation of Key Parts

- `rn - rn2` groups consecutive wins together.
- `COUNT(*)` gives us the length of each winning streak.
- `DENSE_RANK()` identifies the **top streak(s)**.

---


###  What I Learned

This was a great exercise in:
- Applying **window functions** like `ROW_NUMBER()`.
- Using the **“row number difference” technique** to group consecutive sequences.
- Combining `DENSE_RANK()` to get the top-N results in SQL.

---

###  Tags
`#SQL` `#WindowFunctions` `#LeetCodeHard` `#DataAnalytics` `#StreakDetection` `#Tennis` `#ConsecutiveWins` `#InterviewPrep`

