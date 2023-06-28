# Parameters in Cucumber 

## String 

In feature file keep the varaible string inside single quotes as `'Some string variable'`

```java
  @When("I search for {string}") // case sensitive 
  public void func_2(String str){
    driver.findElement(By.linkText(str)).click();
    // access the variable here 
  }
```

## Integer 

```java
@Then("I have atleast {int} results ")
  public void func_3(int count){
    // access the variable here 
  }
```

# Step Data table

Now for multiple values as parameter in a step we create a step data table. 
