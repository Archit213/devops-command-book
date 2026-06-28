# Systemctl.md

# Background Services & Systemctl Automation
------------------------------------------------------------------------

# Table of Contents

-   What are Background Services?
-   What is systemd?
-   What is systemctl?
-   Service Lifecycle
-   Command Reference
-   Creating a Custom Service
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What are Background Services?

Background services (also called **daemons**) are long-running processes
that start automatically or manually and continue running without user
interaction. Examples include web servers, databases, and SSH.

Examples:

-   `httpd`
-   `nginx`
-   `sshd`
-   `docker`
-   `jenkins`

------------------------------------------------------------------------

# What is systemd?

`systemd` is the init system used by most modern Linux distributions. It
manages system startup, services, logging, and dependencies.

------------------------------------------------------------------------

# What is systemctl?

`systemctl` is the command-line utility used to manage services
controlled by systemd.

------------------------------------------------------------------------

# Service Lifecycle

``` text
Start → Running → Stop
           │
        Restart
           │
        Status Check
```

------------------------------------------------------------------------

# Command Reference

## Start a Service

``` bash
systemctl start httpd
```

Starts the specified service.

### Example

``` bash
sudo systemctl start httpd
```

------------------------------------------------------------------------

## Stop a Service

``` bash
systemctl stop httpd
```

Stops a running service.

------------------------------------------------------------------------

## Check Service Status

``` bash
systemctl status httpd
```

Displays service status, logs, PID, and uptime.

------------------------------------------------------------------------

## Enable a Service at Boot

``` bash
systemctl enable httpd
```

Configures the service to start automatically during system boot.

------------------------------------------------------------------------

## Disable a Service

``` bash
systemctl disable httpd
```

Prevents the service from starting automatically at boot.

------------------------------------------------------------------------

## Reload systemd Configuration

``` bash
systemctl daemon-reload
```

Reloads all systemd unit files after creating or modifying service
definitions.

------------------------------------------------------------------------

# Creating a Custom Service

Create the file:

``` text
/etc/systemd/system/myapp.service
```

Example service:

``` ini
[Unit]
Description=My Custom Python Application

[Service]
ExecStart=/usr/bin/python3 /opt/code/myapp.py

[Install]
WantedBy=multi-user.target
```

Reload and start:

``` bash
systemctl daemon-reload
systemctl start myapp
systemctl status myapp
```

Expected output:

``` text
● myapp.service - My Custom Python Application
Loaded: loaded (...)
Active: active (running)
Main PID: 14210 (python3)
```

------------------------------------------------------------------------

# Practical Exercises

## Exercise 1

Start and verify Apache:

``` bash
sudo systemctl start httpd
sudo systemctl status httpd
```

## Exercise 2

Enable automatic startup:

``` bash
sudo systemctl enable httpd
```

## Exercise 3

Reload configuration after editing a unit file:

``` bash
sudo systemctl daemon-reload
sudo systemctl restart httpd
```

------------------------------------------------------------------------

# Best Practices

-   Check service status after starting or stopping.
-   Run `daemon-reload` whenever a unit file changes.
-   Enable only services required at boot.
-   Store custom unit files in `/etc/systemd/system`.

------------------------------------------------------------------------

# Common Mistakes

-   Forgetting `daemon-reload` after editing a service file.
-   Editing the wrong unit file.
-   Starting a service before creating a valid unit definition.
-   Ignoring `systemctl status` output during troubleshooting.

------------------------------------------------------------------------

# Interview Questions

### What is the difference between `start` and `enable`?

-   `start` starts a service immediately.
-   `enable` configures it to start automatically at boot.

### Why is `daemon-reload` required?

It forces systemd to reload updated or newly created service unit files.

### Where are custom systemd service files stored?

`/etc/systemd/system`

------------------------------------------------------------------------

# Summary

This chapter covered:

-   Background services
-   systemd architecture
-   systemctl commands
-   Service lifecycle
-   Creating custom services
-   Managing services in Linux
