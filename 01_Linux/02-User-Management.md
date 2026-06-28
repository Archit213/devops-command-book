# User Accounts, System Information & Package Managers
------------------------------------------------------------------------

# Table of Contents

-   User Management
-   Root vs Regular Users
-   sudo
-   Package Managers
-   RPM vs YUM
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# User Accounts

Linux uses user accounts to control access to system resources.

## Types of Users

  User           Description
  -------------- -----------------------------------------------
  Root           Superuser with unrestricted access.
  Regular User   Limited permissions for day-to-day work.
  Service User   Used by applications and background services.

------------------------------------------------------------------------

# Root vs sudo

The **root** user has unrestricted control over the system.

The **sudo** command allows a regular user to temporarily execute
administrative commands without logging in as root.

Example:

``` bash
sudo ls /root
```

------------------------------------------------------------------------

# Package Managers

Linux package managers install, update, remove, and manage software
packages.

### RPM

-   Low-level package manager
-   Installs `.rpm` files
-   Does **not** resolve dependencies automatically

### YUM

-   High-level package manager
-   Resolves dependencies automatically
-   Downloads packages from configured repositories

------------------------------------------------------------------------

# Command Reference

## 1. Current User

``` bash
whoami
```

Displays the currently logged-in user.

Example:

``` bash
whoami
```

Expected Output:

``` text
devops
```

------------------------------------------------------------------------

## 2. User Information

``` bash
id
```

Displays UID, GID, and group memberships.

------------------------------------------------------------------------

## 3. Switch User

``` bash
su username
```

Example:

``` bash
su root
```

------------------------------------------------------------------------

## 4. Remote Login

``` bash
ssh user@IP
```

Example:

``` bash
ssh devops@192.168.1.10
```

------------------------------------------------------------------------

## 5. Execute Command as Administrator

``` bash
sudo ls /root
```

Lists files in the root user's home directory.

------------------------------------------------------------------------

## 6. Download Using curl

``` bash
curl URL
```

Example:

``` bash
curl https://example.com
curl -o page.html https://example.com
```

------------------------------------------------------------------------

## 7. Download Using wget

``` bash
wget URL
```

Example:

``` bash
wget https://example.com/file.zip
```

------------------------------------------------------------------------

## 8. Detect Linux Distribution

``` bash
ls /etc/*release*
```

Lists release files.

------------------------------------------------------------------------

## 9. Display OS Information

``` bash
cat /etc/*release
```

Expected Output:

``` text
NAME="CentOS Linux"
VERSION="8"
```

------------------------------------------------------------------------

# RPM Commands

## Install Package

``` bash
rpm -i package.rpm
```

## Remove Package

``` bash
rpm -e package
```

## Query Package

``` bash
rpm -q package
```

------------------------------------------------------------------------

# YUM Commands

## Install Package

``` bash
yum install ansible
```

## List Repositories

``` bash
yum repolist
```

## Repository Files

``` bash
ls /etc/yum.repos.d/
```

## Remove Package

``` bash
yum remove ansible
```

## Show Available Versions

``` bash
yum --showduplicates list ansible
```

## Install Specific Version

``` bash
yum install ansible-2.9.10
```

------------------------------------------------------------------------

# Practical Exercises

## Install Ansible

``` bash
yum install ansible
ansible --version
```

## Check OS Version

``` bash
cat /etc/*release
```

## Download a File

``` bash
wget https://example.com/file.zip
```

------------------------------------------------------------------------

# Best Practices

-   Prefer `sudo` instead of logging in as root.
-   Install software using YUM whenever possible.
-   Verify downloaded packages before installation.
-   Use official repositories.

------------------------------------------------------------------------

# Common Mistakes

-   Running commands as root unnecessarily.
-   Installing RPM packages without checking dependencies.
-   Downloading packages from untrusted sources.

------------------------------------------------------------------------

# Interview Questions

### Difference between RPM and YUM?

-   RPM installs packages directly.
-   YUM installs packages and resolves dependencies automatically.

### Difference between `su` and `sudo`?

-   `su` switches to another user.
-   `sudo` executes a single command with elevated privileges.

### What does `whoami` display?

The username of the current logged-in user.

------------------------------------------------------------------------

# Summary

This chapter covered:

-   Linux user management
-   Root vs regular users
-   SSH
-   sudo
-   curl
-   wget
-   RPM
-   YUM
-   Package installation and removal
