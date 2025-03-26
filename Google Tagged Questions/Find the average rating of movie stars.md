## Find the Average Rating of Movie Stars

**Problem ID:** 9605  
**Tags:** Google, Netflix, Medium  
 

---

### Problem Summary

We’re given two tables:
- `nominee_filmography`: contains movies, roles, and ratings for each star.
- `nominee_information`: contains personal info like name and birthday.

We are asked to:
> Find the **average rating** of each movie star using their name as the join key. Include their name and birthday, and **sort by birthday in ascending order**.

---

### Table Schemas

**nominee_filmography**

| Column       | Type   |
|--------------|--------|
| name         | text   |
| amg_movie_id | text   |
| movie_title  | text   |
| role_type    | text   |
| rating       | double |
| year         | bigint |
| id           | bigint |

**nominee_information**

| Column        | Type     |
|---------------|----------|
| name          | text     |
| amg_person_id | text     |
| top_genre     | text     |
| birthday      | datetime |
| id            | bigint   |

---

### My Thought Process

1. Join the two tables using the `name` column.
2. For each person, calculate the average movie rating.
3. Round the average to 2 decimal places for cleaner output.
4. Show `name`, `birthday`, and average rating.
5. Sort the result by `birthday` in ascending order.

---

### SQL Solution

```sql
SELECT ni.birthday, 
       ni.name,
       ROUND(AVG(nf.rating), 2) AS avg_rating
FROM nominee_information ni
JOIN nominee_filmography nf
  ON ni.name = nf.name
GROUP BY ni.birthday, ni.name
ORDER BY ni.birthday;
```

---

### What I Learned

This task is a great reminder of how common it is to join datasets using name fields, and why it’s important to group correctly and round results for reporting.

---

### Tags
`#SQL` `#Ratings` `#MovieStars` `#JoinTables` `#AverageCalculation` `#InterviewPrep
