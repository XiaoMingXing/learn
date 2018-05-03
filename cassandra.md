### Cassandra

Cassandra does not support joins, group by, OR clause, aggregations

Here it is explained, how write process occurs in Cassandra,

1. When write request comes to the node, first of all, it logs in the commit log.
2. Then Cassandra writes the data in the mem-table. Data written in the mem-table on each write request also writes in commit log separately. Mem-table is a temporarily stored data in the memory while Commit log logs the transaction records for back up purposes.
3. When mem-table is full, data is flushed to the SSTable data file.

![](/assets/cassandra_request.png)

In Cassandra, writes are not expensive. Cassandra does not support joins, group by, OR clause, aggregations

The hash ring which used to save data, each cluster node will be assign a token range .

each raw will contain primary key, which is also be hashed to determined which node should be store.

![](/assets/harshring.png)

A node that receives a client query is referred to as the **coordinator **for the client operation

## Th **consistency level \(CAP Theorem\)**

https://docs.datastax.com/en/cassandra/3.0/cassandra/dml/dmlConfigConsistency.html



