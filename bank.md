# Problem Statement: Banking Customer Deposits and Loan Management System

A bank wants to build a **transaction analytics and financial monitoring database** to track:

* Customer profiles
* Deposit accounts (savings/current)
* Loan accounts issued to customers
* Financial activities such as deposits, withdrawals, and loan repayments

The analytics team needs this system to:

* Monitor **customer deposits and withdrawals**
* Track **loan issuance and repayments**
* Identify **high-value customers**
* Detect **loan defaults or delayed payments**
* Generate **monthly revenue and risk analytics**

The database must support:

* Transactional operations (DML)
* Analytical SQL queries (window functions, aggregates)
* Complex joins and financial reporting

---

# Core Entities

The system consists of **4 core tables**:

1. Customers
2. Accounts (deposit accounts)
3. Loans
4. Transactions

This structure allows questions around:

* **One-to-many relationships**
* **Financial analytics**
* **Time-series transaction analysis**

---

# ER Diagram (Conceptual)

```
Customers
   |
   | 1
   |
   |------< Accounts
   |           |
   |           | 1
   |           |
   |           |------< Transactions
   |
   |
   |------< Loans
```

### Relationships

| Relationship           | Description                            |
| ---------------------- | -------------------------------------- |
| Customer → Accounts    | One customer can own multiple accounts |
| Account → Transactions | Each account has many transactions     |
| Customer → Loans       | Customer can have multiple loans       |

---

# Table 1: Customers

Stores customer personal and registration information.

### Columns

| Column      | Type         | Description           |
| ----------- | ------------ | --------------------- |
| customer_id | BIGINT       | Primary key           |
| first_name  | VARCHAR(50)  | Customer first name   |
| last_name   | VARCHAR(50)  | Customer last name    |
| email       | VARCHAR(120) | Unique customer email |
| phone       | VARCHAR(20)  | Contact number        |
| city        | VARCHAR(50)  | Customer city         |
| country     | VARCHAR(50)  | Country               |
| created_at  | DATETIME     | Registration date     |

### SQL

```sql
CREATE TABLE Customers (
    customer_id BIGINT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(120) UNIQUE,
    phone VARCHAR(20),
    city VARCHAR(50),
    country VARCHAR(50),
    created_at DATETIME
);
```

### Concepts Covered

* Primary key
* Unique constraint
* String data types
* Datetime type

---

# Table 2: Accounts

Represents customer deposit accounts (savings/current).

### Columns

| Column       | Type        | Description             |
| ------------ | ----------- | ----------------------- |
| account_id   | BIGINT      | Primary key             |
| customer_id  | BIGINT      | Foreign key             |
| account_type | VARCHAR(20) | Savings/Current         |
| balance      | DOUBLE      | Current account balance |
| opened_date  | DATETIME    | Account opening date    |
| status       | VARCHAR(20) | Active/Closed           |

### SQL

```sql
CREATE TABLE Accounts (
    account_id BIGINT PRIMARY KEY,
    customer_id BIGINT,
    account_type VARCHAR(20),
    balance DOUBLE,
    opened_date DATETIME,
    status VARCHAR(20),
    
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```

### Concepts Covered

* Foreign keys
* Financial numeric fields
* One-to-many relationship

---

# Table 3: Loans

Stores loan accounts issued to customers.

### Columns

| Column        | Type        | Description           |
| ------------- | ----------- | --------------------- |
| loan_id       | BIGINT      | Primary key           |
| customer_id   | BIGINT      | Loan owner            |
| loan_amount   | DOUBLE      | Total loan amount     |
| interest_rate | DOUBLE      | Interest percentage   |
| loan_type     | VARCHAR(50) | Home/Car/Personal     |
| issued_date   | DATETIME    | Loan issue date       |
| loan_status   | VARCHAR(20) | Active/Closed/Default |

### SQL

```sql
CREATE TABLE Loans (
    loan_id BIGINT PRIMARY KEY,
    customer_id BIGINT,
    loan_amount DOUBLE,
    interest_rate DOUBLE,
    loan_type VARCHAR(50),
    issued_date DATETIME,
    loan_status VARCHAR(20),
    
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```

### Concepts Covered

* Financial metrics
* Loan analytics
* Time-based financial records

---

# Table 4: Transactions

Tracks deposits, withdrawals, transfers, and loan repayments.

### Columns

| Column           | Type         | Description                            |
| ---------------- | ------------ | -------------------------------------- |
| transaction_id   | BIGINT       | Primary key                            |
| account_id       | BIGINT       | Linked account                         |
| transaction_type | VARCHAR(30)  | Deposit/Withdraw/Transfer/Loan_Payment |
| amount           | DOUBLE       | Transaction amount                     |
| transaction_date | DATETIME     | Transaction timestamp                  |
| description      | VARCHAR(255) | Transaction description                |

### SQL

```sql
CREATE TABLE Transactions (
    transaction_id BIGINT PRIMARY KEY,
    account_id BIGINT,
    transaction_type VARCHAR(30),
    amount DOUBLE,
    transaction_date DATETIME,
    description VARCHAR(255),
    
    FOREIGN KEY (account_id) REFERENCES Accounts(account_id)
);
```

### Concepts Covered

* Transaction history
* Time-series analysis
* Financial analytics

---

# Final ER Relationship Summary

| Table     | Relationship | Table        |
| --------- | ------------ | ------------ |
| Customers | 1 → Many     | Accounts     |
| Accounts  | 1 → Many     | Transactions |
| Customers | 1 → Many     | Loans        |

---

<details>
<summary>Some list of Question</summary>
### Data Retrieval and Filtering

* Customers with high balances
* Recent transactions
* Loan customers

### Joins

* Customer → Accounts
* Accounts → Transactions
* Customers → Loans

### Aggregations

* Total deposits per customer
* Average loan amount
* Monthly transaction volume

### Window Functions

* Running balance per account
* Rank customers by deposits
* Compare current vs previous transactions

