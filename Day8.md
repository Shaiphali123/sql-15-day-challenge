
# 📘 Day 8 – SQL Constraints & Keys | #SQL15DayChallenge by Shaivi Connect

Welcome to **Day 8** of the **#SQL15DayChallenge** 🚀  
Today, we dive into **SQL Constraints and Keys** – the foundation of data integrity and relational structure.

---

## 🔐 What Are SQL Constraints?

SQL **constraints** are rules enforced on data in tables. They ensure **accuracy**, **reliability**, and **validity**.

### ✅ Common SQL Constraints:

| Constraint | Description |
|-----------|-------------|
| `NOT NULL` | Ensures a column cannot have NULL value |
| `UNIQUE` | Ensures all values in a column are different |
| `PRIMARY KEY` | Combines NOT NULL + UNIQUE. Uniquely identifies each record |
| `FOREIGN KEY` | Links one table’s column to another table’s PRIMARY KEY |
| `CHECK` | Ensures a value meets a specific condition |
| `DEFAULT` | Sets a default value for a column if no value is provided |

---

## 🔑 SQL KEYS – PRIMARY & FOREIGN

### 🔹 Primary Key

- A column (or combination) that uniquely identifies each row.
- **Only one** primary key per table.
- Cannot be `NULL`.

```sql
CREATE TABLE Students (
  StudentID INT PRIMARY KEY,
  Name VARCHAR(50),
  Age INT
);
````

### 🔹 Foreign Key

* A column that creates a **relationship** between two tables.
* References the **primary key** of another table.

```sql
CREATE TABLE Orders (
  OrderID INT PRIMARY KEY,
  StudentID INT,
  FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);
```

---

## 🛠 Example: With All Constraints

```sql
CREATE TABLE Employees (
  EmpID INT PRIMARY KEY,
  Name VARCHAR(50) NOT NULL,
  Email VARCHAR(100) UNIQUE,
  Age INT CHECK (Age >= 18),
  Department VARCHAR(50) DEFAULT 'IT'
);
```

---

## 🎯 Interview Questions

1. 🔹 What is the difference between PRIMARY KEY and UNIQUE?
2. 🔹 Can a table have multiple UNIQUE constraints?
3. 🔹 What happens if you try to insert a NULL into a NOT NULL column?
4. 🔹 What is the role of FOREIGN KEY in normalization?
5. 🔹 Can a table have multiple FOREIGN KEYS?

---

## 💡 Poll Question

> What does the `CHECK` constraint do in SQL?

* A) Ensures no NULL values
* B) Prevents duplicate values
* ✅ C) Validates a column's value against a condition
* D) Links tables together

---

## 🔗 Follow the Series

Keep learning daily with hands-on SQL lessons!

**GitHub:** [Shaivi Connect](https://shaiphali123.github.io/sql-15-day-challenge/)
**Instagram | YouTube | LinkedIn:** `@shaiviconnect`

---

> 🚀 *“Constraints are the soul of clean data!” – Day 8 Complete!*

```



Let me know what you want next: Day 9 (Joins), CI/CD questions, or anything else!
```
