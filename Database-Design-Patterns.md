# 18 Database Design Patterns (Source: Instagram @coderz.py)

## Contents
1. [Sharding](#1-sharding)
2. [Replication](#2-replication)
3. [CQRS](#3-cqrs)
4. [Event Sourcing](#4-event-sourcing)
5. [Database per Service](#5-database-per-service)
6. [Saga Pattern](#6-saga-pattern)
7. [Materialized View](#7-materialized-view)
8. [Read Replica](#8-read-replica)
9. [Write-Ahead-Log](#9-write-ahead-log)
10. [Indexing](#10-indexing)
11. [Denormalization](#11-denormalization)
12. [Partitioning](#12-partitioning)
13. [Cache-Aside](#13-cache-aside)
14. [Star Schema](#14-star-schema)
15. [Polyglot Persistence](#15-polyglot-persistence)
16. [Bloom Filter](#16-bloom-filter)
17. [Consistent Hashing](#17-consistent-hashing)
18. [Two-Phase Commit](#18-two-phase-commit)

## Description

### 1. Sharding
tags: `Scalability`

Split data across multiple DBs using a shard key to scale horizontally.

```
                -------------------
                | router(key % N) |
                -------------------
                        |
                        ↓
            -------------------------
            |           |           |
            ↓           ↓           ↓
    -----------    -----------    -----------
    | Shard 1 |    | Shard 2 |    | Shard 3 |
    -----------    -----------    -----------
```

### 2. Replication
tags: `Availability`

Copy data across nodes so reads survive failures and scale out.

```
            -----------------------
            | Primary DB (writes) |
            -----------------------
                      |
                      ↓
          -------------------------
          |           |           |
          ↓           ↓           ↓
    -----------  -----------  -----------
    | CLone 1 |  | Clone 2 |  | Clone 3 |
    -----------  -----------  -----------

               Replicas (reads)
```

### 3. CQRS
tags: `Architecture`

Separate the write model from the read model for independent scaling.


```
             ------------    Sync    -----------
Command ───> | Write DB |  -------→  | Read DB | ───> Query
             ------------            -----------
```

### 4. Event Sourcing
tags: `Architecture`

Persist state as an append-only sequence of immutable events.

```
    -----------      -----------      -----------      -----------
    | Event 1 | ───> | Event 2 | ───> | Event 3 | ───> | Event 4 |
    -----------      -----------      -----------      -----------
                                                            ↑ (HEAD)
                                                     -----------------
                                                     | Current Event |
                                                     -----------------
```

### 5. Database per Service
tags: `Microservices`

Each microservice owns its schema, no shared tables across services.

```
     -------------     -------------     -------------
     | Service A |     | Service B |     | Service C |
     -------------     -------------     -------------
          |                  |                |
          ↓                  ↓                ↓
    ---------------   ---------------   ---------------
    | Database A1 |   | Database B1 |   | Database C1 |
    ---------------   ---------------   ---------------
```

### 6. Saga Pattern
tags: `Consistency`

Chain local transactions with compensations instead of one big commit.

```
    Step 1 ───> Step 2 ───> Step 3
    ↑           ↓    ↑           ↓
    |           |    |           |
    -------------    -------------

    solid arrow  : next transition
    dashed arrow : compensating rollback
```

### 7. Materialized View
tags: `Performance`

Precompute and cache expensive query results as physical tables.

```
     --------                                     Materialized View
    /______/|                                         ----------
    |      ||  Base Tables                            |--|--|--|
    |  DB  || ─────────────> Precompute + Store ────> |--|--|--|
    |______|/                                         ----------
```

### 8. Read Replica
tags: `Scalability`

Route reads to replicas so the primary only handles writes.
Similar to [Replication](#replication).


### 9. Write-Ahead-Log
tags: `Durability`

Log every change before applying it, guaranteeing crash recovery.

```
    ─────────────────
    | Write Request |
    ─────────────────
           |
          WAL (append-only)
           ↓                           --------
    -----------------   Apply to DB   /______/|
    | ------------- |  ────────────>  |      ||
    | ------------- |                 |  DB  ||
    -----------------                 |______|/
```

### 10. Indexing
tags: `Performance`

Build auxilary structures (B-Tree, Hash) to speed up lookups.


```
                   --------
                   | Root |
                   --------
                      |
                      ↓
        -----------------------------
        |             |             |
        ↓             ↓             ↓
    ----------    ----------    ----------
    | Leaf 1 |    | Leaf 2 |    | Leaf 3 |
    ----------    ----------    ----------
```

### 11. Denormalization
tags: `Performance`

Duplicate data on purpose to avoid costly joins at read time.

```
          -----------
          | Table 1 |
          -----------
              | (FK)                        Denormalized (flat)
              ↓                           -----------------
        ---------------         ──────>   |   |   |   |   |
        |             |                   -----------------
        ↓             ↓
    -----------    -----------
    | Table 2 |    | Table 3 |
    -----------    -----------
```

### 12. Partitioning
tags: `Scalability`

Split one large table into smaller, faster-to-query pieces.

```
   P1   |P2 |  P3
────────|───|────────
 C1  C2  C3  C4  C5
─────────────────────
|   |   |   |   |   |
|---|---|---|---|---|
|   |   |   |   |   |
|---|---|---|---|---|
|   |   |   |   |   |
---------------------

Partitions: P1 {C1, C2}, P2 {C3}, P3 {C4, C5} 
where C1..C5 are columns.
```


### 13. Cache-Aside
### 14. Star Schema
### 15. Ployglot Persistence
### 16. Bloom Filter
### 17. Consistent Hashing
### 18. Two-Phase Commit
