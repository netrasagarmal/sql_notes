# sql_notes

<details>
<summary></summary>
### SQL

[](/static/image.png)

Sure! These are all categories of SQL (Structured Query Language) commands, and each serves a specific purpose in managing and interacting with a database. Here’s a breakdown:

### 1. **DDL (Data Definition Language)**:

- **Purpose**: DDL deals with the structure (schema) of the database. It defines and manages the database objects such as tables, views, indexes, and schemas.
- **Common Commands**:
    - `CREATE`: Defines new database objects (e.g., tables, indexes).
    - `ALTER`: Modifies existing database objects.
    - `DROP`: Deletes database objects (e.g., tables, views).
    - `TRUNCATE`: Removes all rows from a table, but does not delete the table itself.
- **Example**:
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Name VARCHAR(50),
        Position VARCHAR(50)
    );
    
    ```
    

### 2. **DML (Data Manipulation Language)**:

- **Purpose**: DML is used for managing the data within the schema. It allows you to insert, update, delete, and retrieve data.
- **Common Commands**:
    - `SELECT`: Retrieves data from one or more tables.
    - `INSERT`: Adds new rows to a table.
    - `UPDATE`: Modifies existing rows.
    - `DELETE`: Removes rows from a table.
- **Example**:
    
    ```sql
    INSERT INTO Employees (EmployeeID, Name, Position)
    VALUES (1, 'John Doe', 'Manager');
    
    ```
    

### 3. **DCL (Data Control Language)**:

- **Purpose**: DCL controls access to the data in the database. It’s used to grant or revoke permissions for users and roles.
- **Common Commands**:
    - `GRANT`: Gives specific privileges to users (e.g., SELECT, INSERT, DELETE).
    - `REVOKE`: Removes specific privileges from users.
- **Example**:
    
    ```sql
    GRANT SELECT, INSERT ON Employees TO user1;
    
    ```
    

### 4. **TCL (Transaction Control Language)**:

- **Purpose**: TCL deals with transactions within the database. It allows you to manage changes made by DML statements, and ensure data integrity through commit and rollback operations.
- **Common Commands**:
    - `COMMIT`: Saves the changes made by a transaction permanently to the database.
    - `ROLLBACK`: Undoes any changes made in the current transaction.
    - `SAVEPOINT`: Sets a point within a transaction to which you can later roll back.
    - `SET TRANSACTION`: Configures the properties of the current transaction.
- **Example**:
    
    ```sql
    BEGIN TRANSACTION;
    UPDATE Employees SET Position = 'Senior Manager' WHERE EmployeeID = 1;
    COMMIT;
    
    ```
    

### 5. **DQL (Data Query Language)**:

- **Purpose**: DQL is specifically focused on querying and retrieving data from the database.
- **Common Command**:
    - `SELECT`: Retrieves data from one or more tables based on specific criteria.
- **Example**:
    
    ```sql
    SELECT Name, Position FROM Employees WHERE EmployeeID = 1;
    
    ```
    

### Summary of Usage:

- **DDL**: Creates or modifies the database structure.
- **DML**: Deals with data manipulation (insert, update, delete).
- **DCL**: Controls access to data and permissions.
- **TCL**: Manages transaction control (commit, rollback).
- **DQL**: Queries and retrieves data.

### Sample Queries

### 1. **CREATE**: Defines new database objects (e.g., tables, indexes).

- Example: Create a table called `Employees` with an ID, Name, and Position.

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Position VARCHAR(50)
);

```

### 2. **ALTER**: Modifies existing database objects.

- Example: Add a new column `Salary` to the `Employees` table.

```sql
ALTER TABLE Employees ADD Salary INT;

```

### 3. **DROP**: Deletes database objects (e.g., tables, views).

- Example: Delete the `Employees` table.

```sql
DROP TABLE Employees;

```

### 4. **TRUNCATE**: Removes all rows from a table, but does not delete the table itself.

- Example: Remove all rows from the `Employees` table.

