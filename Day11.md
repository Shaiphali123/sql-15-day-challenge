# 📘 Day 11 – SQL Data Manipulation (INSERT, UPDATE, DELETE)

Welcome to Day 11 of the **15-Day SQL Challenge**!  
Today we’ll explore one of the most **frequently used SQL operations** – **Data Manipulation**, focusing on how to:

- 📥 Insert new records (`INSERT`)
- 🔁 Update existing records (`UPDATE`)
- ❌ Delete records (`DELETE`)

Mastering these commands is essential for working with real-world databases.

---

## 🧠 Core Concepts

### 🔹 1. INSERT INTO

Used to add new rows to a table.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
````

**Example:**

```sql
INSERT INTO employees (id, name, salary)
VALUES (101, 'Alice', 50000);
```

👉 You can also insert multiple rows:

```sql
INSERT INTO employees (id, name, salary)
VALUES 
(102, 'Bob', 40000),
(103, 'Carol', 55000);
```

---

### 🔹 2. UPDATE

Used to modify existing data.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Example:**

```sql
UPDATE employees
SET salary = 60000
WHERE id = 101;
```

⚠️ **Always** use the `WHERE` clause, or **all records** will be updated!

---

### 🔹 3. DELETE

Used to remove data from the table.

```sql
DELETE FROM table_name
WHERE condition;
```

**Example:**

```sql
DELETE FROM employees
WHERE id = 101;
```

⚠️ Skipping the `WHERE` clause deletes **all records**!

---

## 💡 Bonus Tips

* Use `TRUNCATE TABLE` to delete all rows quickly (⚠️ can't be rolled back).
* Use `RETURNING` (in some databases) to see what was inserted/updated/deleted.

---

## 📝 Practice Questions

Try writing SQL queries for the following:

1. Insert a new employee into `employees` with `id=201`, `name='John'`, and `salary=45000`.
2. Update John's salary to `50000`.
3. Delete the employee with `id=201`.
4. Insert 3 students into a `students` table with columns `id`, `name`, and `marks`.
5. Update all students with `marks > 90` to add a bonus of `5`.
6. Delete students who failed (marks < 40).
7. Add a new product to a `products` table.
8. Reduce price of all products by 10% using arithmetic operators.
9. Delete all products out of stock (`quantity = 0`).
10. Increase salary of all employees in department 'HR' by 15%.

---

## ✅ Sample Answers

```sql
-- Q1
INSERT INTO employees (id, name, salary)
VALUES (201, 'John', 45000);

-- Q2
UPDATE employees
SET salary = 50000
WHERE id = 201;

-- Q3
DELETE FROM employees
WHERE id = 201;

-- Q5
UPDATE students
SET marks = marks + 5
WHERE marks > 90;

-- Q6
DELETE FROM students
WHERE marks < 40;
```

---

## 📊 Poll Time – Test Your Concept

**Q: What happens if you run the following query without a WHERE clause?**

```sql
UPDATE employees
SET salary = 0;
```

* A) Only one row is updated
* B) No rows are updated
* C) All rows are updated
* D) Query will throw an error

> 💡 **Correct Answer: C) All rows are updated**

---

## 🔍 Interview Tip

**Q: What's the difference between DELETE, TRUNCATE, and DROP?**

| Operation | Removes Data | Rollback Possible | Affects Structure  |
| --------- | ------------ | ----------------- | ------------------ |
| DELETE    | ✅ Yes        | ✅ Yes             | ❌ No               |
| TRUNCATE  | ✅ Yes        | ❌ No              | ❌ No               |
| DROP      | ✅ Yes (all)  | ❌ No              | ✅ Yes (table gone) |

---

## 🔗 Connect With Me

✨ Let’s grow together!

* 💻 [GitHub](https://github.com/Shaiphali123/)
* 📸 [Instagram](https://www.instagram.com/shaiviconnect/).
* 📺 [YouTube](https://www.youtube.com/@shaiphali43)
* 💼 [LinkedIn](https://www.linkedin.com/company/107863493/admin/page-posts/published/)

---

*🚀 Keep going! You're doing great. In **Day 12**, we’ll unlock the magic of **SQL Joins (Inner, Left, Right, Full)**. Stay tuned!*



Let me know if you'd like a **poster**, **HTML version**, or **MCQ quiz questions** for this topic too.
```
