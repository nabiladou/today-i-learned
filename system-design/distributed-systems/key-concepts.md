# Distributed Systems Cheat Sheet

## Replication
Replication means storing copies of the same data on multiple nodes.
It happens continuously:
- On every write
- When a failed node recovers
- Via background synchronization (anti-entropy)

Used for fault tolerance and availability.

---

## Quorums
Quorum: the minimum number of nodes that must respond for a read or write operation to be considered successful in a distributed system.
Quorum is “how many servers must agree.”

Consistency rule:
R + W > N

What it means (plain English) -> At least one node is shared between every read and write, so reads see the latest write.

Tiny example
N = 3 (3 replicas)
W = 2 (write to 2 nodes)
R = 2 (read from 2 nodes)
Since 2 + 2 > 3, consistency is guaranteed.

---

## Sloppy Quorum
Allows read/write quorums to be satisfied by **any available nodes**
when intended replica nodes are unavailable.

Improves availability, allows temporary inconsistency.

---

## Hinted Handoff
Used with sloppy quorums.
A healthy node temporarily stores data for a failed node
and forwards it when the node recovers.

Prevents write failures.

---

## Tombstones
A tombstone is a marker representing deleted data.
Deletes are propagated during replication so old data is not resurrected.
After a grace period, tombstones are physically removed.

---

## Big Picture
Replication + sloppy quorums → high availability  
Hinted handoff + tombstones → eventual consistency
