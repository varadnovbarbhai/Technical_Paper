# SQL Cheatsheet

SQL stands for **Structured Query Language**. It is used to communicate with relational databases to create, retrieve, update, delete, and manage data.

Examples throughout this cheatsheet use IPL-style tables such as `players`, `teams`, and `matches`. Most syntax is standard SQL; PostgreSQL-specific commands are marked.

---

## 1. SQL Command Categories

| Category | Full form | Common commands | Purpose |
|---|---|---|---|
| DDL | Data Definition Language | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` | Defines database structures |
| DML | Data Manipulation Language | `INSERT`, `UPDATE`, `DELETE` | Changes data |
| DQL | Data Query Language | `SELECT` | Retrieves data |
| DCL | Data Control Language | `GRANT`, `REVOKE` | Controls permissions |
| TCL | Transaction Control Language | `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT` | Manages transactions |

## 2. Database Operations (PostgreSQL)

```sql
-- Create a database
CREATE DATABASE ipl_database;

-- Create a user
CREATE USER ipl_user WITH PASSWORD 'password123';

-- Assign database ownership
ALTER DATABASE ipl_database OWNER TO ipl_user;

-- Delete a database (connect to a different database first)
DROP DATABASE IF EXISTS ipl_database;

-- Delete a user/role
DROP ROLE IF EXISTS ipl_user;
```

Useful `psql` commands:

```text
\l                 -- List databases
\c ipl_database    -- Connect to a database
\du                -- List users and roles
\q                 -- Quit psql
```

> `CREATE DATABASE` and `DROP DATABASE` cannot run inside a transaction block. You cannot drop the database to which you are currently connected.

## 3. Table Operations (DDL)

### Create a table

```sql
CREATE TABLE players (
    player_id INT PRIMARY KEY,
    player_name VARCHAR(100) NOT NULL,
    team VARCHAR(50),
    runs INT,
    age INT
);
```

### Inspect tables (PostgreSQL `psql`)

```text
\dt             -- List tables
\d players      -- Describe a table
```

### Alter a table

```sql
-- Add a column
ALTER TABLE players ADD COLUMN wickets INT;

-- Rename a column
ALTER TABLE players RENAME COLUMN age TO player_age;

-- Change a column's data type (PostgreSQL)
ALTER TABLE players ALTER COLUMN runs TYPE BIGINT;

-- Rename a table
ALTER TABLE players RENAME TO ipl_players;
```

### Remove a table or its rows

```sql
-- Delete selected or all rows
DELETE FROM players WHERE team = 'RCB';

-- Delete all rows (keeps the table structure)
TRUNCATE TABLE players;

-- Delete the table structure and its data
DROP TABLE players;
```

**Difference:** `DELETE` removes rows (and can use `WHERE`); `TRUNCATE` removes all rows; `DROP` removes the table itself.

## 4. Common Data Types

| Data type | Description | Example |
|---|---|---|
| `SMALLINT` | Small whole number | `25` |
| `INT` / `INTEGER` | Whole number | `100` |
| `BIGINT` | Large whole number | `1000000` |
| `DECIMAL(p,s)` / `NUMERIC(p,s)` | Exact decimal number | `99.95` |
| `REAL` / `DOUBLE PRECISION` | Approximate decimal number | `3.14` |
| `VARCHAR(n)` | Variable-length text, up to n characters | `'Virat'` |
| `CHAR(n)` | Fixed-length text | `'RCB'` |
| `TEXT` | Variable-length text | `'Player details'` |
| `DATE` | Date | `'2026-11-12'` |
| `TIME` | Time | `'18:30:00'` |
| `TIMESTAMP` | Date and time | `'2026-11-12 18:30:00'` |
| `BOOLEAN` | True/false | `TRUE` |

## 5. Insert Data (`INSERT`)

```sql
-- Insert values for every column, in table-column order
INSERT INTO players
VALUES (1, 'Virat Kohli', 'RCB', 8000, 37);

-- Insert into selected columns
INSERT INTO players (player_id, player_name, team)
VALUES (2, 'Rohit Sharma', 'MI');

