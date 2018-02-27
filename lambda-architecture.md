# Lambda Architecture

When doing streaming process, maybe need to combine the streaming data with historical data to compute the result. For example, if we want to decide whether customer is frequently buy bear or not. we need to calculate the current new coming order with previous orders. Another scenario is when the new streaming data coming in. But some error happen. At this time, Are we throw this data ? No. We need to put it in another persistent place and process it in the future.

Below are typical lambda architecture graph:

Below are explainations of different layers:

Speed layer

Batch layer

Serving layer

### Demo: Log analysis system with lambda architecture

#### Overview

#### Architecture

![](/assets/log_analysis_architect.png)

#### Components

Java program: Use this program to mock log producer. This program will generate logs continuously and save into local log file.

Flume: Use this to distribute log data into kafka and HDFS

Kafka: Use this to receive access logs in real time

HDFS: Use this to store access logs. and Save all the raw access logs. Seems like the data lake of this architecture

Spark Streaming: Use this to processing real-time data from kafka. 

Spark SQL:



#### Code

#### 



