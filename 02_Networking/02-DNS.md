# DNS.md

# Domain Name System (DNS) Resolution
------------------------------------------------------------------------

# Table of Contents

-   What is DNS?
-   DNS Resolution Process
-   DNS Record Types
-   Important Configuration Files
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What is DNS?

The **Domain Name System (DNS)** translates human-readable domain names
(such as `www.google.com`) into IP addresses that computers use to
communicate.

Without DNS, users would need to remember IP addresses instead of domain
names.

------------------------------------------------------------------------

# DNS Resolution Process

``` text
Application
    │
    ▼
/etc/hosts
    │
    ▼
/etc/nsswitch.conf
    │
    ▼
/etc/resolv.conf
    │
    ▼
DNS Server
    │
    ▼
IP Address
```

------------------------------------------------------------------------

# Common DNS Record Types

  Record   Purpose
  -------- ---------------------------------------------------
  A        Maps a hostname to an IPv4 address
  AAAA     Maps a hostname to an IPv6 address
  CNAME    Creates an alias for another hostname
  MX       Mail server record
  NS       Name server record
  TXT      Stores text information (SPF, verification, etc.)

------------------------------------------------------------------------

# Important Configuration Files

## `/etc/hosts`

Stores static hostname-to-IP mappings.

Example:

``` text
192.168.1.115 test
```

------------------------------------------------------------------------

## `/etc/resolv.conf`

Defines DNS servers used for name resolution.

Example:

``` text
nameserver 8.8.8.8
nameserver 1.1.1.1
```

------------------------------------------------------------------------

## `/etc/nsswitch.conf`

Controls the lookup order.

Typical entry:

``` text
hosts: files dns
```

This means Linux checks `/etc/hosts` before querying DNS servers.

------------------------------------------------------------------------

# Command Reference

## 1. View Local Host Mappings

``` bash
cat /etc/hosts
```

Displays locally configured hostname mappings.

------------------------------------------------------------------------

## 2. View DNS Server Configuration

``` bash
cat /etc/resolv.conf
```

Displays configured DNS resolvers.

------------------------------------------------------------------------

## 3. View Name Service Switch Configuration

``` bash
cat /etc/nsswitch.conf
```

Displays the hostname lookup order.

------------------------------------------------------------------------

## 4. Query DNS Using nslookup

``` bash
nslookup example.com
```

Example:

``` bash
nslookup google.com
```

Returns DNS records from the configured name server.

------------------------------------------------------------------------

## 5. Query DNS Using dig

``` bash
dig example.com
```

Example:

``` bash
dig www.google.com
```

Expected Output (excerpt):

``` text
;; ANSWER SECTION:
www.google.com. 300 IN A 216.58.221.78
```

------------------------------------------------------------------------

# Practical Exercises

## Add a Local Host Entry

``` bash
echo "192.168.1.115 test" >> /etc/hosts
```

Verify:

``` bash
ping test
```

Expected Output:

``` text
PING test (192.168.1.115)
```

------------------------------------------------------------------------

## Check DNS Resolution

``` bash
nslookup openai.com
dig openai.com
```

------------------------------------------------------------------------

## Display Resolver Configuration

``` bash
cat /etc/resolv.conf
cat /etc/nsswitch.conf
```

------------------------------------------------------------------------

# Best Practices

-   Use `/etc/hosts` only for local testing.
-   Configure reliable DNS servers.
-   Verify DNS propagation using `dig`.
-   Check `/etc/nsswitch.conf` when troubleshooting resolution order.

------------------------------------------------------------------------

# Common Mistakes

-   Editing `/etc/resolv.conf` on systems where it is auto-generated.
-   Forgetting that `/etc/hosts` overrides DNS.
-   Using incorrect IP addresses in local host mappings.

------------------------------------------------------------------------

# Interview Questions

### What is DNS?

DNS translates domain names into IP addresses.

### Difference between `nslookup` and `dig`?

-   `nslookup` provides basic DNS lookup information.
-   `dig` provides detailed DNS query results for troubleshooting.

### Which file stores local hostname mappings?

`/etc/hosts`

### Which file defines DNS servers?

`/etc/resolv.conf`

### What does `hosts: files dns` mean?

Linux checks local host entries before querying DNS servers.

------------------------------------------------------------------------

# Summary

This chapter covered:

-   DNS fundamentals
-   DNS resolution workflow
-   DNS record types
-   `/etc/hosts`
-   `/etc/resolv.conf`
-   `/etc/nsswitch.conf`
-   `nslookup`
-   `dig`
-   Local hostname mapping
-   DNS troubleshooting
