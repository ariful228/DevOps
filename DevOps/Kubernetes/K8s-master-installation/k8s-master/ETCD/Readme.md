```sql
       +-----------------------+
       |    API Server          |<-- Client Requests
       |  (Reads/Writes State)  |
       +-----------------------+
                 ^
                 |
                 v
       +-----------------------+   +-----------------------+   +-----------------------+
       |      etcd Leader       |   |   etcd Follower #1    |   |   etcd Follower #2    |
       |  (Handles Write Ops)   |   |   (Read Replication)  |   |   (Read Replication)  |
       +-----------------------+   +-----------------------+   +-----------------------+
                 |                          |                         |
                 v                          v                         v
       +-------------------------------------------------------------------------+
       |                                                                         |
       |                 Distributed Consistent Key-Value Store                 |
       |            (Consensus Algorithm - RAFT for Replication)                |
       +-------------------------------------------------------------------------+
                 ^
                 |
                 v
       +-----------------------+
       |  Data Persistence      |
       |  (State Storage on     |
       |  Disk / Snapshot)      |
       +-----------------------+

```


# Explanation of the Process:

**Client Request:**The API server acts as an intermediary for clients, sending read and write requests to etcd.

**etcd Cluster:** etcd operates in a distributed manner, typically with an odd number of nodes (e.g., 3, 5) for quorum-based consensus.

**etcd Leader:** The leader node handles all write operations and ensures the state is replicated across followers.
**etcd Followers:** The follower nodes replicate the data from the leader and serve read requests.
RAFT Consensus Algorithm:

**Consensus:** etcd uses the RAFT algorithm to achieve consensus on changes across the cluster. Write requests must achieve consensus among the majority of nodes (quorum) before being applied.
**Replication:** All followers replicate the data written to the leader to maintain a consistent state across the cluster.
**Data Persistence:** etcd stores its data persistently on disk, ensuring that the cluster's state is durable even in case of failures.

**Summary:**
Leader node manages write operations and coordinates with followers.
Followers replicate data and respond to read requests.
RAFT ensures that changes to the key-value store are consistent and fault-tolerant.