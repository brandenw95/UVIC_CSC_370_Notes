# <u>Final Review</u>

[TOC]

## Study Topics (Table of Contents):

### ER, Tables, Queries, Constraints

- [ER Diagrams](#er-diagrams)
- [Classes](#classes)
- [Mutually exclusive subclasses](#mutually-exclusive-subclasses)
- [Table Creation](#table-creation)
- [Views](#views)
- [SQL](#sql)
- [Correlated Subqueries](#correlated-subqueries)

### External Storage

- [Disks](#disks)
- [Disk Access Time](#disk-access-time)
- [MIN time to read a 16,384-byte block](#min-time-to-read-a-16,384-byte-block)
- [MAX time to read a 16,384-byte block](#max-time-to-read-a-16,384-byte-block)
- [AVG time to read a 16,384-byte block](#avg-time-to-read-a-16,384-byte-block)

### Indexes

#### BTrees

- [Lookup](#lookup)
- [Insertion](#insertion)
- [Structure of B-trees with real blocks](#structure-of-b-trees-with-real-blocks)

#### 2PMMS

- [How many records can we sort?](#how-many-records-can-we-sort)
- [Sorting larger files](#sorting-larger-files)

### Query Evaluation

- [An SQL query and its RA equivalent](#an-sql-query-and-its-ra-equivalent)
- [Running Example – Airline](#running-example--airline)
- [Cost of a Plan (Pushing selections)](#cost-of-a-plan-pushing-selections)

### Concurrency

- [Summarizing the Terminology](#summarizing-the-terminology)
- [Precedence graphs](#precedence-graphs)
- [Two Phase Locking](#two-phase-locking)
- [Shared/Exclusive Locks](#sharedexclusive-locks)
- [Upgrading Locks](#upgrading-locks)
- [Possibility for Deadlocks](#possibility-for-deadlocks)
- [Benefits of Update Locks](#benefits-of-update-locks)

### Recovery from Crashes

#### UNDO

- [Undo with NQ Checkpointing](#undo-with-nq-checkpointing)

#### REDO

- [Redo with Checkpointing](#redo-with-checkpointing)

#### UNDO/REDO

- [Undo/Redo with Checkpointing](#undo/redo-with-checkpointing)
- [UNDO vs REDO vs UNDO/REDO](#undo-vs-redo-vs-undo/redo)

### Database Normalization (BCNF)

- [Births Table](#births-table)
- [Anomalies](#anomalies)
- [Functional Dependencies](#functional-dependencies)
- [Keys of Relations](#keys-of-relations)
- [Boyce-Codd Normal Form](#boyce-codd-normal-form)

#### Decomposition into BCNF

- [Babies Example](#babies-example)

#### Rules About Functional Dependencies

- [Movie Example](#movie-example)

# // Content

## ER, Tables, Queries, Constraints

#### ER Diagrams

#### Classes

#### mutually exclusive subclasses

#### Table Creation

#### Views 

#### SQL

#### Correlated Subqueries

## External Storage

#### Disks

#### Disk Access Time

#### *MIN* time to read a 16,384-byte block

#### *MAX* time to read a 16,384-byte block

#### *AVG* time to read a 16,384-byte block

## Indexes

### BTrees

#### Lookup

#### Insertion

#### Structure of B-trees with real blocks

### 2PMMS

#### How many records can we sort?

#### Sorting larger files

## Query Evaluation

#### An SQL query and its RA equivalent

#### Running Example – Airline

#### Cost of a Plan (Pushing selections)

## Concurrency

#### Summarizing the Terminology

#### Precedence graphs

#### Two Phase Locking

#### Shared/Exclusive Locks

#### Upgrading Locks

#### Possibility for Deadlocks

#### Benefits of Update Locks

## Recovery from Crashes

### UNDO

#### Undo with NQ Checkpointing

### REDO

#### Redo with Checkpointing

### UNDO/REDO

#### Undo/Redo with Checkpointing

#### UNDO vs REDO vs UNDO/REDO

## Database Normalization (BCNF)

#### Births Table

#### Anomalies

#### Functional Dependencies

#### Keys of Relations

#### Boyce-Codd Normal Form

### Decomposition into BCNF

#### Babies Example

### Rules About Functional Dependencies

#### Movie Example