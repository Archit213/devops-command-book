# Application Basics: Node.js Environments
------------------------------------------------------------------------

# Table of Contents

-   What is Node.js?
-   Why Node.js?
-   NPM
-   Local vs Global Packages
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What is Node.js?

Node.js is an open-source, cross-platform JavaScript runtime built on
Google's V8 engine. It allows JavaScript to run outside the browser and
is widely used for backend APIs, automation, microservices, and DevOps
tooling.

------------------------------------------------------------------------

# Why Node.js?

-   Event-driven and non-blocking
-   Excellent for REST APIs
-   Large npm ecosystem
-   Cross-platform
-   Fast development

------------------------------------------------------------------------

# What is NPM?

**NPM (Node Package Manager)** is the default package manager for
Node.js. It installs, updates, and manages project dependencies defined
in `package.json`.

## Local vs Global Installation

  Installation    Scope
  --------------- --------------------------------------------------------
  Local           Available only in the current project (`node_modules`)
  Global (`-g`)   Available system-wide

------------------------------------------------------------------------

# Command Reference

## 1. Check Node.js Version

``` bash
node -v
```

Displays the installed Node.js version.

Example:

``` bash
node -v
```

Expected Output:

``` text
v22.x.x
```

------------------------------------------------------------------------

## 2. Run a JavaScript File

``` bash
node app.js
```

Executes a JavaScript application.

Example:

``` bash
node server.js
```

------------------------------------------------------------------------

## 3. Check NPM Version

``` bash
npm -v
```

Displays the installed npm version.

------------------------------------------------------------------------

## 4. Search Packages

``` bash
npm search express
```

Searches the npm registry for matching packages.

------------------------------------------------------------------------

## 5. Install a Package Locally

``` bash
npm install express
```

Downloads Express into the project's `node_modules` directory and
updates dependencies.

------------------------------------------------------------------------

## 6. Install Project Dependencies

``` bash
npm install
```

Reads `package.json` and installs all required dependencies.

------------------------------------------------------------------------

## 7. Execute Inline JavaScript

``` bash
node -e "console.log(module.paths)"
```

Runs JavaScript directly from the terminal.

Expected Output:

``` text
[
 '/project/node_modules',
 '/node_modules'
]
```

------------------------------------------------------------------------

## 8. Install a Package Globally

``` bash
npm install express -g
```

Installs Express globally.

------------------------------------------------------------------------

# Practical Exercises

## Create a Simple Application

``` bash
echo "console.log('Hello Node.js');" > app.js
node app.js
```

## Initialize and Install Dependencies

``` bash
npm init -y
npm install express
```

## Install Existing Project Dependencies

``` bash
git clone <repository>
cd <repository>
npm install
```

------------------------------------------------------------------------

# Best Practices

-   Use local packages for application dependencies.
-   Commit `package.json` and `package-lock.json`.
-   Avoid unnecessary global packages.
-   Use `npm install` after cloning a project.

------------------------------------------------------------------------

# Common Mistakes

-   Forgetting to run `npm install`.
-   Mixing local and global package usage.
-   Deleting `package-lock.json` accidentally.
-   Running scripts from the wrong directory.

------------------------------------------------------------------------

# Interview Questions

### What is Node.js?

A JavaScript runtime used to build server-side applications.

### What is npm?

The default package manager for Node.js.

### Difference between `npm install` and `npm install express`?

-   `npm install` installs all dependencies from `package.json`.
-   `npm install express` installs only the Express package.

### What does `node -e` do?

Executes JavaScript code directly from the command line.

------------------------------------------------------------------------

# Summary

This chapter covered:

-   Node.js fundamentals
-   NPM
-   Local vs global packages
-   Running JavaScript applications
-   Installing dependencies
-   Package management