```sql
TRUNCATE TABLE Employees;

```

### 5. **SELECT**: Retrieves data from one or more tables.

- Example: Select all columns from the `Employees` table.

```sql
SELECT * FROM Employees;

```

### 6. **INSERT**: Adds new rows to a table.

- Example: Insert a new employee into the `Employees` table.

```sql
INSERT INTO Employees (EmployeeID, Name, Position, Salary)
VALUES (1, 'John Doe', 'Manager', 75000);

```

### 7. **UPDATE**: Modifies existing rows.

- Example: Update the salary of employee with ID 1.

```sql
UPDATE Employees
SET Salary = 80000
WHERE EmployeeID = 1;

```

### 8. **DELETE**: Removes rows from a table.

- Example: Delete the employee with `EmployeeID` 1.

```sql
DELETE FROM Employees
WHERE EmployeeID = 1;

```

### 9. **GRANT**: Gives specific privileges to users (e.g., SELECT, INSERT, DELETE).

- Example: Grant `SELECT` and `INSERT` privileges on `Employees` table to `user1`.

```sql
GRANT SELECT, INSERT ON Employees TO user1;

```

### 10. **REVOKE**: Removes specific privileges from users.

- Example: Revoke `INSERT` privilege on `Employees` table from `user1`.

```sql
REVOKE INSERT ON Employees FROM user1;

```

### 11. **COMMIT**: Saves the changes made by a transaction permanently to the database.

- Example: Commit changes made in a transaction.

```sql
BEGIN TRANSACTION;
UPDATE Employees SET Salary = 90000 WHERE EmployeeID = 2;
COMMIT;

```

### 12. **ROLLBACK**: Undoes any changes made in the current transaction.

- Example: Rollback changes made after an error in a transaction.

```sql
BEGIN TRANSACTION;
UPDATE Employees SET Salary = 95000 WHERE EmployeeID = 2;
ROLLBACK;

```

### 13. **SAVEPOINT**: Sets a point within a transaction to which you can later roll back.

- Example: Set a savepoint within a transaction and then roll back to that point if needed.

```sql
BEGIN TRANSACTION;
SAVEPOINT BeforeSalaryUpdate;
UPDATE Employees SET Salary = 100000 WHERE EmployeeID = 3;
ROLLBACK TO SAVEPOINT BeforeSalaryUpdate;
COMMIT;

```

### 14. **SET TRANSACTION**: Configures the properties of the current transaction.

- Example: Set the transaction isolation level to `SERIALIZABLE` to avoid dirty reads.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN TRANSACTION;
UPDATE Employees SET Salary = 110000 WHERE EmployeeID = 4;
COMMIT;

```

These are the standard SQL commands with examples to illustrate how they can be used in practice. Let me know if you need further clarification on any of them!

### Custom Function in SQL:

To create a **function in SQL** (e.g., in **MySQL** or **PostgreSQL**) that finds numbers appearing **at least three times consecutively** from the `Logs` table, you need to:

1. Use SQL procedural syntax (e.g., in MySQL: `CREATE FUNCTION` or `CREATE PROCEDURE`).
2. Use a cursor or temporary table if needed for more advanced logic (optional for simpler SELECT-based logic).

Since your logic is based on a simple `SELECT` query, you can wrap it into a **stored procedure** (since SQL functions generally cannot return result sets directly like tables — that’s what procedures are for).

### ✅ MySQL Stored Procedure Example:

```sql
DELIMITER //

CREATE PROCEDURE GetConsecutiveNums()
BEGIN
    SELECT DISTINCT l1.num AS ConsecutiveNums
    FROM Logs l1
    JOIN Logs l2 ON l1.id = l2.id - 1
    JOIN Logs l3 ON l1.id = l3.id - 2
    WHERE l1.num = l2.num AND l2.num = l3.num;
END //

DELIMITER ;

```

### To Call the Procedure:

```sql
CALL GetConsecutiveNums();

