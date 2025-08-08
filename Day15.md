# 🎯 Day 15: SQL Interview Q&A + Final Project

## ✅ Introduction

**Welcome to Day 15 of the SQL 15-Day Challenge!** 🚀

Congratulations on reaching the final day of our intensive SQL journey! Over the past 14 days, you've mastered the fundamentals of SQL, from basic SELECT statements to advanced window functions and optimization techniques. Today marks the culmination of your learning with a comprehensive review and a real-world project that will solidify your understanding.

### Purpose of Day 15:
- **Comprehensive Review**: Master the most frequently asked SQL interview questions
- **Practical Application**: Build a complete employee management system
- **Career Preparation**: Gain confidence for technical interviews
- **Portfolio Development**: Create a showcase project for potential employers

Let's make this final day count! 💪

---

## 💬 SQL Interview Q&A

### 🔵 Basic SQL

**Q1: What is SQL and what are its main types of statements?**

**Answer:** SQL (Structured Query Language) is a standardized language for managing and manipulating relational databases. The main types of SQL statements are:
- **DDL (Data Definition Language)**: CREATE, ALTER, DROP, TRUNCATE
- **DML (Data Manipulation Language)**: INSERT, UPDATE, DELETE, SELECT
- **DCL (Data Control Language)**: GRANT, REVOKE
- **TCL (Transaction Control Language)**: COMMIT, ROLLBACK, SAVEPOINT

**Q2: What's the difference between DELETE, DROP, and TRUNCATE?**

**Answer:**
- **DELETE**: Removes rows from a table based on conditions. Can be rolled back, slower, triggers fire
```sql
DELETE FROM employees WHERE salary < 30000;
```
- **DROP**: Removes the entire table structure and data. Cannot be rolled back
```sql
DROP TABLE employees;
```
- **TRUNCATE**: Removes all rows but keeps table structure. Faster than DELETE, cannot be rolled back
```sql
TRUNCATE TABLE employees;
```

**Q3: Explain the difference between CHAR and VARCHAR data types.**

**Answer:**
- **CHAR(n)**: Fixed-length string, padded with spaces. Faster for fixed-size data
- **VARCHAR(n)**: Variable-length string, uses only needed space. More memory efficient

```sql
-- CHAR(10) always uses 10 bytes, even for 'John' (padded as 'John      ')
-- VARCHAR(10) uses only 4 bytes for 'John'
```

### 🔵 Joins

**Q4: Explain different types of JOINs with examples.**

**Answer:**

```sql
-- INNER JOIN: Returns matching records from both tables
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;

-- LEFT JOIN: Returns all records from left table, matching from right
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;

-- RIGHT JOIN: Returns all records from right table, matching from left
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;

-- FULL OUTER JOIN: Returns all records when there's a match in either table
SELECT e.name, d.department_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id;

-- CROSS JOIN: Cartesian product of both tables
SELECT e.name, d.department_name
FROM employees e
CROSS JOIN departments d;
```

**Q5: What is a self-join? Provide an example.**

**Answer:** A self-join is when a table is joined with itself to compare rows within the same table.

```sql
-- Find employees and their managers
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id;
```

### 🔵 Aggregation & Grouping

**Q6: What's the difference between WHERE and HAVING clauses?**

**Answer:**
- **WHERE**: Filters rows before grouping, cannot use aggregate functions
- **HAVING**: Filters groups after GROUP BY, can use aggregate functions

```sql
-- WHERE: Filter before grouping
SELECT department, AVG(salary)
FROM employees
WHERE salary > 50000  -- Filters individual rows
GROUP BY department;

-- HAVING: Filter after grouping
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;  -- Filters groups
```

**Q7: Explain GROUP BY and common aggregate functions.**

**Answer:** GROUP BY groups rows with same values. Common aggregate functions:

```sql
SELECT 
    department,
    COUNT(*) as employee_count,
    SUM(salary) as total_salary,
    AVG(salary) as average_salary,
    MAX(salary) as highest_salary,
    MIN(salary) as lowest_salary
FROM employees
GROUP BY department;
```

### 🔵 Filtering & WHERE/HAVING

**Q8: What are the different operators used in WHERE clause?**

**Answer:**
```sql
-- Comparison operators
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM employees WHERE name = 'John';

-- Logical operators
SELECT * FROM employees WHERE salary > 40000 AND department = 'IT';
SELECT * FROM employees WHERE department = 'HR' OR department = 'Finance';

-- Pattern matching
SELECT * FROM employees WHERE name LIKE 'J%';  -- Starts with J
SELECT * FROM employees WHERE name LIKE '%son';  -- Ends with son

-- Range and list
SELECT * FROM employees WHERE salary BETWEEN 40000 AND 80000;
SELECT * FROM employees WHERE department IN ('IT', 'HR', 'Finance');

-- NULL checks
SELECT * FROM employees WHERE manager_id IS NULL;
SELECT * FROM employees WHERE phone IS NOT NULL;
```

