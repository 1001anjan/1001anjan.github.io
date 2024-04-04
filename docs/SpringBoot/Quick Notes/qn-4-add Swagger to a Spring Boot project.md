---
layout: default
title: Add Swagger to a Spring Boot project
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 4
---
# Add Swagger to a Spring Boot project
To add Swagger to a Spring Boot project in Java, you can follow these steps:

1. Add the following dependencies to your pom.xml file:

````xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
````

2. Create a SwaggerConfig.java file with the following content:
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig {
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.any())
                .paths(PathSelectors.any())
                .build()
                .apiInfo(apiInfo());
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("API Documentation")
                .description("API for your Spring Boot application")
                .version("1.0")
                .build();
    }
}
```
3. Start your Spring Boot application and access the Swagger UI at `http://localhost:8080/swagger-ui.html`.
   Note: The URLs and versions may differ based on your setup.