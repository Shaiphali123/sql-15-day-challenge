# ✅ Day 11: SQL Data Manipulation (INSERT, UPDATE, DELETE)

Welcome to Day 11 of the **SQL 15-Day Learning Challenge**! Today, we’ll explore the fundamental **Data Manipulation Language (DML)** statements: `INSERT`, `UPDATE`, and `DELETE`.

---

## 📘 Concepts Covered

### 🔹 INSERT INTO

```sql
-- Syntax:
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);

-- Example:
INSERT INTO Students (StudentID, Name, Age)
VALUES (1, 'Amit', 22);
```

---

### 🔹 UPDATE

```sql
-- Syntax:
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

-- Example:
UPDATE Students
SET Age = 23
WHERE StudentID = 1;
```

---

### 🔹 DELETE

```sql
-- Syntax:
DELETE FROM table_name
WHERE condition;

-- Example:
DELETE FROM Students
WHERE StudentID = 1;
```

> ⚠️ Always use a `WHERE` clause with `UPDATE` and `DELETE` to avoid affecting all rows.

---

## 🧠 Interview Questions

1. What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?
2. What happens if we forget the `WHERE` clause in a `DELETE` statement?
3. Can we insert multiple rows in one `INSERT` query?
4. What is the return value of `UPDATE` or `DELETE` in most SQL engines?
5. How can you undo a `DELETE` in SQL?

---

## 💻 Practice Problems

**Q1:** Insert a new employee into the `Employees` table with Name = 'John', Age = 30, and Department = 'HR'.  
**Q2:** Update the age of employee with ID 3 to 35.  
**Q3:** Delete the employee whose name is 'David'.  
**Q4:** Insert multiple rows into `Departments` table in a single query.  
**Q5:** Delete all rows from `Temporary_Logs` table.

---

## ✅ Sample Answers

```sql
-- Q1
INSERT INTO Employees (Name, Age, Department)
VALUES ('John', 30, 'HR');

-- Q2
UPDATE Employees
SET Age = 35
WHERE EmployeeID = 3;

-- Q3
DELETE FROM Employees
WHERE Name = 'David';

-- Q4
INSERT INTO Departments (DeptID, DeptName)
VALUES (1, 'HR'), (2, 'IT'), (3, 'Finance');

-- Q5
DELETE FROM Temporary_Logs;
```

---

## 📊 Quiz Questions

**Q1.** Which command is used to modify existing records in a table?  
A) INSERT   B) SELECT   C) UPDATE   D) DELETE  
✅ Correct: C

**Q2.** What happens if `WHERE` is missing in an `UPDATE`?  
A) No rows updated  
B) Error  
C) Only the first row is updated  
D) All rows are updated  
✅ Correct: D

---

## 📌 LinkedIn Poll Idea

**Question:** Which of the following operations can **remove data from a table**?  
- A) INSERT  
- B) DELETE  
- C) UPDATE  
- D) SELECT  

✅ Correct Answer: **B**

---

🗓️ Date: 2025-08-05  
🔁 Stay consistent and keep learning!  