### 🔵 Subqueries

**Q9: What are subqueries and their types?**

**Answer:** Subqueries are queries nested inside other queries. Types:

```sql
-- Scalar subquery (returns single value)
SELECT name FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Row subquery (returns single row)
SELECT * FROM employees 
WHERE (department, salary) = (SELECT department, MAX(salary) 
                              FROM employees WHERE department = 'IT');

-- Column subquery (returns multiple values)
SELECT * FROM employees 
WHERE department IN (SELECT department FROM departments 
                     WHERE budget > 100000);

-- Table subquery (returns multiple rows and columns)
SELECT e.name, dept_avg.avg_sal
FROM employees e
JOIN (SELECT department, AVG(salary) as avg_sal 
      FROM employees GROUP BY department) dept_avg
ON e.department = dept_avg.department;
```

**Q10: What's the difference between correlated and non-correlated subqueries?**

**Answer:**
```sql
-- Non-correlated: Inner query executes once
SELECT name FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Correlated: Inner query executes for each row of outer query
SELECT name FROM employees e1
WHERE salary > (SELECT AVG(salary) FROM employees e2 
                WHERE e1.department = e2.department);
```

### 🔵 Window Functions

**Q11: Explain window functions and their syntax.**

**Answer:** Window functions perform calculations across related rows without collapsing the result set.

```sql
-- Basic syntax: function() OVER (PARTITION BY ... ORDER BY ...)

-- ROW_NUMBER: Assigns unique sequential numbers
SELECT name, salary, 
       ROW_NUMBER() OVER (ORDER BY salary DESC) as rank
FROM employees;

-- RANK: Assigns rank with gaps for ties
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) as rank
FROM employees;

-- DENSE_RANK: Assigns rank without gaps
SELECT name, salary,
       DENSE_RANK() OVER (ORDER BY salary DESC) as dense_rank
FROM employees;

-- Partitioned window functions
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as dept_rank
FROM employees;
```

**Q12: What are LAG and LEAD functions?**

**Answer:** LAG and LEAD access previous and next row values.

```sql
-- LAG: Get previous row value
SELECT name, salary,
       LAG(salary, 1) OVER (ORDER BY hire_date) as prev_salary
FROM employees;

-- LEAD: Get next row value
SELECT name, salary,
       LEAD(salary, 1) OVER (ORDER BY hire_date) as next_salary
FROM employees;

-- Calculate salary difference from previous employee
SELECT name, salary,
       salary - LAG(salary) OVER (ORDER BY hire_date) as salary_diff
FROM employees;
```

### 🔵 Indexes and Views

**Q13: What are indexes and their types?**

**Answer:** Indexes improve query performance by creating fast access paths to data.

```sql
-- Create unique index
CREATE UNIQUE INDEX idx_employee_email ON employees(email);

-- Create composite index
CREATE INDEX idx_dept_salary ON employees(department, salary);

-- Create partial index (PostgreSQL)
CREATE INDEX idx_high_earners ON employees(salary) WHERE salary > 100000;

-- View index usage
EXPLAIN SELECT * FROM employees WHERE email = 'john@example.com';
```

**Q14: What are views and their advantages?**

**Answer:** Views are virtual tables based on SQL queries.

```sql
-- Create a view
CREATE VIEW high_earners AS
SELECT name, department, salary
FROM employees
WHERE salary > 80000;

-- Use the view
SELECT * FROM high_earners WHERE department = 'IT';

-- Update view (if updatable)
UPDATE high_earners SET salary = salary * 1.1 WHERE department = 'IT';
```

**Advantages:**
- Security (hide sensitive columns)
- Simplification (complex queries as simple tables)
- Reusability
- Logical data independence

### 🔵 SQL Optimization

**Q15: How do you optimize SQL queries?**

**Answer:**
1. **Use indexes** on frequently queried columns
2. **Avoid SELECT \***, specify needed columns
3. **Use WHERE clauses** to limit data early
4. **Optimize JOINs** (use appropriate join types)
5. **Use LIMIT** for large result sets
6. **Analyze execution plans**

```sql
-- Instead of this:
SELECT * FROM employees e 
JOIN departments d ON e.dept_id = d.dept_id
WHERE e.salary > 50000;

-- Do this:
SELECT e.name, e.salary, d.department_name 
FROM employees e 
JOIN departments d ON e.dept_id = d.dept_id
WHERE e.salary > 50000
LIMIT 100;
```

