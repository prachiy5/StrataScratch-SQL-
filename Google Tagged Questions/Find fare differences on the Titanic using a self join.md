## Find Fare Differences on the Titanic Using a Self Join

**Problem ID:** 9603  
**Tags:** LinkedIn, Google, Hard  


---

### Problem Summary

We are given the Titanic passenger data in a table called `titanic`. Each row contains details about a passenger including their fare, age, survival status, and travel class (pclass).

We want to:
> For each non-surviving passenger, find the **average absolute fare difference** between them and **all other non-survivors** who:
> - Are in the **same travel class**
> - Have an **age difference of 5 years or less**
> - Are not the same person

---

### Table Schema: `titanic`

| Column       | Type   |
|--------------|--------|
| passengerid  | bigint |
| survived     | bigint |
| pclass       | bigint |
| name         | text   |
| sex          | text   |
| age          | double |
| sibsp        | bigint |
| parch        | bigint |
| ticket       | text   |
| fare         | double |
| cabin        | text   |
| embarked     | text   |

---

### My Thought Process

1. This is a classic **self join** problem, where we compare each passenger to others.
2. We only consider **non-survivors**.
3. Join on **same class**, exclude same passenger ID, and keep only pairs where the **age difference is 5 years or less**.
4. Then, for each passenger, calculate the **average absolute fare difference** between them and the matched passengers.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT t1.passengerid AS passenger1,
           t2.passengerid AS passenger2,
           t1.name AS name1,
           t1.fare AS fare1,
           t2.fare AS fare2
    FROM titanic t1
    INNER JOIN titanic t2
        ON t1.pclass = t2.pclass
       AND t1.passengerid != t2.passengerid
    WHERE t1.survived = 0
      AND t2.survived = 0
      AND t1.age IS NOT NULL
      AND t2.age IS NOT NULL
      AND ABS(t1.age - t2.age) <= 5
)

SELECT name1,
       AVG(ABS(fare1 - fare2)) AS avg_fare_diff
FROM cte
GROUP BY name1;
```

---

### What I Learned

This problem shows how powerful self joins can be when comparing rows within the same dataset. It’s important to include good filtering logic to avoid invalid matches (like a person being compared to themselves), and use functions like `ABS()` for clean calculations.

---

### Tags
`#SQL` `#Titanic` `#SelfJoin` `#FareAnalysis` `#WindowFunctions` `#DataComparison` `#InterviewPrep`
