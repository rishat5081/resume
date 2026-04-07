# 11. SQL DATABASES (PostgreSQL, MySQL)

## 11.1 Core SQL Concepts

### Data Types (PostgreSQL)
**What:** The built-in column types PostgreSQL offers for storing numbers, strings, dates, JSON, arrays, and UUIDs.
**Why:** Choosing the right data type affects storage efficiency, query performance, and validation — interviewers test this to gauge your schema design skills.

```sql
-- Numbers
INTEGER, BIGINT, DECIMAL(10,2), FLOAT, SERIAL (auto-increment)

-- Strings
VARCHAR(255), TEXT, CHAR(10)

-- Date/Time
DATE, TIMESTAMP, TIMESTAMPTZ, INTERVAL

-- Boolean
BOOLEAN

-- JSON (PostgreSQL special)
JSON, JSONB (binary, indexable, faster queries)

-- Arrays (PostgreSQL special)
INTEGER[], TEXT[]

-- UUID
UUID
```

### CRUD Operations
**What:** The four fundamental SQL statements — INSERT, SELECT, UPDATE, DELETE — used to create, read, update, and delete data.
**Why:** CRUD is the backbone of every database interaction, and interviewers expect you to write these queries fluently with proper clauses.

```sql
-- Create
INSERT INTO users (name, email, age) VALUES ('Saad', 'saad@email.com', 28);

-- Read
SELECT * FROM users WHERE age > 25 ORDER BY name ASC LIMIT 10 OFFSET 0;

-- Update
UPDATE users SET name = 'Saad Sohail' WHERE id = 1;

-- Delete
DELETE FROM users WHERE id = 1;
```

### JOINs (Critical Interview Topic)
**What:** SQL operations that combine rows from two or more tables based on a related column between them.
**Why:** JOINs are fundamental to relational databases — every SQL interview will test your ability to write and optimize them.

```sql
-- INNER JOIN — only matching rows from both tables
SELECT u.name, p.title
FROM users u
INNER JOIN posts p ON u.id = p.user_id;

-- LEFT JOIN — all rows from left table + matching from right
SELECT u.name, p.title
FROM users u
LEFT JOIN posts p ON u.id = p.user_id;
-- Users without posts will show with NULL for title

-- RIGHT JOIN — all rows from right table + matching from left
SELECT u.name, p.title
FROM users u
RIGHT JOIN posts p ON u.id = p.user_id;

-- FULL OUTER JOIN — all rows from both tables
SELECT u.name, p.title
FROM users u
FULL OUTER JOIN posts p ON u.id = p.user_id;
```

```
INNER JOIN:     LEFT JOIN:      RIGHT JOIN:     FULL OUTER JOIN:
  ┌───┐           ┌───┐           ┌───┐           ┌───┐
  │ A │∩│ B │     █ A █∩│ B │     │ A │∩█ B █     █ A █∩█ B █
  └───┘           └───┘           └───┘           └───┘
Only matching   All A +          All B +         All from
rows            matching B       matching A      both tables
```

### Indexes
**What:** Data structures (typically B-Trees) that speed up data retrieval by allowing the database to find rows without scanning entire tables.
**Why:** Index design is a top interview topic because it directly impacts query performance — knowing when and how to index separates junior from senior engineers.

```sql
-- B-Tree index (default, most common)
CREATE INDEX idx_users_email ON users(email);

-- Unique index
CREATE UNIQUE INDEX idx_users_email ON users(email);

-- Composite index
CREATE INDEX idx_users_name_age ON users(name, age);
-- Follows "leftmost prefix" rule: this index works for
-- queries on (name), (name, age), but NOT (age) alone

-- Partial index (PostgreSQL)
CREATE INDEX idx_active_users ON users(email) WHERE active = true;

-- GIN index (for JSONB, arrays, full-text search)
CREATE INDEX idx_user_data ON users USING GIN(metadata);
```

**Interview Q: When NOT to add indexes?**
- Small tables (< 1000 rows)
- Columns with low cardinality (boolean, status with 2-3 values)
- Tables with heavy write operations (indexes slow down INSERT/UPDATE)
- Columns rarely used in WHERE/JOIN/ORDER BY

### Transactions & ACID
**What:** A transaction groups multiple SQL operations into a single atomic unit that either fully succeeds or fully rolls back, governed by ACID properties.
**Why:** Interviewers use transactions to test your understanding of data integrity and how to prevent partial updates or race conditions in production systems.

```sql
BEGIN;

UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;

-- If anything fails between BEGIN and COMMIT, nothing is saved
COMMIT;  -- or ROLLBACK; to undo
```

**ACID Properties:**
- **Atomicity** — All or nothing. Either all operations succeed or none do.
- **Consistency** — Database moves from one valid state to another.
- **Isolation** — Concurrent transactions don't interfere with each other.
- **Durability** — Once committed, data survives crashes.

### Aggregate Functions
**What:** SQL functions like COUNT, AVG, SUM, MIN, and MAX that compute a single result from a set of rows, often used with GROUP BY.
**Why:** Aggregate queries are extremely common in interview coding rounds — they test your ability to summarize and analyze data in a single statement.

```sql
SELECT
  department,
  COUNT(*) as total,
  AVG(salary) as avg_salary,
  MAX(salary) as max_salary,
  MIN(salary) as min_salary,
  SUM(salary) as total_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC;
```

### Subqueries vs JOINs
**What:** Two approaches to combining data — subqueries nest a SELECT inside another query, while JOINs merge tables directly.
**Why:** Interviewers ask you to compare these to test whether you understand query execution plans and can choose the more performant approach.

```sql
-- Subquery (slower for large datasets)
SELECT * FROM users
WHERE id IN (SELECT user_id FROM orders WHERE total > 1000);

-- JOIN equivalent (usually faster)
SELECT DISTINCT u.*
FROM users u
INNER JOIN orders o ON u.id = o.user_id
WHERE o.total > 1000;
```

### Window Functions (Advanced)
**What:** Functions like ROW_NUMBER, RANK, and SUM OVER that perform calculations across a set of rows related to the current row without collapsing them.
**Why:** Window functions are a senior-level interview topic that shows you can solve ranking, running totals, and partitioned analytics without subqueries.

```sql
-- ROW_NUMBER, RANK, DENSE_RANK
SELECT
  name,
  department,
  salary,
  ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees;

-- Running total
SELECT
  date,
  amount,
  SUM(amount) OVER (ORDER BY date) as running_total
FROM transactions;
```

### Normalization
**What:** The process of organizing database tables to reduce data redundancy and improve integrity through normal forms (1NF, 2NF, 3NF).
**Why:** Normalization questions test your ability to design clean schemas — interviewers want to see you balance data integrity with query performance.

| Form | Rule | Example |
|------|------|---------|
| **1NF** | No repeating groups, atomic values | Split "skills: JS, Python" into separate rows |
| **2NF** | 1NF + no partial dependencies | Remove columns that depend on part of composite key |
| **3NF** | 2NF + no transitive dependencies | If A→B and B→C, don't store C in same table |

