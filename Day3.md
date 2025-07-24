title: Day 3 - SQL Aggregate Functions
description: Learn SQL Aggregate Functions - SUM, COUNT, AVG, MIN, MAX with examples, interview questions, and practice queries.
---

# 🚀 Day 3: SQL Aggregate Functions

Welcome to **Day 3** of the SQL 15-Day Challenge!  
Today, we’ll explore **Aggregate Functions** that help you summarize and analyze large sets of data.

---

## 📘 What Are Aggregate Functions?

Aggregate functions perform a **calculation on a set of values** and return a **single result**.

---

## 🔹 1. `SUM()`

Returns the total sum of a numeric column.

```sql
SELECT SUM(salary) AS TotalSalary FROM employees;
````

---

## 🔹 2. `COUNT()`

Counts the number of non-null values.

```sql
SELECT COUNT(*) AS TotalEmployees FROM employees;
```

---

## 🔹 3. `AVG()`

Returns the average of a numeric column.

```sql
SELECT AVG(salary) AS AverageSalary FROM employees;
```

---

## 🔹 4. `MIN()`

Returns the smallest value in a column.

```sql
SELECT MIN(salary) AS MinimumSalary FROM employees;
```

---

## 🔹 5. `MAX()`

Returns the largest value in a column.

```sql
SELECT MAX(salary) AS MaximumSalary FROM employees;
```

---

## 🧠 Real-world Example

```sql
SELECT 
    department,
    COUNT(*) AS TotalEmployees,
    AVG(salary) AS AvgSalary,
    MAX(salary) AS MaxSalary,
    MIN(salary) AS MinSalary
FROM employees
GROUP BY department;
```

---

## ❓ Interview Questions

1. Difference between `COUNT(*)` and `COUNT(column_name)`?
2. Can we use `WHERE` with aggregate functions?
3. What does `GROUP BY` do in aggregation?
4. How to get the second highest salary using aggregates?
5. What happens if we use `AVG()` on an empty table?

---

## 💻 Practice Queries

```sql
-- Total quantity sold
SELECT SUM(quantity) FROM sales;

-- Average product price
SELECT AVG(price) FROM products;

-- Count products in each category
SELECT category, COUNT(*) FROM products GROUP BY category;

-- Highest and lowest marks
SELECT MAX(marks), MIN(marks) FROM students;
```

---

## 📌 Key Takeaways

* Aggregate functions return summarized values.
* Commonly used with `GROUP BY` for reporting.
* Useful in dashboards, analytics, and insights.

---

### 🔗 Read Other Days:

👉 [Home - SQL 15-Day Challenge](https://shaiphali123.github.io/sql-15-day-challenge/)

