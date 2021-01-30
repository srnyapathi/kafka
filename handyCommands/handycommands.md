# Kafka 101- One page quick reference

## What is Kafka ? 

> Apache Kafka is a community distributed event streaming platform capable of handling trillions of events a day. Initially conceived as a messaging queue, Kafka is based on an abstraction of a distributed commit log.

TLDR;

In short it is a highly scalable distributed messaging / even based system. It is open source tool and maintained by the community backed by confluent and also they have a paid version for enterprises where there will be additional support . 

## What is the main difference between a Queue and a topic ?
Queue has one sender and one intended recipient , where as a topic has multiple receivers and uses pub/sub model , only interested subscribe to a corresponding topic and they will receive messages accordingly.

## Kafka Terminology
 1. At the heart of the system is **Kafka cluster**.  
 2. A cluster is made up of multiple **brokers**. 
 3. Apache Zookeeper checks the health of the brokers and manages them. 
 4. Clients connect to the brokers and read / write the messages into kafka topic.
 5. Client writes a message into topic using **Kafka Producer API**. 
 6. Client will subscribe to a topic using **kafka consumer API** 

## Downloading kafka	
Kafka can be downloaded from official website [download kafka](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.7.0/kafka_2.13-2.7.0.tgz) 
optional step , you can add the bin directory in your path. This can help you to shorten your command 

# Configuration 
For development purposes , configuration is pretty straight forward . All the configuration is maintained in a folder called config. You need to modify the 
### server.properties
- Search for the line listener configuration and change it to plain text like so
  ```
  listeners=PLAINTEXT://localhost:9092
  ```
- Ensure the ports are not being used by any other services  in your machine .
- Change the following setting to ensure no new topics are created when you try to publish to a topic that does not exist
    ```
    auto.create.topics.enable=false
    ```

# Starting the Kafka server 
1. You need to first start apache zookeeper by running the following command.Navigate to config folder and then execute the below command.
    ```   
    zookeeper-server-start.bat .\zookeeper.properties
    ```
2. Start the server by running the following command.
    ```
    .\kafka-server-start.bat ..\..\config\server.properties
    ```

You should see some output in the console and you will also be seeing some logs in the zookeeper as well.

# Working with kafka server 
## 1. Creating a topic 
You can create the topic using the following command .
```sh
kafka-topics.bat --create --topic <TOPICNAME> -zookeeper <Zookeeper> --replication-factor <REPLICATIONFACTOR> --partitions <NUMBEROFPARTITIONS>
```
- `TOPICNAME` is name of the topic which you wish to create 
- `ZOOKEEPER` host and port of the zoo keeper instance 
- `REPLICATIONFACTOR` Number of replicas of this particular topic should be produced
- `NUMBEROFPARTITIONS` Number of partitions in the particular topic 

## 2. Producing a message
This is a simple command line Producer API that is used to put meesages in a topic from console 
```
kafka-console-producer --broker-list localhost:9092 --topic test-topic
```

## 3. Consuming a message 
This is a simple command line Consumer API that is used to read the messages from a topic

```
\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning
```