### Subqueries / CTEs

* Customers with deposits above average
* Loan risk analysis
* Transaction trend analysis

### Set Operations

* Customers with loans but no accounts
* Customers with accounts but no loans

### DML

* Insert transactions
* Update balances
* Delete closed accounts

### DDL

* Add new columns
* Modify schema
* Drop tables
* Truncate logs

---

# Optional Extension (Advanced Data Engineer Interviews)

You can add additional tables like:

* **Branches**
* **Loan_Payments**
* **Account_Audit_Log**
* **Fraud_Alerts**

These introduce:

* Recursive CTE problems
* Fraud detection analytics
* Time-series financial analysis

---

</details>

---

<details>
<summary>Begineer Level Question</summary>

Below are **30 Beginner–Intermediate (FAANG-style but not trivial) SQL questions with answers** using the **Banking Customer Deposits and Loan Management System schema** we designed.

Schema reminder:

```sql
Customers(customer_id, first_name, last_name, email, phone, city, country, created_at)

Accounts(account_id, customer_id, account_type, balance, opened_date, status)

Loans(loan_id, customer_id, loan_amount, interest_rate, loan_type, issued_date, loan_status)

Transactions(transaction_id, account_id, transaction_type, amount, transaction_date, description)
```

These questions focus on:

* Data retrieval and filtering
* Joins and set operations
* Aggregations
* Window functions
* Subqueries
* CTEs

---

# 1. Retrieve all active accounts ordered by balance (highest first)

```sql
SELECT *
FROM Accounts
WHERE status = 'Active'
ORDER BY balance DESC;
```

---

# 2. Find customers from cities starting with 'New'

```sql
SELECT *
FROM Customers
WHERE city LIKE 'New%';
```

---

# 3. Count number of accounts per account type

```sql
SELECT account_type, COUNT(*) AS total_accounts
FROM Accounts
GROUP BY account_type;
```

---

# 4. Find customers having more than one account

```sql
SELECT customer_id, COUNT(account_id) AS account_count
FROM Accounts
GROUP BY customer_id
HAVING COUNT(account_id) > 1;
```

---

# 5. Retrieve top 5 customers with highest account balances

```sql
SELECT c.customer_id, c.first_name, a.balance
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
ORDER BY a.balance DESC
LIMIT 5;
```

---

# 6. Find total balance per customer

```sql
SELECT customer_id, SUM(balance) AS total_balance
FROM Accounts
GROUP BY customer_id;
```

---

# 7. List all customers and their accounts (including those without accounts)

```sql
SELECT c.customer_id, c.first_name, a.account_id
FROM Customers c
LEFT JOIN Accounts a
ON c.customer_id = a.customer_id;
```

---

# 8. Retrieve all transactions above average transaction amount

```sql
SELECT *
FROM Transactions
WHERE amount >
      (SELECT AVG(amount) FROM Transactions);
```

---

# 9. Find minimum and maximum loan amounts

```sql
SELECT MIN(loan_amount) AS min_loan,
       MAX(loan_amount) AS max_loan
FROM Loans;
```

---

# 10. Retrieve distinct loan types

```sql
SELECT DISTINCT loan_type
FROM Loans;
```

---

# 11. Find customers who have taken loans

```sql
SELECT c.customer_id, c.first_name
FROM Customers c
INNER JOIN Loans l
ON c.customer_id = l.customer_id;
```

---

# 12. Find customers who have accounts but no loans

```sql
SELECT customer_id
FROM Accounts

EXCEPT

SELECT customer_id
FROM Loans;
```

---

# 13. Retrieve all customers who either have loans or accounts

```sql
SELECT customer_id FROM Accounts
UNION
SELECT customer_id FROM Loans;
```

---

# 14. Find accounts opened after 2022

```sql
SELECT *
FROM Accounts
WHERE opened_date > '2022-01-01';
```

---

# 15. Count number of transactions per account

```sql
SELECT account_id, COUNT(*) AS transaction_count
FROM Transactions
GROUP BY account_id;
```

---

# 16. Find total transaction amount per account

```sql
SELECT account_id, SUM(amount) AS total_transactions
FROM Transactions
GROUP BY account_id;
```

---

# 17. Rank customers by total account balance

```sql
SELECT customer_id,
       SUM(balance) AS total_balance,
       RANK() OVER (ORDER BY SUM(balance) DESC) AS rank
FROM Accounts
GROUP BY customer_id;
```

---

# 18. Assign row numbers to transactions per account

```sql
SELECT account_id,
       transaction_id,
       ROW_NUMBER() OVER (PARTITION BY account_id ORDER BY transaction_date) AS rn
FROM Transactions;
```

---

# 19. Find previous transaction amount for each account

```sql
SELECT account_id,
       transaction_date,
       amount,
       LAG(amount) OVER (PARTITION BY account_id ORDER BY transaction_date) AS prev_amount
FROM Transactions;
```

---

# 20. Find next transaction amount using LEAD

```sql
SELECT account_id,
       amount,
       LEAD(amount) OVER (PARTITION BY account_id ORDER BY transaction_date) AS next_amount
FROM Transactions;
```

---

# 21. Find average balance per account type

```sql
SELECT account_type,
       AVG(balance) AS avg_balance
FROM Accounts
GROUP BY account_type;
```

---

# 22. Retrieve customers whose balance is above average

```sql
SELECT *
FROM Accounts
WHERE balance >
(
SELECT AVG(balance)
FROM Accounts
);
```

---

# 23. Find the latest transaction per account

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY account_id ORDER BY transaction_date DESC) AS rn
    FROM Transactions
) t
WHERE rn = 1;
```

---

# 24. Find total loan amount per loan type

```sql
SELECT loan_type,
       SUM(loan_amount) AS total_loans
