## Travelers Who Returned Home

**Problem ID:** Custom  
**Tags:** Window Functions, Real-world Scenario, Easy-Medium  
  

---

### Problem Summary

We’re given a table called `travel_history`. It shows when and where each traveler went. Each row tells us:
- the traveler's name
- which city they started from (`start_city`)
- which city they went to (`end_city`)
- and the date of the travel

Now we want to find out:
> How many travelers ended their journey **in the same city where they started**?

That means we want to look at the **first city** they traveled from, and the **last city** they arrived at, and compare them.

---

### Table Schema: `travel_history`

| Column     | Type     |
|------------|----------|
| traveler   | text     |
| start_city | text     |
| end_city   | text     |
| date       | datetime |

---

### My Thought Process (in a simple way)

1. First, for each traveler, find the **first city** they started from. This tells us their home city.
2. Then, for the same traveler, find the **last city** they reached. This tells us where they ended their journey.
3. If the first start city and last end city are the same, it means they returned home.
4. Finally, count how many such travelers exist.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT traveler,
           FIRST_VALUE(start_city) OVER(PARTITION BY traveler ORDER BY date) AS start_city,
           FIRST_VALUE(end_city) OVER(PARTITION BY traveler ORDER BY date DESC) AS end_city
    FROM travel_history
)

SELECT COUNT(DISTINCT traveler) AS n_travelers_returned
FROM cte
WHERE start_city = end_city;
```

---

### What I Learned

This problem shows how useful window functions like `FIRST_VALUE()` can be when you need to look at the "first" or "last" event for each group. It's also a good reminder that real-world data questions are often about comparing different stages in a journey or process.

---

### Tags
`#SQL` `#TravelData` `#WindowFunctions` `#FirstLast` `#ReturnHome` `#InterviewPrep`
