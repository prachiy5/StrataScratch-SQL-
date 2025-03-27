## Women in the Olympics Before World War 2

**Problem ID:** 9932  
**Tags:** Google, ESPN, Easy  


---

### Problem Summary

Find all **unique female athletes** who participated in the Olympics **before World War 2**.

> Consider the year **1939** as the start of World War II.

Return:
- Unique `name`s of female participants.

---

### Table Schema: `olympics_athletes_events`

| Column | Type   |
|--------|--------|
| id     | bigint |
| name   | text   |
| sex    | text   |
| age    | double |
| height | double |
| weight | double |
| team   | text   |
| noc    | text   |
| games  | text   |
| year   | bigint |
| season | text   |
| city   | text   |
| sport  | text   |
| event  | text   |
| medal  | text   |

---

### SQL Solution

```sql
SELECT DISTINCT name
FROM olympics_athletes_events
WHERE sex = 'F'
  AND year < 1939;
```

---

### What I Learned

This query demonstrates a simple filter and deduplication based on conditions related to gender and historical timeframes. Great for historical or gender-based participation analysis.

---

### Tags
`#SQL` `#Olympics` `#HistoricalData` `#WomenInSports` `#InterviewPrep`
