## Find Business Types Present in the Dataset

**Problem ID:** 9808  
**Tags:** Google, Easy  


---

### Problem Summary

We are working with the `google_adwords_earnings` table, which contains company advertising and workforce data. The task is:
> Find all **unique business types** that are present in the dataset.

---

### Table Schema: `google_adwords_earnings`

| Column           | Type   |
|------------------|--------|
| business_type    | text   |
| n_employees      | bigint |
| year             | bigint |
| adwords_earnings | bigint |

---

### My Thought Process

1. Use `DISTINCT` to get a list of unique values in the `business_type` column.
2. This will return one row per business type.

---

### SQL Solution

```sql
SELECT DISTINCT business_type
FROM google_adwords_earnings;
```

---

### What I Learned

This is a simple and useful way to explore categorical values in a dataset, especially useful for grouping, filtering, or creating dashboard filters.

---

### Tags
`#SQL` `#BusinessTypes` `#AdwordsData` `#ExploratoryAnalysis` `#InterviewPrep`
