# 📅 Day 13: Stored Procedures & Transactions

Welcome to **Day 13** of the SQL 15-Day Challenge!  
Today we dive into **Stored Procedures** and **Transactions** — two of the most powerful features in SQL that help maintain clean, secure, and consistent database operations.

---

## 🧠 What are Stored Procedures?

A **stored procedure** is a saved collection of one or more SQL statements that can be executed on demand.  
They help encapsulate logic, enhance security, and reduce repetition.

### ✅ Benefits of Stored Procedures:

- Modular and reusable
- Better performance (precompiled)
- Centralized logic
- Enhanced security (no direct table access)

---

## 🧾 Syntax of Stored Procedure

```sql
-- Basic Syntax (MySQL / SQL Server)
DELIMITER //
CREATE PROCEDURE procedure_name()
BEGIN
   -- SQL statements
END //
DELIMITER ;
````

### 🔹 Example:

```sql
DELIMITER //
CREATE PROCEDURE GetAllEmployees()
BEGIN
    SELECT * FROM Employees;
END //
DELIMITER ;
```

### 👇 Calling the Procedure

```sql
CALL GetAllEmployees();
```

---

## 🧠 What are Transactions?

A **transaction** is a sequence of SQL statements treated as a single unit.
It ensures **ACID** properties: Atomicity, Consistency, Isolation, Durability.

### ✅ Useful in:

* Financial operations
* Multi-step updates
* Preventing partial updates

---

## 🔐 ACID Properties

| Property    | Description                             |
| ----------- | --------------------------------------- |
| Atomicity   | All steps complete or none at all       |
| Consistency | Keeps DB in valid state after execution |
| Isolation   | Concurrent transactions don't interfere |
| Durability  | Changes are permanent after commit      |

---

## 🔁 Transaction Control Commands

| Command                        | Description                      |
| ------------------------------ | -------------------------------- |
| `BEGIN` or `START TRANSACTION` | Starts a new transaction         |
| `COMMIT`                       | Saves changes permanently        |
| `ROLLBACK`                     | Undoes changes since last commit |

---

## 💡 Example of a Transaction

```sql
START TRANSACTION;

UPDATE Accounts SET balance = balance - 1000 WHERE account_id = 1;
UPDATE Accounts SET balance = balance + 1000 WHERE account_id = 2;

COMMIT;
```

### ❌ If error happens:

```sql
ROLLBACK;
```

---

## 🧪 Stored Procedure with Transaction Example

```sql
DELIMITER //
CREATE PROCEDURE TransferAmount(IN fromID INT, IN toID INT, IN amt DECIMAL(10,2))
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION 
    BEGIN
        ROLLBACK;
    END;

    START TRANSACTION;
    UPDATE Accounts SET balance = balance - amt WHERE account_id = fromID;
    UPDATE Accounts SET balance = balance + amt WHERE account_id = toID;
    COMMIT;
END //
DELIMITER ;
```

---

## 🎯 Practice SQL Problem

🧩 **Problem**:
Create a stored procedure that accepts a department name and returns the count of employees in that department.

<details>
<summary>💡 Click to view the solution</summary>

```sql
DELIMITER //
CREATE PROCEDURE GetEmployeeCountByDept(IN deptName VARCHAR(100))
BEGIN
    SELECT COUNT(*) AS total_employees 
    FROM Employees 
    WHERE department = deptName;
END //
DELIMITER ;

-- Call the procedure
CALL GetEmployeeCountByDept('Sales');
```

</details>

---

## ❓ Interview Questions on Stored Procedures & Transactions

1. **What is a stored procedure and how is it different from a function?**
2. **Why are stored procedures useful in database design?**
3. **How do you handle errors in stored procedures?**
4. **What are the advantages of using transactions in SQL?**
5. **Explain the ACID properties in detail.**
6. **What is the difference between COMMIT and ROLLBACK?**
7. **How would you use transactions in a money transfer use case?**
8. **Can we call a stored procedure inside another stored procedure?**
9. **What happens if a transaction is not committed?**
10. **How do you debug stored procedures when something goes wrong?**

---

## 🧠 Poll Question (LinkedIn Prompt)

**Which statement is TRUE about SQL Transactions?**
A) Transactions can be undone using COMMIT
B) All SQL queries are auto-committed
C) ROLLBACK permanently saves data
D) COMMIT ensures data is saved permanently

✅ Correct Answer: **D**

---

## 🔗 Useful Resources

* [MySQL Stored Procedures Docs](https://dev.mysql.com/doc/)
* [PostgreSQL Transaction Tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html)
* [ACID Explained](https://en.wikipedia.org/wiki/ACID)

---

## 🏁 That’s a Wrap!

You’ve learned how to:

* Create and use **stored procedures**
* Control data consistency using **transactions**
* Implement real-world logic using both together

📢 **Next Up: Day 14 – SQL Performance Tips**

