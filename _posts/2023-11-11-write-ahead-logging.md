---
layout: post
title: "WAL — Write Ahead Logging"
date: 2023-11-11
categories: [databases, tech]
tags: [database, wal, logging, durability, acid]
description: "Understanding Write-Ahead Logging (WAL) and how it ensures data consistency and durability in database systems"
---

Write-Ahead Logging (WAL) is a crucial concept in database management that ensures data durability and helps maintain the integrity of your database, even in the face of unexpected crashes or failures. In this post, we'll explore what WAL is, why it's essential, and how it works.

## What is Write-Ahead Logging (WAL)?

WAL, as the name suggests, involves logging changes before they are committed to the database. Rather than immediately making changes to the database when a query is executed, WAL records the intended changes first.

## Why it is needed?

Imagine you're executing a query to update something in a database, but just before the change is committed, your system crashes. Without WAL, you risk having inconsistent data. Here's how WAL provides a solution:

**Data Consistency:** WAL maintains a log file that records all changes made to the database, ensuring that even if a crash occurs mid-transaction, the database can be restored to a consistent state by replaying the logged changes.

**Persistence:** The WAL file is stored in a non-volatile environment, such as a hard disk or SSD, which means the data is retained even if the database crashes and in-memory data is lost.

**Mitigating File System Caches:** To address potential data loss due to file system caches, the `fsync` system call is employed, forcing the file system to write changes directly to the disk, bypassing caching.

So where does this WAL file is stored? Can we read it to see what queries are stored? Well technically we can, this file is stored in binary format. In PostgreSQL we can view this with the help of `pg_waldump`.

## How it works?

So let's assume your database crashed, but changes are written into WAL. The location and format of the control file can vary depending on the database system and its configuration.

In PostgreSQL, the control file is typically located within the data directory, and it is named `global/pg_control`.

The `pg_control` file contains various control information, including the Checkpoint LSN, and it is crucial for database recovery.

When the database recovers from crash, it reads the Checkpoint LSN from the control file to determine the point in the WAL to which it needs to recover.

**LSN or Log Sequence Number**, is a unique identifier associated with every entry in the WAL file. This LSN value serves as a byte offset within the file. During database recovery, this mechanism proves ingenious.

By reading the LSN from the control file, we can start reading directly from the corresponding byte offset, avoiding the need to iterate through the entire file.

If the LSN in the control file is less than the target LSN (configurable), it signifies that we need to catch up with updates from the WAL file to ensure the database reaches a consistent state.

## Optimizing Database Performance with WAL

WAL not only ensures data durability but also improves database performance. Here's how:

**Reduced Disk I/O:** With a log file in place, the database engine can store changes in a local buffer and periodically push them to disk. This reduces the number of I/O calls to the disk, making the system more efficient.

## Conclusion

Write-Ahead Logging plays a crucial role in ensuring the durability and consistency of database transactions. By logging changes before they are applied, it provides a safety net against data loss during system failures and enhances database performance.

In a world where data integrity is paramount, understanding and implementing WAL can be a game-changer for your database management strategy.