```

---

### 📝 Notes:

- `DELIMITER` is used to change the statement delimiter temporarily so MySQL can parse the body of the procedure.
- This procedure doesn't accept parameters. You could expand it to do so if needed.
- This returns a result set, similar to running the query manually.

Would you like a version for **PostgreSQL** or one that includes input parameters?

### Other Parts of SQL

### 1. **Clauses**:

Clauses are parts of an SQL query that define specific actions and conditions. They help structure the query and control the result set.

- **WHERE Clause**: Filters records that meet a certain condition.
    
    ```sql
    SELECT * FROM Employees WHERE Position = 'Manager';
    
    ```
    
- **ORDER BY Clause**: Sorts the result set by one or more columns.
    
    ```sql
    SELECT * FROM Employees ORDER BY Name ASC;
    
    ```
    
- **GROUP BY Clause**: Groups rows that have the same values into summary rows (like COUNT, AVG).
    
    ```sql
    SELECT Position, COUNT(*) FROM Employees GROUP BY Position;
    
    ```
    
- **HAVING Clause**: Filters records after grouping, used with `GROUP BY`.
    
    ```sql
    SELECT Position, COUNT(*) FROM Employees GROUP BY Position HAVING COUNT(*) > 1;
    
    ```
    
- **LIMIT Clause**: Limits the number of rows returned by the query (used in databases like MySQL).
    
    ```sql
    SELECT * FROM Employees LIMIT 5;
    
    ```
    

### 2. **Operators**:

Operators are used to perform operations on data in SQL. They can be used in conditions (like `WHERE`), in mathematical operations, or for comparisons.

- **Comparison Operators**: Used to compare two values.
    - `=`: Equal to
    - `!=` or `<>`: Not equal to
    - `>`: Greater than
    - `<`: Less than
    - `>=`: Greater than or equal to
    - `<=`: Less than or equal to
    
    ```sql
    SELECT * FROM Employees WHERE Salary > 50000;
    
    ```
    
- **Logical Operators**: Used to combine multiple conditions.
    - `AND`: Returns true if all conditions are true.
    - `OR`: Returns true if at least one condition is true.
    - `NOT`: Reverses the result of a condition.
    
    ```sql
    SELECT * FROM Employees WHERE Position = 'Manager' AND Salary > 60000;
    
    ```
    
- **Arithmetic Operators**: Used for mathematical calculations.
    - `+`: Addition
    - : Subtraction
    - : Multiplication
    - `/`: Division
    - `%`: Modulus (remainder)
    
    ```sql
    SELECT Salary * 12 AS AnnualSalary FROM Employees;
    
    ```
    
- **BETWEEN**: Used to filter a range of values.
    
    ```sql
    SELECT * FROM Employees WHERE Salary BETWEEN 50000 AND 70000;
    
    ```
    
- **IN**: Checks if a value matches any value in a list.
    
    ```sql
    SELECT * FROM Employees WHERE Position IN ('Manager', 'Director');
    
    ```
    
- **LIKE**: Used for pattern matching in string values.
    
    ```sql
    SELECT * FROM Employees WHERE Name LIKE 'J%';  -- Names starting with 'J'
    
    ```
    
- **IS NULL / IS NOT NULL**: Checks for NULL values.
    
    ```sql
    SELECT * FROM Employees WHERE Position IS NOT NULL;
    
    ```
    

### 3. **Aggregate Functions**:

Aggregate functions perform calculations on multiple rows of a table’s column and return a single value. They are often used with `GROUP BY` clauses.

- **COUNT()**: Returns the number of rows that match a specified condition.
    
    ```sql
    SELECT COUNT(*) FROM Employees WHERE Position = 'Manager';
    
    ```
    
- **SUM()**: Returns the sum of a numeric column.
    
    ```sql
    SELECT SUM(Salary) FROM Employees;
    
    ```
    
- **AVG()**: Returns the average value of a numeric column.
    
    ```sql
    SELECT AVG(Salary) FROM Employees;
    
    ```
    
- **MIN()**: Returns the smallest value of a column.
    
    ```sql
    SELECT MIN(Salary) FROM Employees;
    
    ```
    
- **MAX()**: Returns the largest value of a column.
    
    ```sql
    SELECT MAX(Salary) FROM Employees;
    
    ```
    

### 4. **Data Constraints**:

Data constraints are rules applied to table columns to enforce data integrity. They help ensure the correctness, accuracy, and consistency of data.

- **PRIMARY KEY**: Uniquely identifies each record in a table. A primary key column cannot have `NULL` values.
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Name VARCHAR(100)
    );
    
    ```
    
