# SF-Crime-Statistics
SF Crime Statistics with Spark Streaming (Udacity course)

In this project, we have been provided with a real-world dataset, extracted from Kaggle, on San Francisco crime incidents, and we will provide statistical analyses of the data using Apache Spark Structured Streaming. We will draw on the skills and knowledge you've learned in Udacity Streaming course to create a Kafka server to produce data, and ingest data through Spark Structured Streaming.

# Development Environment
I have created my project in the Udacity workspace, but these are the requirements to develop the project locally:

    •	Spark 2.4.3
    •	Scala 2.11.x
    •	Java 1.8.x
    •	Kafka build with Scala 2.11.x
    •	Python 3.6.x or 3.7.x

**--------------------------------------------------------------------------------------------------**
This is the steps made to obtain the desire results:
--------------------------------------------------------------------------------------------------

### STEP 1: Creating a kafka server with police department calls information
First we have to start zookeeper and kafka:

  `/usr/bin/zookeeper-server-start /etc/kafka/zookeeper.properties`
  
  `/usr/bin/kafka-server-start /etc/kafka/server.properties`


Next we have to run our kafka-server (previously we have to create ProducerServer class (we can do it in the same terminal)
  `spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] producer_server.py
  
  `spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] kafka_server.py`
  

And then, we have to check if the server is producing data and we are able to consume it by kafka consumer:

We can check if the topic has been created too (police-department-calls):

  `kafka-topics --list --zookeeper localhost:2181 
 
  `kafka-console-consumer --bootstrap-server localhost:9092 --topic police-department-calls --from-beginning`

![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/kafka-consumer.JPG?raw=true)


### STEP 2: Exploring Information in DataSets
Once we have explore the information with a Jupyter notebook, we can implement data-stream and see the progress reporter by executing the code:

  'spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py
 
  ![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/ProgressReport.JPG?raw=true)
  
The Spark UI:

  ![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/SparkUI.JPG?raw=true)

And the output:

  ![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/output.JPG?raw=true)


### STEP 3: Answer the questions

**1. How did changing values on the SparkSession property parameters affect the throughput and latency of the data?**

We can increase/decrease this two varibles: 

  > maxOffsetPerTrigger 
  
  > maxRatePerPartition
  
in the creation of the Spark Configuration (data_stream.py), and we can look at it in the ReportProgress: `processedRowPerSecond

  ![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/question1.JPG?raw=true)



**2. What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?**

In relation with question 1, I have been testing variations in these four variables to have the best performance by watching the best value for `processedRowPerSecond.


  > maxOffsetPerTrigger 
  
  > maxRatePerPartition
  
  > local[n]
  
  > spark.driver.memory
  
And it looks like these are the optimal values:

  ![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/question2.JPG?raw=true)

  
