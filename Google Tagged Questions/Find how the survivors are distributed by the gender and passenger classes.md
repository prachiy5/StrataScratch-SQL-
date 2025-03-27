## Survivor Distribution by Gender and Class

**Problem ID:** 9882  
**Tags:** Google, Medium  

---

### Problem Summary

Create a report showing how **survivors** are distributed across **gender** and **passenger class**.

Passenger classes:
- `pclass = 1` → First Class
- `pclass = 2` → Second Class
- `pclass = 3` → Third Class

Output:
- Each row represents a **gender**
- Columns show **number of survivors** in each class

---

### Table Schema: `titanic`

| Column      | Type   |
|-------------|--------|
| passengerid | bigint |
| survived    | bigint |
| pclass      | bigint |
| name        | text   |
| sex         | text   |
| age         | double |
| sibsp       | bigint |
| parch       | bigint |
| ticket      | text   |
| fare        | double |
| cabin       | text   |
| embarked    | text   |

---

### SQL Solution

```sql
SELECT 
  sex,
  SUM(CASE WHEN pclass = 1 AND survived = 1 THEN 1 ELSE 0 END) AS first_class,
  SUM(CASE WHEN pclass = 2 AND survived = 1 THEN 1 ELSE 0 END) AS second_class,
  SUM(CASE WHEN pclass = 3 AND survived = 1 THEN 1 ELSE 0 END) AS third_class
FROM titanic
GROUP BY sex
ORDER BY sex;
```

---

### What I Learned

This format is commonly used in reporting where grouped categorical data needs to be displayed across multiple breakdowns like gender and class.

---

### Tags
`#SQL` `#TitanicSurvivors` `#GenderAnalysis` `#GroupBy` `#CaseAggregation` `#InterviewPrep`