FROM Loans
GROUP BY loan_type;
```

---

# 25. Find top 3 highest loan amounts

```sql
SELECT *
FROM Loans
ORDER BY loan_amount DESC
LIMIT 3;
```

---

# 26. Retrieve accounts with transactions in last 30 days

```sql
SELECT DISTINCT account_id
FROM Transactions
WHERE transaction_date >= CURRENT_DATE - INTERVAL '30 days';
```

---

# 27. Create a CTE to calculate customer balances

```sql
WITH customer_balance AS (
    SELECT customer_id, SUM(balance) AS total_balance
    FROM Accounts
    GROUP BY customer_id
)
SELECT *
FROM customer_balance;
```

---

# 28. Use CTE to find top 5 customers by balance

```sql
WITH customer_balance AS (
    SELECT customer_id, SUM(balance) AS total_balance
    FROM Accounts
    GROUP BY customer_id
)
SELECT *
FROM customer_balance
ORDER BY total_balance DESC
LIMIT 5;
```

---

# 29. Find customers with loans above average loan amount

```sql
SELECT *
FROM Loans
WHERE loan_amount >
(
SELECT AVG(loan_amount)
FROM Loans
);
```

---

# 30. Find number of transactions per day

```sql
SELECT DATE(transaction_date) AS transaction_day,
       COUNT(*) AS total_transactions
FROM Transactions
GROUP BY DATE(transaction_date)
ORDER BY transaction_day;
```

---

# Topics Covered in These 30 Questions

### Data Retrieval

* SELECT
* WHERE
* ORDER BY
* DISTINCT
* LIMIT
* LIKE

### Aggregations

* COUNT
* SUM
* AVG
* MIN
* MAX
* GROUP BY
* HAVING

### Joins

* INNER JOIN
* LEFT JOIN

### Set Operations

* UNION
* EXCEPT

### Window Functions

* RANK
* ROW_NUMBER
* LAG
* LEAD

### Subqueries

* Correlated subqueries
* Nested aggregations

### CTEs

* Basic WITH clause
* Analytical queries

---

</details>

---

<details>
<summary>Medim Level Question</summary>

Below are **30 Medium-level FAANG-style SQL interview questions with answers** based on the **Banking Customer Deposits and Loan Management System** schema.

These are **not basic**; they test patterns commonly used in **Data Engineer / Data Scientist SQL interviews** at large companies.

---

# Schema Used

```sql
Customers(customer_id, first_name, last_name, email, phone, city, country, created_at)

Accounts(account_id, customer_id, account_type, balance, opened_date, status)

Loans(loan_id, customer_id, loan_amount, interest_rate, loan_type, issued_date, loan_status)

Transactions(transaction_id, account_id, transaction_type, amount, transaction_date, description)
```

---

# 1. Find **top 5 customers by total account balance**

```sql
SELECT customer_id,
       SUM(balance) AS total_balance
FROM Accounts
GROUP BY customer_id
ORDER BY total_balance DESC
LIMIT 5;
```

---

# 2. Find **customers whose total balance is above the average balance**

```sql
SELECT customer_id, SUM(balance) AS total_balance
FROM Accounts
GROUP BY customer_id
HAVING SUM(balance) >
       (SELECT AVG(balance) FROM Accounts);
```

---

# 3. Find **accounts with transaction count greater than 10**

```sql
SELECT account_id, COUNT(*) AS transaction_count
FROM Transactions
GROUP BY account_id
HAVING COUNT(*) > 10;
```

---

# 4. Find **customers who have both loans and accounts**

```sql
SELECT DISTINCT c.customer_id
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
JOIN Loans l ON c.customer_id = l.customer_id;
```

---

# 5. Find **customers who have accounts but no loans**

```sql
SELECT customer_id
FROM Accounts

EXCEPT

SELECT customer_id
FROM Loans;
```

---

# 6. Find **loan count per customer**

```sql
SELECT customer_id,
       COUNT(*) AS loan_count
FROM Loans
GROUP BY customer_id
ORDER BY loan_count DESC;
```

---

# 7. Find **total transaction amount per account**

```sql
SELECT account_id,
       SUM(amount) AS total_transaction_amount
FROM Transactions
GROUP BY account_id;
```

---

# 8. Rank **customers by total transaction value**

```sql
SELECT a.customer_id,
       SUM(t.amount) total_spent,
       RANK() OVER (ORDER BY SUM(t.amount) DESC) rnk
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id;
```

---

# 9. Find **top account per customer by balance**

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER
           (PARTITION BY customer_id ORDER BY balance DESC) rn
    FROM Accounts
) t
WHERE rn = 1;
```

---

# 10. Find **average loan amount per loan type**

```sql
SELECT loan_type,
       AVG(loan_amount) avg_loan
FROM Loans
GROUP BY loan_type;
```

---

# 11. Find **loan amount greater than average loan**

```sql
SELECT *
FROM Loans
WHERE loan_amount >
(
SELECT AVG(loan_amount)
FROM Loans
);
```

---

# 12. Find **daily transaction totals**

```sql
SELECT DATE(transaction_date) AS day,
       SUM(amount) total_amount
FROM Transactions
GROUP BY DATE(transaction_date)
ORDER BY day;
```

---

# 13. Find **running transaction total per account**

```sql
SELECT account_id,
       transaction_date,
       amount,
       SUM(amount) OVER
       (PARTITION BY account_id ORDER BY transaction_date)
       AS running_total
FROM Transactions;
```

---

# 14. Find **previous transaction amount per account**

```sql
SELECT account_id,
       transaction_date,
       amount,
       LAG(amount) OVER
       (PARTITION BY account_id ORDER BY transaction_date) prev_amount
FROM Transactions;
```

---

# 15. Find **next transaction date per account**

```sql
SELECT account_id,
       transaction_date,
       LEAD(transaction_date)
       OVER (PARTITION BY account_id ORDER BY transaction_date)
       next_txn
FROM Transactions;
```

---

# 16. Find **top 3 accounts with highest balances**

```sql
SELECT *
FROM Accounts
ORDER BY balance DESC
LIMIT 3;
```

