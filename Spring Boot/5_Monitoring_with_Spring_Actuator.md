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

- By default, all endpoints are enables, except for shutdown

