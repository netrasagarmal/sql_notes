# SQL & DBMS Basic QNA
<details>
## SQL QnA

### **1. What is a database?**

A **database** is an organized collection of structured information or data, typically stored in a computer system. A database allows data to be easily accessed, managed, modified, updated, controlled, and organized.

> Example:
> 
> 
> A school database might store data about students, teachers, classes, and grades.
> 

---

### **2. What is a Database Management System (DBMS)?**

A **DBMS** is software that interacts with users, applications, and the database itself to capture and analyze data. It provides tools for creating, retrieving, updating, and managing data in a database.

> Examples of DBMSs:
> 
- MySQL
- PostgreSQL
- Oracle DB
- Microsoft SQL Server
- MongoDB (for NoSQL)

---

### **3. What is a relational database?**

A **relational database** stores data in **tables (also called relations)** that are connected through **relationships**. Each table has rows (records) and columns (attributes), and each row has a unique ID called a **primary key**.

> Example:
> 
> 
> A `Customers` table:
> | CustomerID | Name     | Email             |
> |------------|----------|-------------------|
> | 1          | Alice    | alice@mail.com    |
> | 2          | Bob      | bob@mail.com      |
> 

A `Orders` table:

| OrderID | CustomerID | Product |
| --- | --- | --- |
| 101 | 1 | Laptop |
| 102 | 2 | Keyboard |

The `CustomerID` column in `Orders` is a **foreign key** referencing the `Customers` table.

---

### **4. What is a non-relational database?**

A **non-relational database** (NoSQL) does **not use tables** to store data. Instead, it uses various models like **document**, **key-value**, **wide-column**, or **graph**.

> Example:
> 
> 
> A **document-based** database like MongoDB:
> 

```json
{
  "CustomerID": 1,
  "Name": "Alice",
  "Email": "alice@mail.com",
  "Orders": [
    {"OrderID": 101, "Product": "Laptop"}
  ]
}

```

---

### **5. Explain the difference between OLTP and OLAP.**

| Feature | OLTP (Online Transaction Processing) | OLAP (Online Analytical Processing) |
| --- | --- | --- |
| Purpose | Handle real-time transaction processing | Analyze large volumes of data |
| Operations | Read/write (Insert, Update, Delete) | Read-heavy (queries, aggregation) |
| Data volume | Small to medium | Large data warehouses |
| Users | End-users (e.g., banking systems) | Analysts, decision-makers |
| Example | ATM withdrawals, e-commerce orders | Business intelligence, sales trends |

---

### **6. What are the advantages of using a DBMS?**

- **Data integrity and accuracy**
- **Efficient data access** through indexing and query optimization
- **Data security** and user access control
- **Backup and recovery**
- **Data abstraction and independence**
- **Concurrent access and transaction management**

---

### **7. What are the three levels of database design?**

### a. **Conceptual Level**:

- Focuses on **what** data should be stored.
- High-level view, independent of physical implementation.
- Tools: **ER diagrams**

> Example: Diagram showing entities like Student, Course, and relationships like "enrolls".
> 

### b. **Logical Level**:

- Defines **how** the data will be structured (e.g., tables, columns, data types).
- Still independent of the actual DBMS.

### c. **Physical Level**:

- Deals with **how data is stored** in files, indexes, and memory.
- Concerned with performance and storage.

---

### **8. What is data modeling?**

**Data modeling** is the process of creating a **visual representation** of a system's data. It helps understand data relationships and rules.

- Ensures consistency
- Simplifies communication between stakeholders
- Aids in database design

---

### **9. What are the different types of data models?**

### a. **Relational Model**:

- Uses tables, rows, and columns.
- SQL-based.
- Most popular for structured data.

### b. **Object-Oriented Model**:

- Stores data as **objects**, like in OOP (Object-Oriented Programming).
- Supports complex data types, inheritance.

> Example: PostgreSQL supports object-relational features.
> 

### c. **Hierarchical Model**:

- Organizes data in a **tree-like structure**.
- Each parent can have many children, but each child has only one parent.

> Example: IBM's IMS database.
> 

### d. **Network Model**:

- More flexible than hierarchical, supports many-to-many relationships.

---

### **10. What is an Entity-Relationship (ER) model?**

An **ER model** is a high-level conceptual data model used in **conceptual database design**. It represents data as:

- **Entities**: Objects (e.g., Student, Course)
- **Attributes**: Properties (e.g., Student has Name, Age)
- **Relationships**: Connections (e.g., Student *enrolls in* Course)

> Example ER Diagram:
> 

```
[Student] —enrolls—> [Course]
  |                     |
Name, Age           Title, Credits

```

ER modeling helps translate business requirements into a database structure before physical implementation.

### **Explain Normalization and Denormalization**

### ✅ **Normalization**

Normalization is the process of **organizing data in a database** to reduce **data redundancy** and improve **data integrity**. It involves dividing large tables into smaller, related tables and defining relationships using **keys**.

> Goal:
> 
> 
> Avoid duplicate data, ensure data consistency, and simplify updates.
> 

> Example (Before Normalization):
> 

| StudentID | StudentName | Course1 | Course2 |
| --- | --- | --- | --- |
| 1 | Alice | Math | Physics |
| 2 | Bob | Math | NULL |

> After Normalization (2 Tables):
> 

**Students Table:**

| StudentID | StudentName |
| --- | --- |
| 1 | Alice |
| 2 | Bob |

**Enrollments Table:**

| StudentID | Course |
| --- | --- |
| 1 | Math |
| 1 | Physics |
| 2 | Math |

---

### ❌ **Denormalization**

Denormalization is the process of **combining normalized tables** to improve **read performance** at the cost of some redundancy.

> Example:
> 
> 
> Instead of joining `Customers` and `Orders`, you store customer name directly in the `Orders` table to reduce joins in read-heavy applications like reporting.
> 

---

## ✅ What are Normal Forms?

**Normal Forms** are rules used in database design to reduce **redundancy** (duplicate data) and avoid **anomalies** (update/delete errors). They're applied step by step — each level improves structure.

Let’s go step by step 👇

---

## 🔹 **1st Normal Form (1NF)** — *"Atomic values only"*

A table is in **1NF** if:

- Each cell has a **single (atomic) value** — no multiple values in one cell.

### ❌ Not in 1NF:

| Student | Subjects |
| --- | --- |
| A | Math, English |

> Here, Subjects has multiple values — that's not allowed.
> 

### ✅ In 1NF:

| Student | Subject |
| --- | --- |
| A | Math |
| A | English |

Now each field holds one value → **1NF satisfied**.

---

## 🔹 **2nd Normal Form (2NF)** — *"Fully functionally dependent"*

A table is in **2NF** if:

- It is already in **1NF**.
- **Every non-key column** depends on the **entire primary key**, not just part of it.

### ❌ Not in 2NF:

| StudentID | Course | StudentName |
| --- | --- | --- |
| 1 | Math | Alice |
| 1 | English | Alice |

> Primary Key = (StudentID, Course)
> 
> 
> But `StudentName` only depends on `StudentID` → partial dependency ❌
> 

### ✅ In 2NF (split into two tables):

**Table 1**: Course Enrollment

| StudentID | Course |
| --- | --- |
| 1 | Math |

**Table 2**: Student Info

| StudentID | StudentName |
| --- | --- |
| 1 | Alice |

→ No partial dependency → **2NF satisfied**

---

## 🔹 **3rd Normal Form (3NF)** — *"No transitive dependency"*

A table is in **3NF** if:

- It is already in **2NF**
- There are **no transitive dependencies** (non-key depends on non-key)

### ❌ Not in 3NF:

| StudentID | DeptID | DeptName |
| --- | --- | --- |
| 1 | 101 | Science |

> DeptName depends on DeptID, not directly on StudentID → transitive dependency ❌
> 

### ✅ In 3NF:

**Table 1**: Student Info

| StudentID | DeptID |
| --- | --- |
| 1 | 101 |

**Table 2**: Department Info

| DeptID | DeptName |
| --- | --- |
| 101 | Science |

→ No transitive dependency → **3NF satisfied**

---

## 🔹 **Boyce-Codd Normal Form (BCNF)** — *"Stricter than 3NF"*

A table is in **BCNF** if:

- It is already in **3NF**
- For every dependency `X → Y`, `X` must be a **super key**

### ❗ When 3NF is not enough:

Rare case where:

- A non-super key determines a key column → violates BCNF

---

## 🔹 **4th Normal Form (4NF)** — *"No multi-valued dependencies"*

A table is in **4NF** if:

- It is in **BCNF**
- There are **no multi-valued dependencies**

### ❌ Example of multi-valued dependency:

| Student | Language | Hobby |
| --- | --- | --- |
| A | English | Music |
| A | French | Music |
| A | English | Drawing |
| A | French | Drawing |

> Language and Hobby are independent attributes for Student → leads to data explosion ❌
> 

### ✅ In 4NF:

Split into two tables:

- Student-Language
- Student-Hobby

---

## 🔹 **5th Normal Form (5NF)** — *"No join dependency"*

A table is in **5NF** if:

- It is in **4NF**
- It cannot be broken into smaller tables **without losing data** when joined back

Used in **very advanced database designs** where data is decomposed a lot (rare in typical systems).

---

## ✅ Summary Table:

| Normal Form | Fixes Problems Like | Key Condition |
| --- | --- | --- |
| 1NF | Multi-valued cells | Atomic values only |
| 2NF | Partial dependency | Full dependency on entire primary key |
| 3NF | Transitive dependency | No non-key depending on non-key |
| BCNF | Exceptions to 3NF | Every determinant is a super key |
| 4NF | Multi-valued dependencies | No independent multi-values |
| 5NF | Join dependencies | No unnecessary joins |

---

Would you like a visual ERD-style explanation or quiz questions to test your understanding?

### **What is data redundancy and why is it important to avoid it?**

**Data redundancy** means storing the same data in multiple places.

> Why to avoid:
> 
- Increases **storage costs**
- Leads to **data anomalies** (insertion, update, deletion)
- Makes data **inconsistent**

> Example: If a customer’s address is stored in multiple tables and one is updated but the others are not—leads to inconsistency.
> 

---

### **What are primary and foreign keys?**

### 🔑 **Primary Key**

- Uniquely identifies each record in a table.
- Cannot contain NULL values.

> Example: In Students(StudentID, Name), StudentID is the primary key.
> 

### 🔗 **Foreign Key**

- A field in one table that references the **primary key** of another table.
- Creates relationships between tables.

> Example: In Enrollments(StudentID, CourseID), StudentID is a foreign key referencing Students.
> 

---

### **What are constraints in a database?**

**Constraints** are rules enforced on data columns to maintain data integrity.

### Common Constraints:

- `PRIMARY KEY`: Unique and not null
- `FOREIGN KEY`: Maintains referential integrity
- `NOT NULL`: Prevents null values
- `UNIQUE`: Prevents duplicate values
- `CHECK`: Ensures values meet a condition (e.g., age > 0)
- `DEFAULT`: Assigns default value if none provided

> Example:
> 

```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Age INT CHECK (Age >= 18)
);

```

---

### **How would you design a database for [specific application/scenario]?**

> Let's say the scenario is "Online Bookstore"
> 

### Step-by-step design:

1. **Identify entities**: Users, Books, Orders, Categories
2. **Define attributes**:
    - Users: UserID, Name, Email
    - Books: BookID, Title, Price, CategoryID
    - Orders: OrderID, UserID, OrderDate
    - OrderItems: OrderID, BookID, Quantity
3. **Define relationships**:
    - A user can place many orders
    - An order can contain many books
    - A book belongs to one category

---

### **Explain the process of designing a database schema.**

### ✅ **Steps:**

1. **Requirement Analysis**
    - Understand what data needs to be stored and retrieved
2. **Identify Entities and Relationships**
    - Determine major objects (e.g., Users, Products) and how they interact
3. **Create ER Diagram**
    - Visually represent entities, attributes, and relationships
4. **Choose Data Types**
    - Select appropriate data types for each attribute (INT, VARCHAR, DATE, etc.)
5. **Normalize Data**
    - Apply normalization up to 3NF to eliminate redundancy
6. **Define Primary and Foreign Keys**
    - Ensure every table has a primary key and use foreign keys to link related tables
7. **Implement Constraints**
    - Use constraints (NOT NULL, CHECK, etc.) to enforce business rules
8. **Physical Design**
    - Optimize indexes, partitions, and storage depending on usage

> Example Schema Snippet (for Bookstore):
> 

```sql
CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    Title VARCHAR(100),
    Price DECIMAL(10, 2),
    CategoryID INT,
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);
```

### **1. What are Subqueries?**

### ✅ **Definition:**

A **subquery** (or **inner query**) is a **SQL query nested inside another SQL query**, typically inside a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement or within a clause such as `WHERE`, `FROM`, or `HAVING`.

Subqueries help break complex problems into manageable parts and allow querying based on the results of another query.

---

### 🔹 **Types of Subqueries:**

- **Single-row subquery**: Returns one value
- **Multi-row subquery**: Returns multiple values
- **Correlated subquery**: Depends on the outer query for its values
- **Nested subquery**: A subquery inside another subquery

---

### 📌 **Example: Find employees with salaries higher than the average salary**

```sql
SELECT name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

```

Here, the subquery calculates the average salary, and the outer query fetches employees earning more than that.

---

### **2. Explain the Use of Indexes**

### ✅ **Definition:**

An **index** in a database is a data structure (like a B-tree or hash table) that improves the **speed of data retrieval** operations on a table at the cost of additional **space** and **slower writes** (INSERT/UPDATE/DELETE).

Indexes function like the index of a book—helping the database engine locate data quickly without scanning every row.

---

### 🔍 **Why use indexes?**

- **Faster SELECT queries**
- **Efficient JOINs, WHERE clauses, and ORDER BY**
- **Improve lookup performance for large tables**

---

### 📌 **Example: Creating an index on a column**

```sql
CREATE INDEX idx_employee_name
ON employees(name);

```

Now, searching `WHERE name = 'Alice'` will be much faster.

---

### **3. What are the Different Types of Indexes?**

---

### 🔸 **a) Clustered Index**

- Determines the **physical order** of data in the table.
- Only **one clustered index** is allowed per table.
- The table **is** the index.

> 📌 Example: In SQL Server, if you create a primary key, it creates a clustered index by default.
> 

```sql
CREATE CLUSTERED INDEX idx_emp_id
ON employees(emp_id);

```

This means data rows are **sorted** physically by `emp_id`.

---

### 🔸 **b) Non-Clustered Index**

- **Separate** from the table.
- Contains **pointers** to the actual data rows.
- You can create **multiple non-clustered indexes** on a table.

> 📌 Example:
> 

```sql
CREATE NONCLUSTERED INDEX idx_emp_name
ON employees(name);

```

This builds an index tree of `name`, which points to actual row locations.

---

### 🧠 **Summary Table:**

| Feature | Clustered Index | Non-Clustered Index |
| --- | --- | --- |
| Data Order | Physical | Logical (separate structure) |
| Number per table | One | Many |
| Speed (read) | Faster for range queries | Faster for specific lookups |
| Storage | Part of the table | Separate from the table |

---

### **4. How Would You Optimize SQL Queries for Performance?**

### ✅ **Best Practices:**

1. **Use Proper Indexing**

