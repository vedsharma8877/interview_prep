# Frequently Asked SQL Interview Questions (With Solutions & Explanations)

---

### 1. What is the difference between `INNER JOIN` and `LEFT JOIN`?

**Answer:**
- `INNER JOIN` returns records that have matching values in both tables.
- `LEFT JOIN` returns all records from the left table, and the matched records from the right table. If there is no match, the result is NULL from the right side.

**Example:**
```sql
SELECT a.id, b.name
FROM TableA a
INNER JOIN TableB b ON a.id = b.a_id;
```
Returns only rows with matching `id` in both tables.

```sql
SELECT a.id, b.name
FROM TableA a
LEFT JOIN TableB b ON a.id = b.a_id;
```
Returns all rows from `TableA`, and matching rows from `TableB` (NULL if no match).

---

### 2. How do you find the second highest salary from an Employee table?

**Answer:**
```sql
SELECT MAX(salary) AS SecondHighest
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

**Explanation:**  
The subquery finds the maximum salary. The outer query finds the maximum salary less than the highest, which is the second highest.

---

### 3. What is a `PRIMARY KEY` and a `FOREIGN KEY`?

**Answer:**
- **Primary Key:** Uniquely identifies each record in a table and cannot be NULL.
- **Foreign Key:** A field (or collection of fields) in one table that refers to the `PRIMARY KEY` in another table.

**Example:**
```sql
CREATE TABLE Department (
  DeptID INT PRIMARY KEY,
  DeptName VARCHAR(100)
);

