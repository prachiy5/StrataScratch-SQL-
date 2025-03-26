## Old and Young Athletes Ratio by Olympic Games

**Problem ID:** 9599  
**Tags:** ESPN, Google, Medium  


---

### Problem Summary

We’re given a table called `olympics_athletes_events` with information about Olympic athletes.
Each row includes:
- athlete name
- age
- the Olympic games they competed in

We are asked to:
> For each Olympic games, calculate:
> 1. Number of **old athletes** (age 50 or older)
> 2. Number of **young athletes** (age 25 or younger)
> 3. The **ratio of old to young athletes**

---

### Table Schema: `olympics_athletes_events`

| Column   | Type   |
|----------|--------|
| id       | bigint |
| name     | text   |
| sex      | text   |
| age      | double |
| height   | double |
| weight   | double |
| team     | text   |
| noc      | text   |
| games    | text   |
| year     | bigint |
| season   | text   |
| city     | text   |
| sport    | text   |
| event    | text   |
| medal    | text   |

---

### My Thought Process

1. First, group the data by both `games` and `name` to avoid counting the same athlete multiple times.
2. For each record, mark if the athlete is old (>= 50) or young (<= 25).
3. Then sum the total old and young athletes per Olympic game.
4. Finally, calculate the ratio of old to young athletes for each game.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT games, 
           CASE WHEN age <= 25 THEN 1 ELSE 0 END AS total_young, 
           CASE WHEN age >= 50 THEN 1 ELSE 0 END AS total_old
    FROM olympics_athletes_events 
    GROUP BY games, name
)

SELECT games,
       SUM(total_old) AS old_athletes,
       SUM(total_young) AS young_athletes,
       SUM(total_old) * 1.0 / NULLIF(SUM(total_young), 0) AS old_to_young_ratio
FROM cte
GROUP BY games;
```

---

### What I Learned

This query demonstrates how to use conditional logic with `CASE`, apply grouping to avoid duplicates, and safely calculate ratios using `NULLIF` to prevent division by zero.

---

### Tags
`#SQL` `#Olympics` `#AgeAnalysis` `#RatioCalculation` `#InterviewPrep`
