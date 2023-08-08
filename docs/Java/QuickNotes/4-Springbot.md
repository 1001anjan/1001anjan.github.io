---
layout: default
title: SpringBoot
parent: Quick Notes
grand_parent: Java
nav_order: 4
---
# Scopes in springBoot

In Spring Boot, scopes define the lifecycle and visibility of beans managed by the Spring container. Spring Boot provides several standard scopes that control when and how beans are created, used, and destroyed. Here are the commonly used scopes in Spring Boot:

1. Singleton: This is the default scope in Spring Boot. In singleton scope, a single instance of the bean is created for the entire application context. The same instance is shared and returned whenever the bean is requested.

2. Prototype: In prototype scope, a new instance of the bean is created each time it is requested. This means that every time you request the bean, you get a new instance.

3. Request: In request scope, a new instance of the bean is created for each HTTP request. The bean is bound to the lifecycle of the web request and is available only within that specific request.

4. Session: In session scope, a new instance of the bean is created for each user session. The bean is bound to the lifecycle of the user session and is available throughout the duration of the session.

5. Application: In application scope, a single instance of the bean is created for the entire web application. The bean is shared across multiple requests and sessions.

6. WebSocket: In WebSocket scope, a new instance of the bean is created for each WebSocket connection. The bean is bound to the lifecycle of the WebSocket connection and is available only within that specific connection.

You can specify the scope of a bean using the @Scope annotation on the bean declaration in Spring Boot. For example:
```java
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;

@Component
@Scope("prototype")
public class MyPrototypeBean {
    // Bean implementation
}
```
In this example, the MyPrototypeBean is annotated with @Scope("prototype"), indicating that it should be created in the prototype scope.

It's important to understand the implications of each scope and choose the appropriate scope for your beans based on their usage and requirements.

### Design pattern of SpringBoot

Spring Boot is a popular Java framework that simplifies the development of Java-based applications, especially web applications. It follows several design patterns to provide modular, scalable, and maintainable code. Here are some common design patterns used in Spring Boot:

1. Dependency Injection (DI) and Inversion of Control (IoC): Spring Boot extensively utilizes the DI and IoC design patterns. These patterns enable loose coupling between components by removing the direct dependencies between them. Spring Boot's IoC container (application context) manages the creation and wiring of objects, allowing you to inject dependencies through constructor injection, setter injection, or field injection.

2. MVC (Model-View-Controller): Spring Boot encourages the use of the MVC pattern for building web applications. The MVC pattern separates the application into three components: the model (data), the view (user interface), and the controller (logic). Spring Boot provides the Spring MVC module, which simplifies the implementation of the MVC pattern.

3. Repository Pattern: Spring Boot encourages the use of the Repository pattern to handle data access. The Repository pattern abstracts the data access layer and provides a consistent interface for performing CRUD (Create, Read, Update, Delete) operations on data entities. Spring Data JPA, a part of Spring Boot, provides a powerful implementation of the Repository pattern.

4. Singleton Pattern: Spring Boot's IoC container manages objects as singletons by default. Singleton objects are created only once, and the container shares the same instance across multiple requests. This pattern helps in optimizing resource usage and improving performance.

5. Builder Pattern: Spring Boot utilizes the Builder pattern in various configurations and bean definitions. The Builder pattern provides a way to construct complex objects step by step, allowing you to define optional parameters and improve readability.

6. Template Method Pattern: Spring Boot's JDBC template and JdbcTemplate classes follow the Template Method pattern. This pattern defines a skeleton algorithm in a base class and allows derived classes to provide specific implementation details. In the case of JdbcTemplate, the template methods provide a common structure for executing database operations, while the specific implementation is left to the derived classes.

7. Observer Pattern: Spring Boot's event-driven programming model is based on the Observer pattern. The framework provides an event mechanism where components can publish events, and other components can subscribe to those events. This decoupled approach allows components to react to events without explicit dependencies.

These are just a few examples of the design patterns used in Spring Boot. The framework incorporates various other patterns, such as Factory, Proxy, Decorator, and more, to provide a robust and flexible development experience.

