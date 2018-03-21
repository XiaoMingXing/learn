## Batch layer

### Examples

1. Number of pageviews over time
2. Gender inference
3. Influence score

#### Computing on the batch layer

#### Recomputation algorithms vs incremental algorithms

1. Overview 
   1. Recomputation algorithms calculate the full dataset
   2. incremental algorithms calculate the increment dataset
2. Performance
   1. The amount of resources required to update a batch view with new data \(**how many resources you used?**\)
   2. The size of the batch views produced \(**how many value you output?**\)
3. Human-fault tolerance
4. Generality of the algorithms

#### Scalability in the batch layer

#### MapReduce: a paradigm for Big data computing

1. Scalability
2. Fault-tolerance
3. Generality of MapReduce

##### Characters

1. Multistep computations are unnatural
2. Joins are very complicated to implement manually
3. logical and physical execution tightly coupled

### Pipe diagrams

1. Concepts \(**Spark SQL**\)  
   make the process as pipeline \(functional programing\)

2. Compare with MapReduce  
   1. functions and filters  
   2. Group by  
   3. Aggregators  
   4. Join  
   5. Merge

3. examples  
   1. Number of pageviews over time  
   2. Gender inference  
   3. Influence score



