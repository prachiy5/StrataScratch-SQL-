## Sorting Movies By Duration Time

**Problem ID:** 2163  
**Tags:** Google, Easy  

---

### Problem Summary

We are working with a table called `movie_catalogue`. Each row contains a movie and some details about it. One of the columns is `duration`, which tells us how long the movie is.

We are asked to:
> Sort all the movies in **descending order of duration** and show all the columns in the output.

---

### Table Schema: `movie_catalogue`

| Column        | Type   |
|---------------|--------|
| show_id       | text   |
| title         | text   |
| release_year  | bigint |
| rating        | text   |
| duration      | text   |

---

### My Thought Process

1. We want to sort the data by the `duration` column.
2. We sort it in **descending** order (from longest to shortest).
3. Just use a simple `ORDER BY` with `DESC`.

Note: If `duration` is stored as a text field (like '120 min'), it may require parsing into a number if sorting doesn’t work correctly. But assuming it sorts fine as-is.

---

### SQL Solution

```sql
SELECT *
FROM movie_catalogue
ORDER BY duration DESC;
```

---

### What I Learned

This is a basic sorting question using `ORDER BY`. Always check the datatype of the column when sorting, especially if it’s stored as text and contains extra characters like 'min'.

---

### Tags
`#SQL` `#Sorting` `#Movies` `#OrderBy` `#Duration` `#InterviewPrep
