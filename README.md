# spring-kafka
This project demonstrates the integration of Apache KAFKA with Spring Boot. 

In this post we will integrate Spring Boot and Apache Kafka instance. This project sends the message on topic (tejinder-topic) which is created on Apache KAFKA instance.

First we need to run APACHE KAFKA Instance. Here are the steps for the same, assuming JDK 1.8 is already configured on your system:

1. Download APACHE KAFKA from https://kafka.apache.org/download and extract the zip file. This Kafka installation comes with an inbuilt zookeeper. Zookeeper is mainly used to track status of nodes present in Kafka cluster and also to keep track of Kafka topics, messages, etc.
2. Open command prompt and go to the extracted folder and start the zookeeper 
    C:\kafka_2.12-0.10.2.1>.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

3. Open a new command prompt and start the Apache Kafka.
    C:\kafka_2.12-0.10.2.1>.\bin\windows\kafka-server-start.bat .\config\server.properties
    
4. Open a new command prompt and create a topic with name tejinder-topic, that has only one partition & one replica.    
    
    C:\kafka_2.12-0.10.2.1>.\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic tejinder-topic
    
    And use the below command to see all the topics created :
    
    C:\kafka_2.12-0.10.2.1>.\bin\windows\kafka-topics.bat --list --zookeeper localhost:2181 
    
5. Next Open a new command prompt and create a producer to send message to the above created tejinder-topic and send a message - This is my first message-
    C:\kafka_2.12-0.10.2.1>.\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic tejinder-topic
    This is my first message
    
6. Finally Open a new command prompt and start the consumer which listens to the topic tejinder-topic we just created above. We will get the message we had sent using the producer
    C:\kafka_2.12-0.10.2.1>.\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic tejinder-topic --from-beginning    
    
By running all four components (zookeeper, broker, producer, and consumer) in different terminals, you will be able to enter messages from the producer’s terminal and see them appearing in the subscribed consumer’s terminal. If everything works fine, you will be able to push and see messages.
   
Till now the Apache Kakfa is configured and running properly.

Now next is to configure Apache KAFKA with Spring Boot. For that refer to the files pom.xml, ApacheKafkaWebController.java, KafkaSender.java

The URL to send the message using REST call is http://localhost:8080/tejinder-kafka/producer?message=testMessage

This call will send the message to the Apacke KAFKA topic tejinder-topic, which we have created above.



    
    

