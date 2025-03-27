## Titanic Survivors and Non-Survivors by Class

**Problem ID:** 9881  
**Tags:** Tesla, Google, Medium  

---

### Problem Summary

Create a report showing the number of **survivors and non-survivors** grouped by **passenger class** on the Titanic.

The classes are defined as:
- First class: `pclass = 1`
- Second class: `pclass = 2`
- Third class: `pclass = 3`

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
  survived,
  SUM(CASE WHEN pclass = 1 THEN 1 ELSE 0 END) AS first_class,
  SUM(CASE WHEN pclass = 2 THEN 1 ELSE 0 END) AS second_class,
  SUM(CASE WHEN pclass = 3 THEN 1 ELSE 0 END) AS third_class
FROM titanic
GROUP BY survived;
```

---

### Output
- One row for survivors (`survived = 1`)
- One row for non-survivors (`survived = 0`)
- Each row shows how many passengers were in each class

---

### Tags
`#SQL` `#TitanicAnalysis` `#CASE` `#GroupBy` `#SurvivorReport` `#InterviewPrep`
