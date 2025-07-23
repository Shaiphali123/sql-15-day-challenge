---
layout: default
title: "Day 2 - SQL Clauses & Filtering"
permalink: /day2/
---

🚀 Day 2: SQL Clauses & Filtering

Welcome to **Day 2** of the **SQL 15-Day Challenge with Shaivi Connect**!  
Today, we’ll dive into how to **filter data** using `WHERE`, comparison operators, and pattern matching.

---

🧠 What You'll Learn Today

- ✅ `WHERE` Clause  
- ✅ Comparison Operators (`=`, `>`, `<`, `!=`, `>=`, `<=`)  
- ✅ `BETWEEN`, `IN`, `LIKE`  
- ✅ `IS NULL` and `IS NOT NULL`  

---

🔍 1. SQL WHERE Clause

Used to filter records that fulfill a specified condition.

```sql
SELECT * FROM Customers
WHERE Country = 'India';
⚖️ 2. Comparison Operators

SELECT * FROM Products
WHERE Price > 100;
You can use:

=, !=

>, <

>=, <=

🔁 3. BETWEEN, IN, LIKE

-- BETWEEN
SELECT * FROM Orders
WHERE OrderDate BETWEEN '2024-01-01' AND '2024-12-31';

-- IN
SELECT * FROM Customers
WHERE Country IN ('India', 'USA', 'UK');

-- LIKE
SELECT * FROM Customers
WHERE CustomerName LIKE 'S%';  -- Starts with S
🚫 4. IS NULL and IS NOT NULL

SELECT * FROM Employees
WHERE Department IS NOT NULL;
💡 Interview Questions
What is the difference between WHERE and HAVING?

How does LIKE differ from = in SQL?

When would you use IN instead of multiple OR conditions?

Explain the use of BETWEEN and IS NULL.

🧪 Practice Challenge
Query: Show all employees whose age is between 25 and 35 and whose location is not null.


SELECT * FROM Employees
WHERE Age BETWEEN 25 AND 35
AND Location IS NOT NULL;
📊 Poll of the Day (on LinkedIn)
🗳️ “Which SQL clause do you find most tricky?”

LIKE

BETWEEN

IN

IS NULL

🔗 Vote on LinkedIn: [Insert your poll link here]

🔁 Previous Day
👉 Go to Day 1

✨ Stay consistent. Stay curious.
We grow together — #ShaiviConnect 💫