-- Insert multiple rows
INSERT INTO players (player_id, player_name, team, runs, age)
VALUES
    (3, 'MS Dhoni', 'CSK', 5000, 45),
    (4, 'Hardik Pandya', 'MI', 2500, 32);
```

Prefer specifying column names in `INSERT` statements. It makes the query safer if the table structure changes.

## 6. Retrieve Data (`SELECT`)

```sql
-- All columns and rows
SELECT * FROM players;

-- Specific columns
SELECT player_name, runs
FROM players;

-- Unique team names
SELECT DISTINCT team
FROM players;

-- Return only 5 rows
SELECT *
FROM players
LIMIT 5;

-- Skip 10 rows, then return 5 (PostgreSQL)
SELECT *
FROM players
LIMIT 5 OFFSET 10;
```

## 7. Filter Rows (`WHERE`)

```sql
SELECT *
FROM players
WHERE team = 'RCB';
```

### Comparison operators

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `<>` or `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

### Logical operators

```sql
-- Both conditions must be true
SELECT *
FROM players
WHERE team = 'RCB' AND runs > 5000;

-- At least one condition must be true
SELECT *
FROM players
WHERE team = 'RCB' OR team = 'MI';

-- Negate a condition
SELECT *
FROM players
WHERE NOT team = 'CSK';
```

### Useful filters

```sql
-- Inclusive range
SELECT *
FROM players
WHERE runs BETWEEN 3000 AND 8000;

-- Match any value in a list
SELECT *
FROM players
WHERE team IN ('RCB', 'MI', 'CSK');

-- Pattern matching: names starting with V
SELECT *
FROM players
WHERE player_name LIKE 'V%';

-- Names containing 'koh' (PostgreSQL: case-insensitive)
SELECT *
FROM players
WHERE player_name ILIKE '%koh%';

-- Find missing values
SELECT *
FROM players
WHERE runs IS NULL;

-- Find values that are not missing
SELECT *
FROM players
WHERE runs IS NOT NULL;
```

`LIKE` is generally case-sensitive in PostgreSQL. `ILIKE` is a PostgreSQL extension for case-insensitive matching. `%` means any sequence of characters; `_` means one character.

## 8. Sort Results (`ORDER BY`)

```sql
-- Ascending (default)
SELECT *
FROM players
ORDER BY runs ASC;

-- Descending
SELECT *
FROM players
ORDER BY runs DESC;

-- Sort by multiple columns
SELECT *
FROM players
ORDER BY team ASC, runs DESC;
```

## 9. Aggregate Functions

Aggregate functions calculate a result from multiple rows.

| Function | Purpose |
|---|---|
| `COUNT(*)` | Counts rows |
| `COUNT(column)` | Counts non-NULL values in a column |
| `SUM(column)` | Calculates total |
| `AVG(column)` | Calculates average |
| `MIN(column)` | Finds minimum |
| `MAX(column)` | Finds maximum |

```sql
SELECT COUNT(*) FROM players;
SELECT SUM(runs) FROM players;
SELECT AVG(runs) FROM players;
SELECT MIN(runs) FROM players;
SELECT MAX(runs) FROM players;
```

## 10. Group Rows (`GROUP BY`)

`GROUP BY` puts rows with the same value into groups. It is commonly used with aggregate functions.

```sql
-- Total runs by team
SELECT team, SUM(runs) AS total_runs
FROM players
GROUP BY team;

-- Number of players in each team
SELECT team, COUNT(*) AS player_count
FROM players
GROUP BY team;

-- Average runs by team
SELECT team, AVG(runs) AS average_runs
FROM players
GROUP BY team;
```

Every selected column that is not inside an aggregate function generally needs to be included in `GROUP BY`.

## 11. Filter Groups (`HAVING`)

`HAVING` filters groups after grouping. `WHERE` filters individual rows before grouping.

```sql
SELECT team, COUNT(*) AS player_count
FROM players
GROUP BY team
HAVING COUNT(*) > 3;
```

You can use both:

```sql
SELECT team, SUM(runs) AS total_runs
FROM players
WHERE runs > 100
GROUP BY team
HAVING SUM(runs) > 5000;
```

| `WHERE` | `HAVING` |
|---|---|
| Filters rows | Filters groups |
| Applied before grouping | Applied after grouping |
| Usually does not use aggregate conditions directly | Commonly uses aggregate conditions |

