## Find All Companies With More Than 10 Employees

**Problem ID:** 9807  
**Tags:** Google, Easy  
**Roles:** Data Analyst, BI Analyst, Data Scientist, Data Engineer, ML Engineer  
**Last Updated:** September 2024  

---

### Problem Summary

We’re querying a table that stores Google AdWords earnings and company details. The task is:
> Find all companies that have **more than 10 employees**.

Output all columns from the table.

---

### Table Assumed Schema: `google_adwords_earnings`

| Column        | Type     |
|----------------|----------|
| company_id     | bigint   |
| company_name   | text     |
| n_employees    | int      |
| earnings       | decimal  |
| industry       | text     |
| ...            | ...      |

---

### My Thought Process

1. Simply filter the table where the number of employees is greater than 10.
2. Use `SELECT *` to return all columns as required.

---

### SQL Solution

```sql
SELECT *
FROM google_adwords_earnings
WHERE n_employees > 10;
```

---

### What I Learned

This is a straightforward filtering query — but it’s helpful in workforce analytics and segmentation tasks.

---

### Tags
`#SQL` `#Filtering` `#CompanyData` `#EmployeeCounts` `#InterviewPrep`
