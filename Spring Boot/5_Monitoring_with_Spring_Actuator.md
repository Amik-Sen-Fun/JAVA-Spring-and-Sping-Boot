# Actuater 

- An actuator is a sub-area of a propulsion technique and it describes the creation of a movement or a distortion. 

- Example Code: 

```java
management.endpoint.web.exposure.include = health, info, logger, metrics
management.endpoint.env.enables = true
management.endpoint.beans.enables = true
management.endpoints.enabled-by-default = true
```

|Features|Function|
|---|---|
|AuditEvents|Expose audit event information for the current application|
|Beans| Displays a complete list of all the Spring Beans in your application|
|Caches| Exposes available caches|
|Conditions|Shows the condition that were evaluated on configuration and auto-configuration classes, and the reason why they did or did not match|
|Configprops| Displays a collated list of all @ConfigurationProperties|
|env| Exposes properties from Spring's Configurable Environment|
|Health| Shows the application's health information|
|httptrace| Displays HTTP trace information|
|info|Displays arbitrary application information|
|Loggers|Shows and modifies the configuration of loggers in the application|
|Metrics| Shows metrics information for the current application|
|mappings| Displays a collated list of all @RequestMapping paths|
|sessions| Allows the retrieval and deletion of user sessions from a Spring Session-backed session store|
|threaddump| Performs a thread dump|

- We can access the actuator in the website:  `localhost:8080/actuator/info`


# Exploring the Extremities of Spring Boot Actuator

- By default, all endpoints are enables, except for shutdown.

- Enable/disable an endpoint with: 
    - `management.endpoint.<id>.enables=true/false`
    - `management.endpoints.web.exposure.include = health, info`
    - `management.endpoints.web.exposure.exclude = `


# Custom Endpoints 

- Define your own endpoints with `@Endpoint`
- Define a config class with `@ManagementContextConfiguration`
- Create a `spring.factories` file with this content: 
    - `org.springframework.boot.actuate.autoconfigure.web.ManagementContextConfiguration = \`
    - `yourpackage.yourCustomEndpointConfig`
    
```java
@Endpoint(id="custom")
public class CustomEndpoint{
    private final HashMap<String, Person> map = new HashMap<String, Person>();

    @ReadOperation
    public List<Person> getOperation(){
        return new ArrayList<Person>(map.values());
    }

    @WriteOperation
    public String writeOperation(){
        return "write"
    }

    @DeleteOperation
    public String deleteOperation(){
        return "delete";    
    }
}
```

# Checking Health Indicators

- Health endpoint statuses: 
    - `UP`
    - `DOWN`
    - `OUT_OF_SERVICE`
    - `UNKNOWN`

- Spring Boot 2 comes with several pre-defined health checks, such
    - `DataSourceHealthIndicator`
    - `DiskSpaceHealthIndicator`
    - `MongoHealthIndicator`
    - `RedisHealthIndicator`
    - `CassandraHealthIndicator`
    
```java
@Component
public class CustomHealthIndicator implements HealthIndicator{
    
    @Override
    public Health health(){
        return Health.up().withDetail("user","Amik Sen").build();
    }
}
```

# Reviewing the Metrics 


Metrics:

- JVM Metrics
- CPU Metrics
- FileDescriptor Metrics
- Kafka Consumer Metrics

##  `Promtheus`

It is a metric monitoring system that implemnets a dimensional data model. It allows queries and visualizes data.

- It is installed as a dependency.

- To install a custom metric in Prometheus do: 

```java
@Controller
public class IndexController {
    private Counter myCounter;

    public IndexController(MeterRegistry registry){

        mycounter = Counter.builder("mycustommetric")
                    .description("My custom metric")
                    .register(registry)
    }

    @RequestMapping("/")
    public String index(){
        // blah blah blah
        mycounter.increment(); // increases the metric
    }

}
```



