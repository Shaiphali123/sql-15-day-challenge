# 📋 SQL Complete Cheat Sheet - Quick Reference Guide

## 🎯 Table of Contents
1. [Basic Syntax](#basic-syntax)
2. [Data Types](#data-types)
3. [DDL - Data Definition Language](#ddl-data-definition-language)
4. [DML - Data Manipulation Language](#dml-data-manipulation-language)
5. [SELECT Queries](#select-queries)
6. [Filtering & Conditions](#filtering--conditions)
7. [Joins](#joins)
8. [Grouping & Aggregation](#grouping--aggregation)
9. [Subqueries](#subqueries)
10. [Window Functions](#window-functions)
11. [String Functions](#string-functions)
12. [Date Functions](#date-functions)
13. [Math Functions](#math-functions)
14. [Conditional Logic](#conditional-logic)
15. [Indexes](#indexes)
16. [Views](#views)
17. [Stored Procedures](#stored-procedures)
18. [Triggers](#triggers)
19. [Transactions](#transactions)
20. [Common Patterns](#common-patterns)

---

## 🔷 Basic Syntax

```sql
-- Comments
-- Single line comment
/* Multi-line comment */

-- Basic Query Structure
SELECT column1, column2
FROM table_name
WHERE condition
GROUP BY column1
HAVING group_condition
ORDER BY column1 ASC/DESC
LIMIT 10;
```

---

## 🔷 Data Types

### Common Data Types
```sql
-- Numeric Types
INT, INTEGER           -- Whole numbers
DECIMAL(10,2)         -- Fixed decimal points
FLOAT, REAL           -- Floating point
NUMERIC(10,2)         -- Exact numeric

-- String Types
VARCHAR(255)          -- Variable length string
CHAR(10)             -- Fixed length string
TEXT                 -- Large text data
NVARCHAR(255)        -- Unicode strings

-- Date/Time Types
DATE                 -- Date only (YYYY-MM-DD)
TIME                 -- Time only (HH:MM:SS)
DATETIME             -- Date and time
TIMESTAMP            -- Date and time with timezone

-- Other Types
BOOLEAN              -- True/False
BLOB                 -- Binary data
JSON                 -- JSON data (MySQL 5.7+, PostgreSQL)
```

---

## 🔷 DDL - Data Definition Language

### Create Table
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10,2) DEFAULT 0,
    hire_date DATE,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);
```

### Alter Table
```sql
-- Add column
ALTER TABLE employees ADD COLUMN phone VARCHAR(20);

-- Drop column
ALTER TABLE employees DROP COLUMN phone;

-- Modify column
ALTER TABLE employees MODIFY COLUMN name VARCHAR(150);

-- Rename column
ALTER TABLE employees RENAME COLUMN name TO full_name;

-- Add constraint
ALTER TABLE employees ADD CONSTRAINT chk_salary CHECK (salary > 0);
```

### Drop Table
```sql
DROP TABLE employees;              -- Delete table and data
TRUNCATE TABLE employees;          -- Delete data, keep structure
```

---

## 🔷 DML - Data Manipulation Language

### Insert Data
```sql
-- Single row
INSERT INTO employees (name, email, salary) 
VALUES ('John Doe', 'john@email.com', 50000);

-- Multiple rows
INSERT INTO employees (name, email, salary) VALUES
    ('Jane Smith', 'jane@email.com', 55000),
    ('Bob Johnson', 'bob@email.com', 60000);

-- From another table
INSERT INTO employees_backup 
SELECT * FROM employees WHERE dept_id = 1;
```

### Update Data
```sql
-- Basic update
UPDATE employees 
SET salary = 55000 
WHERE id = 1;

-- Multiple columns
UPDATE employees 
SET salary = salary * 1.1, 
    dept_id = 2 
WHERE hire_date < '2020-01-01';

-- Update with JOIN
UPDATE employees e
JOIN departments d ON e.dept_id = d.id
SET e.salary = e.salary * 1.05
WHERE d.name = 'Engineering';
```

### Delete Data
```sql
-- Basic delete
DELETE FROM employees WHERE id = 1;

-- Delete with condition
DELETE FROM employees 
WHERE hire_date < '2020-01-01' AND salary < 40000;

-- Delete with subquery
DELETE FROM employees 
WHERE dept_id IN (SELECT id FROM departments WHERE budget < 100000);
```

---

## 🔷 SELECT Queries

### Basic SELECT
```sql
-- All columns
SELECT * FROM employees;

-- Specific columns
SELECT name, email, salary FROM employees;

-- Column aliases
SELECT name AS employee_name, 
       salary AS annual_salary 
FROM employees;

-- Calculated columns
SELECT name, 
       salary, 
       salary * 12 AS annual_salary,
       salary * 0.1 AS bonus
FROM employees;
```

### DISTINCT
```sql
-- Unique values
SELECT DISTINCT department FROM employees;

-- Count unique values
SELECT COUNT(DISTINCT department) FROM employees;
```

### LIMIT / TOP
```sql
-- MySQL/PostgreSQL
SELECT * FROM employees LIMIT 10;
SELECT * FROM employees LIMIT 10 OFFSET 20;

-- SQL Server
SELECT TOP 10 * FROM employees;

-- Oracle
SELECT * FROM employees WHERE ROWNUM <= 10;
```

---

## 🔷 Filtering & Conditions

### WHERE Clause
```sql
-- Basic conditions
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM employees WHERE department = 'IT';

-- Multiple conditions
SELECT * FROM employees 
WHERE salary > 40000 AND department = 'IT';

SELECT * FROM employees 
WHERE department = 'IT' OR department = 'HR';

-- BETWEEN
SELECT * FROM employees 
WHERE salary BETWEEN 40000 AND 80000;

-- IN clause
SELECT * FROM employees 
WHERE department IN ('IT', 'HR', 'Finance');

-- NOT IN
SELECT * FROM employees 
WHERE department NOT IN ('IT', 'HR');

-- LIKE patterns
SELECT * FROM employees WHERE name LIKE 'J%';      -- Starts with J
SELECT * FROM employees WHERE name LIKE '%son';    -- Ends with son
SELECT * FROM employees WHERE name LIKE '%an%';    -- Contains an
SELECT * FROM employees WHERE name LIKE 'J_hn';    -- J_hn (4 chars)

-- NULL checks
SELECT * FROM employees WHERE manager_id IS NULL;
SELECT * FROM employees WHERE phone IS NOT NULL;

-- EXISTS
SELECT * FROM employees e
WHERE EXISTS (
    SELECT 1 FROM orders o WHERE o.employee_id = e.id
);
```

---

## 🔷 Joins

### Inner Join
```sql
-- Basic inner join
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;

-- Multiple joins
SELECT e.name, d.department_name, p.project_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id
INNER JOIN employee_projects ep ON e.id = ep.employee_id
INNER JOIN projects p ON ep.project_id = p.id;
```

### Left Join
```sql
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;
```

### Right Join
```sql
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;
```

### Full Outer Join
```sql
SELECT e.name, d.department_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.id;
```

### Cross Join
```sql
SELECT e.name, d.department_name
FROM employees e
CROSS JOIN departments d;
```

### Self Join
```sql
-- Employee and their manager
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.id;
```

---

## 🔷 Grouping & Aggregation

### GROUP BY
```sql
-- Basic grouping
SELECT department, COUNT(*) as employee_count
FROM employees
GROUP BY department;

-- Multiple columns
SELECT department, job_title, COUNT(*) as count
FROM employees
GROUP BY department, job_title;

-- With aggregation functions
SELECT department,
       COUNT(*) as employee_count,
       AVG(salary) as avg_salary,
       SUM(salary) as total_salary,
       MAX(salary) as max_salary,
       MIN(salary) as min_salary
FROM employees
GROUP BY department;
```

### HAVING
```sql
-- Filter groups
SELECT department, COUNT(*) as employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;

-- Multiple HAVING conditions
SELECT department, AVG(salary) as avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000 AND COUNT(*) > 3;
```

### Common Aggregate Functions
```sql
COUNT(*)              -- Count all rows
COUNT(column)         -- Count non-null values
SUM(column)          -- Sum of values
AVG(column)          -- Average value
MAX(column)          -- Maximum value
MIN(column)          -- Minimum value
STDDEV(column)       -- Standard deviation
VARIANCE(column)     -- Variance
```

---

## 🔷 Subqueries

### Scalar Subquery
```sql
-- Returns single value
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### Row Subquery
```sql
-- Returns single row
SELECT * FROM employees
WHERE (department, salary) = (
    SELECT department, MAX(salary) 
    FROM employees 
    WHERE department = 'IT'
);
```

### Column Subquery
```sql
-- Returns multiple values
SELECT * FROM employees
WHERE department IN (
    SELECT name FROM departments WHERE budget > 100000
);
```

### Table Subquery
```sql
-- In FROM clause
SELECT dept_stats.department, dept_stats.avg_salary
FROM (
    SELECT department, AVG(salary) as avg_salary
    FROM employees
    GROUP BY department
) dept_stats
WHERE dept_stats.avg_salary > 50000;
```

### Correlated Subquery
```sql
-- References outer query
SELECT e1.name, e1.salary
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e1.department = e2.department
);
```

---

## 🔷 Window Functions

### ROW_NUMBER
```sql
-- Assign unique row numbers
SELECT name, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) as row_num
FROM employees;

-- Partitioned
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as dept_rank
FROM employees;
```

### RANK / DENSE_RANK
```sql
-- RANK (gaps for ties)
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) as rank
FROM employees;

-- DENSE_RANK (no gaps)
SELECT name, salary,
       DENSE_RANK() OVER (ORDER BY salary DESC) as dense_rank
FROM employees;
```

### LAG / LEAD
```sql
-- Previous row value
SELECT name, salary,
       LAG(salary, 1) OVER (ORDER BY hire_date) as prev_salary
FROM employees;

-- Next row value
SELECT name, salary,
       LEAD(salary, 1) OVER (ORDER BY hire_date) as next_salary
FROM employees;
```

### Aggregate Window Functions
```sql
SELECT name, salary,
       SUM(salary) OVER (PARTITION BY department) as dept_total,
       AVG(salary) OVER (PARTITION BY department) as dept_avg,
       COUNT(*) OVER (PARTITION BY department) as dept_count
FROM employees;
```

### FIRST_VALUE / LAST_VALUE
```sql
SELECT name, department, salary,
       FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary) as min_sal,
       LAST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary) as max_sal
FROM employees;
```

### Running Totals
```sql
SELECT name, salary,
       SUM(salary) OVER (ORDER BY hire_date) as running_total
FROM employees;
```

---

## 🔷 String Functions

### Common String Functions
```sql
-- Length
SELECT LENGTH('Hello World');           -- 11
SELECT CHAR_LENGTH('Hello World');      -- 11

-- Case conversion
SELECT UPPER('hello world');            -- HELLO WORLD
SELECT LOWER('HELLO WORLD');            -- hello world
SELECT INITCAP('hello world');          -- Hello World

-- Trimming
SELECT TRIM('  Hello World  ');         -- 'Hello World'
SELECT LTRIM('  Hello World');          -- 'Hello World'
SELECT RTRIM('Hello World  ');          -- 'Hello World'

-- Substring
SELECT SUBSTRING('Hello World', 1, 5);  -- 'Hello'
SELECT LEFT('Hello World', 5);          -- 'Hello'
SELECT RIGHT('Hello World', 5);         -- 'World'

-- Concatenation
SELECT CONCAT('Hello', ' ', 'World');   -- 'Hello World'
SELECT 'Hello' || ' ' || 'World';       -- 'Hello World' (PostgreSQL)

-- Replace
SELECT REPLACE('Hello World', 'World', 'SQL');  -- 'Hello SQL'

-- Position
SELECT POSITION('World' IN 'Hello World');      -- 7
SELECT CHARINDEX('World', 'Hello World');       -- 7 (SQL Server)

-- Padding
SELECT LPAD('123', 5, '0');             -- '00123'
SELECT RPAD('123', 5, '0');             -- '12300'
```

---

## 🔷 Date Functions

### Current Date/Time
```sql
-- Current date and time
SELECT NOW();                    -- PostgreSQL/MySQL
SELECT GETDATE();               -- SQL Server
SELECT SYSDATE;                 -- Oracle
SELECT CURRENT_TIMESTAMP;      -- Standard SQL

-- Current date only
SELECT CURRENT_DATE;
SELECT CURDATE();               -- MySQL

-- Current time only
SELECT CURRENT_TIME;
SELECT CURTIME();               -- MySQL
```

### Date Formatting
```sql
-- Format dates
SELECT DATE_FORMAT(hire_date, '%Y-%m-%d') FROM employees;     -- MySQL
SELECT TO_CHAR(hire_date, 'YYYY-MM-DD') FROM employees;       -- PostgreSQL/Oracle
SELECT FORMAT(hire_date, 'yyyy-MM-dd') FROM employees;        -- SQL Server
```

### Date Arithmetic
```sql
-- Add/subtract intervals
SELECT hire_date + INTERVAL 1 YEAR FROM employees;            -- MySQL
SELECT hire_date + INTERVAL '1 year' FROM employees;          -- PostgreSQL
SELECT DATEADD(year, 1, hire_date) FROM employees;            -- SQL Server

-- Date differences
SELECT DATEDIFF(CURRENT_DATE, hire_date) as days_employed     -- MySQL
FROM employees;

SELECT CURRENT_DATE - hire_date as days_employed              -- PostgreSQL
FROM employees;
```

### Extract Date Parts
```sql
-- Extract components
SELECT EXTRACT(YEAR FROM hire_date) as hire_year,
       EXTRACT(MONTH FROM hire_date) as hire_month,
       EXTRACT(DAY FROM hire_date) as hire_day
FROM employees;

-- Alternative functions
SELECT YEAR(hire_date), MONTH(hire_date), DAY(hire_date)      -- MySQL
FROM employees;

SELECT DATEPART(year, hire_date), DATEPART(month, hire_date)  -- SQL Server
FROM employees;
```

---

## 🔷 Math Functions

### Basic Math Functions
```sql
-- Arithmetic
SELECT ABS(-15);                 -- 15
SELECT ROUND(15.756, 2);         -- 15.76
SELECT CEILING(15.1);            -- 16
SELECT FLOOR(15.9);              -- 15
SELECT TRUNCATE(15.756, 2);      -- 15.75 (MySQL)
SELECT TRUNC(15.756, 2);         -- 15.75 (Oracle/PostgreSQL)

-- Power and roots
SELECT POWER(2, 3);              -- 8
SELECT SQRT(16);                 -- 4

-- Trigonometric
SELECT PI();                     -- 3.14159...
SELECT SIN(PI()/2);             -- 1
SELECT COS(0);                   -- 1

-- Random
SELECT RAND();                   -- Random between 0 and 1
SELECT RANDOM();                 -- PostgreSQL
```

---

## 🔷 Conditional Logic

### CASE Statement
```sql
-- Simple CASE
SELECT name, salary,
    CASE 
        WHEN salary < 40000 THEN 'Low'
        WHEN salary BETWEEN 40000 AND 70000 THEN 'Medium'
        ELSE 'High'
    END as salary_category
FROM employees;

-- CASE with aggregation
SELECT department,
    SUM(CASE WHEN salary > 50000 THEN 1 ELSE 0 END) as high_earners,
    SUM(CASE WHEN salary <= 50000 THEN 1 ELSE 0 END) as low_earners
FROM employees
GROUP BY department;
```

### NULL Handling
```sql
-- COALESCE (return first non-null)
SELECT name, COALESCE(phone, email, 'No contact') as contact
FROM employees;

-- ISNULL / IFNULL
SELECT name, ISNULL(bonus, 0) as bonus FROM employees;        -- SQL Server
SELECT name, IFNULL(bonus, 0) as bonus FROM employees;        -- MySQL
SELECT name, COALESCE(bonus, 0) as bonus FROM employees;      -- PostgreSQL

-- NULLIF
SELECT NULLIF(department, 'Unknown') FROM employees;
```

---

## 🔷 Indexes

### Create Indexes
```sql
-- Basic index
CREATE INDEX idx_employee_name ON employees(name);

-- Unique index
CREATE UNIQUE INDEX idx_employee_email ON employees(email);

-- Composite index
CREATE INDEX idx_dept_salary ON employees(department, salary);

-- Partial index (PostgreSQL)
CREATE INDEX idx_high_earners ON employees(salary) WHERE salary > 100000;

-- Descending index
CREATE INDEX idx_salary_desc ON employees(salary DESC);
```

### Drop Indexes
```sql
DROP INDEX idx_employee_name;
```

### Index Information
```sql
-- Show indexes (MySQL)
SHOW INDEXES FROM employees;

-- Index usage (PostgreSQL)
SELECT schemaname, tablename, indexname, idx_scan, idx_tup_read
FROM pg_stat_user_indexes;
```

---

## 🔷 Views

### Create Views
```sql
-- Basic view
CREATE VIEW active_employees AS
SELECT name, email, department, salary
FROM employees
WHERE status = 'Active';

-- Complex view
CREATE VIEW department_summary AS
SELECT d.name as department,
       COUNT(e.id) as employee_count,
       AVG(e.salary) as avg_salary,
       SUM(e.salary) as total_payroll
FROM departments d
LEFT JOIN employees e ON d.id = e.dept_id
GROUP BY d.id, d.name;
```

### Use Views
```sql
-- Query view like a table
SELECT * FROM active_employees WHERE department = 'IT';

-- Join views
SELECT ae.name, ds.avg_salary
FROM active_employees ae
JOIN department_summary ds ON ae.department = ds.department;
```

### Modify Views
```sql
-- Update view definition
CREATE OR REPLACE VIEW active_employees AS
SELECT name, email, department, salary, hire_date
FROM employees
WHERE status = 'Active' AND hire_date >= '2020-01-01';

-- Drop view
DROP VIEW active_employees;
```

---

## 🔷 Stored Procedures

### Create Procedure
```sql
-- MySQL/SQL Server
DELIMITER //
CREATE PROCEDURE GetEmployeesByDept(IN dept_name VARCHAR(50))
BEGIN
    SELECT * FROM employees e
    JOIN departments d ON e.dept_id = d.id
    WHERE d.name = dept_name;
END //
DELIMITER ;

-- Execute procedure
CALL GetEmployeesByDept('IT');

-- PostgreSQL
CREATE OR REPLACE FUNCTION get_employees_by_dept(dept_name VARCHAR)
RETURNS TABLE(name VARCHAR, email VARCHAR, salary DECIMAL) AS $$
BEGIN
    RETURN QUERY
    SELECT e.name, e.email, e.salary
    FROM employees e
    JOIN departments d ON e.dept_id = d.id
    WHERE d.name = dept_name;
END;
$$ LANGUAGE plpgsql;

-- Execute function
SELECT * FROM get_employees_by_dept('IT');
```

---

## 🔷 Triggers

### Create Trigger
```sql
-- MySQL
DELIMITER //
CREATE TRIGGER salary_audit
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary != OLD.salary THEN
        INSERT INTO salary_history (employee_id, old_salary, new_salary, change_date)
        VALUES (NEW.id, OLD.salary, NEW.salary, NOW());
    END IF;
END //
DELIMITER ;

-- PostgreSQL
CREATE OR REPLACE FUNCTION audit_salary_change()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.salary != OLD.salary THEN
        INSERT INTO salary_history (employee_id, old_salary, new_salary, change_date)
        VALUES (NEW.id, OLD.salary, NEW.salary, NOW());
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER salary_audit
    AFTER UPDATE ON employees
    FOR EACH ROW
    EXECUTE FUNCTION audit_salary_change();
```

---

## 🔷 Transactions

### Basic Transactions
```sql
-- Start transaction
BEGIN TRANSACTION;  -- SQL Server
BEGIN;              -- PostgreSQL/MySQL
START TRANSACTION;  -- MySQL alternative

-- Your SQL operations
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- Commit or rollback
COMMIT;             -- Save changes
ROLLBACK;           -- Discard changes
```

### Savepoints
```sql
BEGIN;
INSERT INTO employees (name) VALUES ('John Doe');
SAVEPOINT sp1;
INSERT INTO employees (name) VALUES ('Jane Doe');
ROLLBACK TO SAVEPOINT sp1;  -- Only rollback to savepoint
COMMIT;
```

### Transaction Isolation
```sql
-- Set isolation level
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

---

## 🔷 Common Patterns

### Upsert (Insert or Update)
```sql
-- MySQL
INSERT INTO employees (id, name, email) 
VALUES (1, 'John Doe', 'john@email.com')
ON DUPLICATE KEY UPDATE name = VALUES(name), email = VALUES(email);

-- PostgreSQL
INSERT INTO employees (id, name, email) 
VALUES (1, 'John Doe', 'john@email.com')
ON CONFLICT (id) 
DO UPDATE SET name = EXCLUDED.name, email = EXCLUDED.email;

-- SQL Server
MERGE employees AS target
USING (VALUES (1, 'John Doe', 'john@email.com')) AS source (id, name, email)
ON target.id = source.id
WHEN MATCHED THEN UPDATE SET name = source.name, email = source.email
WHEN NOT MATCHED THEN INSERT (id, name, email) VALUES (source.id, source.name, source.email);
```

### Pivot Table
```sql
-- Manual pivot
SELECT 
    department,
    SUM(CASE WHEN job_title = 'Manager' THEN 1 ELSE 0 END) as managers,
    SUM(CASE WHEN job_title = 'Developer' THEN 1 ELSE 0 END) as developers,
    SUM(CASE WHEN job_title = 'Analyst' THEN 1 ELSE 0 END) as analysts
FROM employees
GROUP BY department;

-- SQL Server PIVOT
SELECT department, [Manager], [Developer], [Analyst]
FROM (
    SELECT department, job_title, id
    FROM employees
) AS source_table
PIVOT (
    COUNT(id) FOR job_title IN ([Manager], [Developer], [Analyst])
) AS pivot_table;
```

### Recursive Query (Hierarchy)
```sql
-- Common Table Expression for hierarchy
WITH RECURSIVE employee_hierarchy AS (
    -- Base case
    SELECT id, name, manager_id, 0 as level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case
    SELECT e.id, e.name, e.manager_id, h.level + 1
    FROM employees e
    JOIN employee_hierarchy h ON e.manager_id = h.id
)
SELECT * FROM employee_hierarchy ORDER BY level, name;
```

### Finding Duplicates
```sql
-- Find duplicate records
SELECT email, COUNT(*) as count
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;

-- Get actual duplicate rows
SELECT e1.*
FROM employees e1
JOIN (
    SELECT email
    FROM employees
    GROUP BY email
    HAVING COUNT(*) > 1
) e2 ON e1.email = e2.email;
```

### Row Comparison
```sql
-- Compare consecutive rows
SELECT 
    name,
    salary,
    LAG(salary) OVER (ORDER BY hire_date) as prev_salary,
    salary - LAG(salary) OVER (ORDER BY hire_date) as salary_diff
FROM employees;
```

### Generating Sequences
```sql
-- Generate number sequence (PostgreSQL)
SELECT generate_series(1, 10) as number;

-- MySQL equivalent
SELECT @row_number := @row_number + 1 AS number
FROM employees, (SELECT @row_number := 0) r
LIMIT 10;

-- Find gaps in sequence
WITH numbers AS (
    SELECT generate_series(1, (SELECT MAX(id) FROM employees)) as num
)
SELECT num as missing_id
FROM numbers
LEFT JOIN employees ON numbers.num = employees.id
WHERE employees.id IS NULL;
```

---

## 📚 Quick Tips & Best Practices

### Performance Tips
- Use indexes on frequently queried columns
- Avoid SELECT * in production queries
- Use LIMIT/TOP to restrict large result sets
- Use EXISTS instead of IN for better performance
- Write efficient WHERE clauses

### Code Quality
- Use meaningful table and column aliases
- Format SQL code for readability
- Use consistent naming conventions
- Comment complex queries
- Avoid unnecessary subqueries

### Security
- Use parameterized queries to prevent SQL injection
- Grant minimal necessary permissions
- Regularly backup your databases
- Use transactions for data consistency

---

## 📖 Reference Commands

```sql
-- Database Operations
CREATE DATABASE mydb;
USE mydb;
DROP DATABASE mydb;

-- Show Information
SHOW DATABASES;
SHOW TABLES;
DESCRIBE table_name;
SHOW CREATE TABLE table_name;

-- Permissions
GRANT SELECT, INSERT ON mydb.* TO 'user'@'host';
REVOKE INSERT ON mydb.* FROM 'user'@'host';

-- Backup & Restore (MySQL)
mysqldump -u user -p database_name > backup.sql
mysql -u user -p database_name < backup.sql
```

---

**🎯 This cheat sheet covers 95% of common SQL operations. Bookmark it for quick reference!**

*Happy Querying! 🚀*
