## Find All Records With Words That Start With the Letter 'G'

**Problem ID:** 9806  
**Tags:** Google, Easy  

---

### Problem Summary

We are working with a table `google_word_lists` that contains two columns (`words1`, `words2`) with lists of comma-separated words. The task is:
> Return all rows where **any word** in either column **starts with the letter 'g'**.

---

### Table Schema: `google_word_lists`

| Column  | Type |
|---------|------|
| words1  | text |
| words2  | text |

---

### My Thought Process

1. Since the words are comma-separated, we can't use standard equality.
2. We use `LIKE` to detect:
   - Words that **start the string** with `g` → `'g%'`
   - Words that appear **after a comma** and start with `g` → `'%,g%'`
3. We apply this logic to both `words1` and `words2`.

---

### SQL Solution

```sql
SELECT
    words1,
    words2
FROM
    google_word_lists
WHERE
    (words1 LIKE 'g%' OR words1 LIKE '%,g%') OR 
    (words2 LIKE 'g%' OR words2 LIKE '%,g%');
```

---

### What I Learned

This problem shows how you can scan for patterns inside comma-separated text columns, even if the column isn’t properly normalized.

---

### Tags
`#SQL` `#StringMatching` `#LikeClause` `#TextFilter` `#InterviewPrep`
