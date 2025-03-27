## Price Of A Handyman

**Problem ID:** 9815  
**Tags:** Google, Hard  


---

### Problem Summary

We are analyzing AdWords spend data from the `google_adwords_earnings` table. The task is:
> For **handyman businesses** with **10 or fewer employees**, find the **most common (mode)** value of their **AdWords earnings per employee**.

This gives us the price a small handyman business is typically willing to pay **per employee**.

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

1. Filter rows for `business_type = 'handyman'` and `n_employees <= 10`.
2. Calculate `earning_per_emp = adwords_earnings / n_employees`.
3. Group by `earning_per_emp` and count the number of businesses at each level.
4. Use `DENSE_RANK()` to find the most frequent value — the mode.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT 1.0 * adwords_earnings / n_employees AS earning_per_emp
    FROM google_adwords_earnings
    WHERE n_employees <= 10 AND business_type = 'handyman'
),

cte2 AS (
    SELECT earning_per_emp,
           COUNT(*) AS freq,
           DENSE_RANK() OVER(ORDER BY COUNT(*) DESC) AS rn
    FROM cte
    GROUP BY earning_per_emp
)

SELECT earning_per_emp
FROM cte2
WHERE rn = 1;
```

---

### What I Learned

This query shows how to compute the **mode** using SQL — a powerful way to uncover the most common value in a distribution, especially for business pricing or customer behavior patterns.

---

### Tags
`#SQL` `#AdwordsEarnings` `#Mode` `#SmallBusiness` `#InterviewPrep
