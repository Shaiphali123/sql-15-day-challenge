Here’s your **Day 11: SQL Data Manipulation (INSERT, UPDATE, DELETE)** content in **Markdown format** for your GitHub blog:

---

````markdown
# 📘 Day 11 – SQL Data Manipulation (INSERT, UPDATE, DELETE)

Welcome to Day 11 of the **15-Day SQL Challenge**!  
Today we’ll focus on one of the most frequently used SQL operations – **Data Manipulation**, covering:

- `INSERT`: Add new data
- `UPDATE`: Modify existing data
- `DELETE`: Remove data

---

## 🧠 Concepts

### 🔹 INSERT INTO
Used to add new records into a table.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
````

**Example:**

```sql
INSERT INTO employees (id, name, salary)
VALUES (101, 'Alice', 50000);
```

---

### 🔹 UPDATE

Used to modify existing records.

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

❗ Always use the `WHERE` clause, or all rows will be updated.

---

### 🔹 DELETE

Used to delete existing records.

```sql
DELETE FROM table_name
WHERE condition;
```

**Example:**

```sql
DELETE FROM employees
WHERE id = 101;
```

❗ Without `WHERE`, **all** rows will be deleted!

---

## 🎯 Practice Questions

1. Insert a new product into a `products` table with id 501, name 'Laptop', and price 45000.
2. Update the price of the product with id 501 to 42000.
3. Delete the product with id 501 from the `products` table.
4. Insert 3 new rows into a `students` table.
5. Update all student names to uppercase using `UPPER()` function.
6. Delete all students with marks below 40.

---

## ✅ Sample Answers

```sql
-- Q1
INSERT INTO products (id, name, price)
VALUES (501, 'Laptop', 45000);

-- Q2
UPDATE products
SET price = 42000
WHERE id = 501;

-- Q3
DELETE FROM products
WHERE id = 501;
```

---

## 📊 Poll Time (Test Your Concept)

**Q: What happens if you run `UPDATE employees SET salary = 0;` without a WHERE clause?**

* A) Only one row is updated
* B) No rows are updated
* C) All rows are updated
* D) Query will throw an error

> 💡 Correct Answer: **C) All rows are updated**

---

## 🔗 Connect With Me

* 📘 [GitHub](https://github.com/your-profile)
* 📸 [Instagram](https://instagram.com/your-profile)
* 📺 [YouTube](https://youtube.com/your-channel)

---

*✨ Keep practicing. Tomorrow, we dive into **SQL Joins (Inner, Left, Right, Full)**. Stay tuned!*

Let me know if you’d like a matching poster or HTML version for your blog as well!
```
