## Election Results

**Problem ID:** 2099  
**Tags:** Deloitte, Google, Medium  


---

### Problem Summary

We have a table called `voting_results`. It shows who voted for whom in a city-wide election. Each row tells us:
- the name of the voter
- the name of the candidate they voted for (can be blank if they didn't vote)

The rules are:
- Each person has 1 vote total.
- If they vote for more than one candidate, their 1 vote is **split equally** across all candidates they picked.
- Some people didn't vote at all (the `candidate` column is blank for them).

We want to find out:
> Who got the most votes overall? And in case of a tie, return all top candidates.

Also, to keep things neat, we round votes to 3 decimal places.

---

### Table Schema: `voting_results`

| Column     | Type   |
|------------|--------|
| voter      | text   |
| candidate  | text   |

---

### My Thought Process 

1. First, we figure out how many candidates each voter voted for.
2. If someone voted for 2 people, each of those candidates should get 0.5 vote from that person.
3. We skip the people who didn’t vote.
4. Then we add up all the partial votes each candidate got.
5. Finally, we pick the candidate(s) with the highest total votes.

---

### SQL Solution

```sql
WITH cte AS (
    SELECT voter,
           CASE 
               WHEN candidate IS NULL THEN 0 
               ELSE 1.0 / COUNT(candidate)
           END AS total_voted
    FROM voting_results
    GROUP BY voter
),

cte2 AS (
    SELECT candidate, 
           ROUND(SUM(total_voted), 3) AS total_votes
    FROM cte
    INNER JOIN voting_results vr
        ON vr.voter = cte.voter
    WHERE candidate != ''
    GROUP BY candidate
)

SELECT candidate 
FROM cte2
WHERE total_votes = (SELECT MAX(total_votes) FROM cte2);
```

---

### What I Learned

This problem was a good reminder that sometimes, each row in a dataset doesn’t carry equal weight. We had to calculate a fair share of each vote based on how many candidates a person supported. And rounding the result was important to avoid tiny differences from floating-point errors.

---

### Tags
`#SQL` `#ElectionLogic` `#VoteSplitting` `#WindowFunctions` `#RealWorldScenario` `#InterviewPrep`
