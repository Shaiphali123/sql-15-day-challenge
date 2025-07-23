
---
title: Day 2 - SQL Filtering & Clauses
description: Learn SQL WHERE clause, comparison operators, BETWEEN, IN, LIKE, IS NULL with examples and interview questions.
---

# 🚀 Day 2: SQL Filtering & Clauses

Welcome to **Day 2** of the **SQL 15-Day Challenge with Shaivi Connect**!  
Today, let’s explore how to **filter data** in SQL using the `WHERE` clause, comparison operators, and pattern-matching techniques.

---

## 🧠 What You'll Learn Today

- ✅ `WHERE` Clause  
- ✅ Comparison Operators (`=`, `!=`, `<`, `>`, `<=`, `>=`)  
- ✅ Logical Operators (`AND`, `OR`, `NOT`)  
- ✅ `BETWEEN`, `IN`, `LIKE`  
- ✅ `IS NULL`, `IS NOT NULL`

---

## 🔍 1. SQL WHERE Clause

The `WHERE` clause is used to **filter records** that meet a specific condition.

```sql
SELECT * FROM Customers
WHERE Country = 'India';
````

---

## ⚖️ 2. Comparison Operators

You can use these to compare values:

* `=` (Equal)
* `!=` or `<>` (Not equal)
* `>` / `<` (Greater / Less than)
* `>=` / `<=` (Greater or equal / Less or equal)

```sql
SELECT * FROM Products
WHERE Price > 100;
```

---

## 🧠 3. Logical Operators: AND, OR, NOT

Use them to combine conditions.

```sql
SELECT * FROM Employees
WHERE Department = 'IT' AND Age > 30;

SELECT * FROM Employees
WHERE City = 'Delhi' OR City = 'Mumbai';

SELECT * FROM Employees
WHERE NOT Country = 'India';
```

---

## 🔁 4. BETWEEN, IN, LIKE

**BETWEEN**: Matches values within a range
**IN**: Matches any value from a list
**LIKE**: Matches a pattern

```sql
-- BETWEEN
SELECT * FROM Orders
WHERE OrderDate BETWEEN '2024-01-01' AND '2024-12-31';

-- IN
SELECT * FROM Customers
WHERE Country IN ('India', 'USA', 'UK');

-- LIKE
SELECT * FROM Customers
WHERE CustomerName LIKE 'S%';  -- Starts with 'S'
```

---

## 🚫 5. IS NULL and IS NOT NULL

Used to filter null (missing) or non-null values.

```sql
SELECT * FROM Employees
WHERE Department IS NOT NULL;
```

---

## 💡 Interview Questions

1. What is the difference between `WHERE` and `HAVING`?
2. How does `LIKE` differ from `=` in SQL?
3. When should you use `IN` over multiple `OR` conditions?
4. What is the output of `BETWEEN` if both boundaries are equal?
5. Explain the role of `IS NULL` and why it's important in data analysis.

---

## 🧪 Practice Challenge

🔹 **Query:** Show all employees whose age is between 25 and 35 and whose location is not null.

```sql
SELECT * FROM Employees
WHERE Age BETWEEN 25 AND 35
AND Location IS NOT NULL;
```

---

## 📊 Poll of the Day

🗳️ *“Which SQL clause do you find the most confusing?”*

* LIKE
* BETWEEN
* IN
* IS NULL

👉 Vote here on [LinkedIn](https://www.linkedin.com/company/107863493/admin/dashboard/)

---

## 🔁 Previous Day

👉 [Go to Day 1 - SQL Basics](https://shaiphali123.github.io/sql-15-day-challenge/Day1_Intro_SQL)

---

## 🔗 Connect with Me

* 📸 [Instagram](https://www.instagram.com/shaiviconnect/)
* 💼 [LinkedIn](https://www.linkedin.com/company/107863493/)
* 📺 [YouTube](https://www.youtube.com/@shaiphali43)

---

✨ Stay consistent. Stay curious.
We grow together — **#ShaiviConnect 💫**

```

---



