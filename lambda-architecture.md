# Lambda Architecture

When doing streaming process, maybe need to combine the streaming data with historical data to compute the result. For example, if we want to decide whether customer is frequently buy bear or not. we need to calculate the current new coming order with previous orders. Another scenario is when the new streaming data coming in. But some error happen. At this time, Are we throw this data ? No. We need to put it in another persistent place and process it in the future.

**Below is abstraction level of lambda architecture:**

![](/assets/lambda_architecture.png)

**Below is a more concrete lambda architecture:**

![](/assets/lambda_architect_concrete.png)

**Explainations of different layers:**

##### Batch layer

* Manage master dataset\(all data\). immutable , append-only set of raw data

* pre-computing arbitrary query functions, called batch views

* Techs we can use:  **HDFS/Hive/S3 - Spark/Flink/MapReduce**

##### Speed layer

* compensates for the high latency of updates to the serving layer and deals with recent data only.

* Techs we can use: **HBase - Spark Streaming/Storm**

##### Serving layer

* Indexes the batch views so that they can be queried in low-latency, ad-hoc way.

* Techs we can use:  **Druid / HBase**

#### Reference:

[http://lambda-architecture.net/](http://lambda-architecture.net/)

#### Questions:

* Application logic has to be defined in two different systems \(Batch & Real time\)
* Developer is responsible for reading, writing and managing two different storage systems and perform a final combination and serve thing final result
* Data mush be serialized consistently and kept in sync between two different systems 



As the questions before, there are some common architecture principles or solutions are trying to solve this problem. Which only need to implement lambda architecture. And make it easy to combine batch processing and real-time processing together. It's named "Unified" lambda architecture

#### Unified lambda architecture:

##### [**Summingbird**](https://speakerdeck.com/sritchie/summingbird-streaming-mapreduce-at-twitter)

Based on “monoids”, supporting Hadoop and Storm as backing infrastructure. Used at Twitter with “Manhattan” as read-only store and Memcached as “real-time” store.

**\(I have no idea about this one, lots of code\)**

[**Lambdoop**](http://www.slideshare.net/Datadopter/lambdoop-a-framework-for-easy-development-of-big-data-applications) 

Based on user-defined “operations”, Avro schemas, supports Hadoop and Storm as backing infrastructure and uses HBase as batch store and Redis as real-time store.

**\(Not sure does it close or not. I can't access the formal website\). I think no matter whether it's exist or not. The idea is great to learn. **

Below is short description about Lambdoop:![](/assets/lambdoop2.png)

### Demo: Log analysis system with lambda architecture

#### Architecture

![](/assets/log_analysis_architect.png)

#### Components

**App deploy in Nginx**: Use this program to mock log producer. This program will generate logs continuously and save into local log file.

**Flume:** Use this to distribute log data into kafka and HDFS

**Kafka:** Use this to receive access logs in real time

**HDFS:** Use this to store access logs as raw data. Seems like a data lake

**Spark Streaming:** Use this to processing real-time data from kafka.

**Spark SQL: **Use this to re-computing master dataset to get the result

**MySQL/HBase: **Use one of them to save processing result. one table for batch result, another one for realtime result

**Query App: **Use this to query batch result and realtime result, and merge the results together to provide insight

#### Questions:

* How to merge the Realtime View and Batch View?
* How about if Realtime View result will affect the Batch View result ? Machine Learning Algorithms

#### 



