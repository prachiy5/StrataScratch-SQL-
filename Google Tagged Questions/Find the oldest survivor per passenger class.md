## Find the Oldest Survivor per Passenger Class

**Problem ID:** 9883  
**Tags:** Google, Hard  

---

### Problem Summary

We need to identify the **oldest survivor** in each **passenger class** aboard the Titanic.

Return:
- `pclass`: passenger class
- `name`: name of the oldest survivor in that class
- `age`: age of the oldest survivor

Sort the result by passenger class (ascending).

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
WITH cte AS (
    SELECT 
        pclass,
        name,
        age,
        DENSE_RANK() OVER (PARTITION BY pclass ORDER BY age DESC) AS rn 
    FROM titanic
    WHERE survived = 1
)

SELECT pclass, name, age
FROM cte
WHERE rn = 1
ORDER BY pclass;
```

---

### What I Learned

This task demonstrates how to use window functions like `DENSE_RANK()` to extract the top record per group (passenger class) efficiently.

---

### Tags
`#SQL` `#WindowFunctions` `#TopPerGroup` `#Titanic` `#AgeAnalysis` `#InterviewPrep`
