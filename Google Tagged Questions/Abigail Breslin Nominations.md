## Abigail Breslin Oscar Nominations

**Problem ID:** 10128  
**Tags:** Google, Netflix, Easy  

---

### Problem Summary

Count how many **distinct movies** Abigail Breslin was nominated for an **Oscar**.

Return:
- A single count of distinct nominated movies.

---

### Table Schema: `oscar_nominees`

| Column   | Type   |
|----------|--------|
| year     | bigint |
| category | text   |
| nominee  | text   |
| movie    | text   |
| winner   | tinyint|
| id       | bigint |

---

### SQL Solution

```sql
SELECT COUNT(DISTINCT movie)
FROM oscar_nominees
WHERE nominee = 'Abigail Breslin';
```

---

### What I Learned

This is a simple filter-and-count question using `DISTINCT` for deduplication. Great for quick actor/nominee lookup tasks.

---

### Tags
`#SQL` `#OscarNominations` `#MovieAnalytics` `#CountDistinct` `#InterviewPrep`