- **FOREIGN KEY**: Ensures that a column’s value matches the value in another table's primary key or unique key.
    
    ```sql
    CREATE TABLE Orders (
        OrderID INT PRIMARY KEY,
        EmployeeID INT,
        FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
    );
    
    ```
    
- **UNIQUE**: Ensures all values in a column are distinct.
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Email VARCHAR(100) UNIQUE
    );
    
    ```
    
- **NOT NULL**: Ensures that a column cannot have `NULL` values.
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Name VARCHAR(100) NOT NULL
    );
    
    ```
    
- **CHECK**: Ensures that all values in a column satisfy a specific condition.
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Salary INT CHECK (Salary > 0)
    );
    
    ```
    
- **DEFAULT**: Provides a default value for a column when no value is specified.
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY,
        Position VARCHAR(100) DEFAULT 'Employee'
    );
    
    ```
    

### Summary:

- **Clauses** define the structure and behavior of SQL queries (e.g., `WHERE`, `ORDER BY`, `GROUP BY`).
- **Operators** are used to perform comparisons, logical operations, or arithmetic in SQL.
- **Aggregate Functions** perform operations on multiple rows and return a single value (e.g., `COUNT`, `SUM`, `AVG`).
- **Data Constraints** ensure data integrity by enforcing rules on how data should be entered or maintained in the database.

### Joins in SQL

Joins in SQL allow you to combine rows from two or more tables based on a related column between them. This is crucial for working with relational databases where data is often spread across different tables. There are several types of joins:

### 1. **INNER JOIN**:

- **Purpose**: Returns records that have matching values in both tables.
- **Example**:
    - Imagine you have two tables: `Employees` and `Departments`.
    - `Employees` table:
        
        
        | EmployeeID | Name | DepartmentID |
        | --- | --- | --- |
        | 1 | John Doe | 101 |
        | 2 | Jane Smith | 102 |
        | 3 | Alex Lee | 101 |
    - `Departments` table:
        
        
        | DepartmentID | DepartmentName |
        | --- | --- |
        | 101 | HR |
        | 102 | Engineering |
        | 103 | Marketing |
- **SQL Query** (to get employee names and their department names):
    
    ```sql
    SELECT Employees.Name, Departments.DepartmentName
    FROM Employees
    INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    
    ```
    
- **Result**:
    
    
    | Name | DepartmentName |
    | --- | --- |
    | John Doe | HR |
    | Jane Smith | Engineering |
    | Alex Lee | HR |
- **Explanation**: This query returns employees only for those departments where there is a match between `Employees.DepartmentID` and `Departments.DepartmentID`.

---

### 2. **LEFT JOIN (or LEFT OUTER JOIN)**:

- **Purpose**: Returns all records from the left table (first table) and the matched records from the right table. If there is no match, NULL values are returned for columns from the right table.
- **Example**:
    - **SQL Query** (to get all employees and their department names, including employees who may not belong to any department):
    
    ```sql
    SELECT Employees.Name, Departments.DepartmentName
    FROM Employees
    LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    
    ```
    
- **Result**:
    
    
    | Name | DepartmentName |
    | --- | --- |
    | John Doe | HR |
    | Jane Smith | Engineering |
    | Alex Lee | HR |
    | Mike Brown | NULL |
