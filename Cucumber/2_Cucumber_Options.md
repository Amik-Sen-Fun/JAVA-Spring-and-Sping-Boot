# Features, Glue and Plugin

Inside the test file

```java
@RunWith(Cucumber.class)
@CucumberOptions(
  features = {'featueres'}, 
  glue = {'steps'}, 
  plugin = {"pretty", "html: Report"}
)
// feature contains the location of the feature file
// glue contains step location
// plugin generates a test report in HTML, Json or Junit file
```

# dryRun

```java
@RunWith(Cucumber.class)
@CucumberOptions(
  features = {'featueres'}, 
  glue = {'steps'}, 
  plugin = {"pretty", "html: Report"},
  dryRun = true, 
)
// If true then checks whether step definitions ae present along with features
// If not, it shows them 
```

# strict

```java
@RunWith(Cucumber.class)
@CucumberOptions(
  features = {'featueres'}, 
  glue = {'steps'}, 
  plugin = {"pretty", "html: Report"},
  dryRun = true, 
  strict = true,
)
// Makes it compulsary to add steps to scenarios else, it is failed
```

# monochrome

if true, displays outputs in a clean format

# tags

Inside the feature file we can define tags as:

```java
@P1 @P2   // tag name
Scenario: Search item count  
Given I am at Website home page
When I search of 'IPhone 6s'
Then I validate atleast 1000 items are present 
```

To run tests for a particular tag we use the `tags` option

```java
@RunWith(Cucumber.class)
@CucumberOptions(
  features = {'featueres'}, 
  glue = {'steps'}, 
  plugin = {"pretty", "html: Report"},
  dryRun = true, 
  strict = true,
  monochrome = true, 
  tags = {"@P1"}
)
```

# name

Runs only if the keyword written in `name` is part of a scenario in all feature files

```java
@RunWith(Cucumber.class)
@CucumberOptions(
  features = {'featueres'}, 
  glue = {'steps'}, 
  plugin = {"pretty", "html: Report"},
  dryRun = true, 
  strict = true,
  monochrome = true, 
  name = {"Logo"}
)
// runs only if the keyword written in name is part of a scenario 
```
