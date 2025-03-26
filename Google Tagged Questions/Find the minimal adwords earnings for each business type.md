## Find the Minimal AdWords Earnings for Each Business Type

**Problem ID:** 9811  
**Tags:** Google, Medium  
  

---

### Problem Summary

We are analyzing Google AdWords performance data and want to:
> Find the **minimum AdWords earnings** recorded for **each business type**.

Return both:
- The `business_type`
- Its `minimum earnings`

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

1. We want the lowest earnings per business type.
2. `MIN() OVER(PARTITION BY business_type)` gives us that.
3. Use `DISTINCT` to return only one row per business type.

---

### SQL Solution

```sql
SELECT DISTINCT business_type,
       MIN(adwords_earnings) OVER(PARTITION BY business_type) AS min_earning
FROM google_adwords_earnings;
```

---

### What I Learned

Using a window function like `MIN()` with `PARTITION BY` is a handy way to calculate grouped stats while still keeping access to row-level data.

---

### Tags
`#SQL` `#MinFunction` `#GroupStats` `#AdwordsEarnings` `#InterviewPrep`