- **Explanation**: Here, `Mike Brown` does not have a matching department in the `Departments` table, so `NULL` is returned for the `DepartmentName`.

---

### 3. **RIGHT JOIN (or RIGHT OUTER JOIN)**:

- **Purpose**: Returns all records from the right table (second table) and the matched records from the left table. If there is no match, NULL values are returned for columns from the left table.
- **Example**:
    - **SQL Query** (to get all departments and the employees in them, including departments with no employees):
    
    ```sql
    SELECT Employees.Name, Departments.DepartmentName
    FROM Employees
    RIGHT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    
    ```
    
- **Result**:
    
    
    | Name | DepartmentName |
    | --- | --- |
    | John Doe | HR |
    | Jane Smith | Engineering |
    | Alex Lee | HR |
    | NULL | Marketing |
- **Explanation**: The `Marketing` department has no employees, so `NULL` is returned for the employee name.

---

### 4. **FULL JOIN (or FULL OUTER JOIN)**:

- **Purpose**: Returns all records when there is a match in either left (first) or right (second) table. If there is no match, NULL values are returned for the missing side.
- **Example**:
    - **SQL Query** (to get all employees and departments, whether or not they have a match):
    
    ```sql
    SELECT Employees.Name, Departments.DepartmentName
    FROM Employees
    FULL OUTER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    
    ```
    
- **Result**:
    
    
    | Name | DepartmentName |
    | --- | --- |
    | John Doe | HR |
    | Jane Smith | Engineering |
    | Alex Lee | HR |
    | Mike Brown | NULL |
    | NULL | Marketing |
- **Explanation**: Here, we get all employees and all departments. If there is no match, NULLs appear in the result.

---

### 5. **CROSS JOIN**:

- **Purpose**: Returns the Cartesian product of the two tables, i.e., it combines each row of the first table with all rows of the second table.
- **Example**:
    - **SQL Query** (to combine every employee with every department):
    
    ```sql
    SELECT Employees.Name, Departments.DepartmentName
    FROM Employees
    CROSS JOIN Departments;
    
    ```
    
- **Result** (if there are 3 employees and 3 departments):
    
    
    | Name | DepartmentName |
    | --- | --- |
    | John Doe | HR |
    | John Doe | Engineering |
    | John Doe | Marketing |
    | Jane Smith | HR |
    | Jane Smith | Engineering |
    | Jane Smith | Marketing |
    | Alex Lee | HR |
    | Alex Lee | Engineering |
    | Alex Lee | Marketing |
- **Explanation**: A `CROSS JOIN` will return every possible combination of rows between the two tables. It’s not based on any condition or relationship between the tables.

---

### 6. **SELF JOIN**:

- **Purpose**: Joins a table to itself. Useful when you want to compare rows within the same table.
- **Example**:
    - Imagine the `Employees` table also contains a `ManagerID` column which refers to `EmployeeID`.
    - `Employees` table:
        
        
        | EmployeeID | Name | ManagerID |
        | --- | --- | --- |
        | 1 | John Doe | NULL |
        | 2 | Jane Smith | 1 |
        | 3 | Alex Lee | 1 |
- **SQL Query** (to get employee names along with their manager’s name):
    
    ```sql
    SELECT E.Name AS Employee, M.Name AS Manager
    FROM Employees E
    LEFT JOIN Employees M ON E.ManagerID = M.EmployeeID;
    
    ```
    
- **Result**:
    
    
    | Employee | Manager |
    | --- | --- |
    | John Doe | NULL |
    | Jane Smith | John Doe |
    | Alex Lee | John Doe |
- **Explanation**: This query performs a self join by aliasing the `Employees` table as `E` for employees and `M` for managers.

---

### Summary of Join Types:

- **INNER JOIN**: Returns only matching rows.
- **LEFT JOIN**: Returns all rows from the left table, and matched rows from the right table.
- **RIGHT JOIN**: Returns all rows from the right table, and matched rows from the left table.
- **FULL JOIN**: Returns rows when there is a match in either left or right table.
- **CROSS JOIN**: Returns the Cartesian product of both tables (every combination of rows).
- **SELF JOIN**: Joins a table with itself.

