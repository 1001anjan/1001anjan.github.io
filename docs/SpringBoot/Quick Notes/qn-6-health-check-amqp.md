---
layout: default
title: Health Check AMQP
parent: Quick Notes
grand_parent: Spring Boot
nav_order: 4
---
# Health check AMQP

```java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.GetResponse;
import com.signify.flexc.dataanalytics.amqp.AmqpClient;
import org.springframework.boot.actuate.health.AbstractHealthIndicator;
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.autoconfigure.condition.ConditionalOnProperty;
import org.springframework.context.annotation.Configuration;

@Configuration
@ConditionalOnProperty(value="health.amqp.enabled", havingValue = "true", matchIfMissing = true)
public class AmqpHealthIndicator extends AbstractHealthIndicator {

    private AmqpClient amqpClient;

    public AmqpHealthIndicator(AmqpClient amqpClient){
        this.amqpClient = amqpClient;
    }

    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        Channel channel = amqpClient.getAmqpChannel();
        channel.queueDeclare("health_check_queue", false, false, false, null);
        channel.basicPublish("", "health_check_queue", null, "health_check".getBytes());
        GetResponse response = channel.basicGet("health_check_queue", true);
        if (response != null) {
            Health.up().build();
        }else {
            Health.down().build();
        }
    }
}
```

```java
@Service
public class AmqpClient {

    private static final Logger logger = LoggerFactory.getLogger(AmqpClient.class);
    private static final int PoolSize = 5;

    private ConnectionFactory factory;
    private Connection connection;
    private ExecutorService channelsExecutor;
    private ThreadLocal<Channel> channelsThreadLocal;


    @Value("${amqp.uri}")
    public String AmqpUri;
    
    @PostConstruct
    public void AmqpClient() throws IOException, TimeoutException, URISyntaxException, NoSuchAlgorithmException, KeyManagementException {
        factory = new ConnectionFactory();
        factory.setUri(AmqpUri);
        factory.setAutomaticRecoveryEnabled(true);
        connection = factory.newConnection();
        channelsExecutor = Executors.newFixedThreadPool(PoolSize);
        channelsThreadLocal = new ThreadLocal<Channel>() {
            @Override
            protected Channel initialValue() {
                Channel channel = null;
                try {
                    channel = connection.createChannel();
                } catch (IOException e) {
                    e.printStackTrace();
                }
                return channel;
            }
        };
    }

    public Channel getAmqpChannel(){
        return channelsThreadLocal.get();
    }
}
```
