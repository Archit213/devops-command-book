# Jenkins Backup, Restore & Best Practices
---

# Table of Contents

- ThinBackup Plugin
- Jenkins Backup
- Jenkins Restore
- Jenkins Service Management
- Backup Best Practices
- Common Troubleshooting
- Jenkins Interview Questions
- Complete Command Cheat Sheet

---

# ThinBackup Plugin

ThinBackup is one of the most commonly used Jenkins plugins for backing up Jenkins configuration.

It backs up:

- Jobs
- Plugins
- Users
- Credentials
- System Configuration
- Jenkins Home Configuration

It does **not** back up:

- Build Workspace
- Build Artifacts (unless configured)

---

# Install ThinBackup

Navigate to

```text
Manage Jenkins

↓

Plugins

↓

Available Plugins

↓

Search: ThinBackup

↓

Install
```

Restart Jenkins if required.

---

# Configure Backup

Navigate to

```text
Manage Jenkins

↓

ThinBackup

↓

Settings
```

Select

```text
Backup Directory
```

Example

```text
/var/jenkins_backup
```

---

# Perform Backup

Navigate to

```text
Manage Jenkins

↓

ThinBackup

↓

Backup Now
```

Jenkins will create a backup of:

- Jobs
- Plugins
- Credentials
- Configuration

---

# Restore Backup

Navigate to

```text
Manage Jenkins

↓

ThinBackup

↓

Restore
```

Select the backup folder.

Restore Jenkins.

Restart Jenkins.

---

# Restart Jenkins

Ubuntu

```bash
sudo systemctl restart jenkins
```

Alternative

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

Expected Output

```text
Active: active (running)
```

---

# Jenkins Home

Default location

```text
/var/lib/jenkins
```

Contains

- Jobs
- Plugins
- Users
- Credentials
- Workspace
- Jenkins Configuration

---

# Important Jenkins Directories

| Directory | Purpose |
|------------|----------|
| `/var/lib/jenkins` | Jenkins Home |
| `/var/lib/jenkins/jobs` | Jenkins Jobs |
| `/var/lib/jenkins/plugins` | Installed Plugins |
| `/var/lib/jenkins/workspace` | Workspace |
| `/var/lib/jenkins/secrets` | Credentials & Secrets |

---

# Change Permissions

Sometimes backup folders require permission changes.

Example

```bash
chmod 777 folder_name
```

Example

```bash
chmod 777 /var/jenkins_backup
```

> **Note:** Avoid using `777` in production. Prefer the least-privilege permissions required.

---

# Backup Best Practices

✅ Schedule backups regularly.

✅ Store backups outside the Jenkins server.

✅ Backup before plugin upgrades.

✅ Backup before Jenkins upgrades.

✅ Verify restore process periodically.

---

# Common Troubleshooting

## Jenkins Service Not Running

Check status

```bash
sudo systemctl status jenkins
```

Restart

```bash
sudo systemctl restart jenkins
```

---

## Port 8080 Not Accessible

Check firewall

```bash
sudo ufw status
```

Allow Jenkins

```bash
sudo ufw allow 8080
```

---

## Plugin Installation Failed

Steps

1.

Restart Jenkins

```bash
sudo systemctl restart jenkins
```

2.

Retry installation.

---

## Restore Failed

Verify

- Backup directory exists.
- Correct permissions.
- Restart Jenkins after restore.

---

## Jenkins Won't Start

Check service

```bash
sudo systemctl status jenkins
```

Common causes

- Java not installed
- Incorrect Java version
- Corrupted plugin
- Port already in use

---

# Jenkins Interview Questions

## What is Jenkins?

An open-source automation server used for CI/CD.

---

## What is Jenkins Home?

The directory that stores Jenkins configuration, plugins, jobs, users, and other data.

Default location

```text
/var/lib/jenkins
```

---

## What is ThinBackup?

A Jenkins plugin used to back up and restore Jenkins configuration.

---

## Difference Between Freestyle and Pipeline Jobs?

| Freestyle | Pipeline |
|------------|-----------|
| GUI-based | Pipeline as Code |
| Limited flexibility | Highly flexible |
| Harder to version control | Stored in Git using Jenkinsfile |

---

## What is a Jenkinsfile?

A text file that defines a Jenkins Pipeline using Groovy syntax.

---

## Why Use Pipelines?

- Version control
- Automation
- Reusability
- Multi-stage builds

---

## Where Are Jenkins Plugins Stored?

```text
/var/lib/jenkins/plugins
```

---

## How Do You Restart Jenkins?

```bash
sudo systemctl restart jenkins
```

or

```bash
service jenkins restart
```

---

# Jenkins Command Cheat Sheet

## Go Commands

```bash
go run main.go
go test -v
```

---

## Installation

```bash
sudo apt update -y

sudo apt install openjdk-11-jdk

java -version

wget -q -O -

sudo apt install jenkins
```

---

## Jenkins Service

```bash
sudo systemctl start jenkins

sudo systemctl enable jenkins

sudo systemctl restart jenkins

sudo systemctl status jenkins
```

Alternative

```bash
service jenkins restart

service jenkins status
```

---

## Firewall

```bash
sudo ufw allow 8080

sudo ufw status
```

---

## Initial Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

## Jenkins CLI

```bash
java -jar jenkins-cli.jar help

java -jar jenkins-cli.jar list-jobs

java -jar jenkins-cli.jar build JOB_NAME

java -jar jenkins-cli.jar console JOB_NAME

java -jar jenkins-cli.jar safe-restart
```

---

## SSH

```bash
ssh-keygen

cat ~/.ssh/id_rsa.pub

chmod 700 ~/.ssh

chmod 600 ~/.ssh/id_rsa

ssh -T git@github.com
```

---

## Docker

```bash
docker build -t sample-app .
```

---

# Summary

Congratulations! 🎉

You have completed the Jenkins reference guide.

You now know how to:

- Install Jenkins
- Configure Jenkins
- Manage Plugins
- Use the Jenkins CLI
- Create Freestyle Jobs
- Create Pipeline Jobs
- Write Jenkinsfiles
- Build Multi-stage Pipelines
- Integrate Go Applications
- Build Docker Images
- Backup & Restore Jenkins
- Troubleshoot Jenkins
- Use the most common Jenkins commands

This guide, together with your Linux, Networking, Git, GitHub, Java, Node.js, and Python notes, provides a strong foundation for DevOps learning and day-to-day reference.