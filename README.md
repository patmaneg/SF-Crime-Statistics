# SF-Crime-Statistics
SF Crime Statistics with Spark Streaming (Udacity course)

# STEP 1: Creating a kafka server with police department calls information
First we have to start zookeeper and kafka:
  `/usr/bin/zookeeper-server-start /etc/kafka/zookeeper.properties`
  `/usr/bin/kafka-server-start /etc/kafka/server.properties`

Next we have to run our kafka-server:
  `spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] kakfa_server.py`

And then, we have to check if the server is producing data and we are able to consume it by kafka consumer:
  `kafka-console-consumer --bootstrap-server localhost:9092 --topic police-department-calls --from-beginning`

![Kafka consumer output](https://github.com/patmaneg/SF-Crime-Statistics/blob/master/images/kafka-consumer.JPG?raw=true)

