SQL Practice Repository

This repository contains SQL practice problems, complex queries, and examples across different SQL topics. Each example is designed to showcase SQL capabilities and demonstrate best practices in database query writing.

🔍 Topics Covered
Joins: Inner joins, outer joins, self-joins, and cross joins
Subqueries: Single-row, multi-row, and correlated subqueries
Window Functions: Ranking, aggregation, and analytical functions
Indexes: Index creation, usage, and optimization techniques
Aggregation and Grouping: Aggregate functions and GROUP BY clauses for data summarization

📚 How to Use This Repository
Explore SQL Query Examples: Each file corresponds to a specific SQL topic, containing queries along with explanations and use cases.
Practice Problems: Tackle sample problems with solutions to test and refine your SQL skills.
Reference Queries: Use these queries as a quick reference or as starting points for your own SQL projects.

📈 Example Query
The following example demonstrates how to retrieve the top 5 highest-paid employees in each department:

-- Sample query to find the top 5 highest-paid employees in each department
```sql
WITH RankedSalaries AS (

    SELECT Department, EmployeeName, Salary,
           ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) AS SalaryRank
    FROM Employees
    
)
SELECT Department, EmployeeName, Salary
FROM RankedSalaries
WHERE SalaryRank <= 5;
```



This query uses a Common Table Expression (CTE) and window functions to rank employees by salary within each department, returning only the top 5 highest-paid employees per department.

📌 Additional Example Queries
1. Join Query: Find All Employees and Their Departments
Retrieve employee details along with their department names using an inner join.

```sql

SELECT e.EmployeeName, e.EmployeeID, d.DepartmentName
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```
This query joins the Employees table with the Departments table based on a common column, DepartmentID, to list all employees along with their department names.

2. Subquery: List Employees Earning Above the Company’s Average Salary
Find all employees who earn a salary above the company's average.

```sql

SELECT EmployeeName, Salary
FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```
This query uses a subquery to calculate the average salary in the Employees table and then filters employees with a salary above this average.

3. Window Function: Calculate Running Total of Sales by Date
Show daily sales along with a running total for each day.

```sql

SELECT SaleDate, SalesAmount,
       SUM(SalesAmount) OVER (ORDER BY SaleDate) AS RunningTotal
FROM Sales;
```
Using a window function, this query computes a running total of SalesAmount ordered by SaleDate.

4. Aggregation and Grouping: Count Employees in Each Department
Count the number of employees in each department.

```sql

SELECT DepartmentID, COUNT(EmployeeID) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID
ORDER BY EmployeeCount DESC;
```
This query groups employees by DepartmentID and counts them, providing the number of employees per department, sorted in descending order.

5. Self-Join: Find Employees with the Same Manager
List pairs of employees who report to the same manager.

```sql

SELECT e1.EmployeeName AS Employee1, e2.EmployeeName AS Employee2, e1.ManagerID
FROM Employees e1
JOIN Employees e2 ON e1.ManagerID = e2.ManagerID
WHERE e1.EmployeeID < e2.EmployeeID;
```
By self-joining the Employees table, this query finds all pairs of employees (Employee1 and Employee2) who share the same ManagerID.

6. Common Table Expression (CTE): Find Top N Products by Sales
Using a CTE to retrieve the top 3 products based on total sales.

```sql

WITH ProductSales AS (
    SELECT ProductID, SUM(SalesAmount) AS TotalSales
    FROM Sales
    GROUP BY ProductID
)
SELECT ProductID, TotalSales
FROM ProductSales
ORDER BY TotalSales DESC
LIMIT 3;
```
This query creates a temporary result set (ProductSales) using a CTE and then selects the top 3 products based on total sales.

7. Index Optimization Example: Optimizing a Search Query
Example of creating an index to optimize queries on frequently searched columns.

```sql

CREATE INDEX idx_employee_department ON Employees (DepartmentID);
Creating an index on DepartmentID can speed up queries that frequently search by department, like SELECT * FROM Employees WHERE DepartmentID = 3.
```

8. Conditional Aggregation: Count Employees by Job Title and Department
Get the count of employees by job title within each department.

```sql

SELECT DepartmentID,
       SUM(CASE WHEN JobTitle = 'Manager' THEN 1 ELSE 0 END) AS ManagerCount,
       SUM(CASE WHEN JobTitle = 'Developer' THEN 1 ELSE 0 END) AS DeveloperCount
FROM Employees
GROUP BY DepartmentID;
```
This query uses conditional aggregation to count employees in specific job roles within each department.

📄 Structure
Basic Queries: Simple examples to help you get started.
Intermediate Queries: Queries using joins, aggregations, and grouping.
Advanced Queries: Complex queries involving window functions, CTEs, and optimized indexing.
