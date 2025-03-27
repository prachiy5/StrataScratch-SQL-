## Percentage of Shipable Orders

**Problem ID:** 10090  
**Tags:** Google, Amazon, Medium  


---

### Problem Summary

Find the **percentage of shipable orders**. An order is considered **shipable** if the **customer's address is not null**.

Return:
- A single value: `percent_shipable`

---

### Table Schemas

**orders**
| Column          | Type     |
|------------------|----------|
| id               | bigint   |
| cust_id          | bigint   |
| order_date       | datetime |
| order_details    | text     |
| total_order_cost | bigint   |

**customers**
| Column       | Type   |
|--------------|--------|
| id           | bigint |
| first_name   | text   |
| last_name    | text   |
| city         | text   |
| address      | text   |
| phone_number | text   |

---

### SQL Solution

```sql
SELECT 
  SUM(CASE WHEN address IS NOT NULL THEN 1 ELSE 0 END) * 100 / COUNT(*) AS percent_shipable
FROM orders o
INNER JOIN customers c
  ON o.cust_id = c.id;
```

---

### What I Learned

This problem reinforces the importance of **data quality** (e.g., missing address) when determining fulfillment capability, a key concept in e-commerce and logistics analytics.

---

### Tags
`#SQL` `#ShipableOrders` `#DataQuality` `#PercentageCalculation` `#InterviewPrep`