CREATE TABLE Employee (
  EmpID INT PRIMARY KEY,
  EmpName VARCHAR(100),
  DeptID INT,
  FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

---

### 4. How do you find duplicate records in a table?

**Answer:**
```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1
HAVING COUNT(*) > 1;
```

**Explanation:**  
This groups rows by `column1` and returns any groups with more than one record (duplicates).

---

### 5. What is the difference between `WHERE` and `HAVING` clause?

**Answer:**
- `WHERE` filters rows before grouping.
- `HAVING` filters groups after aggregation.

**Example:**
```sql
SELECT department, COUNT(*)
FROM Employee
WHERE salary > 50000   -- filters rows before grouping
GROUP BY department
HAVING COUNT(*) > 5;   -- filters groups after aggregation
```

---

### 6. Write a query to get the top 3 highest salaries from the Employee table.

**Answer:**
```sql
SELECT DISTINCT salary
FROM Employee
ORDER BY salary DESC
LIMIT 3;
```
*Note: Use `TOP 3` instead of `LIMIT 3` in SQL Server.*

---

### 7. How to update data in SQL?

**Answer:**
```sql
UPDATE Employee
SET salary = salary * 1.1
WHERE department = 'IT';
```
**Explanation:**  
This increases salaries by 10% for IT department employees.

---

### 8. What is a subquery? Provide an example.

**Answer:**  
A subquery is a query nested inside another SQL query.

**Example:**
```sql
SELECT EmpName
FROM Employee
WHERE DeptID = (SELECT DeptID FROM Department WHERE DeptName = 'HR');
```

---

### 9. How to delete duplicate rows from a table?

**Answer:**
```sql
DELETE FROM Employee
WHERE rowid NOT IN (
  SELECT MIN(rowid)
  FROM Employee
  GROUP BY EmpName, DeptID
);
```
*Note: `rowid` is available in some databases like SQLite and Oracle. For others, use a unique column.*

---

### 10. How do you get the count of employees in each department?

**Answer:**
```sql
SELECT DeptID, COUNT(*) AS NumEmployees
FROM Employee
GROUP BY DeptID;
```

---

## Additional Tips

- Understand how indexes work and how they affect query performance.
- Be comfortable with aggregate functions (`SUM`, `AVG`, `COUNT`, `MIN`, `MAX`).
- Practice writing queries involving joins, subqueries, and grouping.

---

**Practice makes perfect! Review these and try modifying them for different scenarios to deepen your understanding.**

# More SQL Interview Questions (With Solutions & Explanations)

---

### 11. What is the difference between `RANK()`, `DENSE_RANK()`, and `ROW_NUMBER()`?

**Answer:**
- `ROW_NUMBER()`: Assigns a unique sequential integer to rows within a partition.
- `RANK()`: Gives the same rank to rows with identical values, but skips the next rank.
- `DENSE_RANK()`: Like `RANK()`, but does not skip any ranks.

**Example:**
```sql
SELECT
  name,
  salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC) as RowNum,
  RANK() OVER (ORDER BY salary DESC) as RankNum,
  DENSE_RANK() OVER (ORDER BY salary DESC) as DenseRankNum
FROM Employee;
```

---

### 12. How do you get the nth highest salary from a table?

**Answer:**
```sql
SELECT DISTINCT salary
FROM Employee e1
WHERE N-1 = (
  SELECT COUNT(DISTINCT salary)
  FROM Employee e2
  WHERE e2.salary > e1.salary
);
```
*Replace `N` with the desired rank (e.g., 3 for third highest).*

---

### 13. What is normalization? Explain different normal forms.

**Answer:**
- **Normalization:** Organizing data to reduce redundancy and improve data integrity.
- **1NF:** Eliminate repeating groups; ensure atomicity.
- **2NF:** 1NF + Remove partial dependencies (every non-key attribute is fully dependent on the primary key).
- **3NF:** 2NF + Remove transitive dependencies (non-key attributes depend only on the primary key).

---

### 14. Write a query to fetch employees who have no manager.

**Answer:**
```sql
SELECT *
FROM Employee
WHERE manager_id IS NULL;
```

---

### 15. What is the use of `COALESCE()` in SQL?

**Answer:**  
`COALESCE()` returns the first non-null value in a list of arguments.

**Example:**
```sql
SELECT EmpName, COALESCE(phone, mobile, 'No Contact') as Contact
FROM Employee;
```
Returns `phone` if present, else `mobile`, else 'No Contact'.

---

### 16. How do you retrieve only the date part from a `DATETIME` column?

**Answer:**
```sql
-- MySQL
SELECT DATE(datetime_column) FROM table_name;

-- SQL Server
SELECT CAST(datetime_column AS DATE) FROM table_name;
```

---

### 17. What is an aggregate function? Name some.

**Answer:**  
Aggregate functions perform calculations on multiple values and return a single value.  
Examples: `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

---

### 18. How would you swap the values of two columns in a table?

**Answer:**
```sql
UPDATE table_name
SET column1 = column2,
    column2 = column1;
```
*Note: In some RDBMS, you may need to use a temp variable or perform in two steps.*

---

### 19. What is a CTE (Common Table Expression)? Give an example.

**Answer:**  
A CTE is a temporary result set which can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.

**Example:**
```sql
WITH SalesCTE AS (
  SELECT EmpID, SUM(Sales) as TotalSales
  FROM Sales
  GROUP BY EmpID
)
SELECT * FROM SalesCTE WHERE TotalSales > 10000;
```

---

### 20. Write a query to select all departments with more than 5 employees.

**Answer:**
```sql
SELECT department, COUNT(*) as NumEmployees
FROM Employee
GROUP BY department
HAVING COUNT(*) > 5;
```

---

### 21. How would you find the employees who joined in the last 30 days?

**Answer:**
```sql
SELECT *
FROM Employee
WHERE join_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);
```
*Change to `GETDATE()-30` for SQL Server.*

---

### 22. What is a self join? Provide an example.

**Answer:**  
A self join is a regular join but the table is joined with itself.

**Example:**
```sql
SELECT A.EmpName AS Employee, B.EmpName AS Manager
FROM Employee A
LEFT JOIN Employee B ON A.manager_id = B.EmpID;
```

---

### 23. How do you remove all rows from a table without deleting the table itself?

**Answer:**
```sql
TRUNCATE TABLE table_name;
```
*Faster than `DELETE FROM table_name;` but cannot be rolled back in some RDBMS.*

---

### 24. What is indexing? What are its types?

**Answer:**
- **Indexing** improves the speed of data retrieval.
- **Types:** Unique Index, Composite Index, Clustered Index, Non-clustered Index, Full-text Index.

---

### 25. How do you find the total, average, minimum, and maximum salary of employees?

**Answer:**
```sql
SELECT
  SUM(salary) as TotalSalary,
  AVG(salary) as AverageSalary,
  MIN(salary) as MinSalary,
  MAX(salary) as MaxSalary
