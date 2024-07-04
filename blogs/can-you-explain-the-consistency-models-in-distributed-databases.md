# Can you explain the consistency models in distributed databases (e.g., CAP theorem)?

## Definition
The CAP theorem, also known as Brewer's theorem, says that distributed databases can’t simultaneously provide more than two of the following guarantees:

- (C) Data Consistency: Every read receives the most recent write or an error.
- (A) Availability: Every request (read or write) receives a (non-error) response, without guarantee that it contains the most recent write.
- (P) Partition tolerance: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.

For example:  
if the system is consistent and highly available, it won’t be able to withstand partial network outages.   
If on the other hand, the system is highly available and partition tolerant, it won’t be able to ensure immediate data consistency.

## Types
Different popular databases can be categorized based on which two of the three guarantees they prioritize

### CA (Consistency and Availability): 
These systems guarantee consistency and availability, but they do not tolerate partitions well. Generally, CA databases are not distributed across multiple sites.

**Relational Databases:**  
- MySQL (single node)
- PostgreSQL (single node)
- Oracle Database
- Microsoft SQL Server

### CP (Consistency and Partition Tolerance):
These systems guarantee consistency and partition tolerance but may not be available for every request if a partition occurs.

**Distributed Databases:**  
- HBase
- MongoDB (when configured for consistency)
- Cassandra (when tuned for consistency)
- Google Bigtable
- Amazon DynamoDB (when using strong consistency)

### AP (Availability and Partition Tolerance):
These systems guarantee availability and partition tolerance but may return stale data if a partition occurs.  

**Distributed Databases:**  
- Cassandra (when tuned for availability)
- Riak
- Couchbase
- Amazon DynamoDB (when using eventual consistency)
- Voldemort

## Key Points:
- **`CA`** systems are typically single-node databases or systems that do not need to handle network partitions, focusing on high consistency and availability within a single node.
- **`CP`** systems sacrifice availability in favor of maintaining consistency across partitions, suitable for applications where the accuracy of data is critical.
- **`AP`** systems prioritize availability and partition tolerance, allowing for more flexibility in handling partitions and network issues but potentially providing stale data.


This categorization helps in choosing the right database system based on the specific needs of consistency, availability, and partition tolerance for an application.