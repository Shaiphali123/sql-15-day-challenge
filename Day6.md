# 📘 Day 6 – ORDER BY & LIMIT in SQL

Welcome to **Day 6** of the **SQL 15-Day Challenge with Shaivi Connect**!

---

## 🔍 What You’ll Learn:
- How to sort results using `ORDER BY`
- How to limit the number of records using `LIMIT`
- Practical examples and use-cases
- Interview questions & practice problems

---

## 📌 ORDER BY

The `ORDER BY` clause is used to **sort the result-set** in either ascending or descending order.

**Syntax:**
```sql
SELECT column1, column2  
FROM table_name  
ORDER BY column1 [ASC|DESC];
````

**Example:**

```sql
SELECT * FROM Employees  
ORDER BY salary DESC;
```

➡️ This returns employees sorted from **highest to lowest salary**.

---

## 📌 LIMIT

The `LIMIT` clause is used to **restrict the number of rows returned** by a query.

**Syntax:**

```sql
SELECT column1, column2  
FROM table_name  
LIMIT number;
```

**Example:**

```sql
SELECT * FROM Employees  
LIMIT 3;
```

➡️ This returns only the **first 3 records** from the table.

---

## ✅ Combined Example:

```sql
SELECT name, salary  
FROM Employees  
ORDER BY salary DESC  
LIMIT 5;
```

🎯 This gets the **top 5 highest-paid employees**.

---

## 🎯 Interview Questions:

1. What is the use of the `ORDER BY` clause in SQL?
2. What is the default sorting order when using `ORDER BY`?
3. How do you get the second highest salary using `ORDER BY` and `LIMIT`?
4. Difference between `LIMIT` and `TOP` in SQL?

---

## 💻 Practice SQL Queries:

1. Get the top 3 oldest employees from the `Employees` table.
2. Find the bottom 5 students with the lowest marks from the `Marks` table.
3. Display the youngest 2 employees based on age.

---

## 📊 Poll for LinkedIn:

> ❓ **What’s the default sort order in SQL when you use ORDER BY without ASC or DESC?**

* A) ASC
* B) DESC
* C) Random
* D) None of the above

✅ **Correct Answer: A) ASC**

---

🔗 [Back to Home Page](https://shaiphali123.github.io/sql-15-day-challenge/)

---

✍️ Created with 💙 by [Shaivi Connect](https://www.linkedin.com/in/shaiphali-bhadani-414a0416b/)

```