FROM Employee;
```

---

Continue practicing with real-world scenarios and different RDBMS for deeper understanding!

# Real SQL Coding Question Examples

---

## 1. Find Employees With Higher Than Average Salary

**Question:**  
Write an SQL query to find all employees who have a salary higher than the average salary in the Employee table.

**Solution:**
```sql
SELECT *
FROM Employee
WHERE salary > (SELECT AVG(salary) FROM Employee);
```

**Explanation:**  
This subquery calculates the average salary, and the outer query returns employees earning above that average.

---

## 2. Retrieve Consecutive Records (Find Missing Dates)

**Question:**  
Given a table `Attendance(date DATE)`, write a query to find all dates where attendance is missing between the minimum and maximum date in the table.

**Solution:**
```sql
SELECT d.generated_date
FROM (
  SELECT DATE_ADD((SELECT MIN(date) FROM Attendance), INTERVAL seq DAY) AS generated_date
  FROM (
    SELECT ROW_NUMBER() OVER () - 1 AS seq
    FROM Attendance
    CROSS JOIN Attendance a2
  ) AS numbers
  WHERE DATE_ADD((SELECT MIN(date) FROM Attendance), INTERVAL seq DAY) <= (SELECT MAX(date) FROM Attendance)
) d
LEFT JOIN Attendance a ON d.generated_date = a.date
WHERE a.date IS NULL;
```

**Explanation:**  
Generates a sequence of dates from the minimum to the maximum date and finds which are missing from the Attendance table.

---

## 3. Customers With No Orders

**Question:**  
Given `Customers(customer_id, name)` and `Orders(order_id, customer_id)`, find customers who have never placed an order.

**Solution:**
```sql
SELECT c.*
FROM Customers c
LEFT JOIN Orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

**Explanation:**  
A LEFT JOIN ensures all customers are included, and filtering for `o.order_id IS NULL` reveals those with no matching orders.

---

## 4. Running Total of Sales

**Question:**  
Given a `Sales(date, amount)` table, write a query to calculate the running total of sales by date.

**Solution:**
```sql
SELECT
  date,
  amount,
  SUM(amount) OVER (ORDER BY date) AS running_total
FROM Sales
ORDER BY date;
```

**Explanation:**  
Uses a window function to compute a cumulative sum of the sales amount ordered by date.

---

## 5. Second Highest Salary Per Department

**Question:**  
Given `Employee(emp_id, name, salary, dept_id)`, get the second highest salary in each department.

**Solution:**
```sql
SELECT dept_id, MAX(salary) AS second_highest_salary
FROM Employee
WHERE salary < (
  SELECT MAX(salary)
  FROM Employee e2
  WHERE e2.dept_id = Employee.dept_id
)
GROUP BY dept_id;
```

**Explanation:**  
For each department, finds the highest salary less than the maximum (the second highest).

---

## 6. Find Duplicate Emails

**Question:**  
Given a `Users(id, email)`, write a query to find all duplicate email addresses.

**Solution:**
```sql
SELECT email, COUNT(*) AS count
FROM Users
GROUP BY email
HAVING COUNT(*) > 1;
```

**Explanation:**  
Groups by email and returns those with more than one occurrence.

---

## 7. Find Top N Records Per Group

**Question:**  
Given `ProductSales(product_id, sale_date, amount)`, write a query to get the top 2 sales per product.

**Solution:**
```sql
SELECT product_id, sale_date, amount
FROM (
  SELECT *,
    ROW_NUMBER() OVER (PARTITION BY product_id ORDER BY amount DESC) AS rn
  FROM ProductSales
) t
WHERE rn <= 2;
```

**Explanation:**  
Uses window functions to rank sales per product and filters for the top 2.

---

## 8. Find Employees With Same Manager

**Question:**  
Given `Employee(emp_id, name, manager_id)`, list all pairs of employees who share the same manager.

**Solution:**
```sql
SELECT e1.name AS employee1, e2.name AS employee2, e1.manager_id
FROM Employee e1
JOIN Employee e2 ON e1.manager_id = e2.manager_id AND e1.emp_id < e2.emp_id;
```

**Explanation:**  
Self-join on manager_id and ensure unique pairs by comparing emp_id.

---

## 9. Highest Order Amount Per Customer

**Question:**  
Given `Orders(order_id, customer_id, amount)`, find the highest order amount for each customer.

**Solution:**
```sql
SELECT customer_id, MAX(amount) AS highest_order
FROM Orders
GROUP BY customer_id;
```

**Explanation:**  
Groups orders by customer and finds the maximum amount.

---

## 10. Employees Who Joined In Last N Days

**Question:**  
Given `Employee(emp_id, name, join_date)`, find those who joined in the last 7 days.

**Solution:**
```sql
SELECT *
FROM Employee
WHERE join_date >= CURRENT_DATE - INTERVAL 7 DAY;
```

**Explanation:**  
Filters employees based on join_date within the last 7 days.

---

Continue practicing with these real-world questions for interviews and coding tests!

# More Real SQL Coding Interview Questions

---

