## Total AdWords Earnings by Business Type

**Problem ID:** 10164  
**Tags:** Google, Easy  

---

### Problem Summary

Calculate the total **AdWords earnings** for each **business type**.

Return:
- `business_type`
- `total_earnings`

---

### Table Schema: `google_adwords_earnings`

| Column          | Type   |
|------------------|--------|
| business_type    | text   |
| n_employees      | bigint |
| year             | bigint |
| adwords_earnings | bigint |

---

### SQL Solution

```sql
SELECT 
  business_type, 
  SUM(adwords_earnings) AS total_earnings
FROM google_adwords_earnings
GROUP BY business_type;
```

---

### What I Learned

This is a simple yet important aggregate query that helps identify which types of businesses are generating the most from AdWords. It's useful in marketing spend and revenue analysis.

---

### Tags
`#SQL` `#Adwords` `#TotalEarnings` `#GroupBy` `#BusinessType` `#InterviewPrep`