## 12. SQL Joins

Joins combine rows from tables using a related column.

Imagine these tables:

**players**

| player_id | player_name | team_id |
|---:|---|---:|
| 1 | Virat Kohli | 10 |
| 2 | Rohit Sharma | 20 |
| 3 | MS Dhoni | 30 |

**teams**

| team_id | team_name |
|---:|---|
| 10 | RCB |
| 20 | MI |
| 40 | KKR |

### INNER JOIN

Only rows with a match in both tables:

```sql
SELECT p.player_name, t.team_name
FROM players AS p
INNER JOIN teams AS t
    ON p.team_id = t.team_id;
```

### LEFT JOIN (LEFT OUTER JOIN)

All rows from the left table, plus matching rows from the right table. Unmatched right-side columns are `NULL`.

```sql
SELECT p.player_name, t.team_name
FROM players AS p
LEFT JOIN teams AS t
    ON p.team_id = t.team_id;
```

### RIGHT JOIN (RIGHT OUTER JOIN)

All rows from the right table, plus matching rows from the left table.

```sql
SELECT p.player_name, t.team_name
FROM players AS p
RIGHT JOIN teams AS t
    ON p.team_id = t.team_id;
```

### FULL OUTER JOIN

All rows from both tables. Unmatched columns on either side are `NULL`.

```sql
SELECT p.player_name, t.team_name
FROM players AS p
FULL OUTER JOIN teams AS t
    ON p.team_id = t.team_id;
```

### CROSS JOIN

Every possible combination of rows from both tables:

```sql
SELECT *
FROM players
CROSS JOIN teams;
```

| Join | What it returns |
|---|---|
| `INNER JOIN` | Matching rows from both tables |
| `LEFT JOIN` | Every left row and matching right rows |
| `RIGHT JOIN` | Every right row and matching left rows |
| `FULL OUTER JOIN` | Every row from both tables |
| `CROSS JOIN` | Every possible row combination |

## 13. Aliases (`AS`)

Aliases give temporary names to columns or tables.

```sql
-- Column aliases
SELECT player_name AS name, runs AS total_runs
FROM players;

-- Table aliases
SELECT p.player_name, t.team_name
FROM players AS p
JOIN teams AS t
    ON p.team_id = t.team_id;
```

`AS` is optional for aliases in PostgreSQL.

## 14. Subqueries

A subquery is a query nested inside another query.

```sql
-- Players with more runs than the overall average
SELECT player_name, runs
FROM players
WHERE runs > (
    SELECT AVG(runs)
    FROM players
);

-- Player(s) with the highest run total
SELECT player_name, runs
FROM players
WHERE runs = (
    SELECT MAX(runs)
    FROM players
);
```

Subqueries can be used with operators such as `IN`, `EXISTS`, `=`, and comparison operators.

```sql
SELECT player_name
FROM players
WHERE team_id IN (
    SELECT team_id
    FROM teams
);
```

## 15. Common Table Expressions (CTEs)

A CTE is a named temporary result set defined using `WITH`. It exists for the duration of one query.

```sql
WITH team_runs AS (
    SELECT team, SUM(runs) AS total_runs
    FROM players
    GROUP BY team
)
SELECT *
FROM team_runs
WHERE total_runs > 5000;
```

CTEs can make complex queries easier to read and maintain.

## 16. Conditional Logic (`CASE`)

`CASE` works like `if / elif / else` in Python.

```sql
SELECT
    player_name,
    runs,
    CASE
        WHEN runs >= 7000 THEN 'Excellent'
        WHEN runs >= 4000 THEN 'Good'
        ELSE 'Average'
    END AS performance
FROM players;
```

## 17. String Functions

| Function | Purpose |
|---|---|
| `UPPER(text)` | Converts text to uppercase |
| `LOWER(text)` | Converts text to lowercase |
| `LENGTH(text)` | Returns string length |
| `TRIM(text)` | Removes leading/trailing spaces |
| `CONCAT(a, b)` | Joins strings |
| `SUBSTRING(text FROM start FOR count)` | Extracts part of a string |
| `REPLACE(text, old, new)` | Replaces text |

