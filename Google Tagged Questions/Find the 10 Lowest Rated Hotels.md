## Find the 10 Lowest Rated Hotels

**Problem ID:** 9875  
**Tags:** Google, Airbnb, Medium  

---

### Problem Summary

We are analyzing hotel ratings from the `hotel_reviews` table. The task is:
> Find the **10 hotels with the lowest average ratings**.

Return:
- `hotel_name`
- `average_score`

---

### Table Schema: `hotel_reviews`

| Column                             | Type    |
|------------------------------------|---------|
| hotel_name                         | text    |
| average_score                      | double  |
| review_date                        | datetime|
| reviewer_score                     | double  |
| ... and others                     | ...     |

---

### My Thought Process

1. Group records by `hotel_name`.
2. For each hotel, compute the **average** score.
3. Use the `RANK()` window function to rank hotels by their average score in ascending order.
4. Filter for the top 10 **lowest** scored hotels.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT hotel_name,
           AVG(average_score) AS average_score,
           RANK() OVER (ORDER BY AVG(average_score)) AS rnk
    FROM hotel_reviews
    GROUP BY hotel_name
)

SELECT hotel_name, average_score
FROM cte
WHERE rnk <= 10;
```

---

### What I Learned

This mirrors the logic for top-rated hotels but in ascending order. Useful when identifying underperforming properties or customer satisfaction issues.

---

### Tags
`#SQL` `#HotelRatings` `#Bottom10` `#Ranking` `#Analytics` `#InterviewPrep`