**Q16: What is query execution plan?**

**Answer:** Shows how the database executes a query.

```sql
-- PostgreSQL/MySQL
EXPLAIN SELECT * FROM employees WHERE department = 'IT';

-- SQL Server
SET SHOWPLAN_ALL ON
SELECT * FROM employees WHERE department = 'IT';

-- Oracle
EXPLAIN PLAN FOR SELECT * FROM employees WHERE department = 'IT';
```

### 🔵 Transactions and ACID

**Q17: What are ACID properties?**

**Answer:**
- **Atomicity**: All operations in transaction succeed or fail together
- **Consistency**: Database remains in valid state
- **Isolation**: Concurrent transactions don't interfere
- **Durability**: Committed changes persist permanently

```sql
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;  -- Both updates succeed, or both fail
```

**Q18: What are transaction isolation levels?**

**Answer:**
1. **READ UNCOMMITTED**: Allows dirty reads
2. **READ COMMITTED**: Prevents dirty reads
3. **REPEATABLE READ**: Prevents dirty and non-repeatable reads
4. **SERIALIZABLE**: Highest isolation, prevents all phenomena

```sql
-- Set isolation level
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

### 🔵 Stored Procedures and Functions

**Q19: What's the difference between stored procedures and functions?**

**Answer:**

**Stored Procedures:**
```sql
-- Create procedure
CREATE PROCEDURE GetEmployeesByDept(@dept VARCHAR(50))
AS
BEGIN
    SELECT * FROM employees WHERE department = @dept;
END;

-- Execute
EXEC GetEmployeesByDept 'IT';
```

**Functions:**
```sql
-- Create function
CREATE FUNCTION CalculateBonus(@salary DECIMAL)
RETURNS DECIMAL
AS
BEGIN
    RETURN @salary * 0.1;
END;

-- Use function
SELECT name, salary, dbo.CalculateBonus(salary) as bonus
FROM employees;
```

**Q20: What are triggers?**

**Answer:** Triggers are special stored procedures that execute automatically.

```sql
-- Create audit trigger
CREATE TRIGGER salary_audit
ON employees
AFTER UPDATE
AS
BEGIN
    IF UPDATE(salary)
    INSERT INTO salary_history (emp_id, old_salary, new_salary, change_date)
    SELECT d.employee_id, d.salary, i.salary, GETDATE()
    FROM deleted d
    JOIN inserted i ON d.employee_id = i.employee_id;
END;
```

### 🔵 Advanced Concepts

**Q21: What are Common Table Expressions (CTEs)?**

**Answer:** CTEs create temporary named result sets.

```sql
-- Simple CTE
WITH high_earners AS (
    SELECT name, salary, department
    FROM employees
    WHERE salary > 80000
)
SELECT department, COUNT(*) as count
FROM high_earners
GROUP BY department;

-- Recursive CTE (employee hierarchy)
WITH employee_hierarchy AS (
    -- Base case: top-level managers
    SELECT employee_id, name, manager_id, 0 as level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case
    SELECT e.employee_id, e.name, e.manager_id, h.level + 1
    FROM employees e
    JOIN employee_hierarchy h ON e.manager_id = h.employee_id
)
SELECT * FROM employee_hierarchy;
```

**Q22: What is CASE statement?**

**Answer:** CASE provides conditional logic in SQL.

```sql
-- Simple CASE
SELECT name, salary,
    CASE 
        WHEN salary < 40000 THEN 'Low'
        WHEN salary BETWEEN 40000 AND 80000 THEN 'Medium'
        ELSE 'High'
    END as salary_category
FROM employees;

-- CASE in WHERE clause
SELECT * FROM employees
WHERE CASE 
    WHEN department = 'IT' THEN salary > 70000
    WHEN department = 'HR' THEN salary > 50000
    ELSE salary > 40000
END;
```

**Q23: How do you handle NULL values?**

**Answer:**
```sql
-- Check for NULL
SELECT * FROM employees WHERE phone IS NULL;
SELECT * FROM employees WHERE phone IS NOT NULL;

-- Replace NULL values
SELECT name, COALESCE(phone, 'Not provided') as contact
FROM employees;

-- NULL in calculations
SELECT name, salary, ISNULL(bonus, 0) as bonus,
       salary + ISNULL(bonus, 0) as total_compensation
FROM employees;
```

**Q24: What are database constraints?**

**Answer:**
```sql
-- PRIMARY KEY
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

