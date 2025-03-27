## Count Occurrences of Words in Drafts

**Problem ID:** 9817  
**Tags:** Google, Medium  


---

### Problem Summary

We are working with a dataset of files in the `google_file_store` table. Each row contains a filename and its corresponding textual content. The task is:
> Count how many times **each word** appears across **all draft files**.

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

1. Filter only filenames that include "draft".
2. Use `STRING_SPLIT()` to break contents into words.
3. Flatten words across rows using `CROSS APPLY`.
4. Group by each word and count the number of times it appears.

---

### SQL Solution

```sql
SELECT LOWER(value) AS word,
       COUNT(*) AS occurrences
FROM google_file_store
CROSS APPLY STRING_SPLIT(contents, ' ')
WHERE filename LIKE '%draft%'
GROUP BY LOWER(value)
ORDER BY occurrences DESC;
```

---

### What I Learned

This pattern is useful for building word clouds, keyword frequency reports, and other natural language analyses using SQL.

---

### Tags
`#SQL` `#TextProcessing` `#WordFrequency` `#StringSplit` `#DraftAnalysis` `#InterviewPrep
