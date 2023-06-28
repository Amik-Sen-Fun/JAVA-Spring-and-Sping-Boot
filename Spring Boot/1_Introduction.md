# Introduction 

- Spring Boot is a support for infrastructure at the application level

- It supports MVC and WebFlux

- In can embeds Tomcat, jetty and Undertow (which are application servers similar to flask or waitress server)

## Features

- Core Features: 
    - SpringApplication
    - Configuration
    - Profiles and logging

- Web applications:
    - MVC
    - Embedded Containers

- DB connection 
    - SQL
    - No SQL

- Messaging

- Testing

## Spring Initialiser 

- Google it 
- Go to website
- Fill the requirements 
- Download the zip file 

We can also install with `scoop`

- `scoop install springboot`: install initial file

- To run the sample app do: `spring run app.groovy`

- The app is hosted in `localhost:8080`

- To enter spring shell do : `spring shell`

## Configuring Classes and Spring automation configuration

- External Configuration
    
    - Environment supplies access to properties for the application to run 
    - These properties are handled by the `Org.springframework.core.env` which accesses the enviroment that gives it information regarding `.properties-files`, `JVM properties` and `System`
    - Application Environment Properties:
        - Settings of dev tools in home directory
        - Properties of tests bounded via `@TestPropertySource`
        - Properties of `@SpringBootTest`
        - Application parameters
        - System variable: `SPRING_APPLICATION_JSON`
        - `ServletContext` parameters
        - `ServletConfig` parameters
        - Java Naming
        - Java system properties
        - OS system properties
        - Random values of namespace
        - Application-\{profile\}.properties outside of the artifact.
        - Application-\{profile\}.properties
inside of the artifact.
        - application.properties outside of artifact
        - application.properties inside of artifact
        - Property loaded with `@PropertySources` of configuration classes
        - Default properties set with the `setDefaultProperties` method of SpringApplication

    - Configuration files can be `java properties file` or `.yaml file`
        - `./config`: of working directory
        - `/config`: of classpath
        - `/root`: of classpath

    - Spring frameworks recommends not to access the environment instance. We can access them via two methods:
        - The `@Value` and Spring Expression Language expressions: to access single variable instances. 
        - Type-safe configuration with `@EnableConfigurationProperties` or `@ConfigurationProperties`.               


- Internal Configuration

    - Profiles
        - Bean registration
        - Configuration profiles
        - Application-\{nameofprofile\}.\[properties|yaml\]
        - Activation with the `spring.profiles.active = nameofprofile` property
    
    - Configuration Classes 
    - Automated classes:
        - `@SpringBootApplication` in the base class
        - `@EnableAutoConfiguration` format
        ```java
        @Configuration
        @EnableAutoConfiguration( 
            exclude = {SecurityAutoConfiguration.class}
        )
        public class XXXConfiguration{
            // blah blah blah
        }
        ``` 

