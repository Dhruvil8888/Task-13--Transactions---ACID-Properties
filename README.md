# Task 13: Transactions & ACID Properties

## 📌 Project Overview
This task demonstrates how **SQL transactions** ensure data safety and consistency.  
It explains **ACID properties** and shows how databases handle failures, rollbacks, and concurrent updates — critical for systems like banking and payments.

---

## 🛠 Tools & Technologies
- **Primary:** MySQL Workbench  
- **Alternatives:** PostgreSQL, BigQuery Sandbox, SQLite  

---

## 📂 Repository Structure
- `task13_transactions_acid.sql` → SQL script demonstrating transactions  
- `README.md` → Documentation (this file)

---

## 🎯 Learning Objectives
- Execute multi-statement transactions
- Use `START TRANSACTION`, `COMMIT`, `ROLLBACK`
- Handle failure scenarios safely
- Understand ACID properties
- Analyze transaction isolation levels
- Prevent dirty reads
- Map transactions to real-world systems

---

## 🗄 Table Used
### `bank_accounts`

| Column | Description |
|------|------------|
| account_id | Unique account |
| account_holder | Account owner |
| balance | Account balance |

---

## 🧪 SQL Code Examples

### Create Table
```sql
CREATE TABLE bank_accounts (
    account_id INT AUTO_INCREMENT PRIMARY KEY,
    account_holder VARCHAR(50),
    balance DECIMAL(10,2) CHECK (balance >= 0)
);
Successful Transaction (COMMIT)
START TRANSACTION;

UPDATE bank_accounts
SET balance = balance - 10000
WHERE account_holder = 'Alice';

UPDATE bank_accounts
SET balance = balance + 10000
WHERE account_holder = 'Bob';

COMMIT;
Failed Transaction (ROLLBACK)
START TRANSACTION;

UPDATE bank_accounts
SET balance = balance - 20000
WHERE account_holder = 'Alice';

UPDATE bank_accounts
SET balance = balance + 20000
WHERE account_holder = 'Charlie';

ROLLBACK;
🔐 ACID Properties Explained
Property	Meaning
Atomicity	All operations succeed or none
Consistency	Data remains valid
Isolation	Transactions don’t interfere
Durability	Committed data is permanent
🔄 Transaction Isolation Levels
Level	Prevents
READ UNCOMMITTED	Nothing
READ COMMITTED	Dirty reads
REPEATABLE READ	Non-repeatable reads
SERIALIZABLE	Phantom reads
🌍 Real-World Mapping
System	Why Transactions Matter
Banking	Money transfers
E-commerce	Order payments
Payroll	Salary processing
Stock trading	Buy/sell execution
