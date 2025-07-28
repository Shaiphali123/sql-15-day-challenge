# 🔗 Day 5: SQL JOINS Explained

Welcome to **Day 5 of the SQL 15-Day Challenge** with **ShaiviConnect**!  
Today, we’re covering one of the most important topics in SQL — **JOINS**.

---

## 🔍 What are JOINS?

SQL **JOINS** are used to combine rows from two or more tables, based on a related column between them (like a foreign key).

---

## 🔗 Types of SQL JOINS

### 1. ✅ INNER JOIN
Returns only matching rows from both tables.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;
````

---

### 2. 🔄 LEFT JOIN (LEFT OUTER JOIN)

Returns all rows from the left table + matching rows from the right.

```sql
SELECT customers.customer_name, orders.order_id
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;
```

---

### 3. 🔁 RIGHT JOIN (RIGHT OUTER JOIN)

Returns all rows from the right table + matching rows from the left.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.customer_id;
```

---

### 4. 🔄 FULL OUTER JOIN

Returns all records when there is a match in either left or right table.

> 🔸 Not supported in MySQL directly — use `UNION` of LEFT and RIGHT JOIN.

```sql
SELECT *
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id
UNION
SELECT *
FROM customers
RIGHT JOIN orders ON customers.customer_id = orders.customer_id;
```

---

### 5. 🔐 CROSS JOIN

Returns the **cartesian product** — every row in table A with every row in table B.

```sql
SELECT *
FROM products
CROSS JOIN categories;
```

---

## 📌 Top 5 Interview Questions

1. **What’s the difference between INNER JOIN and LEFT JOIN?**
2. **How would you fetch customers with no orders using JOINs?**
3. **Is FULL OUTER JOIN supported in MySQL? How do you mimic it?**
4. **What is the output of CROSS JOIN between 5 rows and 3 rows?**
5. **Write a query to get all orders and customer names, even if customer data is missing.**

---

## 🧠 Challenge of the Day

You have two tables:

* `students(id, name)`
* `marks(student_id, score)`

✅ Write a query to get student names along with their scores (including students with no marks).

```sql
SELECT students.name, marks.score
FROM students
LEFT JOIN marks ON students.id = marks.student_id;
```

---

## 🗳️ Poll of the Day

**Which JOIN will return all records from the left table and matched records from the right table?**

* INNER JOIN
* LEFT JOIN ✅
* RIGHT JOIN
* FULL OUTER JOIN

🧠 Vote now on [LinkedIn Poll](#) & share your thoughts!

---

🚀 Stay consistent, stay curious!
🎓 Follow **#ShaiviConnect** to keep leveling up in SQL & tech interviews.

```


