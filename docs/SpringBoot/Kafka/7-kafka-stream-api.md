---
layout: default
title: Kafka Stream Api
parent: Kafka
grand_parent: Spring Boot
nav_order: 7
---
### Kafka Streams API 
Kafka Streams API is a library provided by Apache Kafka, an open-source distributed streaming platform. It enables developers to build stream processing applications and microservices that consume, transform, and produce data streams in real-time.

The Kafka Streams API allows you to create and deploy scalable and fault-tolerant stream processing applications by leveraging the messaging and storage capabilities of Apache Kafka. It provides a high-level DSL (Domain-Specific Language) and a low-level Processor API, giving developers flexibility in choosing the level of abstraction that best suits their needs.

Key features of the Kafka Streams API include:
1. Stream Processing: It allows you to process and transform data streams in real-time. You can perform operations such as filtering, mapping, aggregating, joining, and windowing on the streams of data.
2. Fault Tolerance: The API handles fault tolerance automatically by leveraging the fault-tolerant storage of Kafka. It ensures that data is not lost in case of failures and provides exactly-once processing semantics.
3. Scalability: Kafka Streams applications can scale horizontally to handle large amounts of data by distributing the processing workload across multiple instances.
4. Event Time Processing: The API supports event time processing, which allows you to process events based on their timestamps, enabling accurate handling of out-of-order events.
5. Stateful Processing: Kafka Streams supports stateful processing, where you can maintain and update the state based on the data in the stream. This allows you to perform complex computations and aggregations.
6. Integration with Kafka Ecosystem: Kafka Streams seamlessly integrates with Apache Kafka and other Kafka ecosystem components. You can easily consume data from Kafka topics, produce output to Kafka topics, and integrate with other systems and frameworks in the Kafka ecosystem.

### Here are a few real-life use cases where Kafka Streams API can be applied:
1. Real-time Analytics: Kafka Streams can be used to process and analyze streaming data in real-time, allowing organizations to gain insights and make data-driven decisions as events occur. For example, you can calculate real-time metrics, perform aggregations, and generate reports based on the incoming data streams.
2. Fraud Detection: Kafka Streams can be utilized to detect fraudulent activities in real-time. By processing and analyzing streaming data from various sources such as transaction logs, user behavior, and historical data, you can identify patterns and anomalies that indicate fraudulent behavior, enabling timely intervention and prevention.
3. Internet of Things (IoT) Data Processing: With the proliferation of IoT devices generating massive amounts of data, Kafka Streams can be used to process and analyze sensor data streams in real-time. This can include tasks such as filtering, aggregating, and correlating sensor readings to derive meaningful insights and trigger actions based on specific conditions or events.
4. Social Media Sentiment Analysis: Kafka Streams can be employed to perform sentiment analysis on social media streams in real-time. By processing and analyzing the text data from social media platforms, you can extract sentiment scores, identify trends, and gain insights into public opinion, enabling businesses to respond promptly to customer feedback or market trends.
5. Click stream Processing: Kafka Streams can be used to process and analyze clickstream data from websites or mobile apps in real-time. This can involve tasks such as tracking user behavior, analyzing session data, generating personalized recommendations, and performing A/B testing to optimize user experiences and conversions.
6. Event-driven Microservices: Kafka Streams can be utilized to build event-driven microservices architectures. By consuming and processing events from Kafka topics, you can create scalable and loosely coupled microservices that react to specific events, enabling real-time data processing, synchronization, and orchestration across different components of a distributed system.

These are just a few examples, but Kafka Streams API can be applied to various other use cases that involve real-time data processing, analytics, and event-driven architectures. Its flexibility, scalability, and integration capabilities make it a powerful tool for building stream processing applications.

#### Example Code
The code example below implements a WordCount application that is elastic, highly scalable, fault-tolerant, stateful, and ready to run in production at large scale

