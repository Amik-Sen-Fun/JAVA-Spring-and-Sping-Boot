# What is Maven?

- It is build tool for process of building a project.

- It is writen in JAVA or C#.

- Every Maven project has a `pom.xml` file which stands for project object model file.

- Apart from thet every maven project has a :
  - `src` folder that contains the production code inside `main` and inside it the `java` folder contains it
  - `test` folder that contains the test source code

# Structure of a `pom.xml` file:

- First we have the `groupID`, `artifactID` and `version` which is standard info that we look. in maven repository once we upload our project there.

- Next we have packing details, in our case it is a `jar` file

- Next we have the `build` section where we add `plugins`. Adding a plugin is similar to adding a dependecy and refer documentation. 

- Lastly we have the `dependecy` tag components that are the external dependecies that we would be needing to run the project. Simple copy dependency from repo in the pom file to add one.

# Maven Project commands

- To package a maven project into a JAR file write : `mvn package`
- To look inside the JAR file do : `jar tvf ..location.jar`
- To clean a maven project and remove the created files do : `mvn clean`
- To test a maven project do : `mvn test`
- To just compile the producton code and install newly defined dependencies do : `mvn compile`
- To compile the test code dp : `mvn test-compile`
- To install a mavin project do: `mvn install` 
- To see the dependency tree of a maven project do: `mvn dependency:tree`

# Different Invocation mode in Maven

- We can invoke maven through
    - `mvn phase`: phase can be test, compile 
    - `mvn plugin:goal`: plugin example can be archtype and goal generate so command becomes `archetype:generate`

# Supper POM and Effective POM

- With every maven installation we have a `Super pom file` inside the installation folder inside `lib` and `maven-model-builder-x.x.y.jar` file.

- The Effective POM = Super POM + the POM file we will write for a project. 

# Build life cycle in Maven

There are three lifecycle method: 

- Clean Lifecycle 
- Default Lifecycle : Always run by default 
- Site Lifecycle

See details in documentation 


