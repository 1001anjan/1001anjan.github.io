---
layout: default
title: Sample Example
parent: Spring Reactor
grand_parent: Spring Boot
nav_order: 6
---
# Sample Example

Here is an example of a Spring Reactor implementation using `WebClient`, `PostgreSQL` with `iBatis`

```java
@Service
public class WebClientPostgresService {

    private final WebClient webClient;
    private final SqlSessionFactory sqlSessionFactory;

    public WebClientPostgresService(WebClient.Builder webClientBuilder, DataSource dataSource) {
        this.webClient = webClientBuilder.baseUrl("https://api.example.com").build();
        this.sqlSessionFactory = new SqlSessionFactoryBuilder().build(new PooledDataSource(dataSource));
    }

    public Mono<Response> getDataWithRetryAndTimeout(String path) {
        return webClient.get().uri(path)
                .retrieve()
                .bodyToMono(Response.class)
                .retryBackoff(3, Duration.ofSeconds(1), Duration.ofSeconds(5))
                .timeout(Duration.ofSeconds(5), Mono.error(new TimeoutException("Timeout occurred")))
                .subscribeOn(Schedulers.elastic());
    }

    public Mono<Integer> insertData(Data data) {
        return Mono.fromCallable(() -> {
            try (SqlSession session = sqlSessionFactory.openSession()) {
                DataMapper mapper = session.getMapper(DataMapper.class);
                return mapper.insert(data);
            }
        }).subscribeOn(Schedulers.parallel());
    }
}

@RestController
@RequestMapping("/data")
public class WebClientPostgresController {

    private final WebClientPostgresService service;

    public WebClientPostgresController(WebClientPostgresService service) {
        this.service = service;
    }

    @GetMapping("/{path}")
    public Mono<Response> getData(@PathVariable String path) {
        return service.getDataWithRetryAndTimeout(path);
    }

    @PostMapping
    public Mono<Integer> insertData(@RequestBody Data data) {
        return service.insertData(data);
    }
}

```

In this example, we have a `WebClientPostgresService` that uses a `WebClient` to call a REST API and a `SqlSessionFactory` to connect to a `PostgreSQL` database using iBatis. The `getDataWithRetryAndTimeout` method is used to retrieve data from the API and applies a retry logic with a backoff of 3 attempts, an initial duration of 1 second, and a max duration of 5 seconds. It also applies a timeout of 5 seconds and returns a `TimeoutException` if the request takes longer than 5 seconds to complete. The method also uses the `Schedulers.elastic` scheduler to run the task in a separate thread.

The `insertData` method is used to insert data into the `PostgreSQL` database using `iBatis`. It returns a `Mono` that represents the result of the insert operation. The method uses the `Schedulers.parallel` scheduler to run the task in a separate thread.

The `WebClientPostgresController` is a REST endpoint that uses the `WebClientPostgresService` to retrieve data from the API and insert data into the database. The `/data/`

### Create a configuration class for `MyBatis`:
```java
@Configuration
@MapperScan("com.example.mapper")
public class MyBatisConfig {

    @Bean
    public DataSource dataSource() {
        // Configuration for the database connection pool, such as setting the maximum number of connections.
        return DataSourceBuilder.create()
                .driverClassName("org.postgresql.Driver")
                .url("jdbc:postgresql://localhost:5432/mydatabase")
                .username("user")
                .password("password")
                .build();
    }
    
    @Bean
  public SqlSessionFactory sqlSessionFactory(DataSource dataSource) throws Exception {
    SqlSessionFactoryBean sessionFactory = new SqlSessionFactoryBean();
    sessionFactory.setDataSource(dataSource);
    return sessionFactory.getObject();
  }
}
```
### Create a DAO interface with the desired operations:
```java
@Mapper
public interface UserMapper {

  @Select("SELECT * FROM users WHERE id = #{id}")
  User getUserById(@Param("id") int id);
  
  // Add other operations
}
```

### Inject the SqlSessionFactory and the DAO into your service class:
```java
@Service
public class UserService {

  @Autowired
  private SqlSessionFactory sqlSessionFactory;
  
  @Autowired
  private UserMapper userMapper;

  public User getUserById(int id) {
    try (SqlSession sqlSession = sqlSessionFactory.openSession()) {
      return userMapper.getUserById(id);
    }
  }
  
  public Mono<Integer> insert(Person person) {
    return Mono.fromCallable(() -> {
        try (SqlSession sqlSession = sqlSessionFactory.openSession()) {
            sqlSession.insert("insertPerson", person);
            sqlSession.commit();
            return 1;
        }
    });
}
  
  // Add other methods
}
```

### Inject the UserService into your controller class:
```java
@RestController
public class UserController {

  @Autowired
  private UserService userService;

  @GetMapping("/users/{id}")
  public User getUserById(@PathVariable int id) {
    return userService.getUserById(id);
  }
  
  // Add other methods
}
```
