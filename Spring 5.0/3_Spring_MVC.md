# Introduction
Some **Advantages** of JSP:
- Directly handled requests from browsers
- Made use of model containing simple JAVA beans
- performs queries to database
- handles logic flow 

Some **Disadvantages** of JSP: 
- complex JSPs
- Hardly seperation of concerns

Model 2 Architecture of JAVA:
- **Model**: Contains the data that is viewed and manages by the view section
- **View**: Use the model to render the screen
- **Controller**: Controls the flows and populates the model

Some other features:
- Requests are handled by different `servlets`
- Proper authorization can be ensured

In front controller method: The front controller takes request and distributes over servlets. 
Some other responsibilites of the front controller: 
- Usually called the Dispatcher servlet because of this service distribution feature
- Provides provision to add common functionality
- Decides which view to render

`<mvc:annotation-driven>` feature:
- Request mapping
- Exception handling
- Data binding and validation
- Automatic conversion - when `@RequestBody` is used

# MVC Architecture

- Example of Request mapping, controller and request body
  ```java
  @Controller
  public class BasicController{
    @RequestMapping( value = "/welcome")
    @ResponseBody
    public String welcome(){
      return "Welcome to MVC";
    }
  }
  ```
  
- Example to set values in the model
  ```java
  @Controller
  public class BasicController{
    @RequestMapping( value = "/welcome", method = RequestMethod.GET) // to be invoked only for GET method 
    @ResponseBody
    public String welcome(ModelMap model){
      model.put("name", "Amik"); // In JSP file access this value as `${name}`
      return "Welcome model map";
    }
  }
  ```
  
- Example of a POJO (Plain Old Java Object) form
  ```java
  public class User{
    
    private String guid;

    @Size(min = 6, message = "atleast enter 6 characters")
    private String name; 
  }
  ```

Some other validators:
- `@NotNull`
- `@Pattern`
- `@Size`
- `@Max`
- `@Min`
- `@Past`
- `@Future`

# Important concepts behing MVC architecture

- **Request Mapping** is used to map URI/URL to controller
  - Done at class or method level
  - Optional methods like GET, POST, PUT

- Types of arguments
  - ..ModelMap : Maps data with controller 
  - ..BindingResult : For validators
  - @PreDestroy : Used to free resources that were allocated before
  - @RequestParam: To access specific HTTP request parameters
  - @RequestHeader: To access specific HTTP request headers
  - @SessionAttribute: To access HTTP session parameters
  - @RequestAttribute: To access specific HTTP request attributes
  - @PathVariable: Access variables from the URI template
 
- Some Rules:
  - **Implicite enriching of model**: Model is part of return type - enriched with command object and results are added to model.
  - **Implicite determination of view**: if view is not given, `DefaultRequestToViewNameTranslater`

- Return Types
  - ModelAndView
  - View
  - Model
  - String
  - Map

- View resolution
  - Direct generation of JSON, XML or atom
  - For multiple view resolution we have following strategies:
    - XmlViewResolver
    - UrlBasedViewResolver
    - ResourceBundleViewResolver
    - ContentNegotiatingViewResolver

# Handler Mapping and Interceptors

- Mapping between URL and controller is done by handler mapping
- Handler Intercepter are used to intercept requests to handlers
- Logs the content of request and response

- Overriding Methods in Handler Interceptor Adapter
  - ```java
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object Handler){
        // blah blah 
    }
    ```
  - ```java
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object Handler, ModelAndView modelAndView){
        // blah blah 
    }
    ```
  - ```java
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object Handler, Exception Ex){
        // blah blah 
    }
    ```

  - `InitBinder`
