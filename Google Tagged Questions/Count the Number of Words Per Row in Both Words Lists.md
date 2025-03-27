## Count the Number of Words Per Row in Both Words Lists

**Problem ID:** 9812  
**Tags:** Google, Medium  


---

### Problem Summary

We are working with the `google_word_lists` table which contains two columns `words1` and `words2`, each containing comma-separated words.

Our task is:
> Count how many total words there are in **each row**, combining both `words1` and `words2`.

---

### Table Schema: `google_word_lists`

| Column  | Type |
|---------|------|
| words1  | text |
| words2  | text |

---

### My Thought Process

1. Combine `words1` and `words2` into a single comma-separated string.
2. Count how many commas are present using:
   - `LENGTH(words) - LENGTH(REPLACE(words, ',', ''))`
3. Since the number of words is always **1 more than the number of commas**, add 1 to the result.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT CONCAT(words1, ',', words2) AS words
    FROM google_word_lists
)

SELECT LENGTH(words) - LENGTH(REPLACE(words, ',', '')) + 1 AS n_words
FROM cte;
```

---

### What I Learned

This is a clean technique to count items in a comma-separated string using basic string functions — useful when working with improperly normalized data.

---

### Tags
`#SQL` `#StringFunctions` `#WordLists` `#CommaSeparated` `#InterviewPrep
