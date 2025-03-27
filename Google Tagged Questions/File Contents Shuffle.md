## File Contents Shuffle

**Problem ID:** 9818  
**Tags:** Google, Hard  

---

### Problem Summary

We’re working with the `google_file_store` table, which includes filenames and their contents. The task is:
> For the file `final.txt`, alphabetically sort all the words, lowercase them, and output the results under a new file name: `wacky.txt`.

Return two columns:
- `filename` = `'wacky.txt'`
- `contents` = alphabetically sorted word string (space-separated)

Punctuation does **not** need to be removed.

---

### Table Schema: `google_file_store`

| Column   | Type    |
|----------|---------|
| filename | varchar |
| contents | varchar |

---

### My Thought Process

1. Filter for `filename = 'final.txt'`.
2. Use `STRING_SPLIT()` to break the content into individual words.
3. Convert each word to lowercase.
4. Use `STRING_AGG()` to reassemble the words, ordered alphabetically.

---

### SQL Solution

```sql
WITH cte AS (
  SELECT LOWER(value) AS value
  FROM google_file_store
  CROSS APPLY STRING_SPLIT(contents, ' ')
  WHERE filename = 'final.txt'
)

SELECT 'wacky.txt' AS filename,
       STRING_AGG(value, ' ') WITHIN GROUP (ORDER BY value) AS contents
FROM cte;
```

---

### What I Learned

This is a great example of using string manipulation, sorting, and aggregation in SQL to simulate a file transformation — useful in content pipelines and text processing.

---

### Tags
`#SQL` `#TextTransformation` `#AlphabeticalSort` `#FileRename` `#InterviewPrep