- Index frequently filtered or joined columns
- Avoid indexing columns with high update frequency unless necessary

**2. Avoid SELECT** 

- Fetch only the columns you need

```sql
SELECT name, age FROM employees;

```

3. **Use WHERE Clause with Filtering Conditions**

- Reduces result set size

```sql
SELECT * FROM orders WHERE status = 'Delivered';

```

4. **Avoid Functions on Indexed Columns**

- Using functions disables index usage

```sql
-- Bad: disables index
WHERE YEAR(order_date) = 2024

-- Better:
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31'

```

### 5. **Use JOINs Instead of Subqueries Where Appropriate**

- JOINs are often more efficient than correlated subqueries

### 6. **Use EXPLAIN (or Execution Plan)**

- Helps analyze how the database executes your query

```sql
EXPLAIN SELECT * FROM orders WHERE status = 'Pending';

```

### 7. **Limit Result Sets**

- Use `LIMIT` or `TOP` to restrict the number of rows for large queries

### 8. **Optimize JOINs**

- Use appropriate keys and indexes
- Avoid joining large tables unnecessarily

### 9. **Normalize for Storage Efficiency**

- Reduce redundancy, smaller tables = faster access

### 10. **Denormalize for Reporting**

- Create materialized views or summary tables for analytics

### **1. What is Data Integrity?**

### ✅ **Definition:**

**Data integrity** refers to the **accuracy, consistency, and reliability** of data stored in a database. It ensures that data is **correct**, **valid**, and **maintained throughout its lifecycle**, especially during operations like insert, update, or delete.

### 🔍 **Types of Data Integrity:**

- **Entity Integrity:** Ensures each row in a table has a unique, non-null primary key.
- **Referential Integrity:** Maintains consistency between related tables using foreign keys.
- **Domain Integrity:** Ensures values in a column are from a defined domain (e.g., data type, range).
- **User-defined Integrity:** Business rules (e.g., salary > 0).

### 📌 **Example:**

If a `Student` table has a `StudentID` as the primary key, entity integrity ensures that:

```sql
INSERT INTO Students(StudentID, Name) VALUES (NULL, 'Alice'); -- ❌ Fails (NULL not allowed)

```

---

### **2. What is Referential Integrity?**

### ✅ **Definition:**

**Referential integrity** is a type of data integrity that ensures **relationships between tables** remain consistent. Specifically, it means that **foreign keys must match a primary key** in the referenced table or be NULL.

### 📌 **Example:**

Two tables:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

```

You cannot insert an order with `CustomerID = 999` unless that ID exists in the `Customers` table.

---

### **3. What are Transactions?**

### ✅ **Definition:**

A **transaction** is a sequence of one or more SQL operations that are executed as a **single logical unit of work**. It either **completes entirely (COMMIT)** or **does nothing at all (ROLLBACK)** if any part fails.

> Think of a bank transfer: deduct from one account and add to another. If either fails, the whole operation should fail.
> 

### 📌 **Example:**

```sql
BEGIN;

UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;

COMMIT;

```

If the second `UPDATE` fails, the transaction can be rolled back to avoid inconsistent data.

---

### **4. What are ACID Properties?**

ACID properties ensure **reliable processing** of transactions in a database.

### 🔸 **A – Atomicity**

- A transaction is **all or nothing**
- If one part fails, the entire transaction fails

> 💡 Example: Bank transfer. If debit succeeds but credit fails, rollback both.
> 

---

### 🔸 **C – Consistency**

- A transaction moves the database from one **valid state to another**
- All constraints (like foreign keys) remain intact

> 💡 Example: Transferring money should not violate balance constraints or relationships.
> 

---

### 🔸 **I – Isolation**

- Concurrent transactions are **independent** of each other
- Partial results of one transaction are not visible to others until it is committed

> 💡 Example: Two users booking the last seat on a flight — isolation prevents both from succeeding.
> 

---

### 🔸 **D – Durability**

- Once a transaction is **committed**, it is **permanently stored**, even if the system crashes

> 💡 Example: If a transaction is committed before a power outage, it remains saved after recovery.
> 

---

### **5. Explain Concurrency Control**

### ✅ **Definition:**

**Concurrency control** is the management of **simultaneous operations** on a database to prevent **conflicts**, **data anomalies**, and ensure **transaction isolation**.

### 🔍 **Why Needed?**

- Prevents issues like:
    - **Lost Updates**
    - **Dirty Reads**
    - **Non-repeatable Reads**
    - **Phantom Reads**

---

### 🔸 **Techniques for Concurrency Control:**

- **Locking** (pessimistic):
    - **Read Lock (Shared)** – multiple reads allowed
    - **Write Lock (Exclusive)** – only one writer
- **Timestamp Ordering**
- **Optimistic Concurrency Control** – assumes no conflicts, checks before commit
- **Multiversion Concurrency Control (MVCC)** – keeps multiple versions of data for isolation

> 📌 Example:
Two users trying to update the same record:
> 

```sql
-- User A begins transaction
BEGIN;
UPDATE Inventory SET Stock = Stock - 1 WHERE ItemID = 1;

-- User B also begins transaction
BEGIN;
UPDATE Inventory SET Stock = Stock - 1 WHERE ItemID = 1; -- This may be blocked or fail

```

Locks or MVCC would ensure correctness.

---

### **6. How Would You Handle Data Backups and Recovery?**

### ✅ **Definition:**

**Data backup** is the process of creating **copies of database data** to prevent loss, and **recovery** is the process of restoring data from backups after a failure.

---

### 🔸 **Types of Backups:**

- **Full Backup**: Entire database
- **Incremental Backup**: Only data changed since last backup
- **Differential Backup**: Data changed since last full backup

---

### 🔸 **Recovery Techniques:**

- **Restore from backup** + **replay transaction logs**
- Use **RAID**, **snapshots**, or **cloud backups**
- Ensure **automatic scheduled backups** and **off-site storage**

---

### 📌 **Example Backup Command (PostgreSQL):**

```bash
pg_dump -U db_user -F c -b -v -f backup_file.backup my_database

```

### 📌 **Example Recovery:**

After a crash:

1. Restore the full backup
2. Apply logs to replay changes made after the backup

### **1. What Are Common Performance Bottlenecks in a Database?**

### ✅ **Definition:**

A **performance bottleneck** in a database occurs when a particular component or process **slows down overall database performance**, affecting query response times, throughput, or resource usage.

---

### 🔹 **Common Bottlenecks Include:**

1. **Slow Queries**
    - Poorly written SQL, lack of indexes, or unnecessary joins.
    - Example: Using `SELECT *` or missing `WHERE` clauses.
2. **Lack of Indexing**
    - Full table scans for large datasets.
    - Example: Query on a column with no index:
        
        ```sql
        SELECT * FROM orders WHERE status = 'shipped';
        
        ```
        
3. **Locking and Blocking**
    - Long-running transactions or deadlocks prevent other transactions from proceeding.
4. **Insufficient Hardware Resources**
    - Limited CPU, memory, or disk I/O throughput.
5. **High Concurrency Load**
    - Too many users or processes querying simultaneously.
6. **Improper Data Modeling**
    - Bad normalization or denormalization, redundant data.
7. **Missing or Inefficient Caching**
    - Re-executing the same queries without caching results.

---

### **2. What Are Different Techniques for Optimizing Database Performance?**

### ✅ **Definition:**

**Database performance optimization** refers to techniques used to **speed up data retrieval and storage** while ensuring consistency, availability, and correctness.

---

### 🔹 **Key Techniques Include:**

---

### 🟡 **1. Indexing**

- **Definition**: Creating structures to allow faster lookups.
- Example:
    
    ```sql
    CREATE INDEX idx_name ON employees(name);
    
    ```
    
- Benefit: Reduces lookup time from O(n) to O(log n) in large datasets.

---

### 🟡 **2. Partitioning**

- **Definition**: Dividing large tables into smaller, manageable pieces (called partitions) based on criteria like range, hash, or list.
- Benefit: Improves query performance and maintenance.

---

### 🟡 **3. Query Optimization**

- Using EXPLAIN plans, rewriting subqueries, reducing joins, selecting needed columns.

---

### 🟡 **4. Caching**

- **Definition**: Storing frequently accessed data in-memory to reduce redundant queries.
- Types:
    - Application-level (e.g., Redis, Memcached)
    - Database-level (e.g., PostgreSQL shared buffers)

---

### 🟡 **5. Connection Pooling**

- Reusing database connections to reduce overhead of opening/closing connections.

---

### 🟡 **6. Materialized Views**

- Precompute and store query results for complex aggregations.

---

### 🟡 **7. Archiving and Purging Old Data**

- Removes unnecessary load from active datasets.

---

### **3. What Is Database Partitioning?**

### ✅ **Definition:**

**Database partitioning** is the process of dividing a large table (or index) into **smaller, more manageable segments**, called **partitions**, based on a defined strategy, so queries can run faster and data management becomes easier.

Each partition can be stored separately and queried independently, even though it appears as a single table to users.

---

### 🔹 **Types of Partitioning:**

- **Range Partitioning** – e.g., based on date ranges
- **List Partitioning** – e.g., based on predefined values (e.g., region = 'US')
- **Hash Partitioning** – e.g., evenly distribute data using a hash function
- **Composite Partitioning** – combination of the above

---

### 📌 **Example: Range Partitioning**

```sql
CREATE TABLE sales (
  id INT,
  sale_date DATE,
  amount DECIMAL
)
PARTITION BY RANGE (sale_date) (
  PARTITION p_2023 VALUES LESS THAN ('2024-01-01'),
  PARTITION p_2024 VALUES LESS THAN ('2025-01-01')
);

```

Now, a query on 2024 data will only scan partition `p_2024`.

---

### ✅ **Benefits of Partitioning:**

- Improves **query performance**
- Allows **faster backups** and **archiving**
- Enables **parallel processing**
- Reduces **index size** per partition

---

### **4. How Would You Troubleshoot a Performance Issue in a Database?**

### ✅ **Definition:**

Troubleshooting a performance issue involves identifying the root cause of **slow query performance, resource contention, or failures**, and applying the appropriate fixes.

---

### 🔹 **Step-by-Step Troubleshooting Process:**

---

1. **Identify Symptoms**
    - Slow response times
    - Increased CPU/memory usage
    - Deadlocks or timeouts

---

1. **Analyze Slow Queries**
    - Use tools like `EXPLAIN`, `ANALYZE`, or SQL Server’s Query Profiler.
    - Look for:
        - Full table scans
        - Missing indexes
        - Large joins or nested subqueries

---

1. **Check Index Usage**
    - Ensure proper indexes exist on frequently filtered or joined columns.
    - Detect unused or bloated indexes.

---

1. **Monitor Resource Usage**
    - CPU, memory, disk I/O, and network bandwidth.
    - Use tools like `top`, `htop`, database dashboards, or cloud monitoring.

---

1. **Inspect Locking/Blocking**
    - Use tools to see who is holding locks and causing blocking (e.g., `pg_stat_activity` in PostgreSQL)

---

1. **Review Query Execution Plans**
    - Look at cost, number of rows read, type of join used, and use of indexes.

---

1. **Check Database Configuration**
    - Connection pool size, cache size, buffer size, parallel execution settings.

---

1. **Test with Simulated Load**
    - Use tools like Apache JMeter or custom scripts to simulate traffic.

---

### 📌 **Example Scenario:**

**Problem**: A report query takes 2 minutes to load.

**Diagnosis:**

- Use `EXPLAIN` to find a full table scan on a 5M-row table.
- See that the `status` column is not indexed.

**Solution:**

```sql
CREATE INDEX idx_status ON reports(status);

```

---

### **1. What is Database Replication?**

### ✅ **Definition:**

**Database replication** is the process of **copying and maintaining database objects (like tables or entire databases)** in multiple locations (usually servers). This allows for **redundancy**, **high availability**, **disaster recovery**, and **load balancing**.

---

### 🔹 **Types of Replication:**

- **Master-Slave Replication:** One primary node handles writes, replicas handle reads.
- **Master-Master Replication:** Multiple nodes allow both read and write operations.
- **Synchronous vs. Asynchronous Replication:** Immediate vs. delayed syncing.

---

### 📌 **Example:**

In MySQL:

- A **primary server** handles insert/update/delete.
- A **replica server** gets updates via binary logs and applies them.

Use case: A web app reads data from replicas to reduce load on the primary.

---

### **2. What is Sharding?**

### ✅ **Definition:**

**Sharding** is a **horizontal partitioning** technique that splits a large database into smaller, **independent parts called shards**, each stored on a different server. Each shard contains a subset of the data.

---

### 📌 **Example:**

A `Users` table with 10 million users can be split:

- Shard 1: Users with `user_id` 1–3M
- Shard 2: Users with `user_id` 3M–6M
- Shard 3: Users with `user_id` 6M–10M

This distributes both **storage** and **query load** across multiple servers.

---

### **3. What is the CAP Theorem?**

### ✅ **Definition:**

The **CAP theorem** states that in a distributed system, it is **impossible** to simultaneously guarantee all three of the following:

- **C – Consistency:** Every read receives the most recent write.
- **A – Availability:** Every request receives a (non-error) response.
- **P – Partition Tolerance:** The system continues to work despite network failures.

---

### 🔹 **Trade-offs:**

A distributed system can only **guarantee two out of three**:

- **CP systems** (Consistency + Partition tolerance): sacrifice availability
    
    *Example: HBase*
    
- **AP systems** (Availability + Partition tolerance): sacrifice consistency
    
    *Example: Couchbase*
    
- **CA systems** (Consistency + Availability): not possible under partition tolerance

---

### **4. What Are NoSQL Databases and When Would You Use Them?**

### ✅ **Definition:**

**NoSQL databases** are **non-relational databases** designed to handle **large volumes of unstructured, semi-structured, or structured data**. They provide high **scalability**, **flexibility**, and **performance** for modern applications.

---

### 🔹 **Types of NoSQL Databases:**

- **Document-based (e.g., MongoDB)**
- **Key-Value Stores (e.g., Redis)**
- **Wide-Column Stores (e.g., Cassandra)**
- **Graph Databases (e.g., Neo4j)**

---

### 🔹 **When to Use:**

- Schema flexibility is needed
- Handling big data and high throughput
- Storing hierarchical or nested data (e.g., JSON)
- High availability over strict consistency

---

### 📌 **Example:**

In MongoDB:

```json
{
  "name": "Alice",
  "orders": [{"id": 1, "product": "Laptop"}, {"id": 2, "product": "Phone"}]
}

```

---

### **5. What is a Materialized View?**

### ✅ **Definition:**

A **materialized view** is a **precomputed, stored result of a query**. Unlike regular views, which are virtual and recomputed on access, materialized views **store actual data**, which can be refreshed periodically.

---

### 📌 **Example:**

```sql
CREATE MATERIALIZED VIEW total_sales AS
SELECT customer_id, SUM(amount) AS total
FROM sales
GROUP BY customer_id;

```

Used for faster querying of complex aggregations like dashboards or reports.

---

### **6. What is a Stored Procedure?**

### ✅ **Definition:**

A **stored procedure** is a **precompiled set of one or more SQL statements**, stored in the database, which can be executed repeatedly by calling its name.

---

### 📌 **Example:**

```sql
CREATE PROCEDURE GetOrdersByCustomer(IN customer_id INT)
BEGIN
  SELECT * FROM orders WHERE customer_id = customer_id;
