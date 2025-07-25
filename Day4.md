
# 📊 Day 4: SQL GROUP BY & HAVING

Welcome to **Day 4 of the SQL 15-Day Challenge** with **ShaiviConnect**!  
Today, we’re going to master two powerful clauses in SQL — **GROUP BY** and **HAVING**.

---

## 🔹 What is `GROUP BY`?

`GROUP BY` is used to **group rows** that have the same values into summary rows. It is often used with **aggregate functions** like `SUM`, `COUNT`, `AVG`, `MIN`, and `MAX`.

✅ **Example:**

```sql
SELECT department, COUNT(*) 
FROM employees
GROUP BY department;
````

This will return a count of employees in each department.

---

## 🔸 What is `HAVING`?

`HAVING` is used to **filter the results of grouped records**.
It works like a `WHERE` clause, but for **aggregated data**.

✅ **Example:**

```sql
SELECT department, COUNT(*) 
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

This shows departments that have more than 10 employees.

---

## 🎯 Real-Life Scenario

You run a store and want to:

* Group sales by product → `GROUP BY`
* Only show products with more than 50 sales → `HAVING`

```sql
SELECT product_name, COUNT(*) AS total_sales
FROM sales
GROUP BY product_name
HAVING COUNT(*) > 50;
```

---

## 📌 Top 5 Interview Questions

1. **What is the difference between `WHERE` and `HAVING`?**
   ➤ `WHERE` filters rows before grouping.
   ➤ `HAVING` filters groups after grouping.

2. **Can we use `HAVING` without `GROUP BY`?**
   ➤ Yes, if you're using aggregate functions.

3. **Write a query to find departments having more than 5 employees.**

   ```sql
   SELECT department, COUNT(*)
   FROM employees
   GROUP BY department
   HAVING COUNT(*) > 5;
   ```

4. **What error occurs if you use `WHERE COUNT(*) > 5`?**
   ➤ You get an error — because `WHERE` doesn’t support aggregate functions.

5. **How can you sort results after using `GROUP BY`?**
   ➤ Use `ORDER BY` after `GROUP BY` or `HAVING`.

---

## 🧠 Challenge of the Day

Write a query to:

* Group orders by customer
* Calculate total order amount
* Show only those customers whose total is more than ₹10,000

```sql
SELECT customer_id, SUM(order_amount) AS total_amount
FROM orders
GROUP BY customer_id
HAVING SUM(order_amount) > 10000;
```

---

## 🗳️ Poll of the Day (for LinkedIn)

**Question:** Which SQL clause is used to filter grouped data?

* WHERE
* GROUP BY
* HAVING ✅
* ORDER BY

👉 Comment your answer or vote on our [LinkedIn Poll](#)!

---

## 🖼️ Poster – Day 4

![Day 4 - SQL GROUP BY & HAVING](../assets/day4-groupby-having.png)

---

✅ Keep Learning. Keep Growing.
💡 Follow **#ShaiviConnect** for daily insights & interview prep tips!

````