```java
package com.example.kafkaStream.dsl;

import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.common.utils.Bytes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.KTable;
import org.apache.kafka.streams.kstream.Materialized;
import org.apache.kafka.streams.kstream.Produced;
import org.apache.kafka.streams.state.KeyValueStore;

import java.util.Arrays;
import java.util.Properties;

public class WordCountApplication {

    public static void main(final String[] args) throws Exception {
        Properties props = new Properties();
        props.put(StreamsConfig.APPLICATION_ID_CONFIG, "wordcount-application");
        props.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        props.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass());
        props.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass());


        StreamsBuilder builder = new StreamsBuilder();
        KStream<String, String> textLines = builder.stream("example-topic");
        KTable<String, Long> wordCounts = textLines
                .flatMapValues(textLine -> Arrays.asList(textLine.toLowerCase().split("\\W+")))
                .groupBy((key, word) -> word)
                .count(Materialized.<String, Long, KeyValueStore<Bytes, byte[]>>as("counts-store"));
        wordCounts.toStream().peek((key, value) -> System.out.println("[key: "+key+"] [value: "+value+"]")).to("output-topic", Produced.with(Serdes.String(), Serdes.Long()));

        KafkaStreams streams = new KafkaStreams(builder.build(), props);
        streams.start();
    }

}
```

* Official Link for DSL api: https://kafka.apache.org/35/documentation/streams/developer-guide/dsl-api
* Kafka Stream Processor Api: https://kafka.apache.org/35/documentation/streams/developer-guide/dsl-api

