# Jenkins Dashboard, Plugins & CLI
---

# Table of Contents

- Unlock Jenkins
- Initial Setup
- Jenkins Dashboard
- Plugin Manager
- Installing Plugins
- Restart Jenkins
- Jenkins CLI
- SSH Authentication
- Command Reference
- Practical Exercises

---

# Unlock Jenkins

After installing Jenkins, open your browser:

```text
http://<SERVER_IP>:8080
```

Retrieve the administrator password.

## Command

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### Description

Displays the initial administrator password required to unlock Jenkins.

---

# Initial Setup

After entering the administrator password:

1. Click **Install Suggested Plugins**
2. Wait for plugin installation.
3. Create the first administrator account.
4. Save and Continue.
5. Save and Finish.
6. Start using Jenkins.

---

# Jenkins Dashboard

After logging in, the Jenkins Dashboard is displayed.

Important sections:

- New Item
- Build History
- Manage Jenkins
- Credentials
- People
- Build Queue
- Executor Status

---

## New Item

Used to create:

- Freestyle Project
- Pipeline
- Multi-Configuration Project
- Folder

---

## Build History

Displays

- Successful Builds
- Failed Builds
- Running Builds

---

## Workspace

Every job has its own workspace.

Typical location:

```text
/var/lib/jenkins/workspace/
```

The workspace stores:

- Source code
- Build artifacts
- Temporary files

---

## Configure

Allows modification of:

- Build Steps
- SCM
- Triggers
- Build Environment
- Post Build Actions

---

## Build Now

Immediately triggers a build.

Useful after modifying:

- Source Code
- Pipeline
- Build Configuration

---

## Console Output

Displays complete execution logs.

Useful for debugging:

- Build failures
- Test failures
- Shell script output
- Pipeline execution

---

# Plugin Manager

Navigate to:

```text
Manage Jenkins

↓

Plugins
```

Plugins extend Jenkins functionality.

Examples:

- Git Plugin
- GitHub Plugin
- Docker Plugin
- Pipeline Plugin
- ThinBackup Plugin
- SSH Plugin
- Go Plugin

---

# Install Plugins

Steps:

```text
Manage Jenkins

↓

Plugins

↓

Available Plugins

↓

Search Plugin

↓

Install

↓

Restart Jenkins (if required)
```

---

## Recommended Plugins

| Plugin | Purpose |
|---------|----------|
| Git | Git Integration |
| GitHub | GitHub Integration |
| Docker | Docker Builds |
| Pipeline | Pipeline Jobs |
| ThinBackup | Backup & Restore |
| SSH | SSH Authentication |
| Go | Build Go Applications |

---

# Jenkins CLI

Jenkins provides a Command Line Interface (CLI) for managing Jenkins remotely.

Download:

```text
http://SERVER_IP:8080/jnlpJars/jenkins-cli.jar
```

---

# Basic CLI Syntax

```bash
java -jar jenkins-cli.jar -s http://SERVER_IP:8080 COMMAND
```

---

# Display Help

```bash
java -jar jenkins-cli.jar help
```

Description:

Displays all available Jenkins CLI commands.

---

# List Jobs

```bash
java -jar jenkins-cli.jar list-jobs
```

Description:

Lists every Jenkins job.

---

# Build a Job

```bash
java -jar jenkins-cli.jar build JOB_NAME
```

Example

```bash
java -jar jenkins-cli.jar build go-test
```

---

# View Console Output

```bash
java -jar jenkins-cli.jar console JOB_NAME
```

Example

```bash
java -jar jenkins-cli.jar console go-test
```

---

# Safe Restart

```bash
java -jar jenkins-cli.jar safe-restart
```

Description

Restarts Jenkins after running builds finish.

---

# SSH Authentication

Generate SSH Key

```bash
ssh-keygen
```

Display Public Key

```bash
cat ~/.ssh/id_rsa.pub
```

The public key is copied into:

```text
GitHub

or

Jenkins Credentials
```

---

# File Permissions

Secure the SSH directory.

```bash
chmod 700 ~/.ssh
```

Secure the private key.

```bash
chmod 600 ~/.ssh/id_rsa
```

---

# Verify SSH Authentication

```bash
ssh -T git@github.com
```

Expected Output

```text
Hi username!

You've successfully authenticated.
```

---

# Restart Jenkins

Ubuntu

```bash
sudo systemctl restart jenkins
```

or

```bash
service jenkins restart
```

---

# Check Jenkins Status

```bash
sudo systemctl status jenkins
```

or

```bash
service jenkins status
```

---

# Command Reference

| Command | Description |
|----------|-------------|
| `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` | Retrieve initial admin password |
| `java -jar jenkins-cli.jar help` | Display CLI help |
| `java -jar jenkins-cli.jar list-jobs` | List all Jenkins jobs |
| `java -jar jenkins-cli.jar build JOB_NAME` | Build a Jenkins job |
| `java -jar jenkins-cli.jar console JOB_NAME` | View console output |
| `java -jar jenkins-cli.jar safe-restart` | Safe restart Jenkins |
| `ssh-keygen` | Generate SSH key pair |
| `cat ~/.ssh/id_rsa.pub` | Display public SSH key |
| `chmod 700 ~/.ssh` | Secure SSH directory |
| `chmod 600 ~/.ssh/id_rsa` | Secure private key |
| `ssh -T git@github.com` | Verify GitHub SSH authentication |
| `sudo systemctl restart jenkins` | Restart Jenkins |
| `sudo systemctl status jenkins` | Check Jenkins service |
| `service jenkins restart` | Restart Jenkins (alternative) |
| `service jenkins status` | Check Jenkins status (alternative) |

---

# Practical Exercises

## Exercise 1

Generate an SSH key.

```bash
ssh-keygen
```

---

## Exercise 2

Display the public key.

```bash
cat ~/.ssh/id_rsa.pub
```

---

## Exercise 3

Restart Jenkins.

```bash
sudo systemctl restart jenkins
```

---

## Exercise 4

List all Jenkins jobs.

```bash
java -jar jenkins-cli.jar list-jobs
```

---

## Exercise 5

View console output.

```bash
java -jar jenkins-cli.jar console JOB_NAME
```

---

# Summary

This chapter covered:

- Unlocking Jenkins
- Initial configuration
- Jenkins Dashboard
- Plugin Manager
- Installing Plugins
- Jenkins CLI
- SSH Authentication
- Restarting Jenkins
- Jenkins CLI commands