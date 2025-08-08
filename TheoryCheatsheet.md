# 🧠 SQL Theory Cheatsheet

Your quick revision guide for SQL basics to intermediate concepts. Perfect for interviews and daily practice.

---

## 1. 📌 Basic SQL Commands

### SELECT
```sql
SELECT column1, column2 FROM table_name;
````

### INSERT

```sql
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
```

### UPDATE

```sql
UPDATE table_name SET column1 = value1 WHERE condition;
```

### DELETE

```sql
DELETE FROM table_name WHERE condition;
```

---

## 2. 📑 SQL Clauses

### WHERE

```sql
SELECT * FROM Employees WHERE age > 30;
```

### ORDER BY

```sql
SELECT * FROM Employees ORDER BY salary DESC;
```

### GROUP BY & HAVING

```sql
SELECT department, COUNT(*) FROM Employees GROUP BY department HAVING COUNT(*) > 5;
```

### DISTINCT

```sql
SELECT DISTINCT department FROM Employees;
```

---

## 3. 🔗 Joins

### INNER JOIN

```sql
SELECT A.name, B.salary FROM Employees A INNER JOIN Salary B ON A.id = B.emp_id;
```

### LEFT JOIN

```sql
SELECT A.name, B.salary FROM Employees A LEFT JOIN Salary B ON A.id = B.emp_id;
```

### RIGHT JOIN

```sql
SELECT A.name, B.salary FROM Employees A RIGHT JOIN Salary B ON A.id = B.emp_id;
```

### FULL JOIN

```sql
SELECT A.name, B.salary FROM Employees A FULL JOIN Salary B ON A.id = B.emp_id;
```

---

## 4. 📊 Aggregate Functions

```sql
SELECT COUNT(*), AVG(salary), MIN(age), MAX(age) FROM Employees;
```

---

## 5. 🔍 Subqueries

```sql
SELECT name FROM Employees WHERE salary > (SELECT AVG(salary) FROM Employees);
```

---

## 6. 🔒 SQL Constraints

* `PRIMARY KEY`
* `FOREIGN KEY`
* `UNIQUE`
* `NOT NULL`
* `CHECK`
* `DEFAULT`

---

## 7. ⚙️ Normalization

* **1NF**: Atomic values only
* **2NF**: 1NF + no partial dependency
* **3NF**: 2NF + no transitive dependency

---

## 8. 🧾 SQL Statement Types

* **DDL**: CREATE, ALTER, DROP
* **DML**: SELECT, INSERT, UPDATE, DELETE
* **DCL**: GRANT, REVOKE
* **TCL**: COMMIT, ROLLBACK, SAVEPOINT

---

## 9. 📚 Indexes & Views

### Index

```sql
CREATE INDEX idx_name ON Employees (name);
```

### View

```sql
CREATE VIEW view_name AS SELECT name, salary FROM Employees;
```

---

## 10. ⚙️ Stored Procedures & Functions

### Stored Procedure

```sql
CREATE PROCEDURE GetEmployees()
BEGIN
  SELECT * FROM Employees;
END;
```

### Function

```sql
CREATE FUNCTION GetTotalEmployees() RETURNS INT
BEGIN
  DECLARE total INT;
  SELECT COUNT(*) INTO total FROM Employees;
  RETURN total;
END;
```

---

## 11. 💡 Interview Tips

* Practice JOINs and subqueries.
* Understand normalization properly.
* Know the differences between WHERE and HAVING.
* Be ready to write queries on paper.

---

Happy Learning! 🚀
