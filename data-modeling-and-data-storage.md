## Data storage for the batch layer

Requirements for the storage

* Immutable
* Parallel bulk write and efficiency reads
* Scalable storage
* Cost effective and Performance tuning

### Distributed filesystem

##### Typical distributed filesystems

* HDFS
* S3
* Cloud Storage

##### The Architecture

The Restricts

### Questions

1. How to split 1GB files into blocks in HDFS?
2. Do we need schema validation in master dataset?
3. If data types of master dataset are complex. so how to choose the best suitable storage frameworks
4. Does master dataset same meaning as data lake?



