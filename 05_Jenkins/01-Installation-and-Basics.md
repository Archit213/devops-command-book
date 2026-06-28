# Jenkins Installation & Basics
---

# Table of Contents

- What is Jenkins?
- CI/CD Overview
- Application Testing
- Jenkins Installation
- Initial Jenkins Setup
- Command Reference
- Practical Exercises

---

# What is Jenkins?

Jenkins is an open-source automation server used to automate building, testing, and deploying applications.

---

# CI/CD Overview

| CI (Continuous Integration) | CD (Continuous Delivery) | Continuous Deployment |
|-----------------------------|--------------------------|-----------------------|
| Automatically builds and tests code after every commit | Keeps software ready for deployment | Automatically deploys after successful testing |

---

# Sample Go Application

According to the notes, the sample application contains:

- `main.go`
- `controller/`
- Unit tests

---

# Run the Application

## Command

```bash
go run main.go
```

### Description

Compiles and runs the Go application.

### Example

```bash
go run main.go
```

---

# Run Unit Tests

## Command

```bash
go test -v
```

### Description

Runs all Go unit tests in verbose mode.

### Example

```bash
cd controller
go test -v
```

### Sample Output

```text
=== RUN   TestHomePage
--- PASS: TestHomePage
PASS
ok      sample-app/controller
```

---

# Jenkins Installation

## Step 1 – Connect to the Server

```bash
ssh username@public_ip
```

### Description

Connects to the remote Linux server where Jenkins will be installed.

---

## Step 2 – Update Package Repository

```bash
sudo apt update -y
```

### Description

Updates the local package index.

---

## Step 3 – Install Java

```bash
sudo apt install openjdk-11-jdk
```

### Description

Installs OpenJDK 11, which is required to run Jenkins.

---

## Verify Java Installation

```bash
java -version
```

### Sample Output

```text
openjdk version "11"
```

---

## Step 4 – Add Jenkins Repository Key

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key
```

### Description

Downloads the Jenkins GPG key.

> **Note:** Follow the latest Jenkins documentation to add the repository correctly, as the installation method may change over time.

---

## Step 5 – Install Jenkins

```bash
sudo apt install jenkins
```

### Description

Installs the Jenkins package.

---

## Step 6 – Start Jenkins Service

```bash
sudo systemctl start jenkins
```

### Description

Starts the Jenkins service.

---

## Step 7 – Enable Jenkins at Boot

```bash
sudo systemctl enable jenkins
```

### Description

Configures Jenkins to start automatically after a system reboot.

---

## Step 8 – Check Jenkins Status

```bash
sudo systemctl status jenkins
```

### Description

Displays the current status of the Jenkins service.

### Sample Output

```text
Active: active (running)
```

---

## Step 9 – Allow Jenkins Through Firewall

```bash
sudo ufw allow 8080
```

### Description

Allows incoming traffic on Jenkins' default port.

---

## Verify Firewall Rules

```bash
sudo ufw status
```

---

## Step 10 – Retrieve Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### Description

Displays the initial administrator password required to unlock Jenkins.

---

# Access Jenkins

Open a web browser and navigate to:

```text
http://<SERVER_IP>:8080
```

Paste the password retrieved in the previous step.

---

# Command Reference

| Command | Description |
|----------|-------------|
| `go run main.go` | Run the Go application |
| `go test -v` | Execute Go unit tests |
| `ssh username@public_ip` | Connect to remote server |
| `sudo apt update -y` | Update package index |
| `sudo apt install openjdk-11-jdk` | Install Java |
| `java -version` | Verify Java installation |
| `wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key` | Download Jenkins GPG key |
| `sudo apt install jenkins` | Install Jenkins |
| `sudo systemctl start jenkins` | Start Jenkins service |
| `sudo systemctl enable jenkins` | Enable Jenkins at boot |
| `sudo systemctl status jenkins` | Check Jenkins status |
| `sudo ufw allow 8080` | Open Jenkins port |
| `sudo ufw status` | Display firewall rules |
| `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` | Retrieve Jenkins admin password |

---

# Practical Exercises

## Exercise 1 – Run the Sample Application

```bash
go run main.go
```

---

## Exercise 2 – Execute Unit Tests

```bash
go test -v
```

---

## Exercise 3 – Install Jenkins

```bash
sudo apt update -y
sudo apt install openjdk-11-jdk
sudo apt install jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

---

# Summary

This chapter covered:

- Jenkins overview
- CI/CD basics
- Running a Go application
- Running Go tests
- Installing Java
- Installing Jenkins
- Starting Jenkins
- Enabling Jenkins at boot
- Opening port 8080
- Retrieving the initial admin password