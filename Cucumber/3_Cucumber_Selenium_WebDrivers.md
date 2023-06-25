# Preperations

- The serenity dependenct that we wrote, installed all selenium related dependency
- Create a folder `WebDriver` and keep the `chromewebdriver` executable there.

# Creation of Driver

- Inside the `steps` class where you want to make the driver write
 
```java
public class Steps{
  Webdriver = driver;

  @Given("I am at Website Home Page")
  public void func_1(){
    System.setProperty("web.chrome.driver", 'webDriver/chromedriver'); // second parameter is file location of driver
    driver = new ChromeDriver(); // define driver
    driver.get("https://www.google.com"); // go to link
  }

  @When("I click on search link")
  public void func_2(){
    driver.findElement(By.linkText("Search")).click();
  }

  @Then("I should be at search page")
  public void func_3(){
    String expURL = "https://www.google.com/search";
    String actURL = driver.getCurrentUrl();
    if(!expURL.equals(actURL)){
      fail("Page navigation failed");
    }
    driver.quit();
  }
}
```
# Cucumber Global Hooks 

- `@Before` hook : executed before `When`

- `@After` hook : executed after `Then`
  ```java
  public class Common_Steps{
    WebDriver driver;

    @Before
    public void setUp(){
      System.setProperty("web.chrome.driver", 'webDriver/chromedriver'); // second parameter is file location of driver
      driver = new ChromeDriver(); // define driver
    }

    @After
    public void tearDown() throws Exception {
      driver.quit();
      Thread.sleep(1000);
    }

    public WebDriver getDriver(){
      return driver; // to access the driver
    }
  }
  ```
- We are able to use this driver because we installed the dependency pico-container

  ```java
  // to use driver inside step file we do 
  public class Something{
    public Something(Common_Steps cs){
      this.driver = cs.getDriver();
    }
    // Common_Steps is what we defined in previous point 
  }
  ```
