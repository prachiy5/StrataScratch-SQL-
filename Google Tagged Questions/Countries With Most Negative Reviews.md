## Countries With Most Negative Reviews

**Problem ID:** 9878  
**Tags:** Google, Airbnb, Medium  


---

### Problem Summary

We are analyzing hotel reviews to find out which **countries (reviewer nationalities)** have submitted the highest number of **negative reviews**.

> A review is considered negative if the `negative_review` column **is not equal to** "No Negative".

Return:
- `reviewer_nationality`
- number of valid negative reviews they gave

Sort by count in descending order.

---

### Table Schema: `hotel_reviews`

| Column                 | Type    |
|------------------------|---------|
| reviewer_nationality   | text    |
| negative_review        | text    |
| ... other columns ...  | ...     |

---

### SQL Solution

```sql
SELECT 
  reviewer_nationality,
  COUNT(negative_review) AS n
FROM hotel_reviews
WHERE negative_review != 'No Negative'
GROUP BY reviewer_nationality
ORDER BY n DESC;
```

---

### What I Learned

This query gives us a geographic view of dissatisfaction based on text feedback, which could be helpful for understanding service perceptions by region.

---

### Tags
`#SQL` `#TextFilter` `#NegativeReviews` `#CustomerInsights` `#InterviewPrep`