---

# 17. Find **number of customers per city**

```sql
SELECT city,
       COUNT(*) total_customers
FROM Customers
GROUP BY city
ORDER BY total_customers DESC;
```

---

# 18. Find **customers who opened accounts after 2023**

```sql
SELECT DISTINCT customer_id
FROM Accounts
WHERE opened_date > '2023-01-01';
```

---

# 19. Find **customers who made transactions above 10,000**

```sql
SELECT DISTINCT a.customer_id
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
WHERE t.amount > 10000;
```

---

# 20. Find **loan customers with highest interest rate**

```sql
SELECT *
FROM Loans
ORDER BY interest_rate DESC
LIMIT 5;
```

---

# 21. Find **accounts with highest transaction totals**

```sql
SELECT account_id,
       SUM(amount) total_amount
FROM Transactions
GROUP BY account_id
ORDER BY total_amount DESC
LIMIT 5;
```

---

# 22. Find **customers with the most transactions**

```sql
SELECT a.customer_id,
       COUNT(*) txn_count
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
ORDER BY txn_count DESC;
```

---

# 23. Find **latest transaction per account**

```sql
SELECT *
FROM (
SELECT *,
ROW_NUMBER() OVER
(PARTITION BY account_id ORDER BY transaction_date DESC) rn
FROM Transactions
) t
WHERE rn = 1;
```

---

# 24. Find **loan total per customer**

```sql
SELECT customer_id,
       SUM(loan_amount) total_loan
FROM Loans
GROUP BY customer_id;
```

---

# 25. Find **accounts opened per year**

```sql
SELECT EXTRACT(YEAR FROM opened_date) year,
       COUNT(*) accounts
FROM Accounts
GROUP BY year
ORDER BY year;
```

---

# 26. Find **customers with balances greater than their city's average**

```sql
SELECT *
FROM (
SELECT c.city,
       a.customer_id,
       a.balance,
       AVG(a.balance) OVER(PARTITION BY c.city) city_avg
FROM Accounts a
JOIN Customers c
ON a.customer_id = c.customer_id
) t
WHERE balance > city_avg;
```

---

# 27. Find **customers who have more than one loan**

```sql
SELECT customer_id,
       COUNT(*) loan_count
FROM Loans
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

---

# 28. Find **customers whose total transactions exceed total loan amount**

```sql
SELECT a.customer_id
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
HAVING SUM(t.amount) >
(
SELECT SUM(l.loan_amount)
FROM Loans l
WHERE l.customer_id = a.customer_id
);
```

---

# 29. Use CTE to find **top customers by transaction value**

```sql
WITH customer_txn AS (
SELECT a.customer_id,
       SUM(t.amount) total_txn
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
)
SELECT *
FROM customer_txn
ORDER BY total_txn DESC
LIMIT 5;
```

---

# 30. Use CTE to calculate **transaction rank per account**

```sql
WITH ranked_txn AS (
SELECT *,
       RANK() OVER
       (PARTITION BY account_id ORDER BY amount DESC) rnk
FROM Transactions
)
SELECT *
FROM ranked_txn
WHERE rnk <= 3;
```

---

# Concepts Covered (FAANG Interview Focus)

### Data Retrieval

* SELECT
* WHERE
* ORDER BY
* LIMIT
* DISTINCT

### Aggregation

* COUNT
* SUM
* AVG
* GROUP BY
* HAVING

### Joins

* INNER JOIN
* multi-table joins

### Set Operations

* UNION / EXCEPT

### Window Functions

* RANK
* ROW_NUMBER
* LAG
* LEAD
* running totals

### Subqueries

* correlated subqueries
* nested aggregations

### CTEs

* intermediate aggregations
* ranking logic

---

</details>

---

<details>
<summary>Hard Level Question</summary>
Below are **30 HARD (FAANG-level) SQL interview questions with solutions** using the **Banking Customer Deposits and Loan Management System schema**.

These problems reflect **real patterns used in senior data engineer / analytics engineer interviews**:

* running balances
* gap & island problems
* fraud detection
* cohort analysis
* ranking within partitions
* recursive CTEs
* advanced window analytics

---

# Schema

```sql
Customers(customer_id, first_name, last_name, email, phone, city, country, created_at)

Accounts(account_id, customer_id, account_type, balance, opened_date, status)

Loans(loan_id, customer_id, loan_amount, interest_rate, loan_type, issued_date, loan_status)

Transactions(transaction_id, account_id, transaction_type, amount, transaction_date, description)
```

---

# 1. Find **top 3 customers by total deposits per city**

```sql
SELECT *
FROM (
    SELECT c.city,
           a.customer_id,
           SUM(t.amount) total_deposit,
           ROW_NUMBER() OVER (PARTITION BY c.city ORDER BY SUM(t.amount) DESC) rn
    FROM Customers c
    JOIN Accounts a ON c.customer_id = a.customer_id
    JOIN Transactions t ON a.account_id = t.account_id
    WHERE t.transaction_type = 'Deposit'
    GROUP BY c.city, a.customer_id
) t
WHERE rn <= 3;
```

---

# 2. Compute **running balance per account**

```sql
SELECT account_id,
       transaction_date,
       amount,
       SUM(amount) OVER
       (PARTITION BY account_id ORDER BY transaction_date) running_balance
FROM Transactions;
```

---

# 3. Find **accounts with decreasing balances across transactions**

```sql
SELECT account_id
FROM (
    SELECT account_id,
           amount,
           LAG(amount) OVER (PARTITION BY account_id ORDER BY transaction_date) prev_amt
    FROM Transactions
) t
WHERE amount < prev_amt;
```

---

# 4. Find **customers whose loan amount exceeds total deposits**

```sql
SELECT c.customer_id
FROM Customers c
JOIN Loans l ON c.customer_id = l.customer_id
GROUP BY c.customer_id, l.loan_amount
HAVING l.loan_amount >
(
SELECT SUM(t.amount)
FROM Accounts a
JOIN Transactions t ON a.account_id = t.account_id
WHERE a.customer_id = c.customer_id
);
```

---

# 5. Find **accounts with transactions occurring within 5 minutes of each other**

```sql
SELECT account_id,
       transaction_date,
       prev_txn
