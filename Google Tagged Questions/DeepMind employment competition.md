## DeepMind Employment Competition

**Problem ID:** 10070  
**Tags:** Google, Medium  

---

### Problem Summary

We are analyzing the results of a DeepMind employment competition. The task is to:
> Calculate the **average score for each team** and return the result sorted in **descending** order by score.

Return:
- `team_id`
- `avg_score`

---

### Table Schemas

**google_competition_participants**
| Column     | Type   |
|------------|--------|
| member_id  | bigint |
| team_id    | bigint |

**google_competition_scores**
| Column       | Type   |
|--------------|--------|
| member_id    | bigint |
| member_score | double |

---

### SQL Solution

```sql
SELECT 
  team_id, 
  AVG(member_score) AS avg_score
FROM google_competition_participants gp
INNER JOIN google_competition_scores gs
  ON gp.member_id = gs.member_id
GROUP BY team_id
ORDER BY avg_score DESC;
```

---

### What I Learned

This is a classic example of joining participant and score data, then aggregating the scores to evaluate overall team performance. Sorting helps quickly identify the top-performing teams.

---

### Tags
`#SQL` `#CompetitionResults` `#AverageScores` `#TeamAnalysis` `#JoinAndGroup` `#InterviewPrep`
