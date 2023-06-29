# Request Processing in Spring Web MVC

# Configuring Paths for stylesheets and images in a MVC application 

- Inside the `static` folder inside `src\main\resources` add two folders namely:
    - `css`: to add the stylesheets
    - `img`: to add images that would be used in the application 

- Now to access these folders in the application. Inside `src\main\java`
    - Add a package with some name `com.example.demo` say, inside it define a class `WebConfig` which MVC Web configuration (in the add option). 
    ```java
    public class WebConfig implements WebMvcConfigurer{
    
        @Override
        public void addResourceHandlers(ResourceHandlerRegistry registry){
            registry.addResourceHandler("/css/**").addResourceLocation("/css");
            registry.addResourceHandler("/img/**").addResourceLocation("/img");
        }
    }
    ``` 

# Creating the view and the controller

## Views

- Views can be in HTML, JSP or other format.
- In general, we use template engine such as Thymeleaf, FreeMarker, Mustache or Groovy
- If you are mixing then build your own view resolver
- You can have multiple controller as well.

## Controller 

- Controllers deal with requests and parameters.
- Marked with `@Controller` or `@RestController`
- Known HTTP verbs that can be handled are: 
    - GET
    - POST
    - PUT
    - DELETE

## How to do so?

- First set your HTML file in the templates folder. 

- Now make a `package` and inside it define a `webController` class.

- Above the class give an annotation of `@Controller` 

- Now define a function inside the class and give annotation of `@RequestMapping` to habdle requests. 

```java
public class webController{
    @RequestMapping("/")
    public String index(){
        return "index"; 
    }
}
```

- Now inside package define a class `UserGreeting` which will be a `Model` class.
    - For each `Model` we need to define a getter and setter. 
    ```java
    public class UserGreeting{
        private String name;
        
        // getter
        public String getName(){
            return name;
        }

        // setter
        public void setName(String name){
            this.name = name;
        }
    }
    ```

- Now we change the Controller in order to get and post methos to this model. 

```java
public class webController{
    @GetMapping("/")
    public String index(Model model){
        model.addAttribute("userGreeting", new UserGreeting());
        return "index";
    }
    
    @PostMapping("/")
    public String index(@ModelAttribute("userGreeting") UserGreeting newUser, Model model){

        model.addAttribute("user", newUser.getName());
    }

}
```

- In the HTML file we have defined a form for get or post methods. We will define the HTML file as: 
    - Since we are using Thymeleaf template we are using some specific syntax to write functions
```html
<form action="#" method="POST" th:object="${userGreeting}" th:action="@/">
    Your Name: <input type="text" th:field="*{name}"/>
    <input type="submit" value="Greet!"/>
</form>

<th:block th:if="${user!=null}">

<p> Hello <span th:utext"${user}"></span> </p>

</th:block>
```

# Using Starters and Defining the Entry Point 

## Starter

- Starters are a set of dependencies descriptors 
- Easy to access technologies 
- Example:
    - `spring-starter`
    - `spring-starter-web`
    - `spring-starter-thymeleaf`

## Entrypoint

Entrypoint of our application is defined as :

```java
// The entry point is the main method

@SpringBootApplication
public class XXXApplication{
    public static void main(Strin[] args){
        SpringApplication.run(XXXApplication.class, args);
    }
}
```
# Testing your application 

Packages that could be used for testing:

- Junit
- Spring test and Spring boot test: for utilities and integration test 
- AssertJ
- Hamcrest: of matcher object
- Mockito
- JSONassert: assertion library for JSON
- JSONPath: XPath for JSON

## Unit Test

- Single Components work according to theor specifications

## Integration Test
- Components work together as a whole or not 
- Example:
    - `@RunWith(SpringRunner.class)`
    - `@SpringBootTest`
    - `@AutoConfigureMockMvc`

