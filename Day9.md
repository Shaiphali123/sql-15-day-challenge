title: "Day 9: SQL Views & Indexing"
description: "Learn about SQL Views and Indexes, their purpose, benefits, syntax, and interview-level questions with real-world examples."
author: "Shaivi Connect"
date: 2025-08-01
---

# 📅 Day 9: SQL Views & Indexing — #ShaiviConnect SQL 15-Day Challenge

Welcome to **Day 9** of our SQL series!  
Today we’re covering two powerful concepts that help you manage **performance** and **data abstraction**:

👉 **SQL Views**  
👉 **SQL Indexing**

---

## 👁️‍🗨️ What is a SQL View?

A **View** is a **virtual table** based on the result-set of a SQL query.

It does **not store data** physically but helps:
- Simplify complex queries
- Improve data security
- Enable abstraction and reusability

### ✅ Syntax:
```sql
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
````

### 🔄 Updating a View:

```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

### ❌ Dropping a View:

```sql
DROP VIEW view_name;
```

---

## 📌 Example: Creating a View

Let’s create a view of active employees.

```sql
CREATE VIEW active_employees AS
SELECT id, name, department
FROM employees
WHERE status = 'active';
```

Now you can query:

```sql
SELECT * FROM active_employees;
```

---

## 🧠 Real-Life Use Case (View)

In an e-commerce system, create a view for **daily active orders** to simplify analytics:

```sql
CREATE VIEW daily_orders AS
SELECT order_id, customer_id, order_date
FROM orders
WHERE DATE(order_date) = CURDATE();
```

---

## ⚙️ What is Indexing?

An **index** in SQL is like a book's table of contents — it helps the database **find rows faster** without scanning the entire table.

Indexing is most useful for:

* Large datasets
* Columns used in WHERE, JOIN, ORDER BY, GROUP BY

---

### ✅ Types of Indexes:

| Type                | Description                   |
| ------------------- | ----------------------------- |
| **Single-column**   | Index on one column           |
| **Composite**       | Index on multiple columns     |
| **Unique Index**    | Ensures all values are unique |
| **Full-text Index** | Used for text search          |

---

### 🛠️ Syntax:

```sql
-- Basic index
CREATE INDEX index_name ON table_name (column_name);

-- Composite index
CREATE INDEX idx_name ON table_name (col1, col2);

-- Drop an index
DROP INDEX index_name ON table_name;
```

---

### ⚡ Performance Tip:

Using indexes on columns with **high selectivity** (i.e., unique values) yields the best performance boost.

---

## 🧪 Practice Questions:

1. Create a view of employees who joined after 2022.
2. Create a view combining employee and department tables.
3. Add an index on the `email` column of a `users` table.
4. What happens when you try to update a view with a `GROUP BY`?

---

## ❓ Interview Questions:

1. What is a view? How is it different from a table?
2. Can you perform INSERT/UPDATE on a view?
3. What are the pros and cons of using indexes?
4. Difference between clustered and non-clustered indexes?
5. When would you avoid indexing a column?

---

## 🗳️ Poll of the Day

**Which of these improves query speed the most?**

* [ ] Adding indexes
* [ ] Using SELECT \*
* [ ] Using multiple joins
* [ ] Creating views

✅ Correct Answer: **Adding indexes**

---

## 🔗 Stay Connected

* 🌐 [Shaivi SQL Blog](https://shaiphali123.github.io/sql-15-day-challenge/)
* 📸 [Instagram: @ShaiviConnect](https://www.instagram.com/shaiviconnect)
* 🧑‍💻 [GitHub](https://github.com/Shaiphali123)



Also ready to give you an **Instagram caption**, **LinkedIn poll setup**, or **Reel script** if needed!
```
