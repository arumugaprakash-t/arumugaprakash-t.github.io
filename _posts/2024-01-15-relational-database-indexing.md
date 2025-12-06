---
layout: post
title: "Relational Database Indexing"
date: 2024-01-15
categories: [databases, tech]
tags: [database, indexing, performance, sql]
description: "An introduction to database indexing and how it enhances query performance"
---

Indexing is a popular term used in the database domain. In this article, we will explore what an index is and the problems it aims to solve.

**An index is a data structure that enhances the query performance of a database.**

To understand how an index improves query performance, let's consider an example.

```sql
CREATE TABLE players(name varchar(25), age int, team varchar(21));
```

We have a table called `players` with three columns: `name` (varchar, 25 bytes), `age` (int, 4 bytes), and `team` (varchar, 21 bytes). For simplicity, we'll assume that each row occupies 50 bytes in disk memory.

In the file system or storage device, data is read and written in blocks.

**A block is the fundamental unit of data storage.**

Let's assume a default block size of 500 bytes, allowing us to store 10 rows per block. With 100 rows in the players table, we would require 10 blocks to store the data.

To iterate through the entire table, we would need to read all 10 blocks. For example, if we wanted to query the table and find players whose age is 34 using the following SQL statement:

```sql
SELECT * FROM players WHERE age = 34;
```

Assuming each block read takes 1 second, this query would take 10 seconds to traverse the entire table.

## Creating an Index

Now, let's create an index on the age column using the statement:

```sql
CREATE INDEX idx_age ON players(age);
```

The index creates a sorted data structure (B-Tree) that maps each unique age value to the corresponding rows in the table.

This structure allows the database to quickly locate the rows that match a specific age value without scanning the entire table.

When executing a query with a condition on the indexed column, such as `SELECT * FROM players WHERE age = 34`, the database can utilise the index to directly access the specific index entries corresponding to the age value.

This significantly reduces the number of disk accesses required, as it no longer needs to scan all 10 blocks of the table.

## Handling Duplicate Values

As you might notice, there can be duplicate values in the index. Database systems may use slightly different strategies for handling duplicate values in indexes. For example, PostgreSQL uses the insertion order as the tiebreaker for duplicate values. When two rows have the same indexed value, the database will maintain the order in which those rows were inserted into the table.

**Indexes store only the indexed column values and pointers to the corresponding rows, rather than storing the entire row data.**

As a result, when accessing the index, the database needs to read fewer data blocks, further improving query performance.

## Trade-offs

However, indexing also comes with some costs. When data is inserted, updated, or deleted in a table with indexes, the corresponding indexes need to be updated to reflect the changes.

This additional maintenance work introduces overhead in terms of write operations, might slightly slowing down write operations due to the need to update both the table and its associated indexes.

Overall, database indexing provides significant benefits in terms of query performance improvement, but it's important to consider the trade-offs and potential write overhead associated with maintaining indexes.

## What's Next?

You've now grasped the fundamentals of database indexing and how it can significantly enhance query performance. But there's so much more to explore!

In our upcoming blog posts, we'll take a deep dive into two popular indexing techniques: B-tree and hash indexing.
