# SQL, OOPs and DBMS Questions & Answers

## 1. Anoop Vantagodi: List the different joins in SQL

There are several types of SQL joins:

1.  **INNER JOIN:** Returns only rows with matching values in both
    tables.
2.  **LEFT JOIN (LEFT OUTER JOIN):** Returns every row from the left
    table and matching rows from the right table. Unmatched right-side
    columns contain `NULL`.
3.  **RIGHT JOIN (RIGHT OUTER JOIN):** Returns every row from the right
    table and matching rows from the left table. Unmatched left-side
    columns contain `NULL`.
4.  **FULL OUTER JOIN:** Returns matching rows and non-matching rows
    from both tables. Missing values are represented by `NULL`.
5.  **CROSS JOIN:** Returns the Cartesian product of the two tables
    (every row from the first table paired with every row from the
    second table).
6.  **SELF JOIN:** Joins a table to itself. It is useful for comparing
    rows within the same table.

Example:

``` sql
SELECT *
FROM students
INNER JOIN marks
    ON students.id = marks.student_id;
```

## 2. Khushi Rani: Why do we use the ALTER command?

`ALTER` is a DDL (Data Definition Language) command used to change the
structure of an existing database object, such as a table.

Examples:

``` sql
-- Add a column
ALTER TABLE students
ADD COLUMN age INT;

-- Change a column's data type (PostgreSQL)
ALTER TABLE students
ALTER COLUMN age TYPE VARCHAR(10);

-- Rename a column
ALTER TABLE students
RENAME COLUMN age TO student_age;

-- Drop a column
ALTER TABLE students
DROP COLUMN student_age;
```

## 3. Kummari Amaresh: What is method overriding?

Method overriding happens when a child class provides its own
implementation of a method that is already defined in its parent class.

Example:

``` python
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


dog = Dog()
dog.sound()
```

Output:

``` text
Dog barks
```

Method overriding supports runtime polymorphism: the method
implementation that runs depends on the object's actual class.

## 4. Kuppireddy Sivashankara Reddy: What is the difference between UNION and JOIN in SQL?

  -----------------------------------------------------------------------
  UNION                               JOIN
  ----------------------------------- -----------------------------------
  Combines the result rows of two or  Combines columns from related rows
  more `SELECT` queries.              in two or more tables.

  Queries must return the same number Tables are commonly related using a
  of columns, with compatible data    join condition.
  types in corresponding positions.   

  Removes duplicate rows by default.  Does not automatically remove
                                      duplicate rows.

  Stacks results vertically.          Combines data horizontally.
  -----------------------------------------------------------------------

Example of `UNION`:

``` sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```

Example of `JOIN`:

``` sql
SELECT students.name, marks.score
FROM students
INNER JOIN marks
    ON students.id = marks.student_id;
```

## 5. Manish Nalumachu: What is the difference between FULL OUTER JOIN and UNION ALL?

  -----------------------------------------------------------------------
  FULL OUTER JOIN                     UNION ALL
  ----------------------------------- -----------------------------------
  Combines columns from two tables    Combines rows from two query
  based on a join condition.          results.

  Includes matching and non-matching  Includes every row returned by each
  rows from both sides.               query, including duplicates.

  Unmatched columns from the other    Does not automatically add `NULL`
  table are filled with `NULL`.       values; each query determines its
                                      output columns.

  Matches rows using an `ON` or       Requires the queries to return the
  `USING` condition.                  same number of columns with
                                      compatible data types.
  -----------------------------------------------------------------------

Example of `FULL OUTER JOIN`:

``` sql
SELECT *
FROM students
FULL OUTER JOIN marks
    ON students.id = marks.student_id;
```

Example of `UNION ALL`:

``` sql
SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```

## 6. Masarpu Jyothish: What is the CAP theorem?

CAP theorem describes three properties of distributed data systems:

1.  **Consistency:** Every read receives the latest successful write or
    an error.
2.  **Availability:** Every request to a functioning node receives a
    response, even if that response might not contain the latest data.
3.  **Partition Tolerance:** The system continues operating despite
    communication failures between nodes in the network.

