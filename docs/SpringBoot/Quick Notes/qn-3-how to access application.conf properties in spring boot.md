---
layout: default
title: How to access application.conf properties in spring boot
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 3
---
# How to access application.conf properties in spring boot
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