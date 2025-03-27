## Find the Top Ten Hotels With the Highest Ratings

**Problem ID:** 9874  
**Tags:** Google, Expedia, Airbnb, Medium  

---

### Problem Summary

We are working with hotel review data. The task is:
> Find the **top 10 hotels** with the **highest average rating** based on the `average_score` column.

Return:
- `hotel_name`
- `average_score`

Sort by score in descending order.

---

### Table Schema: `hotel_reviews`

| Column                             | Type    |
|------------------------------------|---------|
| hotel_name                         | text    |
| average_score                      | double  |
| review_date                        | datetime|
| reviewer_score                     | double  |
| reviewer_nationality              | text    |
| total_number_of_reviews           | bigint  |
| total_number_of_reviews_reviewer_has_given | bigint |
| ... and others                     | ...     |

---

### My Thought Process

1. First, group reviews by `hotel_name` and calculate the **average** of the `average_score`.
2. Use a window function `RANK()` to sort hotels by average score.
3. Pick the **top 10** using a filter on the rank.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT hotel_name, AVG(average_score) AS average_score
    FROM hotel_reviews 
    GROUP BY hotel_name
),

cte2 AS (
    SELECT *,
           RANK() OVER (ORDER BY average_score DESC) AS rn 
    FROM cte
)

SELECT hotel_name, average_score
FROM cte2
WHERE rn <= 10;
```

---

### What I Learned

This query demonstrates how to apply aggregation and ranking together for top-N analysis — a common task in analytics projects.

---

### Tags
`#SQL` `#Aggregation` `#TopN` `#HotelRatings` `#Ranking` `#InterviewPrep`
