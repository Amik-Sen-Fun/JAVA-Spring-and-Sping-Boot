# Preventing Vulnerabilities by Adding Security

- `SecurityContextHolder`: realises access to **SecurityContext**.
- `SecurityContext`: contains an authentication instance and requests specific information 
- Authentication is represnted as a principle
- `GrantedAuthority`: instances describes the righst of an authentication. 
- `UserDetailsService`: delivers an interface for retriving **UserDetails** with a username or a certificate. 


Features of Authorization: 

- Cross-sectional aspect of an application 
- Explicit queries with code should be avoided 

Security and Spring Web MVC

- `SecurityAutoConfiguration` and `UserDetailsAutoConfiguration`

- The **WebSecurityConfigurerAdapter** bean overwrites the web security auto-configuration. 

```java
@Configuration 
public class WebConfig extends WebSecurityConfigurerAdapter{
    
    @Override
    public void configure(HttpSecurity http) throws Exception{
        http.authorizeRequests()
        .antMatchers("/index").permitAll()
        .antMatchers("/users/**").hasRole("USER")
        .and()
        .formLogin().loginPage("/login").failureUrl("/login-error");

    }
    
    @Autowired 
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception{
        // blah blah blah 
        // code 
    }
}
```

# Using External Configuration in Different Environments 

To configure a different name/location, use:
- `spring.config.name` = name of config file
- `spring.config.location` = location of config file
- `spring.config.additional-location` = location of config file. 

- Example: `Java -jar springproject.jar --spring.config.name = myConfig --spring.config.location = classpath:/ . .`

```java
@Component
@ConfigurationProperties("application")
public class ApplicationProperties{
    // blah blah blah
    application.applicationname = "blah blah blah";
    application.greeting = "blah blah blah";
    application.welcome = "blah blah blah";
}
```
# Segregating your configuration with Profiles

## Profiles 

Parts of your application can be segregated for different environment

```java
@Configuration
@Profile({"eng"})
public class EnglishMessageService{
    // blah blah blah 
}
```

## Adding Active Profiles

Can be used to do multiple database connection or other connection. 

- `Spring.profiles.active`: Sets active profile
- `Spring.profiles.include`: Adds additional profiles to profile.
- `SpringApplication.setAdditionalProfiles(...)`: can be used programmatically.
- `spring.profiles.active = name_of_profile`: Activate properties. 
- `Application-default.properties`: are loaded by default.

# Implementing Logs to Diagnose Errors

- Level, pattern and console/file output can be configured for Logback, JUL, and Log4j2. 
- Common log level are `FATAL`, `ERROR`, `WARN`, `INFO`, `DEBUG` and `TRACE`.
- `ERROR`, `WARN` and `INFO` are logged to console by default. 
- Common Configuration Options


|Name|Function|
|---|---|
|logging.config| Native config file of the logging framework|
|logging.exception-conversion-word|Marker for exception logging; the default is %wEx|
|logging.file| Filename to be logged into|
|logging.path| Path of generated log file|
|logging.level.\*| Level of a logger|
|logging.pattern.console| Pattern used for logging into the console (only logback)|
|logging.pattern.file| Pattern for logging into a file(only logback)|
|logging.pattern.level| Pattern used for log level (only logback)|
|logging.register-shutdown-hook| Flag for whether to register a hook that shuts down the logging subsystem with the application|



- Dependent on the chosen logger we change the following config file: 


|Logger|Config File|
|---|---|
|Logback| Logback-spring.xml, logback-spring.groovy, logback.xml, logback.groovy|
|Log4j2|log4j-spring.xml, log4j2.xml|
|JUL| logging.properties|