END;

```

You can call this with:

```sql
CALL GetOrdersByCustomer(101);

```

Used for encapsulating business logic, reusability, and performance.

---

### **7. What is a Trigger?**

### ✅ **Definition:**

A **trigger** is a **special procedure** that **automatically runs** in response to certain events on a table (e.g., `INSERT`, `UPDATE`, `DELETE`).

---

### 📌 **Example:**

```sql
CREATE TRIGGER log_update
AFTER UPDATE ON employees
FOR EACH ROW
INSERT INTO employee_log(emp_id, action) VALUES (OLD.id, 'updated');

```

Used for auditing, enforcing rules, or automating tasks.

---

### **8. What is a View?**

### ✅ **Definition:**

A **view** is a **virtual table** based on a SQL query. It does not store data but presents data from one or more tables in a customized way.

---

### 📌 **Example:**

```sql
CREATE VIEW active_customers AS
SELECT name, email FROM customers WHERE is_active = TRUE;

```

Querying the view:

```sql
SELECT * FROM active_customers;

```

Used to simplify complex queries, restrict access, and provide abstraction.

---

### 🔹 **OLTP vs OLAP**

1. **What is OLTP?**
    - **Answer**: OLTP (Online Transaction Processing) is a database system optimized for handling a large number of short online transactions (like INSERT, UPDATE, DELETE).
    - **Example**: A banking system where each deposit/withdrawal is a transaction.
2. **What is OLAP?**
    - **Answer**: OLAP (Online Analytical Processing) is designed for analyzing and querying large amounts of data, mostly read-heavy.
    - **Example**: A sales dashboard analyzing monthly revenue trends.
3. **What is the main difference between OLTP and OLAP?**
    - **Answer**:
        - OLTP: Fast read/write, highly normalized data, supports real-time transactions.
        - OLAP: Slow updates, denormalized data, supports complex queries and aggregations.
4. **Can one system serve both OLTP and OLAP?**
    - **Answer**: Typically, no. Modern architectures often separate them using data warehousing (OLAP) and operational DBs (OLTP). Some use HTAP (Hybrid Transaction/Analytical Processing).
5. **Why is normalization common in OLTP systems?**
    - **Answer**: To avoid redundancy, maintain data integrity, and support fast inserts/updates with smaller table sizes.

---

### 🔹 **Indexing (Clustered & Non-Clustered)**

1. **What is an index in SQL?**
    - **Answer**: An index is a data structure that improves the speed of data retrieval. Think of it like a book’s index to quickly locate information.
2. **What is a clustered index?**
    - **Answer**: A clustered index determines the physical order of rows in the table. A table can have only **one** clustered index.
    - **Example**: If you create a clustered index on `EmployeeID`, the rows are physically sorted by `EmployeeID`.
3. **What is a non-clustered index?**
    - **Answer**: A non-clustered index creates a separate structure that points to the actual data row. A table can have **many** non-clustered indexes.
4. **Which index type is better for range queries?**
    - **Answer**: Clustered index is better for range queries (e.g., dates) because data is physically ordered.
5. **Can we create a clustered index on a view?**
- **Answer**: Yes, in SQL Server, indexed views are possible and can have a clustered index, but it requires meeting specific rules.

---

### 🔹 **Views**

1. **What is a view in SQL?**
- **Answer**: A view is a virtual table based on a SELECT query. It doesn’t store data itself, only the SQL logic.
1. **Why use views?**
- **Answer**:
    - Simplifies complex queries.
    - Provides security by hiding columns.
    - Can join multiple tables in one object.
1. **Can a view be updated?**
- **Answer**: Yes, if it’s based on a single table without GROUP BY, DISTINCT, etc. Otherwise, it may be read-only.
1. **What is a materialized view?**
- **Answer**: A view that stores the result set physically. Useful for performance in OLAP. Common in Oracle/PostgreSQL.
1. **Difference between a view and a table?**
- **Answer**:
    - Table: Stores data physically.
    - View: Virtual, doesn’t store data (except materialized views).

---

### 🔹 **Stored Procedures**

1. **What is a stored procedure?**
- **Answer**: A saved set of SQL statements that can be executed repeatedly. Think of it like a function.
1. **Why use stored procedures?**
- **Answer**:
    - Improves performance via precompiled execution.
    - Promotes reusability.
    - Enhances security and modularity.
1. **Can a stored procedure return a value?**
- **Answer**: Yes, using output parameters or `RETURN`.
1. **Can you pass parameters to a stored procedure?**
- **Answer**: Yes, you can pass input and output parameters to customize behavior.
1. **How are stored procedures different from functions?**
- **Answer**:
    - Procedures: Can return 0 or more values, can perform actions (INSERT, UPDATE).
    - Functions: Must return a value, generally used in SELECTs.

---

### 🔹 **Normalization**

1. **What is normalization?**
- **Answer**: The process of organizing data to reduce redundancy and improve integrity.
1. **What is 1NF (First Normal Form)?**
- **Answer**: Ensures each column contains atomic (indivisible) values. No repeating groups.
- **Example**: Instead of `Phone = "123, 456"`, separate into two rows.
1. **What is 2NF (Second Normal Form)?**
- **Answer**: Removes partial dependency; every non-key column should depend on the whole primary key (applies to composite keys).
1. **What is 3NF (Third Normal Form)?**
- **Answer**: Removes transitive dependency. Non-key attributes should not depend on other non-key attributes.
1. **What are BCNF, 4NF, and 5NF?**
- **Answer**:
    - **BCNF** (Boyce-Codd NF): Stricter version of 3NF.
    - **4NF**: Removes multi-valued dependencies.
    - **5NF**: Deals with join dependency to ensure no data loss when decomposing tables.

---

### 🔹 **OLTP vs OLAP**

1. **What is OLTP?**
    - **Answer**: OLTP (Online Transaction Processing) is a database system optimized for handling a large number of short online transactions (like INSERT, UPDATE, DELETE).
    - **Example**: A banking system where each deposit/withdrawal is a transaction.
2. **What is OLAP?**
    - **Answer**: OLAP (Online Analytical Processing) is designed for analyzing and querying large amounts of data, mostly read-heavy.
    - **Example**: A sales dashboard analyzing monthly revenue trends.
3. **What is the main difference between OLTP and OLAP?**
    - **Answer**:
        - OLTP: Fast read/write, highly normalized data, supports real-time transactions.
        - OLAP: Slow updates, denormalized data, supports complex queries and aggregations.
4. **Can one system serve both OLTP and OLAP?**
    - **Answer**: Typically, no. Modern architectures often separate them using data warehousing (OLAP) and operational DBs (OLTP). Some use HTAP (Hybrid Transaction/Analytical Processing).
5. **Why is normalization common in OLTP systems?**
    - **Answer**: To avoid redundancy, maintain data integrity, and support fast inserts/updates with smaller table sizes.

---

### 🔹 **Indexing (Clustered & Non-Clustered)**

1. **What is an index in SQL?**
    - **Answer**: An index is a data structure that improves the speed of data retrieval. Think of it like a book’s index to quickly locate information.
    - **Indexing** is a critical performance **optimization technique** in SQL Server that helps speed up **data retrieval operations**.
2. **What is a clustered index?**
    - **Answer**: A clustered index determines the physical order of rows in the table. A table can have only **one** clustered index.
    - **Example**: If you create a clustered index on `EmployeeID`, the rows are physically sorted by `EmployeeID`.
3. **What is a non-clustered index?**
    - **Answer**: A non-clustered index creates a separate structure that points to the actual data row. A table can have **many** non-clustered indexes.
4. **Which index type is better for range queries?**
    - **Answer**: Clustered index is better for range queries (e.g., dates) because data is physically ordered.
5. **Can we create a clustered index on a view?**
- **Answer**: Yes, in SQL Server, indexed views are possible and can have a clustered index, but it requires meeting specific rules.

---

### 🔹 **Views**

1. **What is a view in SQL?**
- **Answer**: A view is a virtual table based on a SELECT query. It doesn’t store data itself, only the SQL logic.
1. **Why use views?**
- **Answer**:
    - Simplifies complex queries.
    - Provides security by hiding columns.
    - Can join multiple tables in one object.
1. **Can a view be updated?**
- **Answer**: Yes, if it’s based on a single table without GROUP BY, DISTINCT, etc. Otherwise, it may be read-only.
1. **What is a materialized view?**
- **Answer**: A view that stores the result set physically. Useful for performance in OLAP. Common in Oracle/PostgreSQL.
1. **Difference between a view and a table?**
- **Answer**:
    - Table: Stores data physically.
    - View: Virtual, doesn’t store data (except materialized views).

---

### 🔹 **Stored Procedures**

1. **What is a stored procedure?**
- **Answer**: A saved set of SQL statements that can be executed repeatedly. Think of it like a function.
1. **Why use stored procedures?**
- **Answer**:
    - Improves performance via precompiled execution.
    - Promotes reusability.
    - Enhances security and modularity.
1. **Can a stored procedure return a value?**
- **Answer**: Yes, using output parameters or `RETURN`.
1. **Can you pass parameters to a stored procedure?**
- **Answer**: Yes, you can pass input and output parameters to customize behavior.
1. **How are stored procedures different from functions?**
- **Answer**:
    - Procedures: Can return 0 or more values, can perform actions (INSERT, UPDATE).
    - Functions: Must return a value, generally used in SELECTs.

---

### 🔹 **Normalization**

1. **What is normalization?**
- **Answer**: The process of organizing data to reduce redundancy and improve integrity.
1. **What is 1NF (First Normal Form)?**
- **Answer**: Ensures each column contains atomic (indivisible) values. No repeating groups.
- **Example**: Instead of `Phone = "123, 456"`, separate into two rows.
1. **What is 2NF (Second Normal Form)?**
- **Answer**: Removes partial dependency; every non-key column should depend on the whole primary key (applies to composite keys).
1. **What is 3NF (Third Normal Form)?**
- **Answer**: Removes transitive dependency. Non-key attributes should not depend on other non-key attributes.
1. **What are BCNF, 4NF, and 5NF?**
- **Answer**:
    - **BCNF** (Boyce-Codd NF): Stricter version of 3NF.
    - **4NF**: Removes multi-valued dependencies.
    - **5NF**: Deals with join dependency to ensure no data loss when decomposing tables.

---

Would you like these questions in a PDF or formatted flashcards?
</details>

# SQL Interview Preparation – 30 Questions with Detailed Answers
<details>
The objective is not just to learn SQL commands. You should understand:

- What happens internally when a query executes.
- Why we use a particular SQL construct.
- What happens in different scenarios and edge cases.
- How to solve the same problem using different approaches.
- How to choose the right approach for large datasets.

I'll use standard SQL concepts with PostgreSQL-style examples wherever possible. Some syntax and behaviour may differ slightly between MySQL, SQL Server, Oracle and PostgreSQL.

# Section 1: SQL Fundamentals and Query Execution

## Q1. What is the logical execution order of a SQL query?

Consider the following query:

```
SELECT department, COUNT(*) AS emp_count
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING COUNT(*) > 5
ORDER BY emp_count DESC
LIMIT 10;
```

Answer:

When we write a SQL query, we generally write it in this order:

1. SELECT
2. FROM
3. WHERE
4. GROUP BY
5. HAVING
6. ORDER BY
7. LIMIT

However, SQL logically processes the query in a different order.

Logical query execution order

1. FROM / JOIN

   Identifies the source tables and combines records using joins.
2. WHERE

   Filters individual rows based on conditions.
3. GROUP BY

   Groups the remaining records based on specified columns.
4. HAVING

   Filters the groups based on aggregate conditions.
5. SELECT

   Determines which columns and expressions appear in the output.
6. DISTINCT

   Removes duplicate result rows, if specified.
7. ORDER BY

   Sorts the final result.
8. LIMIT / OFFSET

   Restricts the number of returned rows.

Conceptual logical order. The physical execution plan can be different because the database optimizer may rearrange operations.

Why can we use an alias in ORDER BY but generally not in WHERE?

Consider:

```
SELECT
    salary * 12 AS annual_salary
FROM employees
WHERE annual_salary > 600000;
```

This generally fails because WHERE is logically evaluated before SELECT. Therefore, the alias `annual_salary` has not yet been defined at that stage.

But this works:

```
SELECT
    salary * 12 AS annual_salary
FROM employees
ORDER BY annual_salary DESC;
```

ORDER BY is processed after SELECT, so the alias is available.

Does logical execution order mean physical execution happens in exactly that order?

No. Logical execution order explains the meaning of a query, not necessarily how the database physically executes it.

The database optimizer can:

- Push filters closer to the data source.
- Reorder joins.
- Use indexes.
- Choose hash joins, nested-loop joins or merge joins.
- Parallelize certain operations.

For example, even though WHERE logically comes after FROM, the database might use an index to retrieve only matching records rather than scanning the entire table.

## Q2. What is the difference between WHERE and HAVING?

Answer:

Both WHERE and HAVING are used to filter data, but they operate at different stages.

- WHERE filters individual records before grouping.
- HAVING filters groups after aggregation.

Let's understand this with an example.

Suppose we have an employee table:

| emp_id | department | salary |
| ------ | ---------- | ------ |
| 1      | IT         | 80000  |
| 2      | IT         | 90000  |
| 3      | IT         | 40000  |
| 4      | HR         | 60000  |
| 5      | HR         | 70000  |
| 6      | Sales      | 30000  |

Example 1: Using WHERE

Find employees earning more than 50,000 in each department.

```
SELECT department, COUNT(*) AS total_employees
FROM employees
WHERE salary > 50000
GROUP BY department;
```

First, WHERE removes employees earning 50,000 or less.

Remaining records:

| department | salary |
| ---------- | ------ |
| IT         | 80000  |
| IT         | 90000  |
| HR         | 60000  |
| HR         | 70000  |

Then GROUP BY groups these records.

Output:

| department | total_employees |
| ---------- | --------------- |
| IT         | 2               |
| HR         | 2               |

Example 2: Using HAVING

Find departments where the average salary is greater than 65,000.

```
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 65000;
```

First, all records are grouped by department.

The database calculates:

| department | avg_salary |
| ---------- | ---------- |
| IT         | 70000      |
| HR         | 65000      |
| Sales      | 30000      |

Then HAVING filters groups.

Output:

| department | avg_salary |
| ---------- | ---------- |
| IT         | 70000      |

### Your specific subquestions

1\. Can we use HAVING and WHERE together?

Yes. This is very common.

```
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 60000;
```

Execution:

1. WHERE removes employees earning 30,000 or less.
2. GROUP BY groups the remaining employees.
3. AVG calculates the average salary.
4. HAVING retains departments with an average above 60,000.

2\. Can we use HAVING without GROUP BY?

Yes.

For example:

```
SELECT COUNT(*)
FROM employees
HAVING COUNT(*) > 5;
```

Here, the entire result is treated as one group because there is no GROUP BY.

If the employee count is greater than 5, the query returns one row. Otherwise, it returns zero rows.

3\. Can we use HAVING without GROUP BY and WHERE?

Yes. The previous example already demonstrates this.

```
SELECT SUM(salary)
FROM employees
HAVING SUM(salary) > 100000;
```

4\. Can we use WHERE without GROUP BY?

Absolutely.

```
SELECT *
FROM employees
WHERE salary > 50000;
```

WHERE does not depend on GROUP BY.

5\. What happens when we use HAVING COUNT(\*) > 5 without GROUP BY?

The entire table is treated as one group.

If the table contains 10 employees, COUNT(\*) returns 10, and the condition is true.

If it contains 4 employees, the condition is false, and no row is returned.

6\. What is the difference between filtering salary using WHERE and average salary using HAVING?

```
-- Individual employee salary
SELECT *
FROM employees
WHERE salary > 50000;
```

This identifies individual employees.

```
-- Department average salary
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

