---
layout: default
title: Example of @EnableConfigurationProperties(AppConfig.class)
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 4
permalink: /qn-3-Example of @EnableConfigurationProperties(AppConfig.class)/
---
# Example of @EnableConfigurationProperties(AppConfig.class)
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

