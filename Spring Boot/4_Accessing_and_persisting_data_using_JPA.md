# Defining Spring Data

Features of **Spring Data**: 

- It provides a familiar, consistent, Spring-based programming model for data access. 
- Powerful repository and custom object-mapping abstractions. 
- Dynamic query derivation from repository method names. 
- Implement domain base classes, provide basic properties. 
- Support for transparent auditing (created, last changed)
- Possibilty to integrate custom repository code
- Advanced integration with Spring MVC controllers
- Experimental support for cross-store persistence 

## Relational Databases

Access to relational databases is realised with these starters: 

- `spring-boot-starter-data-jpa`
- `spring-boot-starter-jdbc`
- `spring-boot-starter-jooq`
- A driver starter (MySQL, or postgres)


Spring Boot provides auto-configuration for MongoDB, Neo4j, Elasticsearch etc. 

## Database initialization 

- Spring Data JPA uses Hibernate as a default JPA implementation 
- It uses the domain model of your application to derive a schema. 

Steps for Creating Database Initialization:

- Annotate your classes with `@Entity @Table(name = "nameOfYourTable")`
- Annotate your attributes with `@Column(name = "nameOfYourColumn")`
- Annotate your application class with
    `@EnableJpaRepositories("com.demo.app")`;

- Add these entries to your `application.properties` file: 
    - `spring.jpa.generate-ddl = true;`
    - `spring.jpa.hibernate.ddl-auto = create;`
    - `spring.datasource.url = jdbc:mysql://localhost:3306/test.`


There are three ways to interact with your database: 
- jdbcTemplate
- JPA
- JOOQ (Java Object Oriented Querying)

```java
// blah blah blah 
spring.datasource.username = something
spring.datasource.password = XXXXX
spring.datasource.driver-class-name = com.mysql.jdbc.Driver
```

# Using Plain and Simple SQL with JDBC Template

- Create an interface with methods 
- Create an implementation of this interface
- Use JDBCTemplate 

```java
@Service 
public class PersonServiceImpl implements PersonService{

    @Autowired
    private JdbcTemplate jdbcTemplate;


    @Override
    public void addPerson(Person person){
        Long pid = 0; 
            
        String maxB = "SELECT * FROM ABC";
        
        pid = jdbcTemplate.query(maxB, new ResultSetExtractor<Long>(){
    
            @Override
            public Long extractData(ResultSet rs) throws SQLException, DataAccessException{
                long maxid;
                rs.next();
                maxid = rs.getLong(1);
                return maxid;
            }
        })
    }
}
```
# Using JPA for Managing Relation Data

- It provides complete abstraction over the DAO layer
- It uses JPA for mapping DAO objects. 

#### Relations between Tables:

Methods
- @OneToOne
- @ManyToOne
- @OneToMany
- @ManyToMany
- Table contact - mappedBy attribute to the relation
- Table person - @JoinColumn annotation with the joining id information 

```java
import javax.persistence.Table;

@Entity
@Table(name = "Person")
public class Person{
    
    @Id
    @GenerateValue(startegy GenerationType.AUTO)
    private int id; 

    @Column(name = "firstname", length=20, nullable=false)
    private String firstName;

    // blah blah blah
}
```
# JPA with NoSQL Databases

```java
public interface MyRepository extends MongoRepository{
    @Query("("{'lastname': ?0 }")")
    public List<Person> findByLastName(String lastname){
        // blah blah blah
    }
}
```