### Functions in SQL

## **1. String Functions**

Used for manipulating and processing string values.

### **Example Functions:**

| Function | Description | Example & Output |
| --- | --- | --- |
| `UPPER()` | Converts a string to uppercase | `SELECT UPPER('hello');` → `HELLO` |
| `LOWER()` | Converts a string to lowercase | `SELECT LOWER('HELLO');` → `hello` |
| `LENGTH()` | Returns the length of a string | `SELECT LENGTH('SQL');` → `3` |
| `SUBSTRING()` | Extracts a portion of a string | `SELECT SUBSTRING('Database', 1, 4);` → `Data` |
| `CONCAT()` | Joins two or more strings | `SELECT CONCAT('SQL', ' Server');` → `SQL Server` |
| `TRIM()` | Removes spaces from both ends | `SELECT TRIM(' SQL ');` → `SQL` |
| `REPLACE()` | Replaces part of a string | `SELECT REPLACE('abc', 'b', 'z');` → `azc` |

---

## **2. Numeric Functions**

Used for mathematical operations on numeric data.

### **Example Functions:**

| Function | Description | Example & Output |
| --- | --- | --- |
| `ABS()` | Returns the absolute value | `SELECT ABS(-10);` → `10` |
| `ROUND()` | Rounds a number to the nearest integer or decimal places | `SELECT ROUND(5.678, 2);` → `5.68` |
| `CEIL()` | Rounds a number up | `SELECT CEIL(4.2);` → `5` |
| `FLOOR()` | Rounds a number down | `SELECT FLOOR(4.9);` → `4` |
| `POWER()` | Returns the power of a number | `SELECT POWER(2, 3);` → `8` |
| `SQRT()` | Returns the square root of a number | `SELECT SQRT(16);` → `4` |
| `MOD()` | Returns the remainder of division | `SELECT MOD(10, 3);` → `1` |

---

## **3. Date and Time Functions**

Used for handling and manipulating date and time values.

### **Example Functions:**

| Function | Description | Example & Output |
| --- | --- | --- |
| `NOW()` | Returns current date and time | `SELECT NOW();` → `2025-02-08 12:00:00` |
| `CURDATE()` | Returns current date | `SELECT CURDATE();` → `2025-02-08` |
| `CURTIME()` | Returns current time | `SELECT CURTIME();` → `12:00:00` |
| `DATE_ADD()` | Adds a time interval to a date | `SELECT DATE_ADD('2025-02-08', INTERVAL 10 DAY);` → `2025-02-18` |
| `DATE_SUB()` | Subtracts a time interval from a date | `SELECT DATE_SUB('2025-02-08', INTERVAL 10 DAY);` → `2025-01-29` |
| `EXTRACT()` | Extracts part of a date | `SELECT EXTRACT(YEAR FROM '2025-02-08');` → `2025` |
| `DAYNAME()` | Returns the name of the day | `SELECT DAYNAME('2025-02-08');` → `Saturday` |

---

## **4. Aggregate Functions**

Used for performing calculations on multiple rows.

### **Example Functions:**

| Function | Description | Example & Output |
| --- | --- | --- |
| `COUNT()` | Counts rows in a result set | `SELECT COUNT(*) FROM employees;` |
| `SUM()` | Returns the sum of a numeric column | `SELECT SUM(salary) FROM employees;` |
| `AVG()` | Returns the average value | `SELECT AVG(salary) FROM employees;` |
| `MAX()` | Returns the maximum value | `SELECT MAX(salary) FROM employees;` |
| `MIN()` | Returns the minimum value | `SELECT MIN(salary) FROM employees;` |

---

## **5. Conversion Functions**

Used to convert data from one type to another.

### **Example Functions:**