This identifies departments based on their average salary.

Interview takeaway: WHERE filters records; HAVING filters aggregated results. HAVING can also be used without GROUP BY when the entire result is treated as one group.

## Q3. What happens when you use GROUP BY?

Answer:

GROUP BY combines rows having the same values in specified columns into logical groups. We generally use it with aggregate functions such as SUM, COUNT, AVG, MIN and MAX.

Consider:

| emp_id | employee_name | department | salary |
| ------ | ------------- | ---------- | ------ |
| 1      | Amit          | IT         | 80000  |
| 2      | Rahul         | IT         | 90000  |
| 3      | Priya         | HR         | 70000  |
| 4      | Neha          | HR         | 60000  |

Query:

```
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

Output:

| department | sum    |
| ---------- | ------ |
| IT         | 170000 |
| HR         | 130000 |

The database groups employees based on department and calculates the total salary for each group.

Why does this query fail?

```
SELECT department, employee_name, SUM(salary)
FROM employees
GROUP BY department;
```

Because employee_name is neither:

- Included in GROUP BY.
- Nor aggregated using an aggregate function.

There are multiple employee names in each department. SQL cannot determine which employee name should represent the department.

Correct version:

```
SELECT
    department,
    employee_name,
    SUM(salary)
FROM employees
GROUP BY department, employee_name;
```

Now each unique combination of department and employee_name becomes a group.

Can we group by multiple columns?

Yes.

```
SELECT department, designation, COUNT(*)
FROM employees
GROUP BY department, designation;
```

This creates groups based on the combination of department and designation.

Difference between GROUP BY and DISTINCT

DISTINCT removes duplicate combinations, whereas GROUP BY creates groups that can be used with aggregation.

```
SELECT DISTINCT department
FROM employees;
```

Returns unique departments.

```
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

Returns each department and its employee count.

Both can sometimes produce similar results, but their purposes are different.

## Q4. What is the difference between COUNT(\*), COUNT(1) and COUNT(column_name)?

Answer:

All three are used for counting, but their NULL-handling behaviour differs.

Suppose the table contains:

| emp_id | salary |
| ------ | ------ |
| 1      | 50000  |
| 2      | 60000  |
| 3      | NULL   |
| 4      | 70000  |
| 5      | NULL   |

1\. COUNT(\*)

```
SELECT COUNT(*) FROM employees;
```

Returns 5.

It counts all rows, including rows containing NULL values.

2\. COUNT(1)

```
SELECT COUNT(1) FROM employees;
```

Returns 5.

The expression 1 is a non-NULL constant, so every row is counted.

3\. COUNT(column_name)

```
SELECT COUNT(salary) FROM employees;
```

Returns 3.

It counts only non-NULL salary values.

4\. COUNT(DISTINCT column_name)

```
SELECT COUNT(DISTINCT salary)
FROM employees;
```

Returns 3 in this example because 50,000, 60,000 and 70,000 are three distinct non-NULL values.

Does COUNT(1) perform better than COUNT(\*)?

Generally, no. Modern database optimizers handle both efficiently, and there is typically no meaningful performance difference.

For counting all rows, COUNT(\*) is the clearest and most standard choice.

## Q5. What is the difference between NULL, 0 and an empty string?

Answer:

These three represent different things.

| Value | Meaning                                           |
| ----- | ------------------------------------------------- |
| NULL  | Missing or unknown value                          |
| 0     | Actual numeric value zero                         |
| ''    | Empty string, meaning a string with no characters |

Consider a salary column:

| Employee | Salary |
| -------- | ------ |
| A        | 50000  |
| B        | 0      |
| C        | NULL   |

- Employee A has a salary of 50,000.
- Employee B has an actual salary value of zero.
- Employee C has no known salary value.

Why doesn't column = NULL work?

SQL uses three-valued logic:

- TRUE
- FALSE
- UNKNOWN

NULL represents an unknown value.

Therefore:

```
SELECT *
FROM employees
WHERE salary = NULL;
```

Does not return NULL salary rows.

Correct approach:

```
SELECT *
FROM employees
WHERE salary IS NULL;
```

What is COALESCE?

COALESCE returns the first non-NULL value from the supplied arguments.

```
SELECT
    employee_name,
    COALESCE(salary, 0) AS salary
FROM employees;
```

If salary is NULL, it returns zero.

You can also provide multiple fallback values:

```
SELECT COALESCE(phone, alternate_phone, 'Not Available')
FROM customers;
```

What happens when you perform arithmetic with NULL?

Generally, the result becomes NULL.

For example:

```
SELECT 1000 + NULL;
```

Returns NULL.

How do aggregate functions handle NULL?

Most standard aggregate functions ignore NULL values.

For example:

| Salary |
| ------ |
| 10000  |
| 20000  |
| NULL   |

```
SELECT AVG(salary)
FROM employees;
```

Returns 15,000, not 10,000.

AVG calculates the average using only non-NULL values.

COUNT(\*) counts all three rows, while COUNT(salary) counts only two.

# Section 2: Joins, Subqueries and Combining Tables

## Q6. How can you combine two tables vertically and horizontally?

Answer:

There are two common ways of combining data:

1. Vertical combination: stacking rows from multiple tables.
2. Horizontal combination: combining columns from multiple tables.

### A. Vertical combination – UNION and UNION ALL

Suppose we have two tables:

Employees_Jan:

| emp_id | name  |
| ------ | ----- |
| 1      | Amit  |
| 2      | Rahul |

Employees_Feb:

| emp_id | name  |
| ------ | ----- |
| 3      | Priya |
| 4      | Neha  |

We want to stack February records below January records.

Using UNION ALL:

```
SELECT emp_id, name
FROM employees_jan

UNION ALL

SELECT emp_id, name
FROM employees_feb;
```

Output:

| emp_id | name  |
| ------ | ----- |
| 1      | Amit  |
| 2      | Rahul |
| 3      | Priya |
| 4      | Neha  |

UNION ALL retains duplicates.

Using UNION:

```
SELECT emp_id, name
FROM employees_jan

UNION

SELECT emp_id, name
FROM employees_feb;
```

UNION removes duplicate result rows.

| Feature            | UNION                        | UNION ALL        |
| ------------------ | ---------------------------- | ---------------- |
| Combines rows      | Yes                          | Yes              |
| Removes duplicates | Yes                          | No               |
| Performance        | Can require extra processing | Generally faster |
| Use case           | Need unique results          | Need all records |

What if column names are different?

The column names do not need to be identical. However, both queries must return the same number of columns in corresponding positions, with compatible data types.

```
SELECT emp_id, employee_name
FROM employees_jan

UNION ALL

SELECT id, name
FROM employees_feb;
```

The output column names generally come from the first SELECT.

### B. Horizontal combination – JOIN

Suppose:

Employees:

| emp_id | name  | dept_id |
| ------ | ----- | ------- |
| 1      | Amit  | 10      |
| 2      | Rahul | 20      |

Departments:

| dept_id | department_name |
| ------- | --------------- |
| 10      | IT              |
| 20      | HR              |

Query:

```
SELECT
    e.emp_id,
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output:

| emp_id | name  | department_name |
| ------ | ----- | --------------- |
| 1      | Amit  | IT              |
| 2      | Rahul | HR              |

Important distinction: UNION combines rows based on column positions. JOIN combines columns based on a matching relationship between rows.

## Q7. Can you join two tables without using the JOIN keyword?

Answer:

Yes. We can combine tables without explicitly writing the JOIN keyword.

There are multiple approaches.

### Approach 1: Using WHERE (Implicit Join)

Consider:

Employees:

| emp_id | name  | dept_id |
| ------ | ----- | ------- |
| 1      | Amit  | 10      |
| 2      | Rahul | 20      |

Departments:

| dept_id | department |
| ------- | ---------- |
| 10      | IT         |
| 20      | HR         |

Query:

```
SELECT *
FROM employees e, departments d
WHERE e.dept_id = d.dept_id;
```

This produces the matching records from both tables.

How does this work?

The comma between the tables creates a Cartesian product conceptually.

For example:

Employees have 2 rows and Departments have 2 rows.

The initial Cartesian product contains:

2 × 2 = 4 combinations.

The WHERE condition then filters out combinations where department IDs do not match.

Only 2 matching combinations remain.

This is known as an implicit INNER JOIN.

### Approach 2: Using a Subquery

Suppose we want to find employees who belong to the IT department.

```
SELECT *
FROM employees
WHERE dept_id IN (
    SELECT dept_id
    FROM departments
    WHERE department = 'IT'
);
```

The inner query identifies the department ID of IT.

The outer query finds employees belonging to that department.

This achieves a similar filtering result without explicitly joining the tables.

### Approach 3: Using EXISTS

```
SELECT *
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.dept_id = e.dept_id
);
```

For each employee, SQL checks whether a matching department exists.

### JOIN vs Subquery

| Feature      | JOIN                                      | Subquery                                             |
| ------------ | ----------------------------------------- | ---------------------------------------------------- |
| Main purpose | Combine related data                      | Filter, calculate or retrieve data                   |
| Output       | Can return columns from both tables       | Depends on the subquery structure                    |
| Use case     | Combining employee and department details | Finding employees belonging to a specific department |
| Performance  | Depends on execution plan                 | Depends on execution plan                            |

Which is faster?

There is no universal answer.

Modern optimizers can transform many subqueries into joins or semi-joins. The actual execution plan, indexes, data distribution and query structure determine performance.

Interview point: You can join tables using WHERE, but explicit JOIN syntax is generally preferred because it makes relationships and join conditions clearer.

## Q8. Explain all types of JOINs with practical examples.

Answer:

JOINs are used to combine records from two or more tables based on a related column.

Let's use two tables.

Employees:

| emp_id | name  | dept_id |
| ------ | ----- | ------- |
| 1      | Amit  | 10      |
| 2      | Rahul | 20      |
| 3      | Priya | 30      |
| 4      | Neha  | NULL    |

Departments:

| dept_id | department |
| ------- | ---------- |
| 10      | IT         |
| 20      | HR         |
| 40      | Finance    |

### 1. INNER JOIN

Returns only records having matching values in both tables.

```
SELECT *
FROM employees e
INNER JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output:

| name  | department |
| ----- | ---------- |
| Amit  | IT         |
| Rahul | HR         |

Priya and Neha are excluded because they do not have matching departments.

Finance is excluded because it has no matching employee.

### 2. LEFT JOIN

Returns all records from the left table and matching records from the right table.

```
SELECT *
FROM employees e
LEFT JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output:

| name  | department |
| ----- | ---------- |
| Amit  | IT         |
| Rahul | HR         |
| Priya | NULL       |
| Neha  | NULL       |

All employees are retained.

If no department matches, the department columns contain NULL.

### 3. RIGHT JOIN

Returns all records from the right table and matching records from the left table.

```
SELECT *
FROM employees e
RIGHT JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output:

| name  | department |
| ----- | ---------- |
| Amit  | IT         |
| Rahul | HR         |
| NULL  | Finance    |

All departments are retained.

### 4. FULL OUTER JOIN

Returns matching records plus unmatched records from both tables.

```
SELECT *
FROM employees e
FULL OUTER JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output:

| name  | department |
| ----- | ---------- |
| Amit  | IT         |
| Rahul | HR         |
| Priya | NULL       |
| Neha  | NULL       |
| NULL  | Finance    |

Note: FULL OUTER JOIN is supported in PostgreSQL and SQL Server, but MySQL does not directly support it.

### 5. CROSS JOIN

Returns every possible combination of rows between two tables.

```
SELECT *
FROM employees
CROSS JOIN departments;
```

If Employees contains 4 rows and Departments contains 3 rows:

Total output = 4 × 3 = 12 rows.

It is useful for generating combinations, such as every product with every available size.

### 6. SELF JOIN

A table is joined with itself.

Suppose we have:

| emp_id | employee_name | manager_id |
| ------ | ------------- | ---------- |
| 1      | Amit          | NULL       |
| 2      | Rahul         | 1          |
| 3      | Priya         | 1          |

We want employee names along with their manager names.

```
SELECT
    e.employee_name,
    m.employee_name AS manager_name
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.emp_id;
```

Output:

| employee_name | manager_name |
| ------------- | ------------ |
| Amit          | NULL         |
| Rahul         | Amit         |
| Priya         | Amit         |

Can joins increase the number of rows?

Yes. If one employee matches multiple records in another table, that employee appears multiple times.

For example, one customer with three transactions produces three rows when joined with the transactions table.

## Q9. What is the difference between INNER JOIN and LEFT JOIN?

Answer:

The primary difference is how unmatched records are handled.

Consider:

Employees:

| emp_id | name | dept_id |
| ------ | ---- | ------- |
| 1      | A    | 10      |
| 2      | B    | 20      |
| 3      | C    | 30      |

Departments:

| dept_id | department |
| ------- | ---------- |
| 10      | IT         |
| 20      | HR         |

INNER JOIN:

```
SELECT *
FROM employees e
INNER JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output: A and B only.

Employee C is excluded because department 30 does not exist.

LEFT JOIN:

```
SELECT *
FROM employees e
LEFT JOIN departments d
    ON e.dept_id = d.dept_id;
```

Output: A, B and C.

Employee C appears with NULL department details.

How do you find employees who don't belong to any department?

```
SELECT e.*
FROM employees e
LEFT JOIN departments d
    ON e.dept_id = d.dept_id
WHERE d.dept_id IS NULL;
```

This is called an anti-join pattern.

How do you find departments having no employees?

```
SELECT d.*
FROM departments d
LEFT JOIN employees e
    ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;
```

This identifies departments without matching employees.

## Q10. What happens when you join two tables containing duplicate joining-column values?

Answer:

This is one of the most important practical SQL concepts because it can cause unexpected row multiplication and incorrect aggregations.

Consider:

Employees:

| emp_id | department_id |
| ------ | ------------- |
| 1      | 10            |
| 2      | 10            |
| 3      | 20            |

Projects:

| project_id | department_id |
| ---------- | ------------- |
| 101        | 10            |
| 102        | 10            |
| 103        | 20            |

Query:

```
SELECT *
FROM employees e
JOIN projects p
    ON e.department_id = p.department_id;
```

Output:

| emp_id | project_id | department_id |
| ------ | ---------- | ------------- |
| 1      | 101        | 10            |
| 1      | 102        | 10            |
| 2      | 101        | 10            |
| 2      | 102        | 10            |
| 3      | 103        | 20            |

Total rows = 5.

Why?

Department 10 has:

- 2 employees.
- 2 projects.

Therefore, it produces:

2 × 2 = 4 combinations.

Department 20 produces one combination.

