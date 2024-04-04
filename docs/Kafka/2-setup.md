---
layout: default
title: Kafka Setup
parent: Kafka
nav_order: 2
---
# To set up Kafka follow these steps:
1. Install Java: Kafka requires Java to run. Check if you have Java installed by opening Terminal and running the command `java -version`.
2. Download Kafka: Go to the Apache Kafka website (https://kafka.apache.org/downloads) and download the latest stable release of Kafka. Choose the binary version and download the .tgz file.
3. Extract Kafka: Open Terminal and navigate to the directory where you downloaded the Kafka .tgz file. Extract the contents of the file using the following command, replacing `<kafka-version>` with the actual version you downloaded:
```markdown
tar -xzf kafka_<kafka-version>.tgz
```
4. Start the ZooKeeper server: Kafka uses ZooKeeper for coordination. Start ZooKeeper by running the following command from the Kafka directory:
```markdown
bin/zookeeper-server-start.sh config/zookeeper.properties
```
ZooKeeper will start running on `localhost:2181`.
5. Start the Kafka broker: Open a new Terminal window and navigate to the Kafka directory. Start the Kafka broker by running the following command:
```markdown
bin/kafka-server-start.sh config/server.properties
```
Kafka will start running on `localhost:9092` by default.
6. Verify Kafka setup: Open a new Terminal window and run the following command to create a test topic:
```markdown
bin/kafka-topics.sh --create --topic test-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```
This command creates a topic named "test-topic" with one partition and a replication factor of 1.
7. Publish and consume test messages: In separate Terminal windows, run the following commands to produce and consume test messages:
* Producer Terminal:
```markdown
bin/kafka-console-producer.sh --topic test-topic --bootstrap-server localhost:9092
```
This will open a console where you can type and publish messages.
* Consumer Terminal:
```markdown
bin/kafka-console-consumer.sh --topic test-topic --bootstrap-server localhost:9092 --from-beginning
```

### Quick Debug:
```markdown
anjanjana@Anjans-MacBook-Pro kafka-3.5.0-src % bin/zookeeper-server-start.sh config/zookeeper.properties

Classpath is empty. Please build the project first e.g. by running './gradlew jar -PscalaVersion=2.13.10'
anjanjana@Anjans-MacBook-Pro kafka-3.5.0-src % ./gradlew jar -PscalaVersion=2.13.10
```

### Run multiple Kafka brokers
To run multiple Kafka brokers, you need to configure and start multiple instances of Kafka on different ports. Each Kafka broker will act as an independent node in the Kafka cluster. Here are the general steps to run multiple Kafka brokers:

1. Configure Kafka properties: Create separate configuration files for each Kafka broker. Copy the `server.properties` file, which is located in the Kafka installation directory, for each broker instance. Rename the copied files, such as `server1.properties`, `server2.properties`, and so on, for easy identification.
2. Update broker-specific properties: Open each configuration file and modify the following properties to ensure uniqueness for each broker:
   * `broker.id`: Assign a unique ID to each broker. The ID must be an integer and should be different for each broker.
   * `listeners`: Set the listeners property to define the network interfaces and ports for each broker. For example, you can have `PLAINTEXT://localhost:9092` for the first broker, `PLAINTEXT://localhost:9093` for the second, and so on.
   * `log.dirs`: Specify different directories for the log files of each broker. It's recommended to have separate directories to avoid data conflicts.

3. Configure ZooKeeper connection: In each configuration file, specify the connection details of the ZooKeeper ensemble by updating the `zookeeper.connect` property. Ensure that all brokers use the same ZooKeeper ensemble.
4. Start each Kafka broker: Open a separate Terminal window for each broker instance. Navigate to the Kafka installation directory and run the following command for each broker, replacing `<broker-id>` with the unique ID assigned to each broker, and `<config-file>` with the respective configuration file:
    ```markdown
    bin/kafka-server-start.sh config/<config-file>
    ```
    For example, to start the first broker with `server1.properties`:
    ```markdown
    bin/kafka-server-start.sh config/server1.properties
    ```
    Similarly, start the other brokers with their respective configuration files.
5. Verify broker status: Once all the brokers are started, you can verify their status by running the following command for each broker in separate Terminal windows:
    ```markdown
    bin/kafka-topics.sh --list --bootstrap-server localhost:<port>
    ```
   Replace `<port>` with the appropriate port number for each broker (e.g., 9092, 9093, etc.). This command will list all the topics available on that particular broker.



