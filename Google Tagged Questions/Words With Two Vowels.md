## Words With Two Vowels

**Problem ID:** 9794  
**Tags:** Google, Hard  

---

### Problem Summary

We’re given a table called `google_word_lists` that contains lists of words in two columns: `words1` and `words2`. These columns store comma-separated words.

Our goal is:
> Find all **distinct words** from either column that contain **exactly 2 vowels**.

---

### Table Schema: `google_word_lists`

| Column  | Type |
|---------|------|
| words1  | text |
| words2  | text |

---

### My Thought Process

1. Combine `words1` and `words2` into a single string per row.
2. Use `STRING_SPLIT()` to break the combined string into individual words.
3. Convert each word to lowercase and count the total number of vowels (a, e, i, o, u).
4. Filter words where the total vowel count equals exactly 2.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT CONCAT(words1, ',', words2) AS words
    FROM google_word_lists
),

cte2 AS (
    SELECT value
    FROM cte
    CROSS APPLY STRING_SPLIT(words, ',')
)

SELECT DISTINCT value
FROM cte2
WHERE (
    LEN(value) - LEN(REPLACE(LOWER(value), 'a', '')) +
    LEN(value) - LEN(REPLACE(LOWER(value), 'e', '')) +
    LEN(value) - LEN(REPLACE(LOWER(value), 'i', '')) +
    LEN(value) - LEN(REPLACE(LOWER(value), 'o', '')) +
    LEN(value) - LEN(REPLACE(LOWER(value), 'u', ''))
) = 2;
```

---

### What I Learned

This query is a great example of:
- Text parsing from delimited lists
- Using string manipulation to count characters
- Solving character-level pattern problems with SQL

---

### Tags
`#SQL` `#StringManipulation` `#VowelCount` `#TextProcessing` `#InterviewPrep