## 11. Find Employees Who Earn the Highest Salary in Each Department

**Question:**  
Given `Employee(emp_id, name, salary, dept_id)`, write a query to find the employees with the maximum salary in their department.

**Solution:**
```sql
SELECT e.*
FROM Employee e
JOIN (
  SELECT dept_id, MAX(salary) AS max_salary
  FROM Employee
  GROUP BY dept_id
) m ON e.dept_id = m.dept_id AND e.salary = m.max_salary;
```

---

## 12. Find Departments With No Employees

**Question:**  
Given `Department(dept_id, dept_name)` and `Employee(emp_id, name, dept_id)`, write a query to list all departments without employees.

**Solution:**
```sql
SELECT d.*
FROM Department d
LEFT JOIN Employee e ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;
```

---

## 13. Find the Median Salary in the Employee Table

**Question:**  
Write a query to find the median salary from the `Employee` table.

**Solution:**  
*Works in databases supporting window functions:*
```sql
SELECT AVG(salary) AS median_salary
FROM (
  SELECT salary,
         ROW_NUMBER() OVER (ORDER BY salary) AS rn,
         COUNT(*) OVER () AS total
  FROM Employee
) t
WHERE rn IN (FLOOR((total+1)/2), CEIL((total+1)/2));
```

---

## 14. List Employees Who Have Not Received Any Bonus

**Question:**  
Given `Employee(emp_id, name)` and `Bonus(emp_id, bonus_amount)`, write a query to list employees who have never received a bonus.

**Solution:**
```sql
SELECT e.*
FROM Employee e
LEFT JOIN Bonus b ON e.emp_id = b.emp_id
WHERE b.emp_id IS NULL;
```

---

## 15. Find Top 3 Most Frequently Ordered Products

**Question:**  
Given `Orders(order_id, product_id)`, write a query to find the three most ordered products.

**Solution:**
```sql
SELECT product_id, COUNT(*) AS order_count
FROM Orders
GROUP BY product_id
ORDER BY order_count DESC
LIMIT 3;
```

---

## 16. Find Employees With Palindromic Names

**Question:**  
Write a query to find all employees whose names are palindromes.

**Solution:**  
*Example for PostgreSQL:*
```sql
SELECT *
FROM Employee
WHERE name = REVERSE(name);
```

---

## 17. Get All Managers With More Than 2 Direct Reports

**Question:**  
Given `Employee(emp_id, name, manager_id)`, write a query to find all managers with more than two direct reports.

**Solution:**
```sql
SELECT manager_id, COUNT(*) AS report_count
FROM Employee
WHERE manager_id IS NOT NULL
GROUP BY manager_id
HAVING COUNT(*) > 2;
```

---

## 18. Find All Customers Who Placed Orders in Every Month of 2024

**Question:**  
Given `Orders(order_id, customer_id, order_date)`, write a query to find customer IDs who placed at least one order in every month of 2024.

**Solution:**
```sql
SELECT customer_id
FROM Orders
WHERE YEAR(order_date) = 2024
GROUP BY customer_id
HAVING COUNT(DISTINCT MONTH(order_date)) = 12;
```

---

## 19. Find Employees Whose Name Starts and Ends With a Vowel

**Question:**  
Write a query to get all employees whose names start and end with a vowel.

**Solution:**  
*Example for MySQL:*
```sql
SELECT *
FROM Employee
WHERE LOWER(SUBSTRING(name, 1, 1)) IN ('a','e','i','o','u')
  AND LOWER(RIGHT(name, 1)) IN ('a','e','i','o','u');
```

---

## 20. Find the Longest Streak of Days With Sales

**Question:**  
Given `Sales(sale_date, amount)`, write a query to find the longest streak of consecutive days with at least one sale.

**Solution:**  
*Works in databases supporting window functions:*
```sql
WITH dates AS (
  SELECT DISTINCT sale_date FROM Sales
),
grp AS (
  SELECT sale_date,
         DATE_SUB(sale_date, INTERVAL ROW_NUMBER() OVER (ORDER BY sale_date) DAY) AS grp
  FROM dates
)
SELECT MIN(sale_date) AS streak_start,
       MAX(sale_date) AS streak_end,
       COUNT(*) AS streak_length
FROM grp
GROUP BY grp
ORDER BY streak_length DESC
LIMIT 1;
```
*Adjust date functions for your RDBMS (e.g., use `DATEADD`, `DATEDIFF`, etc. for SQL Server).*

---

**Practice with these challenging, practical problems to build real SQL fluency!**