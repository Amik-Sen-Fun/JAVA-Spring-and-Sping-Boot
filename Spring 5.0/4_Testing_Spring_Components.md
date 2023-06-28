# Testing plan: `@Service` components

## Writing Integration Tests

As an integration test it involves the interaction between some service and some data access components. 

So we need to ask JUnit to :
- Not load `@Controllers`
- Only load `@Service` and dependencies
    - Example `@DataRepository`

```java
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.None)
public class SomeIntegrationTest {
    // some code

    // Assertion codes
    assertNotNull(value); // checks whether value is null or not 
    assertEquals(value1, value2); // checks whether value1 and value2 are equal or noot
}
```


