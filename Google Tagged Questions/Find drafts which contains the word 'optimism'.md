## Find Drafts Which Contain the Word 'Optimism'

**Problem ID:** 9805  
**Tags:** Google, Easy  

---

### Problem Summary

We’re working with a table `google_file_store` that stores filenames and file contents. The task is:
> Find all **draft files** that contain the word **'optimism'**.

Return both:
- The `filename`
- The `contents` of the file

---

### Table Schema: `google_file_store`

| Column    | Type |
|-----------|------|
| filename  | text |
| contents  | text |

---

### My Thought Process

1. Check if the `filename` includes the word "draft" (case-insensitive assumed).
2. Use `LIKE '% optimism %'` to find instances where 'optimism' appears as a word (with spaces around it).
3. Use `DISTINCT` to remove duplicates (if any).

---

### SQL Solution

```sql
SELECT DISTINCT filename, contents
FROM google_file_store
WHERE contents LIKE '% optimism %'
  AND filename LIKE '%draft%';
```

---

### What I Learned

This is a simple but effective use of SQL string pattern matching. It helps you search within document archives, logs, or content repositories.

---

### Tags
`#SQL` `#StringSearch` `#Drafts` `#TextFilter` `#InterviewPrep`
