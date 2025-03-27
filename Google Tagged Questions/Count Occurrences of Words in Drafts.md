## Count Occurrences of Words in Drafts

**Problem ID:** 9817  
**Tags:** Google, Medium  

---

### Problem Summary

We are working with a dataset of files in the `google_file_store` table. Each row contains a filename and its corresponding textual content. The task is:
> Count how many times **each word** appears across **all drafts**.

Return two columns:
- `word`
- `occurrences`

---

### Table Schema: `google_file_store`

| Column   | Type |
|----------|------|
| filename | text |
| contents | text |

---

### My Thought Process

1. Use `STRING_SPLIT()` to split `contents` by spaces into individual words.
2. Clean up punctuation (e.g., remove commas and periods).
3. Group the results by each word (`value`) and count them.

---

### SQL Solution

```sql
SELECT 
  value, 
  COUNT(*) AS occ
FROM google_file_store
CROSS APPLY STRING_SPLIT(REPLACE(REPLACE(contents, ',', ''), '.', ''), ' ')
GROUP BY value
ORDER BY occ DESC;
```

---

### What I Learned

This is a classic use case of unstructured text processing in SQL. Cleaning text before analysis helps avoid counting variations of the same word (like `hello,` vs `hello`).

---

### Tags
`#SQL` `#TextAnalysis` `#WordFrequency` `#Drafts` `#InterviewPrep
