## Google Fit User Tracking: Average Session Distance

**Problem ID:** 10067  
**Tags:** Google, Hard  
 

---

### Problem Summary

We are asked to calculate the **average session distance** for Google Fit users in two different ways:

1. **Taking into account the curvature of the Earth** using the spherical distance formula.
2. **Assuming a flat surface**.

The session distance is calculated using only the start and end GPS locations (min and max step_id) **within the same session and day**. Sessions with only one step should be excluded.

---

### Table Schema: `google_fit_location`

| Column     | Type   |
|------------|--------|
| user_id    | text   |
| session_id | bigint |
| step_id    | bigint |
| day        | bigint |
| latitude   | double |
| longitude  | double |
| altitude   | double |

---

### SQL Solution

```sql
WITH cte AS (
  SELECT user_id, session_id, day,
         MIN(step_id) AS first_step,
         MAX(step_id) AS last_step
  FROM google_fit_location
  GROUP BY user_id, session_id, day
  HAVING COUNT(*) > 1
),

cte2 AS (
  SELECT c.user_id, c.session_id,
         gf1.latitude AS first_lat,
         gf1.longitude AS first_lon,
         gf2.latitude AS last_lat,
         gf2.longitude AS last_lon
  FROM cte c
  JOIN google_fit_location gf1
    ON c.user_id = gf1.user_id AND c.session_id = gf1.session_id AND c.first_step = gf1.step_id
  JOIN google_fit_location gf2
    ON c.user_id = gf2.user_id AND c.session_id = gf2.session_id AND c.last_step = gf2.step_id
),

cte3 AS (
  SELECT user_id, session_id,
         6371 * ACOS(
           SIN(RADIANS(first_lat)) * SIN(RADIANS(last_lat)) +
           COS(RADIANS(first_lat)) * COS(RADIANS(last_lat)) *
           COS(RADIANS(last_lon - first_lon))
         ) AS distance_curvature,
         111 * SQRT(POWER(last_lat - first_lat, 2) + POWER(last_lon - first_lon, 2)) AS distance_flat
  FROM cte2
)

SELECT 
  AVG(distance_curvature) AS avg_curved,
  AVG(distance_flat) AS avg_flat,
  AVG(distance_curvature - distance_flat) AS diff
FROM cte3;
```

---

### What I Learned

This query demonstrates spatial analysis using both spherical and Euclidean distance formulas in SQL. It's a practical exercise in understanding geolocation tracking accuracy and session-based summarization.

---

### Tags
`#SQL` `#GeospatialAnalysis` `#HaversineFormula` `#FlatDistance` `#GoogleFit` `#InterviewPrep