FROM (
SELECT account_id,
       transaction_date,
       LAG(transaction_date)
       OVER (PARTITION BY account_id ORDER BY transaction_date) prev_txn
FROM Transactions
) t
WHERE transaction_date - prev_txn <= INTERVAL '5 minutes';
```

---

# 6. Identify **customers with transactions in 3 consecutive days**

```sql
SELECT DISTINCT customer_id
FROM (
SELECT a.customer_id,
       DATE(transaction_date) dt,
       LAG(DATE(transaction_date),2)
       OVER (PARTITION BY a.customer_id ORDER BY DATE(transaction_date)) prev2
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
) t
WHERE dt - prev2 = INTERVAL '2 days';
```

---

# 7. Find **most common transaction type per account**

```sql
SELECT *
FROM (
SELECT account_id,
       transaction_type,
       COUNT(*) cnt,
       RANK() OVER(PARTITION BY account_id ORDER BY COUNT(*) DESC) r
FROM Transactions
GROUP BY account_id, transaction_type
) t
WHERE r = 1;
```

---

# 8. Detect **duplicate transactions (same amount within 10 minutes)**

```sql
SELECT *
FROM (
SELECT account_id,
       amount,
       transaction_date,
       LAG(transaction_date)
       OVER (PARTITION BY account_id, amount ORDER BY transaction_date) prev
FROM Transactions
) t
WHERE transaction_date - prev <= INTERVAL '10 minutes';
```

---

# 9. Find **top 5% customers by deposits**

```sql
SELECT *
FROM (
SELECT customer_id,
       SUM(amount) total_deposit,
       NTILE(20) OVER (ORDER BY SUM(amount) DESC) bucket
FROM Accounts a
JOIN Transactions t ON a.account_id = t.account_id
GROUP BY customer_id
) t
WHERE bucket = 1;
```

---

# 10. Compute **monthly revenue trend**

```sql
SELECT month,
       revenue,
       revenue - LAG(revenue) OVER (ORDER BY month) growth
FROM (
SELECT DATE_TRUNC('month', transaction_date) month,
       SUM(amount) revenue
FROM Transactions
GROUP BY month
) t;
```

---

# 11. Find **longest gap between transactions per account**

```sql
SELECT account_id,
       MAX(transaction_date - prev_txn) longest_gap
FROM (
SELECT account_id,
       transaction_date,
       LAG(transaction_date)
       OVER (PARTITION BY account_id ORDER BY transaction_date) prev_txn
FROM Transactions
) t
GROUP BY account_id;
```

---

# 12. Find **customers contributing to top 80% deposits (Pareto)**

```sql
WITH cust_dep AS (
SELECT a.customer_id,
       SUM(t.amount) total_dep
FROM Accounts a
JOIN Transactions t ON a.account_id = t.account_id
GROUP BY a.customer_id
),
ranked AS (
SELECT *,
       SUM(total_dep) OVER(ORDER BY total_dep DESC) cum_dep,
       SUM(total_dep) OVER() total
FROM cust_dep
)
SELECT *
FROM ranked
WHERE cum_dep <= total * 0.8;
```

---

# 13. Find **median transaction amount**

```sql
SELECT percentile_cont(0.5)
WITHIN GROUP (ORDER BY amount)
FROM Transactions;
```

---

# 14. Identify **inactive accounts (no transaction for 6 months)**

```sql
SELECT account_id
FROM Transactions
GROUP BY account_id
HAVING MAX(transaction_date) <
CURRENT_DATE - INTERVAL '6 months';
```

---

# 15. Find **customers with highest loan-to-deposit ratio**

```sql
SELECT c.customer_id,
       SUM(l.loan_amount) /
       SUM(t.amount) ratio
FROM Customers c
JOIN Loans l ON c.customer_id = l.customer_id
JOIN Accounts a ON c.customer_id = a.customer_id
JOIN Transactions t ON a.account_id = t.account_id
GROUP BY c.customer_id
ORDER BY ratio DESC
LIMIT 5;
```

---

# 16. Find **first transaction per account**

```sql
SELECT *
FROM (
SELECT *,
ROW_NUMBER() OVER
(PARTITION BY account_id ORDER BY transaction_date) rn
FROM Transactions
) t
WHERE rn = 1;
```

---

# 17. Find **customers with deposits but no withdrawals**

```sql
SELECT DISTINCT a.customer_id
FROM Accounts a
JOIN Transactions t ON a.account_id = t.account_id
WHERE t.transaction_type = 'Deposit'

EXCEPT

SELECT DISTINCT a.customer_id
FROM Accounts a
JOIN Transactions t ON a.account_id = t.account_id
WHERE t.transaction_type = 'Withdrawal';
```

---

# 18. Generate **transaction sequence numbers**

```sql
SELECT account_id,
       transaction_date,
       ROW_NUMBER() OVER
       (PARTITION BY account_id ORDER BY transaction_date)
FROM Transactions;
```

---

# 19. Identify **customers with increasing deposit trend**

```sql
SELECT *
FROM (
SELECT a.customer_id,
       t.transaction_date,
       t.amount,
       LAG(t.amount)
       OVER (PARTITION BY a.customer_id ORDER BY t.transaction_date) prev
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
WHERE t.transaction_type = 'Deposit'
) t
WHERE amount > prev;
```

---

# 20. Find **accounts whose transaction amounts exceed account balance**

```sql
SELECT a.account_id
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
WHERE t.amount > a.balance;
```

---

# 21. Find **customers with transactions in every month of a year**

```sql
SELECT customer_id
FROM (
SELECT a.customer_id,
       COUNT(DISTINCT DATE_TRUNC('month',transaction_date)) m
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
) t
WHERE m = 12;
```

---

# 22. Find **top transaction per account**

```sql
SELECT *
FROM (
SELECT *,
ROW_NUMBER() OVER
(PARTITION BY account_id ORDER BY amount DESC) rn
FROM Transactions
) t
WHERE rn = 1;
```

---

# 23. Find **loan customers with no transactions**

```sql
SELECT customer_id
FROM Loans

