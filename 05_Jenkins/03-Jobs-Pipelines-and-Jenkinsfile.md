# Jenkins Jobs, Pipelines & Jenkinsfile
---

# Table of Contents

- Jenkins Jobs
- Freestyle Project
- Pipeline Project
- Pipeline Concepts
- Jenkinsfile
- Declarative Pipeline
- Multi-Stage Pipeline
- Go Plugin
- Docker Plugin
- Build Pipeline Example
- Command Reference
- Practical Exercises

---

# Jenkins Jobs

A **Job** is a task Jenkins executes automatically.

Common job types:

- Freestyle Project
- Pipeline
- Multi-Branch Pipeline

---

# Freestyle Project

A Freestyle Project is the simplest Jenkins job.

## Create a Freestyle Job

1. Dashboard
2. New Item
3. Enter Job Name
4. Select **Freestyle Project**
5. Click **OK**

---

## Configure Source Code

Example:

Git Repository

```text
https://github.com/user/sample-app.git
```

Branch

```text
main
```

---

## Build Step

Example

Execute Shell

```bash
go test -v
```

or

```bash
go run main.go
```

Click

```text
Save

↓

Build Now
```

---

# Pipeline Project

Pipeline Jobs define the complete CI/CD workflow using a **Jenkinsfile**.

Advantages

- Version Controlled
- Repeatable
- Easy to maintain
- Supports multiple stages

---

# Pipeline Workflow

```text
GitHub

↓

Checkout

↓

Build

↓

Test

↓

Deploy
```

---

# Create a Pipeline Job

1. Dashboard
2. New Item
3. Enter Job Name
4. Pipeline
5. OK

---

# Pipeline Script

Pipeline can be written

- Directly in Jenkins
- Inside a Jenkinsfile

Recommended:

Store the Jenkinsfile inside the Git repository.

---

# Declarative Pipeline

Basic syntax

```groovy
pipeline {

    agent any

    stages {

    }

}
```

---

# Pipeline Keywords

| Keyword | Purpose |
|----------|----------|
| pipeline | Defines the pipeline |
| agent | Defines where pipeline runs |
| stages | Collection of stages |
| stage | Individual phase |
| steps | Commands executed in the stage |

---

# Agent

Runs the pipeline on any available Jenkins node.

```groovy
agent any
```

---

# Stage

Stages divide work into logical sections.

Example

```text
Build

↓

Test

↓

Deploy
```

---

# Steps

Commands executed inside each stage.

Example

```groovy
steps {

    sh 'go test -v'

}
```

---

# Complete Pipeline Example

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Building Application'

            }

        }

        stage('Test') {

            steps {

                sh 'go test -v'

            }

        }

        stage('Deploy') {

            steps {

                echo 'Deploying Application'

            }

        }

    }

}
```

---

# Multi-Stage Pipeline

```text
Checkout

↓

Build

↓

Unit Test

↓

Package

↓

Deploy
```

Each stage executes sequentially.

If one stage fails,

remaining stages stop.

---

# Jenkinsfile

A **Jenkinsfile** stores the pipeline configuration inside the project repository.

Advantages

- Version Controlled
- Easy collaboration
- Pipeline as Code

Typical repository

```text
project/

├── Jenkinsfile

├── main.go

├── go.mod

└── controller/
```

---

# Build Go Application

Example

```groovy
pipeline {

    agent any

    stages {

        stage('Test') {

            steps {

                sh 'go test -v'

            }

        }

    }

}
```

---

# Go Plugin

The Go Plugin allows Jenkins to configure Go automatically.

Configuration

```text
Manage Jenkins

↓

Tools

↓

Go Installations
```

---

# Docker Plugin

Docker Plugin allows Jenkins to build Docker images.

Typical Docker build command

```bash
docker build -t sample-app .
```

Pipeline example

```groovy
pipeline {

    agent any

    stages {

        stage('Docker Build') {

            steps {

                sh 'docker build -t sample-app .'

            }

        }

    }

}
```

---

# Pipeline Execution

Click

```text
Build Now
```

Monitor progress

```text
Build History

↓

Console Output
```

---

# Common Pipeline Flow

```text
Developer Push

↓

GitHub

↓

Jenkins Trigger

↓

Checkout

↓

Build

↓

Test

↓

Docker Build

↓

Deploy
```

---

# Command Reference

| Command | Description |
|----------|-------------|
| `go run main.go` | Run Go application |
| `go test -v` | Execute Go tests |
| `docker build -t sample-app .` | Build Docker image |

---

# Jenkinsfile Reference

## Minimal Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Hello Jenkins'

            }

        }

    }

}
```

---

## Build and Test Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh 'go build'

            }

        }

        stage('Test') {

            steps {

                sh 'go test -v'

            }

        }

    }

}
```

---

## Build, Test and Docker Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh 'go build'

            }

        }

        stage('Test') {

            steps {

                sh 'go test -v'

            }

        }

        stage('Docker') {

            steps {

                sh 'docker build -t sample-app .'

            }

        }

    }

}
```

---

# Practical Exercises

## Exercise 1

Create a Freestyle Project.

Run

```bash
go test -v
```

---

## Exercise 2

Create a Pipeline Job.

Use

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Hello Jenkins'

            }

        }

    }

}
```

---

## Exercise 3

Modify the pipeline.

Add

- Build
- Test
- Docker Build

---

# Summary

This chapter covered

- Freestyle Jobs
- Pipeline Jobs
- Jenkinsfile
- Declarative Pipeline
- Pipeline Stages
- Agent
- Steps
- Go Plugin
- Docker Plugin
- Multi-Stage Pipelines
- Build Workflow