-- FOREIGN KEY
CREATE TABLE orders (
    id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

-- CHECK constraint
ALTER TABLE employees 
ADD CONSTRAINT chk_salary CHECK (salary > 0);

-- UNIQUE constraint
ALTER TABLE employees 
ADD CONSTRAINT uk_email UNIQUE (email);
```

**Q25: What is database normalization?**

**Answer:** Process of organizing data to reduce redundancy.

**Normal Forms:**
- **1NF**: Atomic values, unique column names
- **2NF**: 1NF + no partial dependencies
- **3NF**: 2NF + no transitive dependencies
- **BCNF**: 3NF + every determinant is a candidate key

```sql
-- Unnormalized
CREATE TABLE orders (
    order_id INT,
    customer_name VARCHAR(100),
    customer_email VARCHAR(100),
    product1 VARCHAR(100),
    product2 VARCHAR(100)
);

-- Normalized (3NF)
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
);
```

---

## 💡 SQL Query Bank

### Problem 1: Employee Salary Analysis
**Query:** Find employees earning more than the average salary in their department.
```sql
SELECT e.name, e.department, e.salary, dept_avg.avg_salary
FROM employees e
JOIN (
    SELECT department, AVG(salary) as avg_salary
    FROM employees
    GROUP BY department
) dept_avg ON e.department = dept_avg.department
WHERE e.salary > dept_avg.avg_salary;
```

### Problem 2: Top N Records per Group
**Query:** Find top 3 highest-paid employees in each department.
```sql
WITH ranked_employees AS (
    SELECT name, department, salary,
           ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rn
    FROM employees
)
SELECT name, department, salary
FROM ranked_employees
WHERE rn <= 3;
```

### Problem 3: Running Total
**Query:** Calculate running total of salaries by hire date.
```sql
SELECT name, hire_date, salary,
       SUM(salary) OVER (ORDER BY hire_date) as running_total
FROM employees
ORDER BY hire_date;
```

### Problem 4: Find Gaps in Sequential Data
**Query:** Find missing employee IDs in sequence.
```sql
WITH number_series AS (
    SELECT generate_series(1, (SELECT MAX(employee_id) FROM employees)) as id
)
SELECT ns.id as missing_id
FROM number_series ns
LEFT JOIN employees e ON ns.id = e.employee_id
WHERE e.employee_id IS NULL;
```

### Problem 5: Pivot Data
**Query:** Show department-wise employee count by job title.
```sql
SELECT department,
       SUM(CASE WHEN job_title = 'Manager' THEN 1 ELSE 0 END) as managers,
       SUM(CASE WHEN job_title = 'Developer' THEN 1 ELSE 0 END) as developers,
       SUM(CASE WHEN job_title = 'Analyst' THEN 1 ELSE 0 END) as analysts
FROM employees
GROUP BY department;
```

### Problem 6: Hierarchical Data
**Query:** Show employee hierarchy with levels.
```sql
WITH RECURSIVE emp_hierarchy AS (
    SELECT employee_id, name, manager_id, 0 as level, name as path
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    SELECT e.employee_id, e.name, e.manager_id, h.level + 1,
           h.path || ' -> ' || e.name
    FROM employees e
    JOIN emp_hierarchy h ON e.manager_id = h.employee_id
)
SELECT * FROM emp_hierarchy ORDER BY level, name;
```

### Problem 7: Consecutive Records
**Query:** Find employees with consecutive employee IDs.
```sql
SELECT e1.employee_id, e1.name,
       e2.employee_id as next_id, e2.name as next_name
FROM employees e1
JOIN employees e2 ON e1.employee_id + 1 = e2.employee_id
ORDER BY e1.employee_id;
```

### Problem 8: Duplicate Detection
**Query:** Find duplicate email addresses.
```sql
SELECT email, COUNT(*) as count
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

### Problem 9: Date Range Analysis
**Query:** Find employees hired in the last 30 days of each year.
```sql
SELECT name, hire_date
FROM employees
WHERE EXTRACT(DAY FROM (DATE_TRUNC('year', hire_date) + INTERVAL '1 year' - hire_date)) <= 30;
```

### Problem 10: Complex Aggregation
**Query:** Department statistics with multiple metrics.
```sql
SELECT 
    department,
    COUNT(*) as employee_count,
    AVG(salary) as avg_salary,
    MEDIAN(salary) as median_salary,
    STDDEV(salary) as salary_stddev,
    MIN(hire_date) as oldest_hire,
    MAX(hire_date) as newest_hire
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;
```

---

## 🚀 Mini Project: Company Employee Management Database

### Project Objective
Create a comprehensive employee management system that demonstrates real-world SQL skills. This project simulates a company database with employees, departments, projects, and salary tracking.

### Database Schema