EXCEPT

SELECT DISTINCT customer_id
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id;
```

---

# 24. Compute **7-day moving average transaction amount**

```sql
SELECT transaction_date,
       AVG(amount) OVER
       (ORDER BY transaction_date
       ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)
FROM Transactions;
```

---

# 25. Identify **largest transaction gap globally**

```sql
SELECT MAX(transaction_date - prev_txn)
FROM (
SELECT transaction_date,
       LAG(transaction_date)
       OVER (ORDER BY transaction_date) prev_txn
FROM Transactions
) t;
```

---

# 26. Find **customers sharing the same city**

```sql
SELECT c1.customer_id,
       c2.customer_id,
       c1.city
FROM Customers c1
JOIN Customers c2
ON c1.city = c2.city
AND c1.customer_id < c2.customer_id;
```

---

# 27. Find **loan customers who also hold accounts**

```sql
SELECT customer_id
FROM Loans
INTERSECT
SELECT customer_id
FROM Accounts;
```

---

# 28. Generate **date series using recursive CTE**

```sql
WITH RECURSIVE dates AS (
SELECT DATE('2024-01-01') d
UNION ALL
SELECT d + INTERVAL '1 day'
FROM dates
WHERE d < '2024-01-31'
)
SELECT * FROM dates;
```

---

# 29. Find **accounts with highest withdrawal frequency**

```sql
SELECT account_id,
       COUNT(*) withdrawals
FROM Transactions
WHERE transaction_type = 'Withdrawal'
GROUP BY account_id
ORDER BY withdrawals DESC
LIMIT 5;
```

---

# 30. Find **customers whose deposits increased month-over-month**

```sql
SELECT *
FROM (
SELECT a.customer_id,
       DATE_TRUNC('month',t.transaction_date) month,
       SUM(t.amount) amt,
       LAG(SUM(t.amount))
       OVER(PARTITION BY a.customer_id ORDER BY DATE_TRUNC('month',t.transaction_date)) prev
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id, month
) t
WHERE amt > prev;
```

---

# What These Questions Test (FAANG SQL Patterns)

These cover **real interview patterns**:

### Advanced Window Functions

* running totals
* LAG / LEAD comparisons
* moving averages
* ranking per partition

### Time-Series Analysis

* monthly growth
* inactivity detection
* transaction gaps

### Analytical SQL

* Pareto (80/20 rule)
* customer segmentation
* trend detection

### Complex Joins

* self joins
* multi-table joins
* cross entity analysis

### Set Operations

* UNION
* INTERSECT
* EXCEPT

### Advanced CTE Usage

* recursive CTE
* multi-stage aggregation

---
</details>

---

<details>
<summary>Important FAAG Level Question</summary>

Below are **50 important FAANG-style SQL interview questions with answers** based on the **Banking Customer Deposits & Loan Management System**.

These mimic the style used in companies like **NVIDIA, Amazon, Uber, Meta, Google**, focusing on:

* ranking problems
* pagination (row ranges like 10–20, 45–55)
* revenue/amount aggregation
* time-series analysis
* fraud detection
* running totals
* cohort-like customer analysis

---

# Schema Used

```sql
Customers(customer_id, first_name, last_name, email, city, created_at)

Accounts(account_id, customer_id, account_type, balance, opened_date)

Loans(loan_id, customer_id, loan_amount, interest_rate, loan_type, issued_date)

Transactions(transaction_id, account_id, transaction_type, amount, transaction_date)
```

---

# SECTION 1 — Row Position / Pagination Problems (like interviewer asked)

---

## 1 Get the **3rd last transaction**

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER (ORDER BY transaction_date DESC) rn
    FROM Transactions
) t
WHERE rn = 3;
```

---

## 2 Retrieve rows **10–20**

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER (ORDER BY transaction_date) rn
    FROM Transactions
) t
WHERE rn BETWEEN 10 AND 20;
```

---

## 3 Retrieve rows **45–55**

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER (ORDER BY transaction_date) rn
    FROM Transactions
) t
WHERE rn BETWEEN 45 AND 55;
```

---

## 4 Retrieve **last 10 transactions**

```sql
SELECT *
FROM Transactions
ORDER BY transaction_date DESC
LIMIT 10;
```

---

## 5 Retrieve **5th highest transaction**

```sql
SELECT *
FROM (
    SELECT *,
           RANK() OVER (ORDER BY amount DESC) rnk
    FROM Transactions
) t
WHERE rnk = 5;
```

---

# SECTION 2 — Revenue / Amount Aggregation (NVIDIA-style)

---

## 6 Total transaction amount per account

```sql
SELECT account_id,
       SUM(amount) total_amount
FROM Transactions
GROUP BY account_id
ORDER BY total_amount DESC;
```

---

## 7 Total deposits per customer

```sql
SELECT a.customer_id,
       SUM(t.amount) deposits
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
WHERE t.transaction_type = 'Deposit'
GROUP BY a.customer_id;
```

---

## 8 Monthly bank transaction revenue

```sql
SELECT DATE_TRUNC('month', transaction_date) month,
       SUM(amount) revenue
FROM Transactions
GROUP BY month
ORDER BY month;
```

---

## 9 Top 3 customers by deposits

```sql
SELECT *
FROM (
SELECT a.customer_id,
       SUM(t.amount) total_dep,
       ROW_NUMBER() OVER(ORDER BY SUM(t.amount) DESC) rn
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
) t
WHERE rn <= 3;
```

---

