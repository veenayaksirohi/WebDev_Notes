---
tags:
  - sql
  - index
  - table-of-contents
aliases:
  - SQL Notes Index
  - SQL TOC
date: 2025-12-25
---

# 🗄️ SQL Notes — Table of Contents

A comprehensive guide to SQL fundamentals and advanced topics for interview preparation and practical application.

---

## 📚 Course Structure

### [[SQL Basics & Fundamentals|1. SQL Basics & Fundamentals]]

- **Overview**: Introduction to SQL, relational databases, and DBMS
- **Syntax structure**: Statements, clauses, semicolons, case insensitivity
- **Data types**: INT, VARCHAR, DATE, BOOLEAN, DECIMAL
- **Operators**: Arithmetic, comparison, logical, LIKE, IN, BETWEEN
- **Interactivity**: SELECT basics, querying single tables

### [[Data Definition Language (DDL)|2. Data Definition Language (DDL)]]

- **CREATE DATABASE/TABLE**: Defining schemas and structures
- **ALTER TABLE**: Adding/modifying/dropping columns
- **DROP/RENAME**: Removing or renaming objects
- **Constraints**: NOT NULL, DEFAULT, CHECK

### [[Data Manipulation Language (DML)|3. Data Manipulation Language (DML)]]

- **INSERT**: Adding single/multiple rows
- **UPDATE**: Modifying existing data
- **DELETE**: Removing rows
- **MERGE/UPSERT**: Insert-or-update operations

### [[4. Querying with SELECT|4. Querying with SELECT]]

- **Basic SELECT**: Columns, aliases (AS), DISTINCT
- **Filtering**: WHERE clause, conditions, operators
- **Sorting**: ORDER BY ASC/DESC
- **Limiting**: LIMIT, OFFSET, TOP

### [[5. Keys & Constraints|5. Keys & Constraints]]

- **Primary Key**: UNIQUE + NOT NULL identification
- **Foreign Key**: Referential integrity between tables
- **Unique Key**: No duplicates (allows NULLs)
- **Candidate/Super/Alternate Keys**: Theoretical foundations
- **Composite Keys**: Multi-column uniqueness

### [[6. Joins & Relationships|6. Joins & Relationships]]

- **INNER JOIN**: Matching rows between tables
- **LEFT/RIGHT JOIN**: Including non-matches
- **FULL OUTER JOIN**: All rows from both
- **Self Joins**: Relating table to itself
- **Cross Join**: Cartesian product

### [[7. Aggregate Functions & GROUP BY|7. Aggregate Functions & GROUP BY]]

- **Aggregates**: COUNT, SUM, AVG, MIN, MAX
- **GROUP BY**: Grouping for aggregates
- **HAVING**: Filtering groups
- **Window functions**: ROW_NUMBER, RANK, PARTITION BY

### [[8. Subqueries & Set Operations|8. Subqueries & Set Operations]]

- **Scalar subqueries**: Single value returns
- **Correlated subqueries**: Nested dependencies
- **EXISTS/NOT EXISTS**: Checking existence
- **UNION/INTERSECT/EXCEPT**: Combining result sets

### [[9. Advanced Querying|9. Advanced Querying]]

- **Common Table Expressions (CTE)**: WITH clause
- **Recursive CTEs**: Hierarchical data
- **Pivoting/Unpivoting**: Row-column transformations
- **Indexes**: Performance optimization
- **Views**: Virtual tables

### [[10. Transactions & Advanced Topics|10. Transactions & Advanced Topics]]

- **ACID properties**: Atomicity, Consistency, Isolation, Durability
- **Transaction control**: BEGIN, COMMIT, ROLLBACK
- **Locks & Isolation Levels**: READ UNCOMMITTED to SERIALIZABLE
- **Stored Procedures/Functions**: Reusable code
- **Triggers**: Automatic actions on events

---

## 🔗 External Resources

- [SQL Practice Online](https://www.sql-practice.com/)
- [LeetCode SQL Problems](https://leetcode.com/problemset/database/)
- [HackerRank SQL](https://www.hackerrank.com/domains/sql)