```sql
SELECT UPPER(player_name) FROM players;
SELECT LOWER(player_name) FROM players;
SELECT LENGTH(player_name) FROM players;
SELECT TRIM(player_name) FROM players;
SELECT CONCAT(player_name, ' - ', team) FROM players;
SELECT SUBSTRING(player_name FROM 1 FOR 5) FROM players;
SELECT REPLACE(team, 'RCB', 'Bangalore') FROM players;
```

## 18. Numeric Functions

| Function | Purpose |
|---|---|
| `ROUND(number, decimals)` | Rounds a number |
| `CEIL(number)` | Rounds upward |
| `FLOOR(number)` | Rounds downward |
| `ABS(number)` | Returns absolute value |
| `MOD(a, b)` | Returns remainder |
| `POWER(a, b)` | Calculates a to the power of b |

```sql
SELECT ROUND(12.567, 2);
SELECT CEIL(12.3);
SELECT FLOOR(12.9);
SELECT ABS(-25);
SELECT MOD(10, 3);
SELECT POWER(2, 3);
```

## 19. Date and Time Functions (PostgreSQL)

```sql
SELECT CURRENT_DATE;
SELECT CURRENT_TIME;
SELECT CURRENT_TIMESTAMP;

-- Extract year or month
SELECT EXTRACT(YEAR FROM CURRENT_DATE);
SELECT EXTRACT(MONTH FROM CURRENT_DATE);

-- Add an interval
SELECT CURRENT_DATE + INTERVAL '5 days';

-- Difference between two dates (returns number of days)
SELECT DATE '2026-11-12' - DATE '2026-11-01';
```

## 20. Constraints

Constraints enforce rules on table data.

| Constraint | Purpose |
|---|---|
| `PRIMARY KEY` | Uniquely identifies each row; cannot be NULL |
| `FOREIGN KEY` | Enforces a relationship with another table |
| `UNIQUE` | Prevents duplicate values |
| `NOT NULL` | Requires a value |
| `CHECK` | Requires a condition to be true |
| `DEFAULT` | Supplies a value when one is not provided |

```sql
CREATE TABLE teams (
    team_id INT PRIMARY KEY,
    team_name VARCHAR(50) NOT NULL UNIQUE
);

CREATE TABLE players (
    player_id INT PRIMARY KEY,
    player_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18),
    team_id INT REFERENCES teams(team_id),
    status VARCHAR(20) DEFAULT 'active'
);
```

## 21. Set Operations

Set operations combine the results of two `SELECT` queries. The queries must return the same number of columns with compatible data types.

### UNION

Combines results and removes duplicate rows:

```sql
SELECT player_name AS name FROM players
UNION
SELECT team_name AS name FROM teams;
```

### UNION ALL

Combines results and keeps duplicates:

```sql
SELECT player_name AS name FROM players
UNION ALL
SELECT team_name AS name FROM teams;
```

### INTERSECT

Returns rows common to both results:

```sql
SELECT player_name FROM players
INTERSECT
SELECT player_name FROM retired_players;
```

### EXCEPT

Returns rows from the first result that do not appear in the second:

```sql
SELECT player_name FROM players
EXCEPT
SELECT player_name FROM retired_players;
```

## 22. Window Functions

Window functions calculate values across related rows without collapsing those rows into one result per group (unlike `GROUP BY`).

### ROW_NUMBER

Assigns a unique sequential number:

```sql
SELECT
    player_name,
    runs,
    ROW_NUMBER() OVER (ORDER BY runs DESC) AS row_num
FROM players;
```

### RANK

Tied rows share a rank, and the next rank is skipped:

```sql
SELECT
    player_name,
    runs,
    RANK() OVER (ORDER BY runs DESC) AS player_rank
FROM players;
```

### DENSE_RANK

Tied rows share a rank, but the next rank is not skipped:

```sql
SELECT
    player_name,
    runs,
    DENSE_RANK() OVER (ORDER BY runs DESC) AS player_rank
FROM players;
```

### PARTITION BY

Divides rows into groups for the window calculation:

```sql
SELECT
    player_name,
    team,
    runs,
    RANK() OVER (
        PARTITION BY team
        ORDER BY runs DESC
    ) AS team_rank
FROM players;
```