### Spring Security
Spring Security is a powerful and widely-used security framework for Java applications. It provides comprehensive security services for securing your application, including authentication, authorization, session management, and various attack protections.

To implement Spring Security in your application, you can follow these general steps:

Add Spring Security Dependency: Include the Spring Security dependency in your project's build configuration. If you are using Maven, you can add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

2. Configure Spring Security: Create a configuration class that extends `WebSecurityConfigurerAdapter` and override its methods to configure security settings. You can define authentication providers, authorization rules, session management, and more. For example:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public/**").permitAll()
                .antMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .loginPage("/login")
                .permitAll()
                .and()
            .logout()
                .permitAll();
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN");
    }
}
```
In this example, we configure the HTTP security rules, define a login page, specify which URLs require authentication or authorization, and provide in-memory user credentials.

3. Implement UserDetailsService (Optional): If you want to load user details from a database or other external sources, you can implement the `UserDetailsService` interface and override its `loadUserByUsername()` method.

4. Secure URLs: Annotate your controller methods with appropriate annotations to enforce security. For example, you can use `@PreAuthorize` or `@Secured` annotations to specify access restrictions based on user roles or permissions.

### To authorize user authentication using a database in Spring Security, you can follow these steps:

1. Set up your Database: Configure your database and create a table to store user details, including usernames, passwords, and authorities/roles. You can use any database of your choice, such as MySQL, PostgreSQL, or H2.

2. Implement UserDetailsService: Create a class that implements the `UserDetailsService` interface provided by Spring Security. This interface is responsible for loading user details from the database. You need to override the `loadUserByUsername()` method to fetch user details based on the provided username. Within this method, query your database and retrieve the user details, including the password and authorities. Here's an example using JPA and Hibernate:

```java
@Service
public class UserDetailsServiceImpl implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException("User not found"));

        return new org.springframework.security.core.userdetails.User(
                user.getUsername(),
                user.getPassword(),
                getAuthorities(user.getRoles())
        );
    }

    private Collection<? extends GrantedAuthority> getAuthorities(Set<Role> roles) {
        return roles.stream()
                .map(role -> new SimpleGrantedAuthority(role.getName()))
                .collect(Collectors.toList());
    }
}
```

In this example, `UserRepository` is a custom repository interface that interacts with your database to fetch user information. The `getAuthorities()` method converts the user's roles into a collection of `GrantedAuthority` objects required by Spring Security.

3. Configure Authentication Provider: In your security configuration class, override the `configure(AuthenticationManagerBuilder auth)` method to configure the authentication provider. Use the `userDetailsService()` method to set your custom `UserDetailsService` implementation:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(passwordEncoder());
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    // Other security configurations...
}
```

In this example, we are using the BCryptPasswordEncoder as the password encoder, which is recommended for password storage.

4. Secure Endpoints: Use the `@PreAuthorize` or `@Secured` annotations on your controller methods to define access restrictions based on user roles or authorities. For example:

```java
@RestController
public class MyController {

    @GetMapping("/admin")
    @PreAuthorize("hasRole('ADMIN')")
    public String adminEndpoint() {
        // Handle request for admin-only functionality
    }

    // Other endpoints...
}
```

In this case, the `/admin` endpoint is accessible only to users with the "ADMIN" role.

5. Enable Global Method Security: In your security configuration class (annotated with `@EnableWebSecurity`), enable global method security by adding the `@EnableGlobalMethodSecurity` annotation. This allows you to use annotations such as `@Secured` for method-level security:

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(securedEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    // Configuration details...
}
```

6. Use `@Secured` Annotation: Annotate your methods or endpoints with `@Secured` and specify the required roles in the annotation. For example:
```java
@RestController
public class MyController {

    @GetMapping("/admin")
    @Secured("ROLE_ADMIN")
    public String adminEndpoint() {
        // Handle request for admin-only functionality
        return "Admin Endpoint";
    }

    @GetMapping("/user")
    @Secured({"ROLE_USER", "ROLE_ADMIN"})
    public String userEndpoint() {
        // Handle request for user functionality
        return "User Endpoint";
    }

    // Other endpoints...
}
```