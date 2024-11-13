# Dynamo DB

# Introduction

## Key design target for Dynamo Db
- Amazon need to keep its database services highly available and provide always on experience for customers.
- Handaling fast growing demand at internet scale
- Strict requirement for 99.9 percentile latency so that amazon can make its services very responsive to make customer satisfied.
- Data stored in the database should be persist, customer should not loose their item in shopping cart for example.
- Able to handle data-center level failure.

## Motivations
- Amazon decided to build a new K-V store because existing DBMS iw not able to meet those design target due to undesired features in existing DBMS.
- Data access pattern for Amazon's services are mostly primary key access. As a result, the new schema for new database can be simplified to key value data structure.
- High availability is a higher priority than strong consistency, and traditional DBMS prioritize very strong consistency that limited consistency.
- Highly distributed, loosely coupled service oriented architecture at Amazon requires new

## Use cases for Dynamo Db
- Shopping cart, Session information, product list

## Assumptions and Requirements
- Query model: Data is accessed by using its unique keys. Not supporting operations that span multiple data items. DynamoDb does'not support relational model.
- Dynamo prioritize Availability than consistency in ACID guarantee models. The database does not provide any isolation guarantees and permits only single key update.
- Use of commodity hardware infrastructures. The services have stringent latency requirements (SLA) measured by 99.9th percentile.
- Internal service for Amazon services, no security related requirements and each service user uses distinct instance of Dynamo

### Service level agreement
- Large distributed service oriented infrastructure have strict SLA requirement because services often have multiple dependencies. A client request will using several layers of applications so that a tight SLA of each services can ensure a desirable customer satisfaction.


## Design Overview

- Consistency vs. Availability: Traditional data replication methods prioritize strong consistency but reduce availability during failures. Dynamo opts for eventual consistency, ensuring updates reach all replicas eventually, and prioritizes availability by avoiding write rejections during failures.
- Conflict Resolution: Dynamo resolves update conflicts during reads rather than writes, ensuring it remains "always writable." Applications handle conflict resolution, providing flexibility for specific needs, like merging shopping cart versions.
- Incremental Scalability: Nodes can be added with minimal impact.
- Symmetry and Decentralization: All nodes have equal roles, avoiding single points of failure.
- Heterogeneity: Adapts work distribution to server capabilities, supporting mixed infrastructure.

## System Architecture

### Partitioning
#### Consistent Hashing
One of Dynamo's key design requirements is incremental scalability, which necessitates a mechanism to dynamically partition data across nodes. Dynamo employs consistent hashing as its partitioning scheme. In consistent hashing, the output of a hash function is treated as a circular space or "ring." Each data item, identified by a key, is assigned to a node by hashing the key to determine its position on the ring. The first node encountered in a clockwise traversal from the key's position is responsible for storing that data.

#### Challenges for Consistent Hashing: 
- Skewed Load Distribution: Consistent hashing positions data randomly on the ring, which can result in uneven load distribution across nodes.
- Heterogeneity in Nodes: The basic hashing algorithm does not account for differences in node capacity, leading to inefficiencies in heterogeneous environments.

##### Solutions:
- Even Load Distribution: Each physical node is assigned multiple nodes. This fine-grained partitioning of the ring reduces load skew, as the workload is distributed more evenly across physical nodes.
- Support for Heterogeneity: The number of virtue assigned to each physical node can be adjusted based on its capacity. Nodes with higher capacity can handle more vnodes, ensuring efficient utilization of resources.
- Improved Resilience: When a node becomes unavailable, its vnodes are redistributed evenly among the remaining nodes, minimizing the impact on load distribution. Similarly, when a new node is added, it takes over vnodes from the existing nodes in a balanced manner.
- Preference Lists: To account for failures, Dynamo constructs preference lists, which skip nodes that are unavailable and ensure each key's replicas are spread across distinct physical nodes.

## Replication
### Sloppy Quorum