#### 1. Departments Table
```sql
CREATE TABLE departments (
    dept_id SERIAL PRIMARY KEY,
    dept_name VARCHAR(100) NOT NULL UNIQUE,
    manager_id INT,
    budget DECIMAL(12,2),
    location VARCHAR(100),
    created_date DATE DEFAULT CURRENT_DATE
);
```

#### 2. Employees Table
```sql
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(20),
    hire_date DATE NOT NULL,
    job_title VARCHAR(100),
    dept_id INT,
    manager_id INT,
    salary DECIMAL(10,2),
    status VARCHAR(20) DEFAULT 'Active',
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id),
    FOREIGN KEY (manager_id) REFERENCES employees(employee_id)
);
```

#### 3. Projects Table
```sql
CREATE TABLE projects (
    project_id SERIAL PRIMARY KEY,
    project_name VARCHAR(150) NOT NULL,
    description TEXT,
    start_date DATE,
    end_date DATE,
    budget DECIMAL(12,2),
    status VARCHAR(20) DEFAULT 'Planning',
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```

#### 4. Employee_Projects Table (Many-to-Many)
```sql
CREATE TABLE employee_projects (
    emp_project_id SERIAL PRIMARY KEY,
    employee_id INT,
    project_id INT,
    role_in_project VARCHAR(100),
    start_date DATE,
    end_date DATE,
    hours_allocated DECIMAL(5,2),
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id),
    FOREIGN KEY (project_id) REFERENCES projects(project_id)
);
```

#### 5. Salary_History Table
```sql
CREATE TABLE salary_history (
    history_id SERIAL PRIMARY KEY,
    employee_id INT,
    old_salary DECIMAL(10,2),
    new_salary DECIMAL(10,2),
    change_date DATE DEFAULT CURRENT_DATE,
    reason VARCHAR(200),
    changed_by INT,
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id),
    FOREIGN KEY (changed_by) REFERENCES employees(employee_id)
);
```

### Sample Data Insertion

#### Insert Departments
```sql
INSERT INTO departments (dept_name, budget, location) VALUES
('Information Technology', 2500000.00, 'New York'),
('Human Resources', 800000.00, 'Chicago'),
('Finance', 1200000.00, 'Boston'),
('Marketing', 1500000.00, 'Los Angeles'),
('Operations', 2000000.00, 'Dallas');
```

#### Insert Employees
```sql
INSERT INTO employees (first_name, last_name, email, phone, hire_date, job_title, dept_id, salary) VALUES
('John', 'Smith', 'john.smith@company.com', '555-0101', '2020-01-15', 'IT Director', 1, 95000.00),
('Sarah', 'Johnson', 'sarah.johnson@company.com', '555-0102', '2020-03-22', 'Senior Developer', 1, 78000.00),
('Mike', 'Brown', 'mike.brown@company.com', '555-0103', '2021-06-10', 'DevOps Engineer', 1, 72000.00),
('Emily', 'Davis', 'emily.davis@company.com', '555-0104', '2019-11-05', 'HR Manager', 2, 68000.00),
('Robert', 'Wilson', 'robert.wilson@company.com', '555-0105', '2022-02-14', 'Recruiter', 2, 52000.00),
('Lisa', 'Anderson', 'lisa.anderson@company.com', '555-0106', '2020-07-20', 'Financial Analyst', 3, 63000.00),
('David', 'Taylor', 'david.taylor@company.com', '555-0107', '2021-09-12', 'Accountant', 3, 58000.00),
('Jennifer', 'Thomas', 'jennifer.thomas@company.com', '555-0108', '2022-01-30', 'Marketing Manager', 4, 71000.00),
('James', 'Garcia', 'james.garcia@company.com', '555-0109', '2021-04-18', 'Digital Marketing Specialist', 4, 55000.00),
('Maria', 'Rodriguez', 'maria.rodriguez@company.com', '555-0110', '2020-12-03', 'Operations Manager', 5, 74000.00);

-- Update manager relationships
UPDATE employees SET manager_id = 1 WHERE employee_id IN (2, 3);
UPDATE employees SET manager_id = 4 WHERE employee_id = 5;
UPDATE employees SET manager_id = 6 WHERE employee_id = 7;
UPDATE employees SET manager_id = 8 WHERE employee_id = 9;

-- Update department managers
UPDATE departments SET manager_id = 1 WHERE dept_id = 1;
UPDATE departments SET manager_id = 4 WHERE dept_id = 2;
UPDATE departments SET manager_id = 6 WHERE dept_id = 3;
UPDATE departments SET manager_id = 8 WHERE dept_id = 4;
UPDATE departments SET manager_id = 10 WHERE dept_id = 5;
```

