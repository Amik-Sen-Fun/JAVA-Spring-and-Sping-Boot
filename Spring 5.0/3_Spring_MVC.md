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
    @RequestMapping( value = "/welcome")
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
-   
