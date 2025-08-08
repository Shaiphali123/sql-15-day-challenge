
# 📅 Day 14: SQL Performance Tips

Welcome to **Day 14** of the SQL 15-Day Challenge!  
Today we focus on **SQL performance tuning** – how to write fast, efficient queries that scale well with growing data.

---

## ⚡ Why SQL Performance Matters?

Poorly written queries can:
- Slow down your app
- Lock tables
- Drain server resources
- Impact customer experience

Learning to **optimize SQL** is a crucial skill for any backend or data engineer.

---

## 🔍 Top SQL Performance Tips

### 1. ✅ Use SELECT Only What You Need
```sql
-- Avoid this
SELECT * FROM Employees;

-- Do this
SELECT name, salary FROM Employees;
```

### 2. ✅ Use WHERE to Filter Early
```sql
SELECT name FROM Employees WHERE department = 'Sales';
```

### 3. ✅ Use Proper Indexes
```sql
CREATE INDEX idx_department ON Employees(department);
```

### 4. ✅ Avoid Using Functions on Indexed Columns
```sql
-- This disables index:
SELECT * FROM Employees WHERE YEAR(joining_date) = 2023;

-- Instead:
SELECT * FROM Employees 
WHERE joining_date BETWEEN '2023-01-01' AND '2023-12-31';
```

### 5. ✅ Use EXPLAIN/EXPLAIN PLAN
```sql
EXPLAIN SELECT name FROM Employees WHERE department = 'HR';
```

### 6. ✅ Avoid DISTINCT If Not Needed

### 7. ✅ Use JOINs Efficiently

### 8. ✅ LIMIT Large Results
```sql
SELECT * FROM Sales ORDER BY amount DESC LIMIT 100;
```

### 9. ✅ Normalize Data, but Not Too Much

### 10. ✅ Clean & Archive Old Data

---

## 💼 Real-world Scenario

> 🔄 You’re running a report that takes 12 seconds to load.  
> ➤ Use `EXPLAIN`, add index on `report_date`, and fetch only necessary columns.  
> ⏱ Query now takes 1.2 seconds!

---

## 🧪 Practice Problem

🧩 **Problem:**  
You have a table `Orders(order_id, customer_id, order_date, amount)`.  
Write an optimized query to get the top 5 customers by total order value in 2024.

<details>
<summary>💡 Click to view the solution</summary>

```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM Orders
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 5;
```
</details>

---

## ❓ Top SQL Performance Interview Questions

1. What is indexing? When should you avoid using it?
2. Difference between clustered and non-clustered index?
3. How does SELECT * affect performance?
4. How can EXPLAIN help in query tuning?
5. What is the impact of subqueries vs JOINs?
6. How do you reduce the number of disk I/Os in SQL?
7. How does normalization impact performance?
8. What are materialized views and when should you use them?
9. What is query caching?
10. How do transactions impact performance?

---

## 📊 LinkedIn Poll (Day 14)

**Which of these will most improve SQL performance?**  
A) Using SELECT *  
B) Adding proper indexes  
C) Using multiple subqueries  
D) Avoiding WHERE clause

✅ Correct Answer: **B**

---

## 🧠 Advanced SQL Performance Tips

### 11. Use EXISTS Instead of IN
```sql
SELECT name FROM Employees e
WHERE EXISTS (
  SELECT 1 FROM Departments d 
  WHERE d.location = 'NY' AND d.id = e.department_id
);
```

### 12. Avoid OR in WHERE Clause
```sql
SELECT * FROM Orders 
WHERE status IN ('Pending', 'Processing');
```

### 13. Avoid SELECT in Loops

### 14. Be Cautious with CTEs

---

## 📊 EXPLAIN Output Fields

| Field        | Meaning |
|--------------|--------|
| id           | Step number |
| select_type  | Query type |
| table        | Table name |
| type         | Join type |
| possible_keys| Candidate indexes |
| key          | Used index |
| rows         | Estimated rows |
| Extra        | Additional info |

---

## 📁 Case Study: Dashboard Query

```sql
-- Original (slow)
SELECT * FROM Sales WHERE YEAR(sale_date) = 2024 AND region = 'Asia';

-- Optimized (fast)
SELECT * FROM Sales 
WHERE sale_date BETWEEN '2024-01-01' AND '2024-12-31' AND region = 'Asia';
```

---

## ✅ Final Checklist

- [x] Used indexes?
- [x] Avoided SELECT *?
- [x] Used LIMIT for pagination?
- [x] Normalized only when needed?
- [x] Checked with EXPLAIN?

---

## 📚 Resources

- https://use-the-index-luke.com/
- https://dev.mysql.com/doc/refman/8.0/en/optimization.html

---

## 🏁 Coming Up Next: Day 15 – Final Project + Revision Guide 🎓
