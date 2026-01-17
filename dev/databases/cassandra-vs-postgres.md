# Flexible Schemas in SQL and Cassandra

This document explains flexible schemas, how they are implemented in SQL and Cassandra, and why Cassandra can provide advantages in distributed systems.

---

## 1. What is a Flexible Schema?

A **flexible schema** allows storing data where different records may have different fields or attributes, without altering the table structure every time a new attribute is added.

- **SQL (traditional relational):** Fixed columns; adding new attributes requires `ALTER TABLE`.
- **NoSQL / Cassandra:** Designed for flexible attributes; new data can be added without altering schema.

---

## 2. Implementing Flexible Attributes in SQL

### 2.1 EAV (Entity-Attribute-Value) Model

Instead of adding a column per attribute, do:

```sql
CREATE TABLE user_attributes (
    user_id INT,
    attribute_name VARCHAR(50),
    attribute_value VARCHAR(255),
    PRIMARY KEY (user_id, attribute_name)
);

INSERT INTO user_attributes VALUES (1, 'phone', '123-456-7890');
INSERT INTO user_attributes VALUES (1, 'city', 'New York');
INSERT INTO user_attributes VALUES (1, 'hobby', 'tennis');

SELECT attribute_name, attribute_value
FROM user_attributes
WHERE user_id = 1;

Query:

SELECT attribute_name, attribute_value
FROM user_attributes
WHERE user_id = 1;
```

- Pros: Flexible, no schema changes needed.
- Cons: Queries and indexing are more complex; performance can degrade at scale.

### 2.2 JSON / JSONB Columns (PostgreSQL, MySQL 5.7+)

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    attributes JSONB
);

INSERT INTO users (id, name, attributes)
VALUES (1, 'Alice', '{"phone":"123-456-7890","city":"New York"}');
```
- Pros: No schema changes, easy to store nested data.
- Cons: Harder to index individual attributes, performance may suffer for very large datasets.
  
---

## 3. Cassandra Wide Table
Cassandra is a NoSQL column-family database with flexible schema support.
A wide table allows a single “entity” (like a user) to have many dynamic attributes stored as multiple rows instead of adding new columns for each attribute.

```
CREATE TABLE user_attributes (
    user_id UUID,
    attribute_name text,
    attribute_value text,
    PRIMARY KEY (user_id, attribute_name)
);

INSERT INTO user_attributes (user_id, attribute_name, attribute_value)
VALUES (uuid(), 'phone', '123-456-7890');
INSERT INTO user_attributes (user_id, attribute_name, attribute_value)
VALUES (uuid(), 'city', 'New York');
INSERT INTO user_attributes (user_id, attribute_name, attribute_value)
VALUES (uuid(), 'hobby', 'tennis');
```

You use a primary key composed of:
- ***Partition key*** → groups rows for the same entity
- ***Clustering key*** → sorts rows within that partition
- Each row stores one attribute, similar to SQL EAV.
- No table alterations required for new attributes.

---

## CASSANDRA'S STRENGTH

- Flexible schema + predictable queries: You can store new attributes without schema changes.
- High write throughput: Writes go to the correct partition and are append-only.
- Scalability: Partitioning distributes data; clustering organizes it efficiently.
- Fault tolerance: Replication + partitioning ensures no single point of failure.

| Feature                      | SQL EAV (Flexible Rows)                                                      | Cassandra Wide Table                                                        |
| ---------------------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Schema flexibility**       | ✅ Yes, via EAV                                                               | ✅ Yes, natively designed for wide rows                                      |
| **Scalability**              | ❌ Hard: traditional SQL struggles beyond a single server; sharding is manual | ✅ Built for massive horizontal scaling across many nodes                    |
| **Write performance**        | Medium: frequent inserts/updates can cause contention and locking            | ✅ Extremely fast writes, append-only storage, no table locking              |
| **Read pattern**             | Needs careful indexing; aggregations over EAV are slow                       | ✅ Fast for predictable queries, especially with partition + clustering keys |
| **Distributed availability** | Depends on the database (e.g., MySQL cluster, Postgres BDR)                  | ✅ Designed for multi-datacenter replication and high availability           |
| **Fault tolerance**          | SQL often has single points of failure                                       | ✅ Built-in replication, fault tolerance, no single master node              |




