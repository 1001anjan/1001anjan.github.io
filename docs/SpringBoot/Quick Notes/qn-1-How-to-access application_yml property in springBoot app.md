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