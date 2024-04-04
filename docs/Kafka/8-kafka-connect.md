---
layout: default
title: Kafka Connect Api
parent: Kafka
nav_order: 8
---
### Kafka Connect
Kafka Connect is a framework and component of Apache Kafka, an open-source distributed streaming platform. Kafka Connect allows users to easily integrate Kafka with other data sources and sinks, making it a powerful tool for building data pipelines.

The primary goal of Kafka Connect is to provide a scalable and fault-tolerant way to ingest data into Kafka and to export data from Kafka to other systems. It simplifies the development and management of connectors, which are plugins responsible for connecting Kafka topics to external systems.

Key features of Kafka Connect include:
1. Connectors: Kafka Connect has two types of connectors: Source Connectors and Sink Connectors. Source Connectors are responsible for capturing data from external systems and writing it to Kafka topics. Sink Connectors, on the other hand, read data from Kafka topics and write it to external systems.
2. Scalability: Kafka Connect is designed to scale horizontally, allowing you to distribute the data ingestion and extraction workload across multiple worker nodes. This ensures that the system can handle high data throughput and supports large-scale deployments.
3. Fault-tolerance: Kafka Connect ensures fault tolerance by storing connector configurations and offsets in Kafka itself, using Kafka topics as the configuration store. This allows it to recover from failures and resume processing from where it left off.
4. REST API: Kafka Connect provides a REST API for managing connectors, which allows you to create, modify, and monitor connectors programmatically.
5. Connector Ecosystem: Kafka Connect has a growing ecosystem of community-developed connectors for various data sources and sinks, such as databases, cloud storage, message queues, Hadoop, and more. These connectors can be easily plugged into Kafka Connect and deployed without the need for writing custom code.

By using Kafka Connect, organizations can build robust and efficient data pipelines that can handle real-time data streams, enabling seamless integration between diverse data systems and applications.

### Example
Let's consider a practical example of using Kafka Connect to demonstrate how it can be used to integrate Kafka with an external data source and sink. In this example, we'll use Kafka Connect to ingest data from a text file and write it to a Kafka topic (Source Connector) and then export the data from the Kafka topic to a text file (Sink Connector).
### Source Connector Configuration:
   Assuming we have a CSV file named `input.txt` with the following contents:
   ```markdown
    id,name,age
    1,Alice,30
    2,Bob,35
    3,Charlie,28
   ```
We want to ingest this data into a Kafka topic called `output-topic`.
First, we create a configuration file for the Source Connector (`input-source.properties`):
```yml
name=text-source-connector
connector.class=FileStreamSourceConnector
tasks.max=1
file=/Users/anjanjana/Documents/input.txt
topic=output-topic
```

The Source Connector will read data from the `input.txt` file and write it to the `csv_data_topic` Kafka topic.
### Sink Connector Configuration:
Now, let's create a Sink Connector configuration (`file-sink.properties`) to export data from the Kafka topic to a text file:
```markdown
name=file-sink-connector
connector.class=FileStreamSink
tasks.max=1
file=/Users/anjanjana/Documents/output.txt
topics=output-topic
```

```markdown
bootstrap.servers=localhost:9092

# The converters specify the format of data in Kafka and how to translate it into Connect data. Every Connect user will
# need to configure these based on the format they want their data in when loaded from or stored into Kafka
key.converter=org.apache.kafka.connect.json.JsonConverter
value.converter=org.apache.kafka.connect.json.JsonConverter
# Converter-specific settings can be passed in by prefixing the Converter's setting with the converter we want to apply
# it to
key.converter=org.apache.kafka.connect.storage.StringConverter
value.converter=org.apache.kafka.connect.storage.StringConverter
key.converter.schemas.enable=false
value.converter.schemas.enable=false

offset.storage.file.filename=/tmp/connect.offsets
# Flush much faster than normal, which is useful for testing/debugging
offset.flush.interval.ms=10000

# Set to a list of filesystem paths separated by commas (,) to enable class loading isolation for plugins
# (connectors, converters, transformations). The list should consist of top level directories that include 
# any combination of: 
# a) directories immediately containing jars with plugins and their dependencies
# b) uber-jars with plugins and their dependencies
# c) directories immediately containing the package directory structure of classes of plugins and their dependencies
# Note: symlinks will be followed to discover dependencies or plugins.
# Examples: 
# plugin.path=/usr/local/share/java,/usr/local/share/kafka/plugins,/opt/connectors,
plugin.path=/Users/anjanjana/Documents/applications/kafka-3.5.0-src/kafka-plugins/libs,
```
#### Note:
We need to download required connector jar files, and store in a specific directory. 
In this example we configured
```markdown
plugin.path=/Users/anjanjana/Documents/applications/kafka-3.5.0-src/kafka-plugins/libs,
```
### Starting the Source Connector:
Next, we start the Source Connector using the `kafka-connect` command-line tool with the configuration file:
```markdown
$ kafka/bin/connect-standalone.sh config/connect-standalone.properties config/input-source.properties config/file-sink.properties
```

The Sink Connector will read data from the `input.txt` Kafka topic and write it to the `output.txt` file.

* FileStreamSource connector loads the full content of the file during startup and doesn't dynamically update the content when the file is modified.