## 10 Transaction type generating highest value

```sql
SELECT transaction_type,
       SUM(amount) total
FROM Transactions
GROUP BY transaction_type
ORDER BY total DESC;
```

---

# SECTION 3 — Ranking Problems (Amazon-style)

---

## 11 Top 2 customers per city

```sql
SELECT *
FROM (
SELECT c.city,
       c.customer_id,
       SUM(t.amount) total,
       ROW_NUMBER() OVER(PARTITION BY c.city ORDER BY SUM(t.amount) DESC) rn
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
JOIN Transactions t ON a.account_id = t.account_id
GROUP BY c.city, c.customer_id
) t
WHERE rn <= 2;
```

---

## 12 Rank accounts by balance

```sql
SELECT account_id,
       balance,
       RANK() OVER(ORDER BY balance DESC)
FROM Accounts;
```

---

## 13 Highest transaction per account

```sql
SELECT *
FROM (
SELECT *,
ROW_NUMBER() OVER(PARTITION BY account_id ORDER BY amount DESC) rn
FROM Transactions
) t
WHERE rn = 1;
```

---

## 14 Top loan per loan type

```sql
SELECT *
FROM (
SELECT loan_type,
       loan_id,
       loan_amount,
       ROW_NUMBER() OVER(PARTITION BY loan_type ORDER BY loan_amount DESC) rn
FROM Loans
) t
WHERE rn = 1;
```

---

## 15 Top 10% highest deposits

```sql
SELECT *
FROM (
SELECT a.customer_id,
       SUM(t.amount) total,
       NTILE(10) OVER(ORDER BY SUM(t.amount) DESC) bucket
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
) t
WHERE bucket = 1;
```

---

# SECTION 4 — Running Totals (FAANG classic)

---

## 16 Running transaction total per account

```sql
SELECT account_id,
       transaction_date,
       amount,
       SUM(amount) OVER
       (PARTITION BY account_id ORDER BY transaction_date)
FROM Transactions;
```

---

## 17 Running monthly revenue

```sql
SELECT month,
       SUM(revenue) OVER (ORDER BY month)
FROM (
SELECT DATE_TRUNC('month', transaction_date) month,
       SUM(amount) revenue
FROM Transactions
GROUP BY month
) t;
```

---

## 18 Running deposit total per customer

```sql
SELECT a.customer_id,
       transaction_date,
       SUM(amount) OVER
       (PARTITION BY a.customer_id ORDER BY transaction_date)
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id;
```

---

# SECTION 5 — Time Series (Uber-style)

---

## 19 Days between account opening and first transaction

```sql
SELECT a.account_id,
       MIN(t.transaction_date) - a.opened_date AS days_diff
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.account_id, a.opened_date;
```

---

## 20 Days between first and second transaction

```sql
SELECT account_id,
       transaction_date - prev_date
FROM (
SELECT account_id,
       transaction_date,
       LAG(transaction_date)
       OVER(PARTITION BY account_id ORDER BY transaction_date) prev_date
FROM Transactions
) t;
```

---

## 21 Monthly growth vs previous month

```sql
SELECT month,
       revenue,
       revenue - LAG(revenue) OVER(ORDER BY month)
FROM (
SELECT DATE_TRUNC('month',transaction_date) month,
       SUM(amount) revenue
FROM Transactions
GROUP BY month
) t;
```

---

## 22 Transaction growth percentage

```sql
SELECT month,
       revenue,
       (revenue - LAG(revenue) OVER(ORDER BY month)) *100.0 /
       LAG(revenue) OVER(ORDER BY month)
FROM (
SELECT DATE_TRUNC('month',transaction_date) month,
       SUM(amount) revenue
FROM Transactions
GROUP BY month
) t;
```

---

# SECTION 6 — Fraud Detection

---

## 23 Same amount transactions within 10 minutes

```sql
SELECT *
FROM (
SELECT account_id,
       amount,
       transaction_date,
       LAG(transaction_date)
       OVER(PARTITION BY account_id, amount ORDER BY transaction_date) prev
FROM Transactions
) t
WHERE transaction_date - prev <= INTERVAL '10 minutes';
```

---

## 24 Count repeated payments

```sql
SELECT COUNT(*)
FROM (
SELECT account_id,
       amount,
       transaction_date,
       LAG(transaction_date)
       OVER(PARTITION BY account_id, amount ORDER BY transaction_date) prev
FROM Transactions
) t
WHERE transaction_date - prev <= INTERVAL '10 minutes';
```

---

# SECTION 7 — Customer Analytics

---

## 25 Customers without accounts

```sql
SELECT customer_id
FROM Customers

EXCEPT

SELECT customer_id
FROM Accounts;
```

---

## 26 Customers without transactions

```sql
SELECT customer_id
FROM Accounts

EXCEPT

SELECT DISTINCT a.customer_id
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id;
```

---

## 27 Active customers in last 30 days

```sql
SELECT DISTINCT a.customer_id
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
WHERE transaction_date >= CURRENT_DATE - INTERVAL '30 days';
```

---

## 28 Customers with deposits every month

```sql
SELECT customer_id
FROM (
SELECT a.customer_id,
       COUNT(DISTINCT DATE_TRUNC('month',transaction_date)) m
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
) t
WHERE m = 12;
```

---

# SECTION 8 — First / Last Activity

---

## 29 First transaction per customer

```sql
SELECT *
FROM (
SELECT a.customer_id,
       t.*,
       ROW_NUMBER() OVER
       (PARTITION BY a.customer_id ORDER BY transaction_date) rn
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
) t
WHERE rn = 1;
```

---

## 30 Latest transaction per account

```sql
SELECT *
FROM (
SELECT *,
ROW_NUMBER() OVER(PARTITION BY account_id ORDER BY transaction_date DESC) rn
FROM Transactions
) t
WHERE rn = 1;
```

---

# SECTION 9 — Moving Average

---

## 31 7-day moving average transactions

