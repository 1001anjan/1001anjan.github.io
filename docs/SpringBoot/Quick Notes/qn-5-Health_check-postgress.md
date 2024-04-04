---
layout: default
title: Health Check PostGress SQL
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 5
---
# Health Check PostGress SQL
A health check in Spring Boot is a way to monitor the status of your application's components and dependencies, such as a PostgreSQL database. To perform a health check on a PostgreSQL database, you can create a custom health indicator in your Spring Boot application that connects to the database and checks its status. Here is an example of how you could implement this:

1. Add the following dependency to your build.gradle or pom.xml file to include the PostgreSQL JDBC driver:

```yaml
dependencies {
    implementation 'org.postgresql:postgresql:42.2.14'
}
```
2. Create a new class that implements the HealthIndicator interface:
```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

@Component
public class PostgresHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        try {
            Class.forName("org.postgresql.Driver");
            Connection connection = DriverManager.getConnection("jdbc:postgresql://localhost:5432/postgres", "postgres", "password");
            connection.close();
            return Health.up().build();
        } catch (ClassNotFoundException | SQLException e) {
            return Health.down().build();
        }
    }
}
```

3. In the health method, you can connect to the `PostgreSQL` database using the JDBC driver, and return a `Health.up().build()` if the connection is successful. If the connection fails, return `Health.down().build()` to indicate that the database is not healthy.

You can access the health status of the database by visiting the `/actuator/health` endpoint in your application.

Note: You should customize the JDBC connection string, `username`, and `password` in the code to match your `PostgreSQL` database configuration.
