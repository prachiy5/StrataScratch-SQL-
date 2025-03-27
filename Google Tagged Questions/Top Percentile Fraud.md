## Top 5% Suspicious Claims by State (Fraud Score)

**Problem ID:** 10303  
**Tags:** Google, Netflix, Hard  


---

### Problem Summary

Identify the **top 5 percentile** of claims with the **highest fraud scores** in each state. These are considered the most suspicious and potentially fraudulent.

Return:
- `policy_num`
- `state`
- `claim_cost`
- `fraud_score`

---

### Table Schema: `fraud_score`

| Column      | Type   |
|-------------|--------|
| policy_num  | text   |
| state       | text   |
| claim_cost  | bigint |
| fraud_score | double |

---

### SQL Solution

```sql
WITH cte AS (
  SELECT *,
         PERCENT_RANK() OVER(PARTITION BY state ORDER BY fraud_score DESC) AS pr
  FROM fraud_score
)

SELECT policy_num, state, claim_cost, fraud_score
FROM cte 
WHERE pr <= 0.05;
```

---

### What I Learned

This is a great use case for `PERCENT_RANK()` to isolate top fraud risks in each group. Useful in insurance analytics, audit, and compliance checks.

---

### Tags
`#SQL` `#FraudDetection` `#PercentileRank` `#RiskScoring` `#WindowFunctions` `#InterviewPrep`
