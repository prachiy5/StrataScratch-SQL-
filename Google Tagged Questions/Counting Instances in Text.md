## Counting Instances in Text

**Problem ID:** 9814  
**Tags:** Google, Hard  

---

### Problem Summary

We’re working with a table called `google_file_store` which contains file names and textual content. The task is:
> Count how many times the words **'bull'** and **'bear'** appear in the `contents` column.

Note:
- Only count **full word matches**.
- Words like "bullish" or "bearish" **should not** be counted.

---

### Table Schema: `google_file_store`

| Column   | Type |
|----------|------|
| filename | text |
| contents | text |

---

### My Thought Process

1. We want to count rows where `' bull '` or `' bear '` appears.
2. We wrap the words with spaces in the `LIKE` clause to ensure we're only matching full words.
3. Use `SUM(CASE WHEN ... THEN 1 ELSE 0)` to count matches.
4. Use `UNION ALL` to stack the two word counts.

---

### SQL Solution

```sql
SELECT 
  'bull' AS word,
  SUM(CASE WHEN contents LIKE '% bull %' THEN 1 ELSE 0 END) AS nentry
FROM google_file_store

UNION ALL

SELECT 
  'bear' AS word,
  SUM(CASE WHEN contents LIKE '% bear %' THEN 1 ELSE 0 END) AS nentry
FROM google_file_store;
```

---

### What I Learned

This query helps illustrate word boundary filtering using spaces in a `LIKE` clause. It also highlights how SQL can be used to count keyword occurrences at the row level.

---

### Tags
`#SQL` `#TextSearch` `#WordFrequency` `#StringMatching` `#InterviewPrep`