Total = 4 + 1 = 5 rows.

This is a many-to-many relationship in the resulting join.

What are the different relationships?

| Relationship | Explanation                                 | Example                    |
| ------------ | ------------------------------------------- | -------------------------- |
| One-to-one   | One record matches one record               | Person and unique passport |
| One-to-many  | One record matches multiple records         | Department and employees   |
| Many-to-many | Multiple records can match multiple records | Students and courses       |

How do you prevent inflated aggregations?

Suppose each employee has a salary of 50,000 and we join with projects.

If we calculate:

```
SELECT SUM(e.salary)
FROM employees e
JOIN projects p
    ON e.department_id = p.department_id;
```

Department 10 salary gets counted twice per employee.

This inflates the total.

Possible solutions:

1. Aggregate before joining.
2. Join at the correct grain (the intended level of detail).
3. Use EXISTS if you only need to check whether a matching record exists.
4. Use DISTINCT only when it genuinely matches the intended business logic.

Example:

```
WITH employee_totals AS (
    SELECT department_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM employee_totals;
```

The key is to understand the grain of every table before joining it.

## Q11. What is the difference between EXISTS, IN and JOIN?

Answer:

All three can be used to work with related data, but their behaviour and use cases differ.

### 1. IN

Checks whether a value exists in a list of values.

```
SELECT *
FROM employees
WHERE dept_id IN (
    SELECT dept_id
    FROM departments
    WHERE location = 'Mumbai'
);
```

This finds employees belonging to departments located in Mumbai.

### 2. EXISTS

Checks whether at least one matching record exists.

```
SELECT *
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.dept_id = e.dept_id
      AND d.location = 'Mumbai'
);
```

For every employee, the database checks whether a matching Mumbai department exists.

EXISTS returns TRUE as soon as a qualifying match is established logically, although the physical implementation depends on the optimizer.

### 3. JOIN

Combines columns from related tables.

```
SELECT e.*, d.location
FROM employees e
JOIN departments d
    ON e.dept_id = d.dept_id
WHERE d.location = 'Mumbai';
```

This can return employee and department information together.

What happens when a subquery returns NULL?

This is particularly important for NOT IN.

Suppose the subquery returns:

```
10
20
NULL
```

Then:

```
SELECT *
FROM employees
WHERE dept_id NOT IN (
    SELECT dept_id
    FROM departments
);
```

The presence of NULL can cause the NOT IN condition to evaluate to UNKNOWN for otherwise unmatched values. As a result, you may get no records.

NOT EXISTS is generally safer in this situation:

```
SELECT *
FROM employees e
WHERE NOT EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.dept_id = e.dept_id
);
```

One nuance: if `e.dept_id` itself is NULL, NOT EXISTS will return that employee because no equality match is found. If you want to exclude NULL department IDs, add `e.dept_id IS NOT NULL`.

Which is faster?

There is no fixed rule. The optimizer may transform IN and EXISTS into similar execution strategies.

Use:

- JOIN when you need columns from both tables.
- EXISTS when you only need to check for a match.
- IN when checking membership in a set of values.

## Q12. What are correlated and non-correlated subqueries?

Answer:

A subquery is a query nested inside another SQL query.

There are two important types.

### 1. Non-correlated subquery

A non-correlated subquery is independent of the outer query.

Example:

```
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query calculates the average salary of all employees.

Suppose the average salary is 60,000.

The outer query then returns employees earning more than 60,000.

The inner query does not depend on any employee row from the outer query.

### 2. Correlated subquery

A correlated subquery references columns from the outer query.

Example: Find employees earning more than their department's average salary.

```
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

Here:

- The outer query selects an employee.
- The inner query calculates the average salary of that employee's department.
- The outer query compares the employee's salary with that average.

The inner query references `e.department_id` from the outer query.

Are correlated subqueries always slower?

Not necessarily.

Conceptually, correlated subqueries can appear to execute for every outer row, which may be expensive.

However, database optimizers can sometimes transform them into joins or other efficient execution plans.

For large datasets, compare the actual execution plans rather than assuming one approach is always faster.

# Section 3: Aggregations and Practical SQL Problems

## Q13. How would you find the second-highest salary in an employee table?

Answer:

There are multiple approaches. The important thing is understanding how each approach behaves when duplicate salaries exist.

Consider:

| emp_id | employee_name | salary |
| ------ | ------------- | ------ |
| 1      | Amit          | 100000 |
| 2      | Rahul         | 90000  |
| 3      | Priya         | 90000  |
| 4      | Neha          | 80000  |
| 5      | Karan         | 70000  |

### Approach 1: MAX() with a subquery

```
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

Working:

1. Inner query finds the maximum salary: 100,000.
2. Outer query filters salaries below 100,000.
3. MAX() finds the maximum among the remaining values.

Output: 90,000.

This approach automatically handles duplicate salaries.

### Approach 2: DISTINCT with LIMIT and OFFSET

```
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

Working:

- DISTINCT removes duplicate salaries.
- ORDER BY sorts salaries in descending order.
- OFFSET 1 skips the highest salary.
- LIMIT 1 returns the next salary.

This syntax works in PostgreSQL and MySQL.

### Approach 3: DENSE_RANK()

```
WITH ranked_employees AS (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT DISTINCT salary
FROM ranked_employees
WHERE salary_rank = 2;
```

DENSE_RANK assigns the same rank to employees having the same salary.

Both Rahul and Priya receive rank 2.

### Approach 4: ROW_NUMBER()

```
WITH ranked_employees AS (
    SELECT
        employee_name,
        salary,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC, emp_id
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE rn = 2;
```

This returns the second row, not necessarily the second-highest distinct salary.

Here, it returns Rahul or whichever employee comes second based on the ordering.

Important interview distinction:

| Function   | Behaviour with duplicate salaries                               |
| ---------- | --------------------------------------------------------------- |
| ROW_NUMBER | Assigns a unique number to every row                            |
| RANK       | Assigns the same rank to ties and skips subsequent ranks        |
| DENSE_RANK | Assigns the same rank to ties without skipping subsequent ranks |

If the table contains only one distinct salary, the second-highest distinct salary does not exist, so these approaches return no result or NULL depending on the query.

## Q14. How would you find duplicate records in a table?

Answer:

Duplicates can be identified using GROUP BY and HAVING.

Suppose:

| customer_id | email        |
| ----------- | ------------ |
| 101         | a\@gmail.com |
| 102         | b\@gmail.com |
| 103         | a\@gmail.com |
| 104         | c\@gmail.com |
| 105         | b\@gmail.com |

### 1. Find duplicates based on one column

```
SELECT email, COUNT(*) AS duplicate_count
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

Output:

| email        | duplicate_count |
| ------------ | --------------- |
| a\@gmail.com | 2               |
| b\@gmail.com | 2               |

The query groups records based on email and returns emails appearing more than once.

### 2. Find duplicates based on multiple columns

Suppose a duplicate customer is defined by the combination of first_name and last_name.

```
SELECT
    first_name,
    last_name,
    COUNT(*)