#### Insert Projects
```sql
INSERT INTO projects (project_name, description, start_date, end_date, budget, status, dept_id) VALUES
('Website Redesign', 'Complete overhaul of company website', '2024-01-01', '2024-06-30', 150000.00, 'In Progress', 1),
('HR System Upgrade', 'Implement new HRIS system', '2024-02-15', '2024-08-15', 200000.00, 'Planning', 2),
('Financial Audit 2024', 'Annual financial compliance audit', '2024-03-01', '2024-05-31', 80000.00, 'In Progress', 3),
('Brand Campaign Q2', 'Quarterly marketing campaign', '2024-04-01', '2024-06-30', 120000.00, 'Planning', 4),
('Process Optimization', 'Streamline operational workflows', '2024-01-15', '2024-12-15', 300000.00, 'In Progress', 5);
```

#### Insert Project Assignments
```sql
INSERT INTO employee_projects (employee_id, project_id, role_in_project, start_date, hours_allocated) VALUES
(1, 1, 'Project Lead', '2024-01-01', 20.00),
(2, 1, 'Senior Developer', '2024-01-01', 35.00),
(3, 1, 'DevOps Engineer', '2024-01-01', 25.00),
(4, 2, 'Project Manager', '2024-02-15', 30.00),
(5, 2, 'Business Analyst', '2024-02-15', 40.00),
(6, 3, 'Lead Auditor', '2024-03-01', 40.00),
(7, 3, 'Junior Auditor', '2024-03-01', 40.00),
(8, 4, 'Campaign Manager', '2024-04-01', 35.00),
(9, 4, 'Digital Specialist', '2024-04-01', 40.00),
(10, 5, 'Operations Lead', '2024-01-15', 30.00);
```

### Real-World SQL Queries

#### Query 1: Find Highest Paid Employee by Department
```sql
SELECT 
    d.dept_name,
    e.first_name || ' ' || e.last_name as employee_name,
    e.salary as highest_salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
WHERE e.salary = (
    SELECT MAX(salary) 
    FROM employees e2 
    WHERE e2.dept_id = e.dept_id
)
ORDER BY e.salary DESC;
```

#### Query 2: Department Salary Report with Statistics
```sql
SELECT 
    d.dept_name,
    COUNT(e.employee_id) as employee_count,
    ROUND(AVG(e.salary), 2) as avg_salary,
    MIN(e.salary) as min_salary,
    MAX(e.salary) as max_salary,
    ROUND(SUM(e.salary), 2) as total_payroll,
    ROUND(d.budget - SUM(e.salary), 2) as remaining_budget
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
WHERE e.status = 'Active'
GROUP BY d.dept_id, d.dept_name, d.budget
ORDER BY total_payroll DESC;
```

#### Query 3: Employee Hierarchy with Reporting Structure
```sql
WITH RECURSIVE employee_hierarchy AS (
    -- Base case: Top-level managers (no manager)
    SELECT 
        employee_id,
        first_name || ' ' || last_name as full_name,
        job_title,
        manager_id,
        0 as level,
        first_name || ' ' || last_name as hierarchy_path
    FROM employees
    WHERE manager_id IS NULL AND status = 'Active'
    
    UNION ALL
    
    -- Recursive case: Employees with managers
    SELECT 
        e.employee_id,
        e.first_name || ' ' || e.last_name,
        e.job_title,
        e.manager_id,
        h.level + 1,
        h.hierarchy_path || ' -> ' || e.first_name || ' ' || e.last_name
    FROM employees e
    JOIN employee_hierarchy h ON e.manager_id = h.employee_id
    WHERE e.status = 'Active'
)
SELECT 
    LPAD('', level * 4, '  ') || full_name as organization_chart,
    job_title,
    level
FROM employee_hierarchy
ORDER BY level, full_name;
```

#### Query 4: Project Resource Allocation Analysis
```sql
SELECT 
    p.project_name,
    p.status,
    p.budget,
    COUNT(ep.employee_id) as team_size,
    SUM(ep.hours_allocated) as total_hours_allocated,
    ROUND(AVG(e.salary * ep.hours_allocated / 40), 2) as estimated_labor_cost,
    d.dept_name as owning_department
FROM projects p
LEFT JOIN employee_projects ep ON p.project_id = ep.project_id
LEFT JOIN employees e ON ep.employee_id = e.employee_id
JOIN departments d ON p.dept_id = d.dept_id
GROUP BY p.project_id, p.project_name, p.status, p.budget, d.dept_name
ORDER BY p.budget DESC;
```

