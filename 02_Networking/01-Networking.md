# Networking: Switching & Routing
------------------------------------------------------------------------

# Table of Contents

-   Networking Fundamentals
-   Switching vs Routing
-   IP Addresses & Gateways
-   Routing Tables
-   IP Forwarding
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# Networking Fundamentals

A **switch** connects devices within the same Local Area Network (LAN),
while a **router** connects different networks together and forwards
packets between them.

## Switching vs Routing

  Switching                              Routing
  -------------------------------------- -----------------------------
  Connects devices in the same network   Connects different networks
  Uses MAC addresses                     Uses IP addresses
  Layer 2                                Layer 3

------------------------------------------------------------------------

# Gateway

A **default gateway** is the router that forwards traffic destined for
networks outside the local subnet.

------------------------------------------------------------------------

# IP Forwarding

Linux disables packet forwarding by default. To make a Linux host act as
a router, IP forwarding must be enabled.

------------------------------------------------------------------------

# Command Reference

## 1. List Network Interfaces

``` bash
ip link
```

Displays all network interfaces and their state.

Example:

``` bash
ip link
```

------------------------------------------------------------------------

## 2. Show IP Addresses

``` bash
ip addr
```

Displays all IP addresses assigned to interfaces.

Example:

``` bash
ip addr
```

------------------------------------------------------------------------

## 3. Assign an IP Address

``` bash
ip addr add <IP>/<MASK> dev <INTERFACE>
```

Example:

``` bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

------------------------------------------------------------------------

## 4. Test Connectivity

``` bash
ping <IP>
```

Example:

``` bash
ping 8.8.8.8
```

Expected Output:

``` text
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=12 ms
```

------------------------------------------------------------------------

## 5. View Routing Table

``` bash
ip route
```

or

``` bash
route
```

Displays the routing table.

------------------------------------------------------------------------

## 6. Add a Static Route

``` bash
ip route add <NETWORK>/<MASK> via <GATEWAY>
```

Example:

``` bash
sudo ip route add 192.168.2.0/24 via 192.168.1.6
```

------------------------------------------------------------------------

## 7. Add Default Gateway

``` bash
ip route add default via <GATEWAY>
```

Example:

``` bash
sudo ip route add default via 192.168.1.1
```

------------------------------------------------------------------------

## 8. Check IP Forwarding Status

``` bash
cat /proc/sys/net/ipv4/ip_forward
```

Expected Output:

``` text
0
```

-   `0` = Disabled
-   `1` = Enabled

------------------------------------------------------------------------

## 9. Enable IP Forwarding Temporarily

``` bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

Requires root privileges.

------------------------------------------------------------------------

## Permanent IP Forwarding

Edit:

``` text
/etc/sysctl.conf
```

Add:

``` text
net.ipv4.ip_forward = 1
```

Apply changes:

``` bash
sysctl -p
```

------------------------------------------------------------------------

# Practical Exercises

## Display IP Information

``` bash
ip addr
ip link
```

## Ping a Remote Host

``` bash
ping 8.8.8.8
```

## Add a Static Route

``` bash
sudo ip route add 192.168.2.0/24 via 192.168.1.6
ip route
```

## Enable IP Forwarding

``` bash
echo 1 > /proc/sys/net/ipv4/ip_forward
cat /proc/sys/net/ipv4/ip_forward
```

------------------------------------------------------------------------

# Best Practices

-   Verify routes after adding them.
-   Test connectivity using `ping`.
-   Use `ip` commands instead of legacy networking tools where possible.
-   Make IP forwarding persistent using `sysctl.conf`.

------------------------------------------------------------------------

# Common Mistakes

-   Incorrect subnet mask.
-   Wrong gateway IP.
-   Forgetting to enable IP forwarding.
-   Not verifying routing table after configuration.

------------------------------------------------------------------------

# Interview Questions

### Difference between a switch and a router?

A switch connects devices within the same LAN, while a router connects
different networks.

### What is a default gateway?

It is the router used to send traffic outside the local network.

### What does `ip route` display?

The Linux routing table.

### What does `ip_forward=1` mean?

Packet forwarding is enabled, allowing the host to route traffic.

------------------------------------------------------------------------

# Summary

This chapter covered:

-   Switching
-   Routing
-   Gateways
-   Routing tables
-   IP forwarding
-   Static routes
-   Linux networking commands
