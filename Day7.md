---
title: "Day 7: Subqueries and Nested SELECT in SQL"
description: "Learn how to write subqueries (nested SELECT statements) with real-world examples, interview questions, and practice queries."
author: "Shaivi Connect"
date: 2025-07-31
---

# 📅 Day 7: Subqueries and Nested SELECT in SQL — #ShaiviConnect SQL 15-Day Challenge

Welcome to **Day 7** of our SQL challenge! Today’s topic is all about **Subqueries** — queries inside queries, which help you perform complex filtering and comparison operations.

---

## 🔍 What is a Subquery?

A **subquery** (also called a *nested query* or *inner query*) is a SQL query embedded inside another query.

It is often used in:
- `SELECT` clause
- `WHERE` clause
- `FROM` clause

---

## 🎯 When to Use Subqueries?

- When you need a value derived from another query.
- When you want to filter using aggregate conditions.
- When JOINs are not ideal or readable.

---

## 🧠 Types of Subqueries

| Type | Description |
|------|-------------|
| **Single-row Subquery** | Returns exactly one row |
| **Multiple-row Subquery** | Returns more than one row |
| **Multiple-column Subquery** | Returns more than one column |
| **Correlated Subquery** | Depends on the outer query for execution |

---

## 🧾 Syntax
```sql
SELECT column_name
FROM table_name
WHERE column_name OPERATOR (
  SELECT column_name
  FROM another_table
  WHERE condition
);
````

---

## ✅ Example 1: Basic Subquery

Find all employees who earn more than the average salary.

```sql
SELECT name, salary
FROM employees
WHERE salary > (
  SELECT AVG(salary)
  FROM employees
);
```

---

## ✅ Example 2: Subquery with IN

Find departments that have more than 5 employees.

```sql
SELECT dept_name
FROM departments
WHERE dept_id IN (
  SELECT dept_id
  FROM employees
  GROUP BY dept_id
  HAVING COUNT(*) > 5
);
```

---

## ✅ Example 3: Correlated Subquery

Find employees earning more than the average salary in their own department.

```sql
SELECT e1.name, e1.salary
FROM employees e1
WHERE salary > (
  SELECT AVG(e2.salary)
  FROM employees e2
  WHERE e1.dept_id = e2.dept_id
);
```

---

## ✅ Example 4: Nested Subquery with Aggregation

Find customers who ordered more than the average number of orders per customer.

```sql
SELECT customer_id
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > (
  SELECT AVG(order_count)
  FROM (
    SELECT COUNT(*) AS order_count
    FROM orders
    GROUP BY customer_id
  ) AS avg_orders
);
```

---

## 💡 Real-World Use Case

In an e-learning platform, get the list of students who scored more than the average marks in **their batch**:

```sql
SELECT student_name, marks
FROM students s1
WHERE marks > (
  SELECT AVG(marks)
  FROM students s2
  WHERE s1.batch_id = s2.batch_id
);
```

---

## ❓ Day 7 Interview Questions

1. What is a subquery in SQL?
2. Difference between correlated and non-correlated subquery?
3. Can a subquery return multiple rows? When is it valid?
4. What is the use of subquery in the FROM clause?
5. Write a query to find employees earning more than the average salary of their department.
6. When would you use a subquery over a JOIN?

---

## 🧪 Practice Questions

1. Write a subquery to find employees with salaries higher than **ALL** employees in the 'Marketing' department.
2. Find the names of products that are more expensive than the average price of all products.
3. Retrieve customer names who have never placed an order (use `NOT IN` with subquery).
4. Use a correlated subquery to find the highest-paid employee in each department.

---

## 🗳️ Poll of the Day

**Q: Can a subquery return more than one row?**

* [ ] Yes
* [ ] No
* [ ] Only in SELECT clause
* [ ] Only in WHERE clause

✅ **Correct Answer:** Yes — if the outer query is designed to handle multiple rows (like using `IN` or `EXISTS`).

---

## 📌 Key Takeaways

* Subqueries are powerful tools for writing dynamic and modular queries.
* Use correlated subqueries when the inner query depends on the outer query.
* Subqueries can be placed in SELECT, FROM, or WHERE clauses.

---

## 🔗 Stay Connected

For daily SQL content, challenges, and interview prep, follow:

* 🌐 [Shaivi Connect Blog](https://shaiphali123.github.io/sql-15-day-challenge/)
* 📸 [Instagram: @ShaiviConnect](https://www.instagram.com/shaiviconnect)
* 🧑‍💻 [GitHub](https://github.com/Shaiphali123)

---

*Keep learning. Keep querying. See you on Day 8! 🔥*

```