| Function | Description | Example & Output |
| --- | --- | --- |
| `CAST()` | Converts one data type to another | `SELECT CAST('123' AS INT);` → `123` |
| `CONVERT()` | Converts one data type to another | `SELECT CONVERT(INT, '123');` → `123` |
| `TO_DATE()` | Converts a string to a date | `SELECT TO_DATE('2025-02-08', 'YYYY-MM-DD');` |

---

## **6. Control Flow Functions**

Used to add logic in SQL queries.

### **Example Functions:**

| Function | Description | Example & Output |
| --- | --- | --- |
| `IF()` | Returns a value based on a condition | `SELECT IF(10>5, 'Yes', 'No');` → `Yes` |
| `CASE` | Evaluates conditions and returns values |  |

```sql
SELECT CASE
    WHEN salary > 5000 THEN 'High'
    WHEN salary > 3000 THEN 'Medium'
    ELSE 'Low'
END FROM employees;
``` |

---

## **7. Window Functions**
Used to perform calculations across a set of rows related to the current row.

### **Example Functions:**
| Function | Description | Example |
|----------|------------|---------|
| `RANK()` | Assigns a rank based on ordering | `SELECT employee_name, salary, RANK() OVER (ORDER BY salary DESC) FROM employees;` |
| `DENSE_RANK()` | Assigns rank without skipping values | `SELECT employee_name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) FROM employees;` |
| `ROW_NUMBER()` | Assigns a unique row number to each row | `SELECT employee_name, salary, ROW_NUMBER() OVER (ORDER BY salary DESC) FROM employees;` |

---

## **8. JSON Functions**
Used for handling JSON data (MySQL, PostgreSQL).

### **Example Functions:**
| Function | Description | Example |
|----------|------------|---------|
| `JSON_OBJECT()` | Creates a JSON object | `SELECT JSON_OBJECT('name', 'John', 'age', 30);` |
| `JSON_ARRAY()` | Creates a JSON array | `SELECT JSON_ARRAY('apple', 'banana', 'cherry');` |
| `JSON_EXTRACT()` | Extracts a value from JSON | `SELECT JSON_EXTRACT('{"name": "John"}', '$.name');` |

---

## **Conclusion**
SQL functions are powerful tools for processing and analyzing data efficiently. They simplify calculations, data transformations, and business logic in queries.

Would you like more examples or specific functions explained? 😊
```

### **Views in SQL**

**What is a View?**

A **view** in SQL is a **virtual table** based on the result of a query. It does not store data physically but provides a way to represent data from one or multiple tables in a structured and readable format.

### **Key Features of Views:**

- Acts like a table but does not store data.
- Retrieves data dynamically from underlying tables.
- Simplifies complex queries by encapsulating logic.
- Enhances security by restricting access to specific columns or rows.
- Improves maintainability and reusability.

---

## **Creating a View**

The `CREATE VIEW` statement is used to define a new view.

### **Syntax:**

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;

```

### **Example:**

Let's say we have an **Employees** table:

| emp_id | name | department | salary |
| --- | --- | --- | --- |
| 1 | John | HR | 5000 |
| 2 | Alice | IT | 7000 |
| 3 | Bob | IT | 6500 |

We create a view to show only **IT department employees**:

```sql
CREATE VIEW IT_Employees AS
SELECT emp_id, name, salary
FROM Employees
WHERE department = 'IT';

```

Now, we can retrieve data from the view like a table:

```sql
SELECT * FROM IT_Employees;

```

**Output:**

| emp_id | name | salary |
| --- | --- | --- |
| 2 | Alice | 7000 |
| 3 | Bob | 6500 |

---

## **Updating a View**

To modify an existing view, use `CREATE OR REPLACE VIEW` or `ALTER VIEW`:

```sql
CREATE OR REPLACE VIEW IT_Employees AS
SELECT emp_id, name, department, salary
FROM Employees
WHERE department = 'IT';

```

---

## **Deleting a View**

To remove a view, use:

```sql
DROP VIEW view_name;

```

Example:

