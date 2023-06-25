# Introduction

- TDD: Test cases are developed even before the software. Software is developed to pass these given test cases.
  - Stakeholders should know some language to understand the test cases developed.
   
- BDD: **Behavior Driven Development** inspired from TDD (Test Driven Development), but:
  - It contains a feature file that contains the test cases in human understandable language
  - Format of a Behaviour:
  ```cucumber
  Scenario: Search item count  // some scenario
  Given I am at Website home page
  When I search of 'IPhone 6s'
  Then I validate atleast 1000 items are present 
  ```

  # Creating a Maven Cucumber Project

  - Create a maven project. In the `pom.xml` file of the project get the dependecy of :
    - **Cucumber-junit dependency**:
    ```xml
    <!-- https://mvnrepository.com/artifact/io.cucumber/cucumber-junit -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-junit</artifactId>
        <version>7.11.0</version>
        <scope>test</scope>
    </dependency>
    ```
   - **Cucumber-java dependency**:
    ```xml
    <!-- https://mvnrepository.com/artifact/io.cucumber/cucumber-java -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>7.11.2</version>
    </dependency>
    ```
    - **Cucumber-picocontainer dependency**:
    ```xml
    <!-- https://mvnrepository.com/artifact/io.cucumber/cucumber-picocontainer -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-picocontainer</artifactId>
        <version>7.11.2</version>
    </dependency>
    ```
    - **Serenity-Cucumber dependency**:
    ```xml
    <dependency>
        <groupId>net.serenity-bdd</groupId>
        <artifactId>serenity-cucumber</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>
    ```

> For Eclipse installation just go to store and install cucumber and restart Eclipse. In configure option, do it as a cucumber project

# Creating the Feature file in Cucumber 

- Create a seperate folder named `features` in the project.
- Inside that create a `something.feature` file for writting features.
- Gherkin scenarios are written in a feature file. It has the following format:
  ```
  Feature: Website Homepage Scenario // case sensitive commands
  Scenario: Search item count  // some scenario
  Given I am at Website home page
  When I search of 'IPhone 6s'
  Then I validate atleast 1000 items are present 
  ```
- Now we write the step definition, first run the code, it will generate a snippt. Inside the `src/test/java` create a new `Java Package` inside it create a new **class**, say `Website Home Steps` and paste the snippet there.

# Creating a jUnit test runner 

- Inside the `src/test/java` create a new `Java Package` inside it create a new **class**, say `Test`.
- Include the annotations:
  ```java
  @RunWith(Cucumber.class)
  @CucumberOptions(
    features = {'featueres'}, 
    glue = {'steps'}, 
  )
  // glue contains step location
  ``` 