Other useful window functions include `LAG()`, `LEAD()`, `FIRST_VALUE()`, `LAST_VALUE()`, and aggregate functions used with `OVER()`.

## 23. Views

A view is a saved query that can be queried like a virtual table.

```sql
-- Create a view
CREATE VIEW top_players AS
SELECT player_name, runs
FROM players
WHERE runs > 5000;

-- Query the view
SELECT * FROM top_players;

-- Delete the view
DROP VIEW top_players;
```

## 24. Indexes

Indexes can speed up data retrieval, especially for columns used frequently in filters and joins. They use extra storage and can add overhead to data changes.

```sql
-- Create an index
CREATE INDEX idx_player_name
ON players(player_name);

-- Create a unique index
CREATE UNIQUE INDEX idx_player_email
ON players(email);

-- Drop an index (PostgreSQL)
DROP INDEX idx_player_name;
```

## 25. Transactions (TCL)

A transaction groups operations into one logical unit.

```sql
BEGIN;

UPDATE players
SET runs = 8500
WHERE player_id = 1;

SAVEPOINT after_first_update;

UPDATE players
SET runs = 7000
WHERE player_id = 2;

-- Undo changes made after the savepoint
ROLLBACK TO SAVEPOINT after_first_update;

-- Save the remaining transaction changes
COMMIT;
```

```sql
BEGIN;
DELETE FROM players WHERE player_id = 5;
ROLLBACK;  -- Undo the uncommitted delete
```

| Command | Purpose |
|---|---|
| `BEGIN` | Starts a transaction |
| `COMMIT` | Saves transaction changes |
| `ROLLBACK` | Undoes uncommitted changes |
| `SAVEPOINT` | Creates a point to roll back to |

## 26. CRUD Operations Summary

CRUD means Create, Read, Update, and Delete.

```sql
-- CREATE: add a row
INSERT INTO players (player_id, player_name, team, runs, age)
VALUES (5, 'Ravindra Jadeja', 'CSK', 3000, 37);

-- READ: retrieve rows
SELECT * FROM players;

-- UPDATE: change a row
UPDATE players
SET runs = 3500
WHERE player_id = 5;

-- DELETE: remove a row
DELETE FROM players
WHERE player_id = 5;
```

Always use a suitable `WHERE` condition with `UPDATE` and `DELETE` when you intend to affect only particular rows. Without `WHERE`, every row is affected.

## 27. Import CSV Data in PostgreSQL

First, create a table whose columns and data types match the CSV file.

```sql
CREATE TABLE matches (
    id INT,
    season INT,
    city VARCHAR(100),
    match_date DATE,
    winner VARCHAR(100)
);
```

### Using `COPY`

`COPY` reads a file from the PostgreSQL server's filesystem:

```sql
COPY matches
FROM '/absolute/path/to/matches.csv'
WITH (FORMAT CSV, HEADER TRUE);
```

### Using `\copy` in `psql`

`\copy` reads a file from the machine running the `psql` client:

```text
\copy matches FROM '/absolute/path/to/matches.csv' WITH (FORMAT CSV, HEADER TRUE)
```

For local project work, `\copy` is often easier because it uses your local file permissions. The CSV column order and types must match the target table.

## 28. SQL Query Logical Execution Order

SQL is written in one order, but its logical processing order is different.

Example:

```sql
SELECT team, SUM(runs) AS total_runs
FROM players
WHERE runs > 100
GROUP BY team
HAVING SUM(runs) > 5000
ORDER BY total_runs DESC
LIMIT 5;
```

A simplified logical order is:

| Order | Clause | Purpose |
|---:|---|---|
| 1 | `FROM` | Choose source tables |
| 2 | `JOIN` / `ON` | Combine matching rows |
| 3 | `WHERE` | Filter rows |
| 4 | `GROUP BY` | Form groups |
| 5 | `HAVING` | Filter groups |
| 6 | `SELECT` | Calculate/select output columns |
| 7 | `DISTINCT` | Remove duplicate output rows |
| 8 | `ORDER BY` | Sort output |
| 9 | `LIMIT` / `OFFSET` | Restrict output rows |

This is a simplified logical order; database engines may physically optimize execution differently.