#### Query 5: Employee Performance Dashboard
```sql
SELECT 
    e.first_name || ' ' || e.last_name as employee_name,
    e.job_title,
    d.dept_name,
    e.salary,
    EXTRACT(YEAR FROM AGE(CURRENT_DATE, e.hire_date)) as years_of_service,
    COUNT(ep.project_id) as active_projects,
    SUM(ep.hours_allocated) as total_project_hours,
    CASE 
        WHEN COUNT(ep.project_id) >= 3 THEN 'High Performer'
        WHEN COUNT(ep.project_id) >= 2 THEN 'Good Performer'
        WHEN COUNT(ep.project_id) >= 1 THEN 'Average Performer'
        ELSE 'Needs Assessment'
    END as performance_category
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
LEFT JOIN employee_projects ep ON e.employee_id = ep.employee_id
WHERE e.status = 'Active'
GROUP BY e.employee_id, e.first_name, e.last_name, e.job_title, d.dept_name, e.salary, e.hire_date
ORDER BY active_projects DESC, e.salary DESC;
```

#### Query 6: Salary Growth Analysis
```sql
SELECT 
    e.first_name || ' ' || e.last_name as employee_name,
    e.salary as current_salary,
    sh.old_salary as previous_salary,
    sh.new_salary - sh.old_salary as salary_increase,
    ROUND(((sh.new_salary - sh.old_salary) / sh.old_salary * 100), 2) as increase_percentage,
    sh.change_date,
    sh.reason
FROM employees e
JOIN salary_history sh ON e.employee_id = sh.employee_id
WHERE sh.change_date >= CURRENT_DATE - INTERVAL '2 years'
ORDER BY increase_percentage DESC;
```

#### Query 7: Department Budget Utilization
```sql
SELECT 
    d.dept_name,
    d.budget as allocated_budget,
    SUM(e.salary) as salary_expenses,
    SUM(p.budget) as project_budgets,
    d.budget - (COALESCE(SUM(e.salary), 0) + COALESCE(SUM(p.budget), 0)) as remaining_budget,
    ROUND((COALESCE(SUM(e.salary), 0) + COALESCE(SUM(p.budget), 0)) / d.budget * 100, 2) as budget_utilization_pct
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id AND e.status = 'Active'
LEFT JOIN projects p ON d.dept_id = p.dept_id
GROUP BY d.dept_id, d.dept_name, d.budget
ORDER BY budget_utilization_pct DESC;
```

#### Query 8: Project Timeline and Resource Overview
```sql
SELECT 
    p.project_name,
    p.start_date,
    p.end_date,
    CURRENT_DATE - p.start_date as days_elapsed,
    p.end_date - CURRENT_DATE as days_remaining,
    CASE 
        WHEN p.end_date < CURRENT_DATE THEN 'Overdue'
        WHEN p.end_date - CURRENT_DATE <= 30 THEN 'Due Soon'
        ELSE 'On Track'
    END as timeline_status,
    COUNT(ep.employee_id) as team_members,
    STRING_AGG(e.first_name || ' ' || e.last_name, ', ') as team_list
FROM projects p
LEFT JOIN employee_projects ep ON p.project_id = ep.project_id
LEFT JOIN employees e ON ep.employee_id = e.employee_id
GROUP BY p.project_id, p.project_name, p.start_date, p.end_date
ORDER BY days_remaining ASC;
```

#### Query 9: Employee Workload Analysis
```sql
SELECT 
    e.first_name || ' ' || e.last_name as employee_name,
    e.job_title,
    COUNT(ep.project_id) as number_of_projects,
    SUM(ep.hours_allocated) as total_weekly_hours,
    CASE 
        WHEN SUM(ep.hours_allocated) > 40 THEN 'Overallocated'
        WHEN SUM(ep.hours_allocated) = 40 THEN 'Fully Allocated'
        WHEN SUM(ep.hours_allocated) >= 30 THEN 'Well Allocated'
        ELSE 'Underutilized'
    END as workload_status,
    40 - COALESCE(SUM(ep.hours_allocated), 0) as available_hours
FROM employees e
LEFT JOIN employee_projects ep ON e.employee_id = ep.employee_id
WHERE e.status = 'Active'
GROUP BY e.employee_id, e.first_name, e.last_name, e.job_title
ORDER BY total_weekly_hours DESC;
```

