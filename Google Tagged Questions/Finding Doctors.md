## Finding Doctors with Last Name 'Johnson'

**Problem ID:** 10356  
**Tags:** Google, Easy  

---

### Problem Summary

Find all **doctors** in the employee list whose **last name is 'Johnson'**.

Return:
- `first_name`
- `last_name`

---

### Table Schema: `employee_list`

| Column       | Type     |
|--------------|----------|
| first_name   | text     |
| last_name    | text     |
| profession   | text     |
| employee_id  | bigint   |
| birthday     | datetime |
| birth_month  | bigint   |

---

### SQL Solution

```sql
SELECT first_name, last_name 
FROM employee_list
WHERE last_name = 'Johnson' 
  AND profession = 'Doctor';
```

---

### What I Learned

Simple filters are useful in basic HR or healthcare directory queries. This problem checks basic selection logic.

---

### Tags
`#SQL` `#Filtering` `#DoctorLookup` `#InterviewPrep` `#EmployeeData`
