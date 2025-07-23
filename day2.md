

````markdown
---
layout: default
title: "Day 2 - WHERE Clause in SQL"
---

# 📘 Day 2: SQL `WHERE` Clause – Filter Like a Pro!

Welcome to **Day 2** of the **15-Day SQL Challenge** by [Shaivi Connect](https://www.instagram.com/shaiviconnect/)!

Today, we’re diving into one of SQL’s most powerful tools:  
🎯 The **`WHERE` clause** — your ultimate data filter.

---

## 🔍 What is the `WHERE` Clause?

The `WHERE` clause helps filter rows based on **specific conditions**.  
It’s used with `SELECT`, `UPDATE`, and `DELETE` statements.

---

## ✅ Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
````

---

## 🧪 Sample Table: Employees

| EmpID | Name  | Department | Salary |
| ----- | ----- | ---------- | ------ |
| 1     | Alice | HR         | 45000  |
| 2     | Bob   | IT         | 60000  |
| 3     | Carol | IT         | 55000  |
| 4     | Dave  | HR         | 47000  |
| 5     | Emma  | Finance    | 70000  |

---

## 🎯 Example Queries Using WHERE

### 🔹 Employees in IT Department

```sql
SELECT * FROM Employees
WHERE Department = 'IT';
```

### 🔹 Salary > 50000

```sql
SELECT * FROM Employees
WHERE Salary > 50000;
```

### 🔹 Names Starting with 'A'

```sql
SELECT * FROM Employees
WHERE Name LIKE 'A%';
```

### 🔹 Employees Not in HR

```sql
SELECT * FROM Employees
WHERE Department != 'HR';
```

### 🔹 Salary Between 45000 and 65000

```sql
SELECT * FROM Employees
WHERE Salary BETWEEN 45000 AND 65000;
```

---

## 🔁 Using Multiple Conditions

```sql
SELECT * FROM Employees
WHERE Department = 'IT' AND Salary > 55000;
```

```sql
SELECT * FROM Employees
WHERE Department = 'HR' OR Salary < 50000;
```

---

## ❓ WHERE vs HAVING

| Feature        | WHERE                  | HAVING                   |
| -------------- | ---------------------- | ------------------------ |
| Used For       | Rows before grouping   | Groups after aggregation |
| Works On       | SELECT, UPDATE, DELETE | GROUP BY results         |
| Can Use Alias? | ❌ No                   | ✅ Yes                    |

---

## 💼 Top Interview Questions on `WHERE`

1. ✅ What is the purpose of the `WHERE` clause in SQL?
2. ✅ Can we use `WHERE` with `UPDATE` and `DELETE`?
3. ✅ What's the difference between `WHERE` and `HAVING`?
4. ✅ Can `WHERE` be used with `IN`, `BETWEEN`, and `LIKE`?
5. ✅ Write a query to find employees with name starting with ‘S’ and salary above 60,000.
6. ✅ How does `NULL` handling work with the `WHERE` clause?
7. ✅ How to filter based on multiple values using `IN`?
8. ✅ Is `WHERE` clause executed before `GROUP BY`?

---

## 🧠 LinkedIn Poll for Day 2

**Question:**

> Which SQL clause do you use most often during filtering?

* 🔹 WHERE
* 🔸 HAVING
* 🔹 GROUP BY
* 🔸 ORDER BY

🗳️ Cast your vote & comment why 👇
🎯 [@ShaiviConnect on LinkedIn](https://www.linkedin.com/company/107863493)

---

## 🧪 Practice Tasks

Try writing queries using the Employees table:

1. List employees whose names end with 'a'.
2. Show employees with salary not between 50000 and 65000.
3. Get all employees in Finance or HR.
4. Fetch those earning exactly 55000.
5. Display all non-IT employees with salary above 46000.

---

## 🧾 Summary

| Feature      | Description                         |
| ------------ | ----------------------------------- |
| 🔹 WHERE     | Filters rows based on condition     |
| 🔸 Operators | =, !=, <>, >, <, >=, <=             |
| 🔹 Clauses   | Can use IN, BETWEEN, LIKE, IS NULL  |
| 🔸 Combine   | Use AND, OR, NOT for multiple logic |

---

## 📢 Stay Connected – Shaivi Connect 🚀

* 📸 Instagram: [@shaiviconnect](https://www.instagram.com/shaiviconnect/)
* 🌐 Blog: [15 Days SQL Challenge](https://shaiphali123.github.io/sql-15-day-challenge)
* 💼 LinkedIn: [Shaivi Connect](https://www.linkedin.com/company/107863493)
* ▶️ YouTube: [Shaiphali YouTube](https://www.youtube.com/@shaiphali43)

---

## 🎯 Tomorrow’s Topic: ORDER BY Clause 🔽

Stay tuned for Day 3!
Let’s keep learning & growing together 💙
**#ShaiviConnect | #LearnSQL | #Day2SQLChallenge**

```


