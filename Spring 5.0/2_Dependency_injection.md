# Lets try to understande Dependency Injection

- Say we have a class `BusinessService` which uses an instance of a class `DataService` and in omplemented as:
```java
public class BusinessService{
    public long calculation(User user){
      // some code 
      DataService Data = new DataService();
      // this Data instance is used later in the code somewhere
    }
} 
```

- Problems with this code:
  - Tight coupling of these classes
  - Unit testing is not easily possible of each class

- How to solve this problem?
  - **Create an interface of class `DataService` ** : Relatively loosely coupled code
  - Instead of `BusinessService` creating an instance of `DataService`, we create an instance somewhere
  else and pass it to `BusinessService`
  - Again create an interface of `BusinessService` to further loose coupling

# Spring IOC Container 

- It creates Beans and wire them together (Yes, I have no clue what that means as well :p)
- To create bean, spring framework requires annotations
  - `@Component`: Generic Way to define Beans
  - `@Service` : Business Component 
  - `@Repository` : Data Access Object Component
- To wire the beans, use the annotation
  - `@Autowired`  

# Creating a Spring IOC Container 

- It can be done by using a `Bean Factory` or `Application Context`
- An application context can be in
  - Java : To define a context in `Java` we use annotation of `@Configuration`. However, we have to do a scan to get the beans and wire in files.
  ```java
  @Configuration 
  @ComponentScan(basePackages = {"file_name"})
  class springContext{
      // blah blah code
    
      // write context 
      context = new AnnotationConfigApplicationContext(springContext.class);  // Defining context 
      BusinessService service = context.getBeans(BusinessService.class) // Get the beans 
  }
  ```
    
  - XML : We have an xml file with all the beans and standard template. 
  ```java
  class springContext{
      // blah blah code
    
      // write context 
      context = new ClassPathXMLApplicationContext(springContext.class);  // Defining context 
      BusinessService service = context.getBeans(BusinessService.class) // Get the beans 
  }
  ```

# Defining JUnit Using Spring Context

In this section we will learn about defining JUnits using Spring Context 

```java
import static org.junit.Assert.assertEqual; // import test functions 

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(location = {"/file_name.java"})
  
@Autowired
private BusinessService service

@Test
public void testFunction(){
  long sum = ..;// some logic 
  assertEquals(30, sum);
}
```

# Unit Testing with Mockito

We will see how to write unit test codes using Mockito in Java

```java
import static org.junit.Assert.assertEqual; // import test functions 

@RunWith(MockitoJUnitRunner.class)

public class MockitoTest{
  @Mock
  private DataService dataservice
  
  @InjectMocks
  private BusinessService service = new BusinessServiceInterface() // the interface for building BusinessService
  
  @Test
  public void testFunction(){
    BBDMockito.given(dataservice.retrieveData(.....) // Some code 
    long sum = ..;// some logic 
    assertEquals(30, sum);
  }
}
```

# Dependency Injection Types

- Setter Injection
    - Define a specific `setter` function to inject the value of an object to a function.
    - Comes with non-mandatory dependencies
  
- Constructor Injection 
    - The object is initialised inside the constructor method.
    - It comes with madatory dependencies

> If no independencies available for autowired field then it throws an exception

- Use `@Scope("singleton")` to set the scope of a bean, by default it is singleton

# `@Autowired` annotation

- While using `@Autowired` their are few possible outcomes:
  - One match found
  - More than one match found
  - No match found

In both the later cases, `@Autowired` fails. For **more than one matches** found can be resolved using:
- `@Primary`annotation: for the primary response 
- `@Qualifier`annotation: for further qualifying autowirings
  ```java
  @Qualifier("abc")
  // beans code

  // code .. . .. 
  
  // Some class component code
   @Qualifier("abc")
  ``` 
