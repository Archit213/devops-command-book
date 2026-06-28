# Application Basics: Java Development & Build Pipelines
------------------------------------------------------------------------

# Table of Contents

-   What is Java?
-   JDK vs JRE vs JVM
-   Java Build Process
-   Build Tools
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What is Java?

Java is an object-oriented programming language used to build
cross-platform applications. Java code is compiled into **bytecode**,
which runs on the **Java Virtual Machine (JVM)**.

------------------------------------------------------------------------

# JDK vs JRE vs JVM

  Component   Purpose
  ----------- -----------------------------------------------
  JDK         Development kit containing compiler and tools
  JRE         Runtime environment to run Java programs
  JVM         Executes Java bytecode

------------------------------------------------------------------------

# Java Build Process

``` text
MyClass.java
      │
   javac
      │
MyClass.class
      │
     JVM
      │
Application Runs
```

------------------------------------------------------------------------

# Build Tools

-   **Ant** -- XML-based build automation.
-   **Maven** -- Dependency management and build lifecycle.
-   **Gradle** -- Flexible build automation with Groovy/Kotlin DSL.

------------------------------------------------------------------------

# Command Reference

## 1. Extract JDK Archive

``` bash
tar -xvf openjdk.tar.gz
```

Extracts a compressed JDK archive.

Example:

``` bash
tar -xvf openjdk-21_linux-x64_bin.tar.gz
```

------------------------------------------------------------------------

## 2. Check Java Version

``` bash
java -version
```

Displays the installed Java runtime version.

------------------------------------------------------------------------

## 3. Compile Java Source

``` bash
javac MyClass.java
```

Compiles a Java source file into bytecode.

------------------------------------------------------------------------

## 4. Run a Java Class

``` bash
java MyClass
```

Executes the compiled `.class` file.

------------------------------------------------------------------------

## 5. Create a JAR File

``` bash
jar -cf myApp.jar *.class
```

Packages compiled classes into a JAR archive.

------------------------------------------------------------------------

## 6. Run a JAR File

``` bash
java -jar myApp.jar
```

Runs an executable JAR.

Expected Output:

``` text
[INFO] Starting Spring Boot Application...
```

------------------------------------------------------------------------

## 7. Generate Documentation

``` bash
javadoc -d doc MyClass.java
```

Creates HTML documentation from Java source comments.

------------------------------------------------------------------------

## 8. Build with Ant

``` bash
ant compile
ant jar
```

Runs Ant targets defined in `build.xml`.

------------------------------------------------------------------------

## 9. Build with Maven

``` bash
mvn package
```

Downloads dependencies, runs tests, compiles code, and packages the
application.

------------------------------------------------------------------------

# Practical Exercises

## Compile and Run

``` bash
javac Hello.java
java Hello
```

## Package a JAR

``` bash
jar -cf hello.jar *.class
java -jar hello.jar
```

## Build with Maven

``` bash
mvn clean package
```

------------------------------------------------------------------------

# Best Practices

-   Keep the JDK up to date.
-   Use Maven or Gradle for dependency management.
-   Store source code under version control.
-   Generate Javadocs for public APIs.

------------------------------------------------------------------------

# Common Mistakes

-   Running `java` before compiling with `javac`.
-   Forgetting to include dependencies.
-   Using the JRE instead of the JDK for development.

------------------------------------------------------------------------

# Interview Questions

### What is the difference between JDK, JRE, and JVM?

-   JDK: Development tools.
-   JRE: Runtime environment.
-   JVM: Executes bytecode.

### What does `javac` do?

Compiles `.java` files into `.class` bytecode.

### What does `mvn package` do?

Builds the project, resolves dependencies, runs tests (depending on
configuration), and creates a deployable package.

------------------------------------------------------------------------

# Summary

This chapter covered:

-   Java architecture
-   JDK, JRE, JVM
-   Java compilation
-   JAR packaging
-   Javadoc generation
-   Ant
-   Maven