### Basic Steam Example
```java
package com.example.kafkaStream.dsl;

import org.apache.kafka.common.serialization.Serde;
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.Consumed;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.Produced;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;

public class BasicStream {

    public static void main(String arg[]) throws IOException {
        Properties streamProperties = new Properties();
        try(FileInputStream fis = new FileInputStream("src/main/resources/stream.properties")){
            streamProperties.load(fis);
        }
        streamProperties.put(StreamsConfig.APPLICATION_ID_CONFIG, "basic-stream");
        StreamsBuilder streamsBuilder = new StreamsBuilder();
        final String inputTopic = streamProperties.getProperty("input.topic.name");
        final String outputTopic = streamProperties.getProperty("output.topic.name");

        final String orderNumberStart = "orderNumber-";

        KStream<String, String> firstStream = streamsBuilder.stream(inputTopic, Consumed.with(Serdes.String(), Serdes.String()));

        firstStream.peek(((key, value) -> System.out.println("key: "+key+" Value: "+value)))
                .filter((key, value) -> value.contains(orderNumberStart))
                .mapValues(value -> value.substring(value.indexOf("-") + 1))
                .filter((key, value) -> Long.parseLong(value) > 1000)
                .peek((key, value) -> System.out.println("key: "+key+" Value: "+value))
                .to(outputTopic, Produced.with(Serdes.String(), Serdes.String()));

        KafkaStreams kafkaStreams = new KafkaStreams(streamsBuilder.build(), streamProperties);
        kafkaStreams.start();
    }
}
```
### KTable Example:
```java
package com.example.kafkaStream.dsl;

import ch.qos.logback.core.net.SyslogOutputStream;
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.*;
import org.apache.kafka.streams.state.KeyValueStore;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;

public class KTableExample {

    public static void main(String arg[]) throws IOException {
        Properties streamProperties = new Properties();
        try(FileInputStream fis = new FileInputStream("src/main/resources/stream.properties")){
            streamProperties.load(fis);
        }
        streamProperties.put(StreamsConfig.APPLICATION_ID_CONFIG, "basic-stream");
        StreamsBuilder streamsBuilder = new StreamsBuilder();
        final String inputTopic = streamProperties.getProperty("input.topic.name");
        final String outputTopic = streamProperties.getProperty("output.topic.name");

        final String orderNumberStart = "orderNumber-";

        KTable<String, String> firstKTable = streamsBuilder.table(inputTopic,
                Materialized.as("ktable-store"));

        firstKTable.filter((key, value) -> value.contains(orderNumberStart))
                .mapValues(value -> value.substring(value.indexOf("-") + 1))
                .filter((key, value) -> Long.parseLong(value) > 1000)
                .toStream().peek((key, value) -> System.out.println("key: "+key+" Value: "+value)).to(outputTopic);
        
        KafkaStreams kafkaStreams = new KafkaStreams(streamsBuilder.build(), streamProperties);
        kafkaStreams.start();
    }
}
```
### SpringBoot Example
`KafkaStreamsConfig.java`
```java
package com.example.kafkaStream;

import com.example.kafkaStream.model.UserActivityJoinResult;
import com.example.kafkaStream.model.UserClicks;
import com.example.kafkaStream.model.UserPurchases;
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.kstream.*;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.annotation.EnableKafka;
import org.springframework.kafka.annotation.EnableKafkaStreams;
import org.springframework.kafka.config.KafkaStreamsConfiguration;
import org.springframework.kafka.config.StreamsBuilderFactoryBean;
import org.springframework.kafka.support.serializer.JsonSerde;

import java.util.HashMap;
import java.util.Map;

@Configuration
@EnableKafka
@EnableKafkaStreams
public class KafkaStreamsConfig {

    @Bean
    public KStream<String, String> kStream(StreamsBuilder streamsBuilder) {
        KStream<String, String> stream = streamsBuilder.stream("example-topic");
        stream.mapValues(value -> value.toUpperCase()).to("output-topic");
        return stream;
    }


    @Bean
    public KStream<String, UserClicks> userClicksStream(StreamsBuilder streamsBuilder) {
        KStream<String, UserClicks> stream = streamsBuilder.stream("user-clicks");
        return stream;
    }

    @Bean
    public KStream<String, UserPurchases> userPurchasesStream(StreamsBuilder streamsBuilder) {
        KStream<String, UserPurchases> stream = streamsBuilder.stream("user-purchases");
        return stream;
    }

    @Bean
    public KTable<String, Long> clicksAggregation(KStream<String, UserClicks> userClicksStream) {
        return userClicksStream
                .groupBy((key, value) -> value.getUserId(), Grouped.with(Serdes.String(), new JsonSerde<>(UserClicks.class)))
                .count();
    }

    @Bean
    public KTable<String, Double> purchasesAggregation(KStream<String, UserPurchases> userPurchasesStream) {
        return userPurchasesStream
                .groupBy((key, value) -> value.getUserId(), Grouped.with(Serdes.String(), new JsonSerde<>(UserPurchases.class)))
                .aggregate(
                        () -> 0.0,
                        (key, value, aggregate) -> aggregate + value.getAmount(),
                        Materialized.with(Serdes.String(), Serdes.Double())
                );
    }

    @Bean
    public KStream<String, UserActivityJoinResult> userActivityJoin(KTable<String, Long> clicksAggregation,
                                                                   KTable<String, Double> purchasesAggregation) {

        ValueJoiner<Long, Double, UserActivityJoinResult>  valueJoiner =
                (clickCounts, purchasesCount) -> new UserActivityJoinResult(null, clickCounts, purchasesCount);

        KStream<String, UserActivityJoinResult> userActivityStream =  clicksAggregation
                .join(purchasesAggregation,valueJoiner).toStream();
        userActivityStream.to("user-activity-output-topic");
        return userActivityStream;
    }
    
    @Bean
    public KafkaStreamsConfiguration kStreamsConfig() {
        Map<String, Object> props = new HashMap<>();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("application.id", "my-kafka-streams-app");
        props.put("default.key.serde", Serdes.String().getClass().getName());
        props.put("default.value.serde", Serdes.String().getClass().getName());
        return new KafkaStreamsConfiguration(props);
    }
    @Bean
    public StreamsBuilderFactoryBean defaultKafkaStreamsBuilder(KafkaStreamsConfiguration streamsConfig) {
        return new StreamsBuilderFactoryBean(streamsConfig);
    }
}
```
`KafkaStreamApiApplication.java`
```java
@SpringBootApplication
public class KafkaStreamApiApplication {

	public static void main(String[] args) {
		SpringApplication.run(KafkaStreamApiApplication.class, args);
	}
}
```
`build.gradle`
```groovy
plugins {
	id 'java'
	id 'org.springframework.boot' version '3.1.2'
	id 'io.spring.dependency-management' version '1.1.2'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	sourceCompatibility = '17'
}

repositories {
	mavenCentral()
}

dependencyManagement {
	imports {
		mavenBom "org.springframework.cloud:spring-cloud-dependencies:2022.0.3"
	}
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.kafka:spring-kafka'
	implementation 'org.apache.kafka:kafka-streams'

	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

tasks.named('test') {
	useJUnitPlatform()
}
```

