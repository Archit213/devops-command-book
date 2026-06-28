# Linux Basics & Command Line Interface
------------------------------------------------------------------------

# Table of Contents

-   What is Linux?
-   Why Linux is Important for DevOps
-   Linux Shell
-   Common Linux Shells
-   Linux File System Basics
-   Command Reference
-   Practical Examples
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What is Linux?

Linux is an open-source operating system based on the Unix architecture.
It is widely used in cloud computing, servers, DevOps, networking,
cybersecurity, and software development due to its stability,
flexibility, security, and performance.

Most cloud platforms such as AWS, Azure, and Google Cloud primarily run
Linux-based virtual machines.

------------------------------------------------------------------------

# Why Linux is Important for DevOps

-   Most production servers run Linux.
-   Docker was originally developed for Linux.
-   Kubernetes is built around Linux container technologies.
-   Automation tools such as Ansible and Terraform commonly target Linux
    systems.
-   Linux provides powerful scripting capabilities through Bash.

------------------------------------------------------------------------

# Linux Shell

A Linux shell is a command-line interpreter that accepts user commands
and communicates with the Linux kernel.

Common shells:

-   Bourne Shell (`sh`)
-   Bourne Again Shell (`bash`)
-   Z Shell (`zsh`)
-   C Shell (`csh`)

------------------------------------------------------------------------

# Linux File System Basics

``` text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── opt
├── proc
├── root
├── tmp
├── usr
└── var
```

  Directory   Purpose
  ----------- ------------------------
  `/`         Root directory
  `/home`     User home directories
  `/etc`      Configuration files
  `/var`      Logs and variable data
  `/tmp`      Temporary files
  `/usr`      Installed applications
  `/root`     Root user's home

------------------------------------------------------------------------

# Command Reference

## 1. Display Current Shell

### Command

``` bash
echo $SHELL
```

**Description**

Displays the currently active shell.

**Example**

``` bash
echo $SHELL
```

**Expected Output**

``` text
/bin/bash
```

------------------------------------------------------------------------

## 2. Print Text

``` bash
echo "Hello DevOps"
```

Prints text to the terminal.

Example:

``` bash
echo "Welcome to Linux"
```

------------------------------------------------------------------------

## 3. List Files

``` bash
ls
```

Lists files and directories in the current directory.

Useful options:

``` bash
ls -l
ls -a
ls -lh
ls -la
```

------------------------------------------------------------------------

## 4. Change Directory

``` bash
cd directory_name
```

Example:

``` bash
cd Documents
cd ..
cd ~
```

------------------------------------------------------------------------

## 5. Print Working Directory

``` bash
pwd
```

Example:

``` bash
pwd
```

------------------------------------------------------------------------

## 6. Create Directory

``` bash
mkdir project
```

Example:

``` bash
mkdir DevOps
```

------------------------------------------------------------------------

## 7. Create Nested Directories

``` bash
mkdir -p /tmp/asia/india/bangalore
```

Example:

``` bash
mkdir -p projects/devops/docker
tree projects
```

------------------------------------------------------------------------

## 8. Delete Directory

``` bash
rm -r directory
```

Example:

``` bash
rm -r DevOps
```

------------------------------------------------------------------------

## 9. Display Directory Tree

``` bash
tree directory
```

Example:

``` bash
tree /tmp/asia
```

------------------------------------------------------------------------

## 10. Copy Directory

``` bash
cp -r source destination
```

Example:

``` bash
cp -r project backup
```

------------------------------------------------------------------------

## 11. Create Empty File

``` bash
touch file.txt
```

Example:

``` bash
touch notes.txt
```

------------------------------------------------------------------------

## 12. Create File Using cat

``` bash
cat > file.txt
```

Example:

``` text
cat > hello.txt
Hello DevOps
Linux Basics
Ctrl+D
```

------------------------------------------------------------------------

## 13. Display File Contents

``` bash
cat file.txt
```

Example:

``` bash
cat hello.txt
```

------------------------------------------------------------------------

## 14. Copy File

``` bash
cp source.txt destination.txt
```

Example:

``` bash
cp notes.txt backup.txt
```

------------------------------------------------------------------------

## 15. Move or Rename File

``` bash
mv old.txt new.txt
```

Examples:

``` bash
mv report.txt report_old.txt
mv report.txt /tmp
```

------------------------------------------------------------------------

## 16. Delete File

``` bash
rm file.txt
```

Example:

``` bash
rm notes.txt
```

------------------------------------------------------------------------

# Practical Exercises

## Exercise 1

``` bash
mkdir -p Projects/DevOps/Linux
tree Projects
```

## Exercise 2

``` bash
touch notes.txt
cat > notes.txt
Linux Commands
# Press Ctrl+D
cat notes.txt
```

## Exercise 3

``` bash
cp -r Projects Projects_Backup
```

------------------------------------------------------------------------

# Best Practices

-   Use `pwd` frequently.
-   Verify changes with `ls` or `tree`.
-   Be careful with `rm -r`.

# Common Mistakes

-   Running `rm -r /`
-   Forgetting `-r` with directory copy.
-   Working in the wrong directory.

# Interview Questions

### Why is Linux preferred in DevOps?

Because most cloud infrastructure, containers, and automation tools are
Linux-based.

### Difference between `cp` and `mv`

-   `cp` copies.
-   `mv` moves or renames.

### Difference between `mkdir` and `mkdir -p`

-   `mkdir` creates one directory.
-   `mkdir -p` creates nested directories.