```sql
DROP VIEW IT_Employees;

```

---

## **Types of Views**

### **1. Simple View**

- Based on a single table.
- Does not include aggregate functions.
- Can allow updates if no `JOIN`, `GROUP BY`, or `DISTINCT` is used.

Example:

```sql
CREATE VIEW Employee_Salary AS
SELECT name, salary
FROM Employees;

```

### **2. Complex View**

- Based on multiple tables.
- May include `JOIN`, `GROUP BY`, `HAVING`, or aggregate functions.
- Usually **read-only**.

Example:

```sql
CREATE VIEW Department_Salary AS
SELECT department, AVG(salary) AS Avg_Salary
FROM Employees
GROUP BY department;

```

---

## **Updating Data in a View**

If a view is **based on a single table** without `JOIN` or aggregation, you can `INSERT`, `UPDATE`, and `DELETE` data through the view.

Example:

```sql
UPDATE IT_Employees
SET salary = 7500
WHERE name = 'Alice';

```

### **When Can't a View be Updated?**

- If it contains `JOIN`, `GROUP BY`, or `DISTINCT`.
- If it includes aggregate functions (`SUM()`, `AVG()`, etc.).
- If it has `UNION` or `HAVING`.

---

## **Advantages of Views**

✅ **Simplifies Queries** – Stores complex queries as a simple object.

✅ **Enhances Security** – Restricts access to specific data.

✅ **Encapsulates Business Logic** – Ensures consistency across applications.

✅ **Provides Data Abstraction** – Hides table complexities from users.

---

## **Conclusion**

Views are a powerful feature in SQL that improve query simplicity, security, and maintainability. They allow users to work with pre-defined datasets without directly interacting with underlying tables.

Would you like an example of a **view with joins** or a **real-world use case**? 😊

### Alises

In SQL, **aliases** are temporary names given to **tables** or **columns** to make queries more readable, simplify complex expressions, or reference the same table multiple times (as in self-joins).

## 🔹 Types of Aliases in SQL

There are two main types of aliases:

### 1. **Column Aliases**

- Used to rename a column's output.
- Often used with `AS` (though `AS` is optional).

### ✅ Example:

```sql
SELECT first_name AS Name, salary * 12 AS AnnualSalary
FROM Employees;

```

### 🔍 Output:

| Name | AnnualSalary |
| --- | --- |
| Alice | 72000 |
| Bob | 96000 |
- Here, `first_name` is shown as `Name`.
- `salary * 12` is shown as `AnnualSalary`.

---

### 2. **Table Aliases**

- Used to rename a table temporarily in the query.
- Useful in joins, especially **self-joins** or when dealing with multiple tables with similar columns.

### ✅ Example (with self-join):

```sql
SELECT e1.name AS Employee, e2.name AS Manager
FROM Employees e1
JOIN Employees e2 ON e1.manager_id = e2.id;

```

- `e1` and `e2` are table aliases for the same `Employees` table.
- This allows referencing the same table twice — once for employees, once for managers.

---

## 🔸 Syntax Summary

### Column Alias:

```sql
SELECT column_name AS alias_name
FROM table_name;

```

### Table Alias:

```sql
SELECT *
FROM table_name AS alias_name;

```

> 🔹 Note: AS is optional — you can also write column_name alias_name or table_name alias_name.
> 

---

## 🧠 Why Use Aliases?

| Use Case | Benefit |
| --- | --- |
| Simplify long expressions | Makes code cleaner (`salary * 12 AS Annual`) |
| Handle self-joins | Needed to reference same table multiple times |
| Improve readability | More descriptive column/table names |
| Shorten table names | Useful in complex joins (`Orders o`, `Customers c`) |

---

## 🧪 Practical Example: Join with Aliases

```sql
SELECT o.id AS OrderID, c.name AS CustomerName
FROM Orders o
JOIN Customers c ON o.customer_id = c.id;

```

- `o` is alias for `Orders`
- `c` is alias for `Customers`


</details>