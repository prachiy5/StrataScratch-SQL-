## Number of Customers Without an Order

**Problem ID:** 10089  
**Tags:** Google, Amazon, Medium  

---

### Problem Summary

Find how many customers are **not associated with any order**.

Return:
- A single count value representing customers who **never placed an order**.

---

### Table Schemas

**customers**
| Column       | Type   |
|--------------|--------|
| id           | bigint |
| first_name   | text   |
| last_name    | text   |
| city         | text   |
| address      | text   |
| phone_number | text   |

**orders**
| Column          | Type     |
|------------------|----------|
| id               | bigint   |
| cust_id          | bigint   |
| order_date       | datetime |
| order_details    | text     |
| total_order_cost | bigint   |

---

### SQL Solution

```sql
SELECT COUNT(*)
FROM orders
RIGHT JOIN customers
  ON orders.cust_id = customers.id
WHERE orders.id IS NULL;
```

---

### What I Learned

This pattern uses a `RIGHT JOIN` (or `LEFT JOIN` from `customers` as base) to identify rows that **exist in the customers table but not in the orders table**, indicating inactive or prospective customers.

---

### Tags
`#SQL` `#CustomerAnalysis` `#NoOrders` `#JoinAndFilter` `#InterviewPrep`
