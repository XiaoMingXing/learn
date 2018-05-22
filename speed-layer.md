### Speed layer

### ![](/assets/speed layer.png)

**Real time view must support random write? what's the difference between support random write or not?**

* The speed layer data is at most a few hours old and is vastly smaller than the master dataset
* The speed layer producing views by running a function over all of the recent data
* The speed layer need random-read/random-write databases so that updates can be performed on existing views

Two facets of the speed layer:

* storing the realtime views
* Processing the incoming data stream and update those views

The contents of your realtime views will exactly mirror the contents of your batch views.

The underlying storage layer must therefore meet the following requirements:

* Random reads - the data it contains must be indexed
* Random writes - modify a realtime view with low latncy
* Scalability - must be distributed across many machines
* Fault tolerance - replicating data across machines so there are backups

### The realtime views

The complexities of realtime views

* **Online compaction **- periodically the database must perform compaction to reclaim space. and compaction is a resource-intensive process.

* **Concurrency** - Sharing mutable state across threads is a notoriously complex problem

### The incremental algorithms in speed layer:

The CAP theorem: "When a distributed data system is partitioned, it can be consistent or available but not both"

The scenario:

Suppose you have a simple distributed key/value database, and you replicating data across multiple servers. That means if you become partitioned from one replica, you can still retrieve value from another location. The real problem is how to handle writes under partitions.

* You can refuse to perform an update unless all replicas can be undated at once.\(your data system is consistent but not available\)

* You can choose to update whatever replicas are available and synchronize with other replicas when the partition is resolved. \(your data system is available but not consistent\)

The solutions:

* Use **conflict-free replicated data types** to solve the diverge between partitions
* Use **read repair algorithms **

The questions:

* **What's the use case of eventual accuracy? how to do the eventual accuracy computation?**
* What is sloppy quorums?

  R+W &gt; N guarantees consistency? :  read quorum + writes quorum &gt; number of quorums

  For example, if N equals three in a cluster of five nodes \(A, B, C, D, and E\) and nodes A, B, and C are the top three preferred nodes, then minus any error conditions writes will be made to nodes A, B, and C. But if B and C were not available for a write, then a system using a **sloppy quorum** would write to D and E instead. If this were to happen, then even if the write quorum \(W\) was 3 and the read quorum \(R\) was 2, making R+W&gt;N, a read immediately following this write could return data from B and C, which would be inconsistent because only A, D, and E would have the latest value.

* **Sloppy quorums** - as outlined in the Dynamo paper.

* **Strict quorums** - writes do not persist if we cannot get acks back from W quorum member
* **Strict-warn quorums** - writes return an error if we cannot get acks back from W quorum members; however, the data might persist despite the acknowledgment.

According to the Amazon Dynamo article, Dynamo mitigates this inconsistency through hinted handoffs. If the system needs to write to nodes D and E instead of B and C, it informs D that its write was meant for B and informs E that its write was meant for C. Nodes D and E keep this information in a temporary store and periodically poll B and C for availability. Once B and C become available, D and E send over the writes.

* What's that meaning for only one server in the system will be updating the count for a given replica \(Page. 215\). Why use the maximize number will be correct. how about if the diverged at 0

### The asynchronous update and synchronous updates

* Synchronous updates: the application issues a request directly to the database and blocks until the update is processed.
* Asynchronous updates: update requests are places in a queue with the updates occurring at a later time

### Expiring realtime views

The questions:

* How to decide which parts of data we need to discard?
* How to switch reading data from realtime view into serving layer batch views.

### Cassandra

* Cassandra uses the keys to partition a column family across a cluster
* Online compaction and the need to rebalance key ranges can cause significant pain.



Installation guide:

https://www.digitalocean.com/community/tutorials/how-to-install-cassandra-and-run-a-single-node-cluster-on-ubuntu-14-04



