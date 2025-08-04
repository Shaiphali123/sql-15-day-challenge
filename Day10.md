# 🧩 Day 10 – SQL Functions: Built-in & User Defined

Welcome to **Day 10** of the **30-Day SQL Coding Interview Challenge**!  
Today, we’re learning how SQL uses **functions** to make queries cleaner, faster, and reusable.

---

## 🔹 What is a Function in SQL?

A **function** in SQL is like a mini-program that does a task and gives you a result.

There are **two types**:

1. **Built-in Functions** – Already available in SQL.
2. **User Defined Functions (UDFs)** – You create your own.

---

## ✅ Built-in SQL Functions

These are ready-to-use and work in most SQL databases.

### 📌 Examples:

#### 📦 String Functions:
- `UPPER('abc')` → `ABC`
- `LENGTH('SQL')` → `3`
- `CONCAT('Hello', 'World')` → `HelloWorld`

#### 🔢 Math Functions:
- `ABS(-10)` → `10`
- `ROUND(3.1415, 2)` → `3.14`

#### 📅 Date Functions:
- `NOW()` → Current date/time
- `DATEDIFF('2025-08-04', '2025-08-01')` → `3`

#### 📊 Aggregate Functions:
- `COUNT(*)`, `SUM(column)`, `AVG(column)`

---

## ✅ User Defined Functions (UDFs)

These are **custom functions** you create when built-in ones aren’t enough.

### 🛠️ Example:

```sql
CREATE FUNCTION get_discount(price DECIMAL(10,2))
RETURNS DECIMAL(10,2)
BEGIN
  RETURN price * 0.90;
END;
````

You can now use `get_discount(price)` in your queries!

---

## 🧠 Practice Tasks

1. Use `SUBSTRING()` to get the domain from email addresses
   Example: `john@example.com` → `example.com`

2. Write a UDF to calculate the price *after tax*

```sql
CREATE FUNCTION total_price(price DECIMAL(10,2), tax DECIMAL(5,2))
RETURNS DECIMAL(10,2)
BEGIN
  RETURN price + (price * tax);
END;
```

---

## 💡 Bonus Challenge

Write a UDF to check if a number is a **palindrome** (e.g., `121`, `1331`).

Can you rewrite any old query using a **new** built-in function today?

---

## 📚 Useful Links

* [PostgreSQL Built-in Functions](https://www.postgresql.org/docs/current/functions.html)
* [MySQL User-Defined Functions](https://dev.mysql.com/doc/refman/8.0/en/create-function-udf.html)

---

### 🔍 Summary

* Functions make your code **shorter**, **cleaner**, and **faster**.
* Use **built-in** ones when possible.
* Create **UDFs** for custom logic.

---

📝 View Notes | 🧠 View Problems | ✅ View Solutions
**#Day10 #SQLFunctions #ShaiviConnect #LearnSQL**