```sql
SELECT transaction_date,
       AVG(amount) OVER(
       ORDER BY transaction_date
       ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)
FROM Transactions;
```

---

## 32 Moving average deposits per account

```sql
SELECT account_id,
       transaction_date,
       AVG(amount) OVER(
       PARTITION BY account_id
       ORDER BY transaction_date
       ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)
FROM Transactions;
```

---

# SECTION 10 — Percent of Total

---

## 33 Contribution of each account to total bank transactions

```sql
SELECT account_id,
       SUM(amount),
       SUM(amount) *100.0 /
       SUM(SUM(amount)) OVER()
FROM Transactions
GROUP BY account_id;
```

---

## 34 Contribution per customer

```sql
SELECT customer_id,
       total,
       total *100.0 / SUM(total) OVER()
FROM (
SELECT a.customer_id,
       SUM(t.amount) total
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id
) t;
```

---

# SECTION 11 — Advanced Ranking

---

## 35 Dense rank accounts by balance

```sql
SELECT account_id,
       balance,
       DENSE_RANK() OVER(ORDER BY balance DESC)
FROM Accounts;
```

---

## 36 Second highest loan per loan type

```sql
SELECT *
FROM (
SELECT loan_type,
       loan_amount,
       DENSE_RANK() OVER
       (PARTITION BY loan_type ORDER BY loan_amount DESC) r
FROM Loans
) t
WHERE r = 2;
```

---

# SECTION 12 — Gap Analysis

---

## 37 Longest transaction gap per account

```sql
SELECT account_id,
       MAX(transaction_date - prev_date)
FROM (
SELECT account_id,
       transaction_date,
       LAG(transaction_date)
       OVER(PARTITION BY account_id ORDER BY transaction_date) prev_date
FROM Transactions
) t
GROUP BY account_id;
```

---

## 38 Largest gap globally

```sql
SELECT MAX(transaction_date - prev)
FROM (
SELECT transaction_date,
       LAG(transaction_date) OVER(ORDER BY transaction_date) prev
FROM Transactions
) t;
```

---

# SECTION 13 — Business Analysis

---

## 39 Loan to deposit ratio per customer

```sql
SELECT c.customer_id,
       SUM(l.loan_amount) /
       SUM(t.amount)
FROM Customers c
JOIN Loans l ON c.customer_id = l.customer_id
JOIN Accounts a ON c.customer_id = a.customer_id
JOIN Transactions t ON a.account_id = t.account_id
GROUP BY c.customer_id;
```

---

## 40 Accounts with highest withdrawals

```sql
SELECT account_id,
       SUM(amount)
FROM Transactions
WHERE transaction_type='Withdrawal'
GROUP BY account_id
ORDER BY SUM(amount) DESC
LIMIT 5;
```

---

# SECTION 14 — Misc Advanced

---

## 41 Customers sharing same city

```sql
SELECT c1.customer_id,
       c2.customer_id,
       c1.city
FROM Customers c1
JOIN Customers c2
ON c1.city = c2.city
AND c1.customer_id < c2.customer_id;
```

---

## 42 Customers with both loans and accounts

```sql
SELECT customer_id
FROM Loans
INTERSECT
SELECT customer_id
FROM Accounts;
```

---

## 43 Customers with accounts but no loans

```sql
SELECT customer_id
FROM Accounts
EXCEPT
SELECT customer_id
FROM Loans;
```

---

## 44 Find median transaction

```sql
SELECT percentile_cont(0.5)
WITHIN GROUP (ORDER BY amount)
FROM Transactions;
```

---

## 45 Find accounts with more than 50 transactions

```sql
SELECT account_id
FROM Transactions
GROUP BY account_id
HAVING COUNT(*) > 50;
```

---

## 46 Find customer lifetime transaction value

```sql
SELECT a.customer_id,
       SUM(t.amount)
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id;
```

---

## 47 Find accounts opened each year

```sql
SELECT EXTRACT(YEAR FROM opened_date),
       COUNT(*)
FROM Accounts
GROUP BY 1;
```

---

## 48 Find highest transaction day

```sql
SELECT DATE(transaction_date),
       SUM(amount)
FROM Transactions
GROUP BY 1
ORDER BY SUM(amount) DESC
LIMIT 1;
```

---

## 49 Find customers whose deposits increased month-over-month

```sql
SELECT *
FROM (
SELECT a.customer_id,
       DATE_TRUNC('month',transaction_date) m,
       SUM(amount) total,
       LAG(SUM(amount)) OVER
       (PARTITION BY a.customer_id ORDER BY DATE_TRUNC('month',transaction_date)) prev
FROM Accounts a
JOIN Transactions t
ON a.account_id = t.account_id
GROUP BY a.customer_id, m
) t
WHERE total > prev;
```

---

## 50 Find accounts with highest transaction count per city

```sql
SELECT *
FROM (
SELECT c.city,
       a.account_id,
       COUNT(*) txn_count,
       ROW_NUMBER() OVER
       (PARTITION BY c.city ORDER BY COUNT(*) DESC) rn
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
JOIN Transactions t ON a.account_id = t.account_id
GROUP BY c.city, a.account_id
) t
WHERE rn = 1;
```

---

# Why These 50 Questions Are Valuable

They cover **almost every pattern FAANG SQL interviews test**:

| Pattern                | Example Questions |
| ---------------------- | ----------------- |
| Pagination / row index | 1–5               |
| Aggregation            | 6–10              |
| Ranking                | 11–15             |
| Running totals         | 16–18             |
| Time series            | 19–22             |
| Fraud detection        | 23–24             |
| Customer analytics     | 25–28             |
| First / last events    | 29–30             |
| Moving averages        | 31–32             |
| Percent of total       | 33–34             |
| Advanced ranking       | 35–36             |
| Gap analysis           | 37–38             |
| Business metrics       | 39–40             |
| Set operations         | 41–43             |
| Statistical queries    | 44                |

</details>

---