# Why doesn't MongoDB have availability in the CAP theorem?

## Context
As mentioned before on [CAP theorem](./can-you-explain-the-consistency-models-in-distributed-databases.md), MongoDB belonged to **` Consistency and Partition Tolerance (CP)`**. But MongoDB is a flexible database system that can be configured to prioritize either consistency or availability, depending on the needs of the application.   

When we talk about MongoDB being a **`CP`** system, we are referring to the configurations and settings that prioritize strong consistency even at the cost of availability during networks partition.

## Answer

In MongoDB replica, when there is a partition, mongo selects Consistency over Availability. 

To understand this, you simply need to understand "how MongoDB does replica sets". 
A Replica Set has a single primary node and many nodes play as secondary role. The only "safe" way to commit data is to write to the primary node, and then wait for that data to commit to the majority of nodes in the set.(you will see the flag for `w=majority` when sending write)

```javascript
db.collection('example').insertOne(
  { name: 'test' },
  { writeConcern: { w: 'majority', wtimeout: 5000 } }
);
```
So what happens on a partition? 
- `primary` node goes down: system becomes unavailable while a new primary node is selected. 

- `primary` node is disconnected from too many `secondary` nodes, system becomes unavailable, write operations can not commit, and the system is not availability. Basically, whenever a crisis happens, MongoDB needs to decide what to do, it will choose Consistency over Availability. It will stop accepting writes to the system until it believes that it can safely complete those writes. Other secondary nodes likely elect a new primary node while the previous primary steps down.

If you are familiar with Cassandra or Riak. They actually make a different decision here. If you're not sure which one you need, I suggest testing out Riak to really understand the differences.

## Addiction
While MongoDB can be configured for availability, it doesn't inherently guarantee availability in all scenarios because:  

**1. Default Settings Favor Consistency:**  
- In its default configuration, MongoDB prioritizes consistency by using majority write concerns `(w: "majority")` and read preferences that ensure data consistency `(readPreference: "primary")`.

- This means that in the event of a network partition where a majority of nodes are not available, MongoDB might become unavailable for write operations to maintain consistency.

**2. Primary Node Election:**  
- MongoDB uses replica sets for high availability, with one primary node handling writes and multiple secondary nodes replicating the data.

- During a network partition, if the primary node is isolated and a majority of nodes can't communicate, MongoDB will not elect a new primary, causing write operations to fail. This behavior prioritizes consistency and partition tolerance over availability.

**3. Configuration for Availability:**  

- To achieve high availability, MongoDB can be configured with lower write concerns (w: 1) and read preferences that allow reading from secondary nodes (readPreference: "secondary").
- However, this configuration sacrifices consistency, as writes acknowledged by a single node and reads from potentially stale secondaries might not reflect the most recent data.

