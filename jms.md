###  Configuration:

After installation you must add the following dependency:

```
    <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-activemq</artifactId>
		</dependency>

```

And add some properties to your application.properties

```
spring.activemq.in-memory=false
spring.activemq.pool.enabled=false
spring.activemq.broker-url=tcp://localhost:61616

```

###  Config:

```
@Configuration
public class Config {

    @Value("${spring.activemq.broker-url}")
    private String brokerUrl;

    @Bean
    public Queue queue() {
        return new ActiveMQQueue("standalone.queue");
    }

    @Bean
    public ActiveMQConnectionFactory activeMQConnectionFactory() {
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory();
        factory.setBrokerURL(brokerUrl);
        return factory;
    }

    @Bean
    public JmsTemplate jmsTemplate() {
        return new JmsTemplate(activeMQConnectionFactory());
    }
}


```
### PoducerResource interface/implementation :

```
public interface ProducerResourceInter {

	void publish(String message);

}


```
```
@Service
public class ProducerResource implements ProducerResourceInter{

    @Autowired
    JmsTemplate jmsTemplate;

    @Autowired
    Queue queue;
    
    private static final Logger logger = LoggerFactory.getLogger(LoggingController.class);

    @Override
    public void publish(String message) {

    	  logger.info("PUBLISHER: sending message to queue");
        jmsTemplate.convertAndSend(queue, message);

    }
}

```

###  Consumer:

```
@Component
public class Consumer {
	
	private static final Logger logger = LoggerFactory.getLogger(LoggingController.class);
	

    @JmsListener(destination = "standalone.queue")
    public void consume(String message){
      
    	logger.info("QUEUE: processing message: "+message);
      
    }
}

```
