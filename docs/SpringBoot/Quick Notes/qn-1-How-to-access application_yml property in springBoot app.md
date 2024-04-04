---
layout: default
title: Access application.yml property in springBoot app
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 1
---
# Access application.yml property in springBoot app

In a Spring Boot application, you can access properties defined in the application.yml file by using the @Value annotation and specifying the property key. For example, if you have a property app.name defined in the application.yml file, you can access its value in a controller class like this:

```java
@Value("${app.name}")
private String appName;
```
You can also use the @ConfigurationProperties annotation on a class to bind the properties in the application.yml file to that class. For example, if you have the following properties defined in the application.yml file:
```yaml
app:
  name: MyApp
  version: 1.0
```
You can create a class like this:
```java
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private String version;
    //getters and setters
}
```
And then autowire it in your controller or service class:
```java
@Autowired
private AppProperties appProperties;
```
You can then access the properties using this object.
```java
String appName = appProperties.getName();
String appVersion = appProperties.getVersion();
```
Note that for `@ConfigurationProperties` you'll need to enable it by adding the following annotation in your configuration class or main class
```java
@EnableConfigurationProperties(AppProperties.class)
```

#### Can we use @value in java interface?

No, you cannot use the `@Value` annotation in a Java interface. The `@Value` annotation is used to inject a property value into a field, constructor or setter method, and it can only be used on a class or bean. Since an interface is not a class or bean, it cannot be used to hold state, therefore it is not possible to use `@Value` annotation on interface.

It's worth noting that interfaces in Java do not have any implementation, they only define method signatures. And Spring uses @Value annotation to set the value of a field in a specific instance of a class, which is not possible for interfaces.

If you want to share some properties across multiple classes, you can use the `@ConfigurationProperties` annotation on a class and autowire it in other classes.

Alternatively, you can use `Environment` object to access the property values, or use `PropertySourcesPlaceholderConfigurer` for `XML` based configuration.

#### How to access application.conf properties in spring boot
In Spring Boot, you can access properties defined in the `application.conf` file by using the `@Value` annotation and specifying the property key. For example, if you have a property app.name defined in the `application.conf` file, you can access its value in a controller class like this:
```java
@Value("${app.name}")
private String appName;
```
You can also use the @ConfigurationProperties annotation on a class to bind the properties in the `application.conf` file to that class. For example, if you have the following properties defined in the `application.conf` file:
```yml
app {
  name = "MyApp"
  version = "1.0"
}
```
You can create a class like this:
```java
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private String version;
    //getters and setters
}
```
And then autowire it in your controller or service class:
```java
@Autowired
private AppProperties appProperties;
```
You can then access the properties using this object.
```java
String appName = appProperties.getName();
String appVersion = appProperties.getVersion();
```
In order to use `application.conf` you need to configure the application to use it, the most common way of doing this is by adding the following dependency in your pom.xml file:
```xml
<dependency>
    <groupId>com.typesafe</groupId>
    <artifactId>config</artifactId>
    <version>1.4.0</version>
</dependency>
```
And then, you need to configure the application to look for the `application.conf` file in the classpath, by adding this to your `application.properties` or `application.yml` file:
```yaml
spring.config.name=application
spring.config.location=classpath:
```
Note that for `@ConfigurationProperties` you'll need to enable it by adding the following annotation in your configuration class or main class
```yaml
@EnableConfigurationProperties(AppProperties.class)
```

### Example of @EnableConfigurationProperties(AppConfig.class)
Here is an example of how to use the `@EnableConfigurationProperties` annotation to enable a configuration class called AppConfig:
```java
@Configuration
@EnableConfigurationProperties(AppConfig.class)
public class AppConfig {
    @Value("${app.name}")
    private String appName;

    public String getAppName() {
        return appName;
    }
}
```
In this example, the `@EnableConfigurationProperties` annotation is used on the AppConfig class to indicate that it should be used as a source for configuration properties. The `@Value` annotation is used to inject a property called app.name from the `application.properties` file.

You can then autowire this configuration class in other beans.
```java
@Autowired
AppConfig appConfig;
```