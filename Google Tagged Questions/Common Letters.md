## Common Letters

**Problem ID:** 9823  
**Tags:** Google, Hard  


---

### Problem Summary

We are given two tables: `google_file_store` and `google_word_lists`. Each contains textual data. The task is:
> Find the **top 3 most common letters** across all text fields, excluding the `filename` column. 

Return:
- `firstChar`: the letter
- `count`: number of times it appeared

Order by highest frequency, and return all ties.

---

### Table Schemas

**google_file_store**
| Column   | Type    |
|----------|---------|
| contents | varchar |
| filename | varchar |

**google_word_lists**
| Column | Type    |
|--------|---------|
| words1 | varchar |
| words2 | varchar |

---

### My Thought Process

1. Combine all relevant textual content from both tables.
2. Use a recursive CTE to extract each letter one by one.
3. Filter out nulls and spaces.
4. Count the occurrences of each character.
5. Sort the counts in descending order and return the top 3 (with ties).

---

### SQL Solution

```sql
WITH cte AS (
    SELECT contents AS word FROM google_file_store
    UNION ALL
    SELECT CONCAT(words1, ',', words2) AS word FROM google_word_lists
),

recursive_cte AS (
    SELECT 1 AS initial_count,
           word,
           SUBSTRING(word, 1, 1) AS firstChar
    FROM cte

    UNION ALL

    SELECT initial_count + 1,
           word,
           SUBSTRING(word, initial_count + 1, 1) AS firstChar
    FROM recursive_cte
    WHERE initial_count < LEN(word)
)

SELECT TOP 3 WITH TIES
    firstChar,
    COUNT(*) AS occurrences
FROM recursive_cte
WHERE firstChar IS NOT NULL AND firstChar != ' '
GROUP BY firstChar
ORDER BY occurrences DESC
OPTION (MAXRECURSION 25836);
```

---

### What I Learned

This query is a great example of recursive CTEs used for character-level parsing, which can be powerful for text mining and frequency analysis in SQL.

---

### Tags
`#SQL` `#StringParsing` `#RecursiveCTE` `#LetterFrequency` `#InterviewPrep`