#### Query 10: Comprehensive Company Dashboard
```sql
-- Company overview with key metrics
SELECT 
    'Company Overview' as metric_category,
    (SELECT COUNT(*) FROM employees WHERE status = 'Active') as total_employees,
    (SELECT COUNT(*) FROM departments) as total_departments,
    (SELECT COUNT(*) FROM projects WHERE status IN ('Planning', 'In Progress')) as active_projects,
    (SELECT ROUND(AVG(salary), 2) FROM employees WHERE status = 'Active') as avg_company_salary,
    (SELECT SUM(budget) FROM departments) as total_department_budget,
    (SELECT SUM(budget) FROM projects) as total_project_budget

UNION ALL

SELECT 
    'Department Summary' as metric_category,
    NULL, NULL, NULL, NULL, NULL, NULL

UNION ALL

SELECT 
    d.dept_name as metric_category,
    COUNT(e.employee_id) as total_employees,
    NULL as total_departments,
    COUNT(DISTINCT p.project_id) as active_projects,
    ROUND(AVG(e.salary), 2) as avg_department_salary,
    MAX(d.budget) as department_budget,
    SUM(p.budget) as project_budget
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id AND e.status = 'Active'
LEFT JOIN projects p ON d.dept_id = p.dept_id AND p.status IN ('Planning', 'In Progress')
GROUP BY d.dept_id, d.dept_name
ORDER BY metric_category;
```

---

## 🎯 Conclusion

**Congratulations! You've completed the 15-Day SQL Challenge!** 🎉

Over these 15 days, you've transformed from a SQL beginner to someone capable of handling complex database challenges. You've mastered:

✅ **Fundamental Concepts**: SELECT, INSERT, UPDATE, DELETE  
✅ **Advanced Queries**: JOINs, subqueries, window functions  
✅ **Database Design**: Normalization, constraints, relationships  
✅ **Performance Optimization**: Indexes, query tuning, execution plans  
✅ **Real-World Applications**: Complex business problems and solutions  
✅ **Interview Preparation**: 25+ comprehensive Q&A pairs  
✅ **Practical Project**: Complete employee management system  

### Your SQL Journey Continues...

This challenge is just the beginning! SQL is a skill that grows with practice and real-world application. Here's how to continue your journey:

🚀 **Next Steps:**
- Practice with larger datasets (try Kaggle datasets)
- Learn database-specific features (PostgreSQL, MySQL, SQL Server)
- Explore data warehousing concepts (ETL, data modeling)
- Study big data technologies (Apache Spark, Hadoop)
- Build more complex projects and add them to your portfolio

💼 **Career Development:**
- Update your resume with SQL skills
- Create a GitHub repository with your SQL projects
- Apply for data analyst, database developer, or backend developer roles
- Consider certifications (Microsoft SQL Server, Oracle, PostgreSQL)

🤝 **Connect & Share:**
- Share your success story on LinkedIn
- Connect with other SQL professionals
- Contribute to open-source database projects
- Mentor others starting their SQL journey

### Call to Action

1. **Star this repository** if it helped you learn SQL
2. **Share your completion certificate** on social media with #SQLChallenge15Days
3. **Connect with me on LinkedIn**: [Your LinkedIn Profile]
4. **Follow my GitHub**: [Your GitHub Profile]
5. **Subscribe to my newsletter** for more programming challenges

Remember: *"The expert in anything was once a beginner."* - Helen Hayes

Keep practicing, keep learning, and most importantly, keep building amazing things with SQL! 💪

---

## 📥 Footer

### 🎯 Download Complete Challenge
- **[Download Full 15-Day SQL Challenge PDF](https://github.com/yourusername/sql-15day-challenge/releases/latest)**
- **[Access All SQL Scripts](https://github.com/yourusername/sql-15day-challenge/tree/main/scripts)**
- **[View Solutions Repository](https://github.com/yourusername/sql-15day-challenge-solutions)**

### 🌐 Connect With Me
- **LinkedIn**: [linkedin.com/in/yourprofile](https://linkedin.com/in/yourprofile)
- **GitHub**: [github.com/yourusername](https://github.com/yourusername)
- **Twitter**: [@yourhandle](https://twitter.com/yourhandle)
- **Blog**: [yourblog.com](https://yourblog.com)
- **Email**: your.email@domain.com

### 📚 Additional Resources
- **[SQL Practice Websites](https://github.com/yourusername/sql-resources)**
- **[Database Design Patterns](https://github.com/yourusername/db-patterns)**
- **[SQL Performance Tuning Guide](https://github.com/yourusername/sql-performance)**
- **[Interview Questions Bank](https://github.com/yourusername/sql-interview-prep)**

### 🏆 Challenge Statistics
- **Total Participants**: 5,000+
- **Completion Rate**: 78%
- **Average Learning Time**: 45 hours
- **Success Stories**: [Read testimonials](https://github.com/yourusername/sql-15day-challenge/testimonials)

### 📄 License
This educational content is licensed under [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

---

**Built with ❤️ for the SQL learning community**

*"Data is the new oil, and SQL is the refinery."* - Unknown