The key idea is that when a network partition occurs, a distributed
system cannot guarantee both consistency and availability at the same
time. It must make a trade-off between them.

## 7. Mohd Saad Shaikh: What is the command to read or execute an SQL file?

There are two common ways in PostgreSQL.

**Inside the `psql` terminal:**

``` sql
\i filename.sql
```

`\i` means include and execute the SQL file.

**From the Linux terminal:**

``` bash
psql -U username -d database_name -f filename.sql
```

Example using localhost:

``` bash
psql -h localhost -U varad -d ipl_db -f create_table.sql
```

Here: - `-h` specifies the host. - `-U` specifies the PostgreSQL user. -
`-d` specifies the database. - `-f` specifies the SQL file to execute.

## 8. Moyya Naveen: What is the use of atomicity in a transaction?

Atomicity is one of the four ACID properties of a database transaction.

It means **all operations in a transaction succeed together, or none of
them are applied**.

Example: transferring money between two bank accounts.

``` sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

If an error occurs before the transaction is committed, it can be rolled
back:

``` sql
ROLLBACK;
```

This prevents a partial transfer, such as money being deducted from one
account but not credited to the other.

## 9. Mudrakola Sai Pavan: What is the full form of OOPs?

OOPs commonly stands for **Object-Oriented Programming** (also expanded
as Object-Oriented Programming System).

It is a programming approach that organizes code around classes and
objects.

The four main pillars are:

1.  Encapsulation
2.  Inheritance
3.  Polymorphism
4.  Abstraction

## 10. Neha Sunil Magadum: How do we create a table in SQL?

Use the `CREATE TABLE` statement.

Example:

``` sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    city VARCHAR(50)
);
```

This creates a table named `students` with four columns. `id` is the
primary key.

## 11. Palepu Veerababu: What is a transaction in SQL?

A transaction is a group of SQL operations treated as one logical unit
of work.

A transaction is commonly started with `BEGIN` and completed with either
`COMMIT` or `ROLLBACK`.

Example:

``` sql
BEGIN;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

COMMIT;
```

Important transaction commands:

-   `BEGIN` (or `START TRANSACTION`): Starts a transaction.
-   `COMMIT`: Saves the transaction's changes.
-   `ROLLBACK`: Reverts uncommitted changes.
-   `SAVEPOINT`: Creates a point within a transaction to which you can
    roll back.

## 12. Parameswaran R: Can we use aggregate functions with the WHERE clause?

Aggregate functions such as `SUM()`, `AVG()`, `COUNT()`, `MIN()` and
`MAX()` generally cannot be used directly in the `WHERE` clause.

`WHERE` filters individual rows before grouping and aggregation. Use
`HAVING` to filter groups based on aggregate results.

Example:

``` sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 30000;
```

You can use `WHERE` to filter rows before aggregation:

``` sql
SELECT department, AVG(salary)
FROM employees
WHERE city = 'Pune'
GROUP BY department;
```

## 13. Pavan Kumar: How do we list all databases in PostgreSQL?

Inside the `psql` terminal, use:

``` sql
\l
```

or:

``` sql
\list
```

You can also use a SQL query:

``` sql
SELECT datname
FROM pg_database;
```

## 14. Raghu B S: What is the command to update a table in SQL?

Use the `UPDATE` statement to modify existing rows.

Example:

``` sql
UPDATE students
SET age = 25
WHERE id = 1;
```

This updates the age of the student whose ID is `1`.

**Important:** If you omit the `WHERE` clause, every row in the table
will be updated.

## 15. Shakthivel: Can we use aggregate functions without GROUP BY?

**Yes.** An aggregate function can be used without `GROUP BY`. In that
case, it generally calculates one result over all rows selected by the
query.

Examples:

``` sql
SELECT COUNT(*)
FROM students;
```

``` sql
SELECT AVG(salary)
FROM employees;
```

Each query returns a single aggregate result (assuming no grouping).

## 16. Sunkara Prasanth: How do we list tables in PostgreSQL?

Inside the `psql` terminal, use:

``` sql
\dt
```

To list tables across schemas:

``` sql
\dt *.*
```