FROM customers
GROUP BY first_name, last_name
HAVING COUNT(*) > 1;
```

This identifies duplicate combinations, not just duplicate individual columns.

### 3. Retrieve complete duplicate records

```
SELECT *
FROM (
    SELECT *,
        ROW_NUMBER() OVER (
            PARTITION BY email
            ORDER BY customer_id
        ) AS rn
    FROM customers
) t
WHERE rn > 1;
```

This returns duplicate records while treating the first record for each email as the original.

### 4. Delete duplicates while retaining one record

In PostgreSQL:

```
WITH duplicates AS (
    SELECT
        customer_id,
        ROW_NUMBER() OVER (
            PARTITION BY email
            ORDER BY customer_id
        ) AS rn
    FROM customers
)
DELETE FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM duplicates
    WHERE rn > 1
);
```

This retains the record with the smallest customer_id.

Real-world consideration:

In customer databases, duplicates are not always exact matches.

For example:

- Rahul Sharma
- Rahul S.
- R. Sharma

These may represent the same customer.

Identifying such records requires data cleaning, standardization and potentially fuzzy matching, rather than just GROUP BY.

## Q15. How do you calculate cumulative SUM, running average and percentage contribution?

Answer:

These are common analytical SQL problems, and window functions are particularly useful.

Suppose we have monthly sales:

| month    | sales |
| -------- | ----- |
| January  | 10000 |
| February | 15000 |
| March    | 20000 |
| April    | 5000  |

### 1. Cumulative SUM (Running Total)

We want to calculate total sales up to each month.

```
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS cumulative_sales
FROM monthly_sales;
```

Output:

| Month    | Sales | Cumulative Sales |
| -------- | ----- | ---------------- |
| January  | 10000 | 10000            |
| February | 15000 | 25000            |
| March    | 20000 | 45000            |
| April    | 5000  | 50000            |

How does it work?

- UNBOUNDED PRECEDING means start from the first row in the window.
- CURRENT ROW means include the current row.
- SUM calculates the total across that range.

### 2. Running Average

```
SELECT
    month,
    sales,
    AVG(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_avg
FROM monthly_sales;
```

Output:

| Month    | Sales | Running Average |
| -------- | ----- | --------------- |
| January  | 10000 | 10000           |
| February | 15000 | 12500           |
| March    | 20000 | 15000           |
| April    | 5000  | 12500           |

### 3. Percentage Contribution

We want to know what percentage each month contributes to total sales.

```
SELECT
    month,
    sales,
    ROUND(
        sales * 100.0 / SUM(sales) OVER (),
        2
    ) AS contribution_percentage
FROM monthly_sales;
```

Total sales = 50,000.

Output:

| Month    | Sales | Contribution |
| -------- | ----- | ------------ |
| January  | 10000 | 20%          |
| February | 15000 | 30%          |
| March    | 20000 | 40%          |
| April    | 5000  | 10%          |

Notice that `OVER()` without PARTITION BY or ORDER BY calculates over the entire result set.

Can we calculate these using GROUP BY alone?

GROUP BY is suitable for calculating aggregates at a group level, but it reduces the number of rows.

For cumulative calculations, we generally need window functions because we want to retain individual monthly records while calculating values across multiple rows.

## Q16. How would you find the top 3 highest-paid employees in each department?

Answer:

We can use window functions, especially ROW_NUMBER, RANK and DENSE_RANK.

Suppose:

| Employee | Department | Salary |
| -------- | ---------- | ------ |
| A        | IT         | 100000 |
| B        | IT         | 90000  |
| C        | IT         | 90000  |
| D        | IT         | 80000  |
| E        | HR         | 70000  |
| F        | HR         | 60000  |
| G        | HR         | 50000  |

### Approach 1: Using ROW_NUMBER

```
WITH ranked AS (
    SELECT
        employee_name,
        department,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn <= 3;
```

Working:

1. PARTITION BY divides employees into department-wise groups.
2. ORDER BY sorts salaries within each department.
3. ROW_NUMBER assigns sequential numbers.
4. The outer query filters the first three rows.

It returns exactly three employees per department, if at least three exist.

If there are ties, add a secondary ordering column such as employee_id to make the selection deterministic.

### Approach 2: Using RANK

```
WITH ranked AS (
    SELECT
        employee_name,
        department,
        salary,
        RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
)
SELECT *
FROM ranked
WHERE rnk <= 3;
```

This returns everyone whose rank is 3 or less.

If two employees tie at rank 2, both are included, and the next employee receives rank 4.

### Approach 3: Using DENSE_RANK

```
WITH ranked AS (
    SELECT
        employee_name,
        department,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
)
SELECT *
FROM ranked
WHERE rnk <= 3;
```

This returns employees belonging to the top three distinct salary levels in each department.

Which should you choose?

- Exactly three employees: ROW_NUMBER.
- Employees whose positional rank is within the top three: RANK.
- Employees belonging to the top three distinct salary levels: DENSE_RANK.

## Q17. What is conditional aggregation?

Answer:

Conditional aggregation means applying aggregate functions only to records that satisfy a particular condition.

We generally use CASE WHEN inside SUM or COUNT.

Suppose we have a transactions table:

| customer_id | amount | status  |
| ----------- | ------ | ------- |
| 101         | 1000   | Success |
| 101         | 500    | Failed  |
| 102         | 2000   | Success |
| 102         | 300    | Pending |
| 103         | 1500   | Failed  |

We want to calculate total transactions, successful transactions, failed transactions, successful transaction amount and success percentage.

We can calculate everything in a single query.

```
SELECT
    customer_id,

    COUNT(*) AS total_transactions,

    SUM(
        CASE WHEN status = 'Success'
             THEN 1 ELSE 0 END
    ) AS successful_transactions,

    SUM(
        CASE WHEN status = 'Failed'
             THEN 1 ELSE 0 END
    ) AS failed_transactions,

    SUM(
        CASE WHEN status = 'Success'
             THEN amount ELSE 0 END
    ) AS successful_amount,

    ROUND(
        100.0 *
        SUM(CASE WHEN status = 'Success'
                 THEN 1 ELSE 0 END)
        / NULLIF(COUNT(*), 0),
        2
    ) AS success_percentage

FROM transactions
GROUP BY customer_id;
```

Output:

| Customer | Total | Successful | Failed | Successful Amount | Success % |
| -------- | ----- | ---------- | ------ | ----------------- | --------- |
| 101      | 2     | 1          | 1      | 1000              | 50%       |
| 102      | 2     | 1          | 0      | 2000              | 50%       |
| 103      | 1     | 0          | 1      | 0                 | 0%        |

How does CASE WHEN work here?

For example:

```
SUM(
    CASE WHEN status = 'Success'
         THEN amount ELSE 0 END
)
```

For successful transactions, it returns the amount. For other transactions, it returns zero.

SUM then adds all the resulting values.

What is NULLIF?

NULLIF(a, b) returns NULL when a and b are equal.

Here, it protects against division by zero.

## Q18. How would you find customers who have made purchases in consecutive months?

Answer:

This problem tests date handling, grouping and window functions.

Suppose:

| Customer | Month    |
| -------- | -------- |
| A        | January  |
| A        | February |
| A        | March    |
| B        | January  |
| B        | March    |
| C        | February |
| C        | March    |

We want to identify customers who purchased in consecutive months.

### Approach 1: Using LAG()

First, remove duplicate customer-month combinations if multiple transactions can occur in the same month.

```
WITH monthly_purchases AS (
    SELECT DISTINCT
        customer_id,
        DATE_TRUNC('month', transaction_date) AS purchase_month
    FROM transactions
),
previous_month AS (
    SELECT
        customer_id,
        purchase_month,
        LAG(purchase_month) OVER (
            PARTITION BY customer_id
            ORDER BY purchase_month
        ) AS prev_month
    FROM monthly_purchases
)
SELECT *
FROM previous_month
WHERE purchase_month =
      prev_month + INTERVAL '1 month';
```

Explanation:

1. First, we create one record per customer per month.
2. LAG retrieves the previous purchase month.
3. We compare the current month with the previous month.
4. If the difference is exactly one month, it is a consecutive purchase.

This identifies consecutive month pairs.

### Approach 2: Find customers with three consecutive months

We can use LAG twice:

```
WITH monthly_purchases AS (
    SELECT DISTINCT
        customer_id,
        DATE_TRUNC('month', transaction_date) AS purchase_month
    FROM transactions
),
history AS (
    SELECT
        customer_id,
        purchase_month,
        LAG(purchase_month, 1) OVER (
            PARTITION BY customer_id
            ORDER BY purchase_month
        ) AS prev_month,
        LAG(purchase_month, 2) OVER (
            PARTITION BY customer_id
            ORDER BY purchase_month
        ) AS prev_2_month
    FROM monthly_purchases
)
SELECT DISTINCT customer_id
FROM history
WHERE prev_month = purchase_month - INTERVAL '1 month'
  AND prev_2_month = purchase_month - INTERVAL '2 months';
```

This identifies customers who purchased in three consecutive calendar months.

How do we handle missing months?

LAG makes missing months visible through the date difference.

For example, January followed by March gives a two-month difference, so the consecutive-month condition fails.

Another approach is to use a calendar table and LEFT JOIN transactions to it, which is useful when you need to explicitly represent months with no purchases.

# Section 4: Window Functions and Advanced SQL

## Q19. What are window functions, and how are they different from GROUP BY?

Answer:

Window functions perform calculations across a set of related rows without reducing the number of rows in the original result.

Consider:

| Employee | Department | Salary |
| -------- | ---------- | ------ |
| A        | IT         | 80000  |
| B        | IT         | 90000  |
| C        | HR         | 60000  |
| D        | HR         | 70000  |

### Using GROUP BY

```
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

Output:

| Department | Avg Salary |
| ---------- | ---------- |
| IT         | 85000      |
| HR         | 65000      |

We get two rows because records are grouped.

### Using a window function

```
SELECT
    employee_name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Output:

| Employee | Department | Salary | Department Avg |
| -------- | ---------- | ------ | -------------- |
| A        | IT         | 80000  | 85000          |
| B        | IT         | 90000  | 85000          |
| C        | HR         | 60000  | 65000          |
| D        | HR         | 70000  | 65000          |

The average salary is calculated for each department, but all four employee records are retained.

Why does GROUP BY reduce rows?

Because it produces one result per group.

Why do window functions preserve rows?

Because they calculate additional values over related rows while retaining the individual rows.

What is PARTITION BY?

It divides records into independent groups for window calculations.

What is ORDER BY inside a window function?

It defines the order in which window calculations are performed.

For example:

```
SUM(salary) OVER (
    PARTITION BY department
    ORDER BY joining_date
)
```

This calculates a department-wise running total based on joining date, subject to the window frame.

Can we combine GROUP BY and window functions?

Yes.

For example:

```
WITH dept_sales AS (
    SELECT
        department,
        SUM(sales) AS total_sales
    FROM transactions
    GROUP BY department
)
SELECT
    department,
    total_sales,
    RANK() OVER (
        ORDER BY total_sales DESC
    ) AS sales_rank
FROM dept_sales;
```

First, we aggregate sales department-wise. Then we rank the resulting department totals.

## Q20. Explain ROW_NUMBER(), RANK() and DENSE_RANK().

Answer:

These are ranking window functions used to assign ranks to records based on an ordering condition.

Consider:

| Employee | Salary |
| -------- | ------ |
| A        | 100000 |
| B        | 90000  |
| C        | 90000  |
| D        | 80000  |
| E        | 70000  |

Query:

```
SELECT
    employee_name,
    salary,

    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num,

    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank,

    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS dense_salary_rank

FROM employees;
```

Output:

| Employee | Salary | ROW_NUMBER | RANK | DENSE_RANK |
| -------- | ------ | ---------- | ---- | ---------- |
| A        | 100000 | 1          | 1    | 1          |
| B        | 90000  | 2          | 2    | 2          |
| C        | 90000  | 3          | 2    | 2          |
| D        | 80000  | 4          | 4    | 3          |
| E        | 70000  | 5          | 5    | 4          |

### ROW_NUMBER()

Assigns a unique sequential number to every row.

Even if two employees have the same salary, they receive different row numbers.

If you need predictable ordering among ties, add a secondary column:

```
ROW_NUMBER() OVER (
    ORDER BY salary DESC, emp_id
)
```

### RANK()

Assigns the same rank to records with equal values.

However, it skips the next rank after a tie.

Here, B and C both get rank 2, so D gets rank 4.

### DENSE_RANK()

Also assigns the same rank to equal values, but does not skip ranks.

Therefore, D gets rank 3.

When should you use them?

| Requirement                                               | Function   |
| --------------------------------------------------------- | ---------- |
| Select exactly one top employee per department            | ROW_NUMBER |
| Find all employees in the top 3 positions, including ties | RANK       |
| Find employees in the top 3 distinct salary levels        | DENSE_RANK |
| Remove duplicate records while retaining one              | ROW_NUMBER |

## Q21. What are LAG() and LEAD() functions?

Answer:

LAG and LEAD are window functions that allow us to access values from previous or subsequent rows without performing a self-join.

Consider:

| Customer | Month    | Amount |
| -------- | -------- | ------ |
| A        | January  | 1000   |
| A        | February | 1500   |
| A        | March    | 1200   |

### LAG()

LAG retrieves a value from a previous row.

```
SELECT
    customer_id,
    month,
    amount,
    LAG(amount, 1) OVER (
        PARTITION BY customer_id
        ORDER BY month
    ) AS previous_amount
FROM transactions;
```

Output:

| Month    | Amount | Previous Amount |
| -------- | ------ | --------------- |
| January  | 1000   | NULL            |
| February | 1500   | 1000            |
| March    | 1200   | 1500            |

### LEAD()

LEAD retrieves a value from a subsequent row.

```
SELECT
    customer_id,
    month,
    amount,
    LEAD(amount, 1) OVER (
        PARTITION BY customer_id
        ORDER BY month
    ) AS next_amount
FROM transactions;
```

Output:

| Month    | Amount | Next Amount |
| -------- | ------ | ----------- |
| January  | 1000   | 1500        |
| February | 1500   | 1200        |
| March    | 1200   | NULL        |

### Calculate month-over-month growth

```
WITH monthly_data AS (
    SELECT
        customer_id,
        month,
        amount,
        LAG(amount) OVER (
            PARTITION BY customer_id
            ORDER BY month
        ) AS previous_amount
    FROM transactions
)
SELECT
    customer_id,
    month,
    amount,
    ROUND(
        100.0 * (amount - previous_amount)
        / NULLIF(previous_amount, 0),
        2
    ) AS growth_percentage
FROM monthly_data;
```

For February:

\\[ \frac{1500-1000}{1000}\times100=50\\% \\]

For March:

\\[ \frac{1200-1500}{1500}\times100=-20\\% \\]

So spending increased by 50% in February and decreased by 20% in March.

How would you identify customers whose spending decreased?

Add:

```
WHERE amount < previous_amount
```

in an outer query or CTE.

Important: LAG retrieves the previous available row, not necessarily the previous calendar month. If a customer has no February record, LAG from March might retrieve January. If the business requirement is calendar-month comparison, first create a complete monthly series or explicitly check the date difference.

## Q22. What is the difference between PARTITION BY and GROUP BY?

Answer:

Both divide data into groups, but their behaviour is different.

Consider:

| Employee | Department | Salary |
| -------- | ---------- | ------ |
| A        | IT         | 80000  |
| B        | IT         | 90000  |
| C        | HR         | 60000  |
| D        | HR         | 70000  |

GROUP BY:

```
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

Output:

| Department | Average |
| ---------- | ------- |
| IT         | 85000   |
| HR         | 65000   |

GROUP BY reduces the result to one row per department.

PARTITION BY:

```
SELECT
    employee_name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Output contains all four employees.

PARTITION BY calculates department-level values while retaining employee-level records.

### Comparison

| Feature                       | GROUP BY            | PARTITION BY     |
| ----------------------------- | ------------------- | ---------------- |
| Used with                     | Aggregate functions | Window functions |
| Reduces rows                  | Yes                 | No               |
| Retains individual records    | Generally no        | Yes              |
| Can group by multiple columns | Yes                 | Yes              |
| Requires ORDER BY             | No                  | No               |

Can we use PARTITION BY without ORDER BY?

Yes.

```
SUM(salary) OVER (
    PARTITION BY department
)
```

This calculates the total salary for each department and repeats that total for every employee in the department.

What happens when we use PARTITION BY department ORDER BY salary?

The records are divided department-wise, then ordered by salary within each department.

The resulting window calculation can be used to calculate rankings, running totals, and other ordered analytics.

## Q23. What is the difference between ROWS and RANGE in window functions?

Answer:

ROWS and RANGE define which records are included in the window frame used by an aggregate window function.

Consider:

| Employee | Joining Date | Salary |
| -------- | ------------ | ------ |
| A        | Jan 1        | 50000  |
| B        | Jan 2        | 60000  |
| C        | Jan 2        | 70000  |
| D        | Jan 3        | 80000  |

### 1. ROWS

ROWS works with physical row positions in the ordered result.

```
SELECT
    employee_name,
    salary,
    SUM(salary) OVER (
        ORDER BY joining_date, employee_id
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total
FROM employees;
```

Each row is included sequentially.

For example:

- A: 50,000
- B: 1,10,000
- C: 1,80,000
- D: 2,60,000

### 2. RANGE

RANGE works with the logical ordering values and includes peer rows having the same ordering value in the frame.

```
SELECT
    employee_name,
    joining_date,
    salary,
    SUM(salary) OVER (
        ORDER BY joining_date
        RANGE BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total
FROM employees;
```

For January 2, both B and C are peers because they have the same joining date.

Therefore, both can receive a running total of 1,80,000.

| Employee | Date  | Salary | RANGE total |
| -------- | ----- | ------ | ----------- |
| A        | Jan 1 | 50000  | 50000       |
| B        | Jan 2 | 60000  | 180000      |
| C        | Jan 2 | 70000  | 180000      |
| D        | Jan 3 | 80000  | 260000      |

### What does UNBOUNDED PRECEDING mean?

It means the frame starts from the first available row in the partition.

### What does CURRENT ROW mean?

It defines the frame endpoint at the current row, including peer rows when RANGE semantics apply.

### Other common frame boundaries

- UNBOUNDED PRECEDING: Start of the partition.
- N PRECEDING: N rows or value range before the current row, depending on frame type.
- CURRENT ROW: Current row or its peers, depending on frame type.
- N FOLLOWING: N rows or value range after the current row.
- UNBOUNDED FOLLOWING: End of the partition.

When should you use ROWS vs RANGE?

Use ROWS when you need exact row-by-row calculations, such as running totals.

Use RANGE when you want values with equal ordering keys to be treated together.

A useful interview point: the default window frame can differ in its practical effects depending on the database and function. With an ordered aggregate window, peer rows often receive the same cumulative result under the default RANGE frame. Explicitly specifying the frame avoids ambiguity.

# Section 5: Database Design and Data Modelling

## Q24. What is database normalization and denormalization?

Answer:

Normalization is the process of organizing data into multiple related tables to reduce redundancy and improve data consistency.

Denormalization is the process of combining or duplicating data to improve read performance, often at the cost of additional storage and more complex updates.

Let's understand normalization using an example.

Suppose we have one large table:

| Order_ID | Customer_Name | Customer_City | Product  | Product_Price |
| -------- | ------------- | ------------- | -------- | ------------- |
| 1        | Amit          | Mumbai        | Laptop   | 50000         |
| 2        | Amit          | Mumbai        | Mouse    | 1000          |
| 3        | Rahul         | Pune          | Keyboard | 2000          |

There is repeated customer information.

Amit's name and city appear multiple times.

This creates data redundancy.

### 1NF – First Normal Form

A table is in 1NF when:

- Each column contains atomic values.
- There are no repeating groups or multiple values stored in one cell.
- Each row can be uniquely identified.

Incorrect:

| customer_id | phone_numbers |
| ----------- | ------------- |
| 1           | 9876, 8765    |

Better:

| customer_id | phone_number |
| ----------- | ------------ |
| 1           | 9876         |
| 1           | 8765         |

Each cell contains one value.

### 2NF – Second Normal Form

A table must:

- Already satisfy 1NF.
- Have no partial dependency of a non-key attribute on a proper subset of a candidate key.

This is especially relevant when a table has a composite key.

Example:

Consider an OrderDetails table:

| order_id | product_id | customer_name | quantity |
| -------- | ---------- | ------------- | -------- |
| 1        | 101        | Amit          | 2        |
| 1        | 102        | Amit          | 1        |

Suppose the composite primary key is `(order_id, product_id)`.

Here, customer_name depends only on order_id, not on the complete composite key.

That is a partial dependency.

We can separate it:

Orders

| order_id | customer_name |
| -------- | ------------- |
| 1        | Amit          |

OrderDetails

| order_id | product_id | quantity |
| -------- | ---------- | -------- |
| 1        | 101        | 2        |
| 1        | 102        | 1        |

Now customer information is stored separately.

### 3NF – Third Normal Form

A table must:

- Satisfy 2NF.
- Have no transitive dependency of non-key attributes on a candidate key.

Example:

| employee_id | employee_name | department_id | department_name |
| ----------- | ------------- | ------------- | --------------- |
| 1           | Amit          | 10            | IT              |
| 2           | Rahul         | 10            | IT              |
| 3           | Priya         | 20            | HR              |

Here:

- employee_id determines employee_name and department_id.
- department_id determines department_name.

So department_name depends indirectly on employee_id through department_id.

We separate the tables:

Employees

| employee_id | employee_name | department_id |
| ----------- | ------------- | ------------- |
| 1           | Amit          | 10            |
| 2           | Rahul         | 10            |
| 3           | Priya         | 20            |

Departments

| department_id | department_name |
| ------------- | --------------- |
| 10            | IT              |
| 20            | HR              |

### BCNF – Boyce-Codd Normal Form

BCNF is a stricter version of 3NF.

For every non-trivial functional dependency X → Y, X must be a superkey.

In simple terms, every determinant must be a candidate key or superkey.

It addresses certain anomalies that can remain in tables satisfying 3NF.

### What are insertion, update and deletion anomalies?

Insertion anomaly: You cannot insert a department without inserting an employee if both are stored in the same table and employee data is mandatory.

Update anomaly: If Amit's department name changes, you may need to update multiple records. Missing one update creates inconsistent data.

Deletion anomaly: Deleting the last employee in a department might accidentally remove the only stored information about that department.

Normalization helps prevent these problems.

### What is denormalization?

Suppose an analytics dashboard frequently needs:

- Customer name.
- Customer city.
- Product name.
- Product price.
- Order amount.

Instead of joining multiple normalized tables for every report, we can create a denormalized analytical table containing these fields together.

This reduces some query complexity and can improve read performance.

### When should you normalize and denormalize?

| Scenario                              | Preferred design         |
| ------------------------------------- | ------------------------ |
| Banking transaction system            | Normalized               |
| Customer master database              | Normalized               |
| High-volume transactional application | Usually normalized       |
| Reporting and analytics               | Often denormalized       |
| Data warehouse                        | Often star-schema based  |
| Read-heavy dashboard                  | Denormalization may help |

Interview-level answer:

Normalization improves consistency and reduces redundancy, while denormalization improves read efficiency by reducing joins or precomputing information. The right choice depends on the workload.

## Q25. What are Primary Keys, Foreign Keys, Unique Keys and Composite Keys?

Answer:

These are constraints used to maintain data integrity.

### 1. Primary Key

A primary key uniquely identifies every record in a table.

```
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

Properties:

- Must contain unique values.
- Cannot contain NULL.
- A table has only one primary key constraint, but it can contain multiple columns.

### 2. Foreign Key

A foreign key establishes a relationship between two tables.

```
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

```
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY (dept_id)
        REFERENCES departments(dept_id)
);
```

Now employees can reference only department IDs that exist in the parent table, subject to the foreign-key rules.

A foreign key can contain NULL unless explicitly defined as NOT NULL.

### 3. Unique Key

A UNIQUE constraint ensures that values are unique.

```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

This prevents duplicate email values.

Unlike a primary key, a table can have multiple UNIQUE constraints.

NULL handling under UNIQUE constraints varies across database systems. For example, PostgreSQL normally allows multiple NULLs under a standard UNIQUE constraint.

### 4. Composite Key

A composite key consists of two or more columns that together uniquely identify a record.

Example:

```
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

A student can enroll in multiple courses, and a course can have multiple students.

But the same student-course combination cannot be inserted twice.

### What happens when you delete a parent record with child records?

Suppose department 10 has employees.

If you try to delete department 10, the database may prevent deletion because employees still reference it.

This depends on the foreign-key action.

CASCADE:

```
FOREIGN KEY (dept_id)
REFERENCES departments(dept_id)
ON DELETE CASCADE
```

Deleting a department automatically deletes its referencing employees.

RESTRICT / NO ACTION:

Prevents deleting the department while referencing employees exist. Exact timing and semantics can vary by database.

SET NULL:

Sets the referencing foreign-key column to NULL when the parent is deleted, provided the column permits NULL.

## Q26. What is the difference between OLTP and OLAP databases?

Answer:

OLTP and OLAP are two different types of database workloads.

### OLTP – Online Transaction Processing

OLTP systems handle day-to-day business transactions.

Examples:

- Customer registration.
- Money transfers.
- Order placement.
- Bill payments.
- Telecom recharge.

Characteristics:

- Frequent INSERT, UPDATE and DELETE operations.
- Many concurrent users.
- Usually short-running queries.
- Strong data consistency requirements.
- Often normalized schemas.

Example:

When a Jio customer recharges a mobile number, the transaction system records the recharge and updates the relevant account information.

### OLAP – Online Analytical Processing

OLAP systems are designed for analytics and reporting.

Examples:

- Customer churn analysis.
- Revenue analytics.
- Customer segmentation.
- Sales forecasting.
- Network performance analysis.

Characteristics:

- Large SELECT queries.
- Aggregations over large datasets.
- Historical data analysis.
- Complex joins.
- Often denormalized or dimensional schemas.

### Comparison

| Feature    | OLTP                       | OLAP                                |
| ---------- | -------------------------- | ----------------------------------- |
| Purpose    | Transactions               | Analytics                           |
| Queries    | Short and frequent         | Complex and analytical              |
| Operations | Insert, update, delete     | Mostly reads                        |
| Data       | Current operational data   | Historical and integrated data      |
| Schema     | Often normalized           | Often denormalized                  |
| Users      | Applications and customers | Analysts, data scientists, BI tools |

### What are Fact and Dimension tables?

A fact table stores measurable business events.

Example: `fact_transactions`

| transaction_id | customer_id | product_id | amount |
| -------------- | ----------- | ---------- | ------ |
| 1              | 101         | 501        | 1000   |
| 2              | 102         | 502        | 2000   |

A dimension table stores descriptive information.

Example: `dim_customer`

| customer_id | customer_name | city   |
| ----------- | ------------- | ------ |
| 101         | Amit          | Mumbai |
| 102         | Rahul         | Pune   |

A fact table contains measurements, while dimension tables provide the context for analyzing those measurements.

### What is a Star Schema?

A star schema has one central fact table connected directly to dimension tables.

[DWH | What is a data warehouse? - IONOS UK](https://images.openai.com/static-rsc-4/VUj897JfgtZYlxEMxzUkod-GYFgw4_n27XJMvDWj0eOf_K-Bgf5vnzR7Azzh_WfrgpXiKI7ZbGivovSuW6_E-BulErMhCj9l0A7UIixw9E09HnWh0nS41j5d49Cgnilbz31aSYIqcpn7NBmwM17mAhWebErfKUtyMxQ7oAZgqfc?purpose=inline)

[ionos.co.uk](https://www.ionos.co.uk/digitalguide/online-marketing/web-analytics/dwh-what-is-a-data-warehouse/?utm_source=chatgpt.com)

For example:

- Fact_Transactions
- Dim_Customer
- Dim_Product
- Dim_Date
- Dim_Location

### What is a Snowflake Schema?

In a snowflake schema, dimension tables are further normalized into related tables.

[Star Schema vs Snowflake Schema: Differences & Use Cases | DataCamp](https://images.openai.com/static-rsc-4/3cDebDMdlANA_grugS8kvbfdoHuPEbCmQdZzA_CivIWMO0vYZyFVMsOWgpncies4eoomt8VNnnafDYXt-YMxQvrEKH3rwuwZsoZIk_p5Dr6N8P1upzoJgck41VDdvG4G5QKi2GBPkzpbQBGChJlVYgE8Ca4Y7b54MJLJSqDykrM?purpose=inline)

[datacamp.com](https://www.datacamp.com/blog/star-schema-vs-snowflake-schema?utm_source=chatgpt.com)

For example:

Customer dimension may be split into:

- Customer
- City
- State
- Country

### How would you design a telecom customer analytics warehouse?

A possible structure:

Fact tables:

- Fact_Usage
- Fact_Recharge
- Fact_Billing
- Fact_Network_Events
- Fact_Churn

Dimension tables:

- Dim_Customer
- Dim_Device
- Dim_Plan
- Dim_Location
- Dim_Date
- Dim_Network_Site

You can then analyse:

- Monthly customer usage.
- Recharge trends.
- Churn rates by plan.
- Revenue by geographical location.
- Network quality by tower or site.

An important design consideration is the grain of each fact table. For example, Fact_Usage might store one record per customer per day per service, while Fact_Recharge might store one record per recharge transaction.

# Section 6: SQL Performance and Optimization

## Q27. What is an index, and how does it improve query performance?

Answer:

An index is a data structure maintained by a database to locate records more efficiently without scanning every row in a table.

Think of a book.

Without an index, if you want to find a topic, you might need to read every page.

With an index, you can directly identify the page containing that topic.

Similarly, a database index helps locate records based on indexed columns.

Suppose we have 10 million employee records.

```
SELECT *
FROM employees
WHERE emp_id = 10001;
```

Without a suitable index, the database may perform a full table scan.

With an index on emp_id, it can locate the matching record more efficiently.

### 1. Clustered Index

A clustered index organizes table data according to the index key.

In SQL Server, a table can have one clustered index because the table's rows are organized according to one clustered index structure.

In PostgreSQL, a CLUSTER operation physically reorders a table based on an index, but this ordering is not automatically maintained for future writes.

Therefore, clustered-index behaviour differs between database engines.

### 2. Non-clustered Index

A non-clustered index is a separate index structure that stores indexed values and references to the corresponding table rows.

A table can have multiple non-clustered indexes in SQL Server.

Example:

```
CREATE INDEX idx_employee_salary
ON employees(salary);
```

This creates an index on salary.

### 3. Composite Index

An index built using multiple columns.

```
CREATE INDEX idx_dept_salary
ON employees(department_id, salary);
```

This can help queries such as:

```
SELECT *
FROM employees
WHERE department_id = 10
  AND salary > 50000;
```

Does column order matter?

Yes.

An index on `(department_id, salary)` is generally most useful when queries filter on department_id or on department_id followed by salary.

It is not necessarily equally useful for queries filtering only on salary.

This is commonly called the leftmost-prefix principle in B-tree indexes.

### 4. Covering Index

A covering index contains all the columns needed by a particular query, allowing the database to potentially satisfy the query using the index alone.

For example:

```
CREATE INDEX idx_dept_salary_name
ON employees(department_id, salary, employee_name);
```

Query:

```
SELECT employee_name, salary
FROM employees
WHERE department_id = 10;
```

The index contains all required columns, so the database may avoid accessing the base table.

### Why can too many indexes reduce performance?

Every time data is inserted, updated or deleted, the database may also need to update the relevant indexes.

Therefore, excessive indexing can:

- Increase storage consumption.
- Slow down INSERT operations.
- Slow down UPDATE operations.
- Slow down DELETE operations.
- Increase maintenance overhead.

Why might a query not use an available index?

Some reasons include:

1. The query retrieves a large percentage of the table, making a sequential scan cheaper.
2. The indexed column is wrapped in a function that prevents ordinary index usage.
3. Statistics are outdated.
4. Data types are mismatched or implicit conversions occur.
5. The index column order does not suit the query.
6. The optimizer estimates that another execution strategy is cheaper.

## Q28. How would you optimize a slow SQL query?

Answer:

Suppose a query takes five minutes to execute on a table containing 100 million records.

I would not immediately start adding indexes or rewriting the query.

First, I would understand where the time is being spent.

### Step 1: Examine the execution plan

```
EXPLAIN ANALYZE
SELECT *
FROM transactions
WHERE customer_id = 101;
```

EXPLAIN shows the planned execution strategy.

EXPLAIN ANALYZE in PostgreSQL actually executes the query and reports measured execution details.

I would inspect:

- Sequential scans.
- Index scans.
- Join algorithms.
- Sort operations.
- Estimated versus actual row counts.
- Expensive aggregations.
- Disk spills and parallel execution.

### Step 2: Avoid SELECT \*

Instead of:

```
SELECT *
FROM transactions;
```

Use:

```
SELECT
    customer_id,
    transaction_date,
    amount
FROM transactions;
```

Retrieving unnecessary columns increases data transfer and can increase I/O.

### Step 3: Apply filters efficiently

Suppose we only need successful transactions from 2026.

```
SELECT *
FROM transactions
WHERE status = 'Success'
  AND transaction_date >= '2026-01-01'
  AND transaction_date < '2027-01-01';
```

This reduces the number of records that need to be processed.

The database optimizer may push these filters closer to the data scan.

### Step 4: Check indexing

If customer_id is frequently used for filtering:

```
CREATE INDEX idx_transactions_customer
ON transactions(customer_id);
```

But indexing should be based on query patterns and actual execution plans.

### Step 5: Check joins

Avoid joining large tables unnecessarily.

Check whether:

- Join columns have suitable indexes where relevant.
- The join conditions are correct.
- The join produces unexpected row multiplication.
- The tables can be aggregated before joining.

### Step 6: Consider partitioning

If the table contains transaction history for several years, partitioning by transaction date can help.

For example:

- Transactions_2024
- Transactions_2025
- Transactions_2026

With partitioning, the database can potentially scan only relevant partitions when the query filters on the partition key.

This is called partition pruning.

Note: In a partitioned table, these are logical partitions, not necessarily separate user-managed tables.

### Step 7: Check data skew

Suppose 80% of transactions belong to one customer or one region.

This can create uneven workload distribution in parallel processing systems and distributed databases.

The execution strategy needs to account for data distribution and skew.

### Step 8: Check statistics and query plans

The database optimizer relies on statistics to estimate:

- Number of rows.
- Number of distinct values.
- Value distribution.
- Data selectivity.

Outdated statistics can lead to poor execution plans.

### Practical interview answer

If asked how you would optimize a slow query, you can say:

"I would first inspect the execution plan to identify whether the bottleneck is a table scan, join, sort, aggregation or data movement. Then I would evaluate indexing, filter pushdown, partition pruning, unnecessary columns and join cardinality. After making changes, I would compare execution time and actual execution plans to verify the improvement."

Important: Avoid blindly replacing subqueries with joins or adding indexes. Optimization is based on measured bottlenecks, not assumptions.

## Q29. What is the difference between DELETE, TRUNCATE and DROP?

Answer:

All three are used to remove data or database objects, but their behaviour is different.

### 1. DELETE

DELETE removes selected records from a table.

```
DELETE FROM employees
WHERE department_id = 10;
```

Only employees belonging to department 10 are deleted.

You can also delete all records:

```
DELETE FROM employees;
```

The table structure remains.

### 2. TRUNCATE

TRUNCATE removes all records from a table.

```
TRUNCATE TABLE employees;
```

You cannot use a WHERE condition with TRUNCATE.

The table structure remains, but the data is removed.

It is generally more efficient than deleting every row individually, although implementation details vary.

### 3. DROP

DROP removes the entire database object.

```
DROP TABLE employees;
```

This removes:

- Table structure.
- Table data.
- Associated table-level indexes and constraints.

### Comparison

| Feature                                | DELETE       | TRUNCATE            | DROP              |
| -------------------------------------- | ------------ | ------------------- | ----------------- |
| Removes records                        | Yes          | Yes, all            | Yes               |
| Removes table structure                | No           | No                  | Yes               |
| Supports WHERE                         | Yes          | No                  | No                |
| Can remove selected rows               | Yes          | No                  | No                |
| Generally faster for clearing all rows | Not usually  | Often               | Not applicable    |
| Resets identity values                 | Generally no | Often, DB-dependent | Object is removed |

Can these operations be rolled back?

This is database-specific.

In PostgreSQL, DELETE, TRUNCATE and DROP are transactional and can generally be rolled back if executed within a transaction before commit.

In MySQL, TRUNCATE and DROP are DDL operations that cause implicit commits, so they generally cannot be rolled back like ordinary transactional DELETE operations.

SQL Server also supports transactional rollback for these operations in appropriate transactional contexts.

Interview takeaway: Never assume DELETE, TRUNCATE and DROP have identical rollback or identity-reset behaviour across database systems.

## Q30. What are CTEs, temporary tables and views?

Answer:

These are different ways of organizing and reusing SQL logic.

### 1. CTE – Common Table Expression

A CTE is a named temporary result set defined using the WITH clause.

Example:

```
WITH high_salary_employees AS (
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary_employees;
```

Here, the CTE first defines a logical result containing employees earning more than 50,000.

The outer query uses that result.

Why use CTEs?

- Improve readability.
- Break complex queries into smaller logical steps.
- Reuse intermediate results within a statement.
- Implement recursive queries.

### Can we use multiple CTEs?

Yes.

```
WITH employee_data AS (
    SELECT *
    FROM employees
),
department_data AS (
    SELECT *
    FROM departments
)
SELECT *
FROM employee_data e
JOIN department_data d
    ON e.dept_id = d.dept_id;
```

### What is a recursive CTE?

A recursive CTE references itself to process hierarchical or sequential data.

Example: Employee-manager hierarchy.

```
WITH RECURSIVE employee_hierarchy AS (

    SELECT
        emp_id,
        employee_name,
        manager_id,
        1 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT
        e.emp_id,
        e.employee_name,
        e.manager_id,
        h.level + 1
    FROM employees e
    JOIN employee_hierarchy h
        ON e.manager_id = h.emp_id
)
SELECT *
FROM employee_hierarchy;
```

Working:

1. The initial query finds top-level managers.
2. The recursive query finds employees reporting to them.
3. It continues identifying lower-level employees.
4. The recursion stops when no more matching employees are found.

### 2. Temporary Tables

A temporary table is a physical temporary database object used to store intermediate results.

```
CREATE TEMP TABLE high_salary_employees AS
SELECT *
FROM employees
WHERE salary > 50000;
```

You can then query it:

```
SELECT *
FROM high_salary_employees;
```

Temporary tables generally exist for a session or transaction, depending on the database and configuration.

They are useful when:

- Intermediate data is reused across multiple queries.
- You want to index intermediate results.
- You need to inspect intermediate data.
- Complex processing requires multiple steps.

### 3. Views

A view is a stored SQL query that behaves like a virtual table.

```
CREATE VIEW high_salary_view AS
SELECT *
FROM employees
WHERE salary > 50000;
```

You can query it:

```
SELECT *
FROM high_salary_view;
```

A regular view generally stores the query definition, not the actual query result.

### 4. Materialized Views

A materialized view stores the result of a query physically.

Example:

```
CREATE MATERIALIZED VIEW department_salary_summary AS
SELECT
    department_id,
    AVG(salary) AS avg_salary,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;
```

Unlike a normal view, the materialized view stores the calculated result.

When underlying data changes, the materialized view may become outdated until refreshed.

In PostgreSQL:

```
REFRESH MATERIALIZED VIEW department_salary_summary;
```

### Comparison

| Feature                   | CTE                  | Temporary Table               | View                            | Materialized View   |
| ------------------------- | -------------------- | ----------------------------- | ------------------------------- | ------------------- |
| Purpose                   | Organize query logic | Store intermediate data       | Reuse query definition          | Store query results |
| Physical result storage   | Not inherently       | Yes                           | Generally no                    | Yes                 |
| Lifetime                  | One statement        | Session/transaction dependent | Persistent definition           | Persistent result   |
| Reusable across queries   | No, generally        | Yes, within its lifetime      | Yes                             | Yes                 |
| Can be indexed separately | No                   | Yes                           | Not directly for ordinary views | DB-dependent        |

Are CTEs always materialized?

No.

In PostgreSQL, a non-recursive CTE may be inlined into the main query, depending on its properties and the optimizer.

You can also use MATERIALIZED or NOT MATERIALIZED in supported PostgreSQL versions to influence this behaviour.

Other databases have their own CTE optimization rules.

CTE vs subquery:

Both can produce similar results.

A CTE is generally easier to read when a query contains multiple logical stages. A subquery can be more compact for simple operations.

Neither is automatically faster.

# Section 7: Bonus – 10 Practical SQL Interview Problems with Answers

These are coding-style questions. Try to understand the query step by step because interviewers often change one condition and ask you to modify the solution.

We'll use the following tables.

Employees

| emp_id | name | department_id | salary | joining_date |
| ------ | ---- | ------------- | ------ | ------------ |
| 1      | A    | 10            | 80000  | 2023-01-10   |
| 2      | B    | 10            | 90000  | 2022-05-15   |
| 3      | C    | 20            | 70000  | 2023-06-01   |
| 4      | D    | 20            | 70000  | 2024-01-12   |
| 5      | E    | 30            | 100000 | 2021-03-20   |

Transactions

| transaction_id | customer_id | amount | status  | transaction_date |
| -------------- | ----------- | ------ | ------- | ---------------- |
| 1              | 101         | 1000   | Success | 2026-01-10       |
| 2              | 102         | 2000   | Failed  | 2026-01-12       |
| 3              | 101         | 1500   | Success | 2026-02-10       |
| 4              | 103         | 3000   | Success | 2026-02-15       |
| 5              | 101         | 500    | Failed  | 2026-03-10       |

## Problem 1. Find the second-highest salary in each department.

Answer:

We can use DENSE_RANK().

```
WITH ranked AS (
    SELECT
        emp_id,
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
)
SELECT *
FROM ranked
WHERE rnk = 2;
```

Explanation:

- PARTITION BY department_id creates separate groups for each department.
- ORDER BY salary DESC sorts salaries from highest to lowest.
- DENSE_RANK assigns salary ranks.
- The outer query selects rank 2.

In department 20, both C and D earn 70,000, so there is no second distinct salary. Department 10 has 80,000 as its second-highest salary. Department 30 has only one employee, so it has no second-highest distinct salary.

Result:

| Employee | Department | Salary |
| -------- | ---------- | ------ |
| A        | 10         | 80000  |

## Problem 2. Find employees earning more than their department's average salary.

Answer:

We can solve this using a correlated subquery.

```
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

Explanation:

For every employee:

1. Identify their department.
2. Calculate the average salary of that department.
3. Compare the employee's salary with the department average.
4. Return employees earning more than that average.

Another approach is using a window function:

```
WITH employee_data AS (
    SELECT
        *,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS dept_avg
    FROM employees
)
SELECT *
FROM employee_data
WHERE salary > dept_avg;
```

Both approaches solve the same problem.

## Problem 3. Find the top 2 highest-paid employees in each department.

Answer:

Use ROW_NUMBER():

```
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC, emp_id
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn <= 2;
```

Explanation:

The query independently ranks employees in every department.

- Department 10: B, A.
- Department 20: C, D.
- Department 30: E.

We use ROW_NUMBER because we need at most two employee records per department.

If the requirement were to return all employees tied at the second salary level, we would use RANK or DENSE_RANK instead.

## Problem 4. Find departments having more than 5 employees.

Answer:

```
SELECT
    department_id,
    COUNT(*) AS total_employees
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

Explanation:

- GROUP BY creates department-wise groups.
- COUNT(\*) calculates the number of employees in each department.
- HAVING filters departments whose employee count is greater than 5.

Why not WHERE?

Because we are filtering based on the result of an aggregation, not an individual employee's column value.

## Problem 5. Find customers who have never made a successful transaction.

Answer:

We can use NOT EXISTS.

```
SELECT DISTINCT customer_id
FROM transactions t
WHERE NOT EXISTS (
    SELECT 1
    FROM transactions t2
    WHERE t2.customer_id = t.customer_id
      AND t2.status = 'Success'
);
```

Explanation:

For every customer appearing in the transactions table:

- Check whether a successful transaction exists.
- If no successful transaction exists, return that customer.

For our sample:

- Customer 101 has successful transactions, so exclude.
- Customer 102 has only a failed transaction, so include.
- Customer 103 has a successful transaction, so exclude.

Output:

| customer_id |
| ----------- |
| 102         |

Alternative using GROUP BY and HAVING:

```
SELECT customer_id
FROM transactions
GROUP BY customer_id
HAVING SUM(
    CASE WHEN status = 'Success'
         THEN 1 ELSE 0 END
) = 0;
```

This is also a very common interview solution.

## Problem 6. Calculate the monthly successful transaction amount for each customer.

Answer:

```
SELECT
    customer_id,
    DATE_TRUNC('month', transaction_date) AS transaction_month,
    SUM(amount) AS total_amount
FROM transactions
WHERE status = 'Success'
GROUP BY
    customer_id,
    DATE_TRUNC('month', transaction_date)
ORDER BY customer_id, transaction_month;
```

Explanation:

First, WHERE filters only successful transactions.

Then we group by:

- Customer ID.
- Transaction month.

Finally, SUM calculates the total successful transaction amount for every customer-month combination.

Output:

| Customer | Month    | Amount |
| -------- | -------- | ------ |
| 101      | January  | 1000   |
| 101      | February | 1500   |
| 103      | February | 3000   |

Note: DATE_TRUNC is PostgreSQL syntax. In MySQL, you can use an expression such as `DATE_FORMAT(transaction_date, '%Y-%m-01')`.

## Problem 7. Find customers whose current month's spending is higher than the previous month.

Answer:

We need to calculate monthly spending first, then compare it with the previous month.

```
WITH monthly_sales AS (
    SELECT
        customer_id,
        DATE_TRUNC('month', transaction_date) AS month,
        SUM(amount) AS total_amount
    FROM transactions
    WHERE status = 'Success'
    GROUP BY
        customer_id,
        DATE_TRUNC('month', transaction_date)
),
comparison AS (
    SELECT
        customer_id,
        month,
        total_amount,
        LAG(total_amount) OVER (
            PARTITION BY customer_id
            ORDER BY month
        ) AS previous_amount
    FROM monthly_sales
)
SELECT *
FROM comparison
WHERE total_amount > previous_amount;
```

Explanation:

This query has two stages.

Stage 1: monthly_sales

We aggregate successful transaction amounts for every customer per month.

Stage 2: comparison

LAG retrieves the previous available monthly total for the customer.

Then we compare:

```
total_amount > previous_amount
```

For customer 101:

- January: 1,000.
- February: 1,500.
- March: No successful transaction.

February spending is greater than January spending, so customer 101 is returned.

Important: This compares against the previous available month in the data, not necessarily the immediately preceding calendar month. If missing months must count as zero, generate a customer-month calendar and fill missing values before applying LAG.

## Problem 8. Find duplicate customer records based on customer ID.

Answer:

```
SELECT
    customer_id,
    COUNT(*) AS occurrence_count
FROM customers
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

This returns customer IDs appearing more than once.

If we want the complete duplicate records:

```
WITH duplicate_records AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY created_at
        ) AS rn
    FROM customers
)
SELECT *
FROM duplicate_records
WHERE rn > 1;
```

The first record is retained based on created_at ordering, and subsequent occurrences are identified as duplicates.

If created_at can tie, add a unique ID as a secondary ordering column.

## Problem 9. Calculate the cumulative transaction amount for each customer.

Answer:

```
SELECT
    customer_id,
    transaction_date,
    amount,
    SUM(amount) OVER (
        PARTITION BY customer_id
        ORDER BY transaction_date, transaction_id
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS cumulative_amount
FROM transactions;
```

Explanation:

- PARTITION BY customer_id separates customers.
- ORDER BY transaction_date, transaction_id establishes transaction order.
- SUM calculates the cumulative amount.
- ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW includes all previous rows and the current row.

For customer 101:

| Date   | Amount | Cumulative |
| ------ | ------ | ---------- |
| Jan 10 | 1000   | 1000       |
| Feb 10 | 1500   | 2500       |
| Mar 10 | 500    | 3000       |

Notice that this includes failed transactions too. If the requirement is cumulative successful transactions, add:

```
WHERE status = 'Success'
```

before the window calculation.

## Problem 10. Find the percentage of successful transactions out of total transactions for each customer.

Answer:

```
SELECT
    customer_id,
    COUNT(*) AS total_transactions,

    SUM(
        CASE WHEN status = 'Success'
             THEN 1 ELSE 0 END
    ) AS successful_transactions,

    ROUND(
        100.0 *
        SUM(
            CASE WHEN status = 'Success'
                 THEN 1 ELSE 0 END
        ) / NULLIF(COUNT(*), 0),
        2
    ) AS success_percentage

FROM transactions
GROUP BY customer_id;
```

Explanation:

We calculate three things:

1. Total transaction count.
2. Successful transaction count.
3. Successful transaction percentage.

Formula:

\\[ \text{Success Percentage} = \frac{\text{Successful Transactions}} {\text{Total Transactions}}\times100 \\]

For customer 101:

- Total transactions = 3.
- Successful transactions = 2.

\\[ \frac{2}{3}\times100=66.67\\% \\]

Output:

| Customer | Total | Successful | Success % |
| -------- | ----- | ---------- | --------- |
| 101      | 3     | 2          | 66.67%    |
| 102      | 1     | 0          | 0%        |
| 103      | 1     | 1          | 100%      |

# Section 8: Additional Concepts You Should Know for a 5-Year Experienced Engineer

The 30 questions cover the main SQL interview syllabus, but I would also recommend understanding these concepts because they frequently appear in experienced-level interviews.

| Concept                       | What you should understand                                      |
| ----------------------------- | --------------------------------------------------------------- |
| ACID properties               | Atomicity, Consistency, Isolation and Durability                |
| Transactions                  | BEGIN, COMMIT, ROLLBACK                                         |
| Isolation levels              | Read Uncommitted, Read Committed, Repeatable Read, Serializable |
| Deadlocks                     | Why two transactions can block each other                       |
| Query optimizer               | How databases choose execution plans                            |
| Index scan vs table scan      | When each is preferred                                          |
| Hash Join vs Nested Loop Join | How database engines combine tables                             |
| Partitioning vs indexing      | How they solve different performance problems                   |
| Stored procedures             | Reusable SQL logic stored in the database                       |
| Triggers                      | Automatically executing logic on database events                |

## How to approach your SQL preparation

I would divide your preparation into three levels.

Level 1 – Strong fundamentals

Must master

Q1–Q12 and Q24–Q26

Understand SQL execution, filtering, joins, subqueries, normalization and data modelling.

Level 2 – Analytical SQL

Must master

Q13–Q23

Focus on aggregations, ranking, window functions, LAG, LEAD, cumulative calculations and practical problems.

Level 3 – Performance and internals

Experienced level

Q27–Q30 and additional concepts

Understand indexes, query optimization, execution plans, transactions and database internals.

## One final recommendation

For your AI Engineer interviews, I would give particular importance to SQL in the context of large-scale data processing.

For example, imagine an interviewer gives you a scenario:

"You have 500 million customer transaction records across multiple tables. You need to identify customers whose monthly spending has dropped by 40% compared to the previous month. How would you write and optimize the SQL query?"

A good answer should demonstrate that you understand:

1. How to aggregate transactions at the customer-month level.
2. How to use LAG() to compare monthly spending.
3. How to handle missing months and NULL values.
4. How to avoid duplicate records caused by joins.
5. How to optimize the query using partitioning, filtering and execution plans.

That combination of SQL fundamentals, analytical problem-solving and performance understanding is what I'd expect from a strong 5-year engineer.

</details>

## SQL theory questions:

<details>
<summary></summary>
1. Fundamental Concepts:
What is a database?
What is a database management system (DBMS)?
What is a relational database?
What is a non-relational database?
    
    Explain the difference between OLTP and OLAP.
    What are the advantages of using a DBMS?
    What are the three levels of database design? (Conceptual, Logical, Physical)
    What is data modeling?
    What are the different types of data models? (Relational, Object-oriented, Hierarchical)
    What is an Entity-Relationship (ER) model?
    
2. Data Modeling and Schema Design:
Explain normalization and denormalization.
What are the different normal forms (1NF, 2NF, 3NF)?
What is data redundancy and why is it important to avoid it?
What are primary and foreign keys?
What are constraints in a database?
How would you design a database for [specific application/scenario]?
Explain the process of designing a database schema.

3. SQL and Database Languages:
What is SQL?
Explain different SQL statements (SELECT, INSERT, UPDATE, DELETE, CREATE, ALTER).
What are joins?
What are subqueries?
Explain the use of indexes.
What are the different types of indexes? (Clustered, Non-clustered)
How would you optimize SQL queries for performance?

4. Data Integrity and Security:
What is data integrity?
What is referential integrity?
What are transactions?
What are ACID properties? (Atomicity, Consistency, Isolation, Durability)
Explain concurrency control.
How would you handle data backups and recovery?

5. Performance and Optimization:
What are common performance bottlenecks in a database?
What are different techniques for optimizing database performance? (Indexing, partitioning, caching)
What is database partitioning?
How would you troubleshoot a performance issue in a database?

6. Advanced Concepts:
What is database replication?
What is sharding?
What is the CAP theorem?
What are NoSQL databases and when would you use them?
What is a materialized view?
What is a stored procedure?
What is a trigger?
What is a view?

</details>