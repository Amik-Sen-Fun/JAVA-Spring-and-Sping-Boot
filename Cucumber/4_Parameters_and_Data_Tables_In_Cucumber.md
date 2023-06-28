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

- Now for multiple values as parameter in a step we create a step data table. 

```java
@P149 // tag name 
Scenario: Advance Search an Item 
  Given I am at Website home page
  When I need to advanced search an item 
    | keyword | exclude | min | max |
    | Iphone9 |  new    | 10  | 200 | 
```

- To use this step datatable in java do 

```java
  @When("I need to advanced search an item") // case sensitive 
  public void I_need_to_advanced_search_an_item(DataTable datatable){
    
    // to access the data table do
    datatable.cell(row, col) // give numeic value to row and col with 0 indexing with 0 row as headers
  }
```

# Scenario Outline Table

```java
@P149 // tag name 
Scenario Outline: Home page link
  Given I am at Website home page
  When I click on '<link>' 
  Then Validate that '<url>' is navigated and Title contains '<name>'
  
Examples:
    | link | url | name |
    | Iphone9 | new | 200 | // random shit example
```

Do `dryRun` get snippet and write code accordinly. 
