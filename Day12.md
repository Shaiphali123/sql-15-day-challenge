# 📘 Day 12: SQL Data Definition (CREATE, DROP, ALTER)

Welcome to **Day 12** of the **SQL 15-Day Challenge**!  
Today we will focus on **Data Definition Language (DDL)** which includes:

- `CREATE`: to create new database objects
- `DROP`: to remove objects
- `ALTER`: to modify existing objects

---

## ✅ What is DDL?

DDL stands for **Data Definition Language**. It is used to define and modify the structure of database objects like **tables**, **schemas**, **indexes**, etc.

---

## 1️⃣ CREATE Statement

Used to create new database objects like tables, views, databases.

### 🔹 Syntax:

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
````

### 🔸 Example:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10, 2)
);
```

---

## 2️⃣ DROP Statement

Used to delete database objects permanently.

### 🔹 Syntax:

```sql
DROP TABLE table_name;
```

### 🔸 Example:

```sql
DROP TABLE employees;
```

⚠️ **Caution:** All data in the table will be lost permanently.

---

## 3️⃣ ALTER Statement

Used to **add**, **modify**, or **drop** columns in an existing table.

### 🔹 Syntax to add a column:

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### 🔹 Syntax to modify a column:

```sql
ALTER TABLE table_name
MODIFY column_name new_datatype;
```

### 🔹 Syntax to drop a column:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### 🔸 Example:

```sql
ALTER TABLE employees
ADD department VARCHAR(30);
```

---

## 🧠 Interview Questions

1. What is the difference between DDL and DML?
2. Can you undo a DROP statement?
3. What is the difference between ALTER and UPDATE?
4. How do you change the data type of a column?
5. Can you rename a column using ALTER?

---

## 🧪 Practice Questions

1. Create a table `books` with columns: `book_id`, `title`, `author`, `price`.
2. Add a new column `publisher` to `books` table.
3. Drop the column `price` from `books`.
4. Modify the column `title` to increase its size to 100 characters.
5. Drop the `books` table.

---

## 🔗 Explore More

[🔗 View Full Series](https://shaiphali123.github.io/sql-15-day-challenge/)

---

### 🚀 Keep Learning, Keep Practicing!