This example demonstrates a basic use case of Kafka Connect to integrate external data sources and sinks with Apache Kafka, providing a seamless way to build data pipelines and stream data between various systems. Note that this is a simplified example, and Kafka Connect supports a wide range of connectors for different data sources and sinks, making it highly versatile for real-world use cases.

---
In Kafka Connect, you can configure the serializers and deserializers (also known as converters) for data serialization and deserialization by specifying them in the Kafka Connect worker configuration. Kafka Connect provides built-in converters for various data formats, including plain text, JSON, Avro, and more. The exact steps to configure the converters depend on the data format you want to use. I'll provide examples for plain text and JSON data formats:

### Plain Text Serialization:
To configure Kafka Connect for plain text serialization, follow these steps:
* Open the Kafka Connect worker configuration file (`connect-distributed.properties` or `connect-standalone.properties`).
* Set the following properties:
    ```markdown
    key.converter=org.apache.kafka.connect.storage.StringConverter
    value.converter=org.apache.kafka.connect.storage.StringConverter
   ```
  These configurations specify the StringConverter for both the key and value serialization, which will treat the data as plain text.
### JSON Serialization:
To configure Kafka Connect for JSON serialization, follow these steps:
* Open the Kafka Connect worker configuration file (`connect-distributed.properties` or `connect-standalone.properties`).
* Set the following properties:
    ```markdown
    key.converter=org.apache.kafka.connect.json.JsonConverter
    value.converter=org.apache.kafka.connect.json.JsonConverter
    key.converter.schemas.enable=false
    value.converter.schemas.enable=false
   ```
    * The `JsonConverter` will serialize the data as JSON.
    * The `key.converter.schemas.enable=false` and 
    * `value.converter.schemas.enable=false` configurations disable schema support. If you are producing plain JSON data without schema information, you need to set these properties to false.

* If you want to use a specific custom converter, you can implement your custom converter class and specify it in the `key.converter` and `value.converter` properties. Custom converters must implement the `org.apache.kafka.connect.storage.Converter` interface.

For example, if you have a custom converter class called `com.example.CustomConverter`, you would set the properties as follows:
```markdown
key.converter=com.example.CustomConverter
value.converter=com.example.CustomConverter
```
Keep in mind that using built-in converters like `StringConverter` and `JsonConverter` is usually sufficient for most use cases. Custom converters are useful when you need to handle specific serialization/deserialization requirements not provided by the built-in converters.

---
#### Kafka Connect for MongoDb
To connect MongoDB and Apache Kafka, you can use the "MongoDB Connector for Apache Kafka." This connector enables you to capture changes (inserts, updates, deletes) occurring in MongoDB and then produce these changes as events to a Kafka topic. This way, you can leverage the power of Kafka to stream data from MongoDB to other downstream systems or applications.

### Install the MongoDB Connector for Apache Kafka:
* Download the connector from the Confluent Hub: https://www.confluent.io/hub/mongodb/kafka-connect-mongodb
* Follow the installation instructions provided by Confluent for the connector.

`mongodb-source-connect.properties`
```markdown
name=mongodb-source-connector
connector.class=com.mongodb.kafka.connect.MongoSourceConnector

# Define the tasks max to parallelize the data import (adjust according to your needs).
tasks.max=1

# MongoDB connection string.
connection.uri=mongodb://localhost:27017

# The MongoDB database and collection to read data from.
# You can use a comma-separated list for multiple collections.
# For example: "database=mydb,collection=mycollection1,mycollection2"
database=productDb
collection=products

# The name of the field in each MongoDB document to use as the Kafka message key.
# If not specified, Kafka Connect will use a generated key.
key.converter=org.apache.kafka.connect.storage.StringConverter
key.field=_id

# Define the Kafka topic(s) to which the data will be produced.
# If you use topic.prefix, the actual Kafka topic will be "topic.prefix.database.collection".
# Otherwise, you can set "topic=<your_kafka_topic_name>" directly.
# For example, "topic=my_topic".
#value.converter=org.apache.kafka.connect.json.JsonConverter
value.converter=org.apache.kafka.connect.storage.StringConverter
value.converter.schemas.enable=false
topic=output-topic
errors.tolerance= all

# Define the time-based strategy to create the topic if it doesn't exist.
# For example, use 'none' to disable auto-creation, or 'create' to enable it.
# For more fine-grained topic configuration, consider using a separate topic management tool.
#topic.creation.enable=none

# Define the replication factor for the auto-created topics.
# Adjust the value according to your Kafka cluster's replication requirements.
#topic.creation.default.replication.factor=3

# Define the number of partitions for the auto-created topics.
# Adjust the value according to your requirements and expected workload.
#topic.creation.default.partitions=3

# Define the poll interval in milliseconds. This specifies how often the connector will poll for new data changes.
poll.max.batch.size=1000
poll.await.time.ms=500

# Define the initial synchronization behavior.
# If 'initial.sync.source' is set to 'true', the connector will load all existing data from the collection.
# If 'initial.sync.source' is set to 'false', the connector will only read new changes.
initial.sync.source=true
```

* Start Mongo Connector 
```markdown
bin/connect-standalone.sh config/connect-standalone.properties config/mongodb-source-connect.properties
```









