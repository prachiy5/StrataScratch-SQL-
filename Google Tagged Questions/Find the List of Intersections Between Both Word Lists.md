## Find the List of Intersections Between Both Word Lists

**Problem ID:** 9816  
**Tags:** Google, Hard  

---

### Problem Summary

We’re working with the `google_word_lists` table that contains two columns `words1` and `words2`. Each column contains comma-separated word lists. The task is:
> Extract and return the **intersection of words** that appear in **both lists**.

---

### Table Schema: `google_word_lists`

| Column  | Type |
|---------|------|
| words1  | text |
| words2  | text |

---

### My Thought Process

1. The words are not split into individual rows, so we first need to **split them** using a recursive approach or `substring_index()` logic.
2. Use a **number generator** to simulate string splitting.
3. Extract individual words from both `words1` and `words2` columns into separate lists (`w1`, `w2`).
4. Use a `SELECT ... WHERE IN` to return words that exist in both lists.

---

### SQL Solution

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS n
    UNION 
    SELECT n + 1 FROM numbers WHERE n <= 10
),

w1 AS (
    SELECT DISTINCT SUBSTRING_INDEX(SUBSTRING_INDEX(words1, ',', n), ',', -1) AS wd1
    FROM google_word_lists
    CROSS JOIN numbers
    WHERE n <= (LENGTH(words1) - LENGTH(REPLACE(words1, ',', '')) + 1)
),

w2 AS (
    SELECT DISTINCT SUBSTRING_INDEX(SUBSTRING_INDEX(words2, ',', n), ',', -1) AS wd2
    FROM google_word_lists
    CROSS JOIN numbers
    WHERE n <= (LENGTH(words2) - LENGTH(REPLACE(words2, ',', '')) + 1)
)

SELECT wd1
FROM w1
WHERE wd1 IN (SELECT wd2 FROM w2);
```

---

### What I Learned

This solution demonstrates how to break down delimited values in SQL and perform set-based logic to compare and intersect lists.

---

### Tags
`#SQL` `#StringSplit` `#RecursiveCTE` `#WordLists` `#InterviewPrep
