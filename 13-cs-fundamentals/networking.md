---
title: "Networking"
tags: ["cs-fundamentals","networking"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Networking

## Definition

Computer networking is the study of how devices communicate over digital systems. It is governed by a set of layered protocols that ensure data is sent and received accurately across different hardware and software.

## The OSI Model vs TCP/IP

The **OSI Model** (7 layers) is a theoretical framework; the **TCP/IP Model** (4 layers) is the practical implementation used by the internet.

| OSI Layer | TCP/IP Layer | Key Protocols | Purpose |
| :--- | :--- | :--- | :--- |
| 7. Application | Application | HTTP, DNS, SMTP, SSH | User-facing data exchange |
| 6. Presentation | Application | SSL/TLS, JPEG, GIF | Data encoding/Encryption |
| 5. Session | Application | NetBIOS, RPC | Session management |
| 4. Transport | Transport | TCP, UDP | End-to-end reliability/flow control |
| 3. Network | Internet | IP, ICMP, BGP | Routing and addressing |
| 2. Data Link | Network Access | Ethernet, ARP, MAC | Hop-to-hop delivery |
| 1. Physical | Network Access | Fiber, Radio, Cable | Binary transmission |

## Deep Dives into Protocols

### 1. TCP vs UDP
- **TCP (Transmission Control Protocol)**: Connection-oriented. Ensures reliability via the **Three-Way Handshake** (SYN $\rightarrow$ SYN-ACK $\rightarrow$ ACK), sequence numbers, and retransmissions. Used for: HTTP, SSH, FTP.
- **UDP (User Datagram Protocol)**: Connectionless. "Fire and forget." No guarantee of delivery or order. Used for: Video streaming, Gaming, DNS.

### 2. DNS (Domain Name System)
DNS is the "phonebook of the internet," translating human-readable names (`google.com`) to IP addresses.
- **Recursive Resolver**: The server that does the work for the client.
- **Root Server $\rightarrow$ TLD Server $\rightarrow$ Authoritative Server**: The hierarchy used to find the IP.
- **Caching**: DNS records are cached at the browser, OS, and ISP levels to reduce latency.

### 3. HTTP/1.1 $\rightarrow$ HTTP/2 $\rightarrow$ HTTP/3
- **HTTP/1.1**: Request-Response. Suffers from **Head-of-Line (HOL) Blocking** (one slow request blocks all others).
- **HTTP/2**: Introduces **Multiplexing** (many requests over one TCP connection) and Server Push. Solves application-layer HOL blocking.
- **HTTP/3**: Replaces TCP with **QUIC** (built on UDP). Solves transport-layer HOL blocking (packet loss in one stream doesn't block other streams).

## Networking Security

- **TLS/SSL**: Encrypts the transport layer. Uses a handshake to agree on a symmetric session key using asymmetric encryption.
- **WebSockets**: A full-duplex communication channel over a single TCP connection. Upgraded from HTTP via a `101 Switching Protocols` response.

## Working Code Example: Network Latency Analysis

This Bash snippet demonstrates how to analyze network connectivity and latency to a specific server.

```bash
# 1. Check basic connectivity and RTT (Round Trip Time)
ping -c 4 google.com

# 2. Trace the route to see every hop (路由器) the packet takes
# Uses ICMP Time-to-Live (TTL) to map the path
traceroute google.com

# 3. Check if a specific port is open (e.g., HTTPS 443)
nc -zv google.com 443
```

**Complexity**: Network latency is $O(1)$ for a single request, but the overall time is $\text{RTT} \times \text{number of round trips}$.

## Interview questions

### Q1: What happens when you type a URL into a browser?
**Model answer**: 
1. **DNS Lookup**: Browser checks cache $\rightarrow$ OS cache $\rightarrow$ Resolver $\rightarrow$ Root $\rightarrow$ TLD $\rightarrow$ Authoritative DNS to get the IP.
2. **TCP Handshake**: Browser initiates a 3-way handshake with the server.
3. **TLS Handshake**: Client and server agree on encryption keys.
4. **HTTP Request**: Browser sends a GET request.
5. **Server Response**: Server processes the request and sends back HTML/JSON.
6. **Rendering**: Browser parses HTML, requests CSS/JS, and renders the page.

### Q2: What is a 3-way handshake in TCP?
**Model answer**: It establishes a reliable connection: 
1. **SYN**: Client sends a sequence number $X$.
2. **SYN-ACK**: Server acknowledges $X$ (sends $X+1$) and sends its own sequence $Y$.
3. **ACK**: Client acknowledges $Y$ (sends $Y+1$).
Connection established.

### Q3: How does a Load Balancer work?
**Model answer**: A load balancer sits between the client and a pool of servers. It uses algorithms (Round Robin, Least Connections, IP Hash) to distribute traffic. It can also perform "Health Checks" to stop sending traffic to failing servers.

### Q4: Difference between a Hub, a Switch, and a Router?
**Model answer**: 
- **Hub**: Physical layer; broadcasts all traffic to all ports (inefficient).
- **Switch**: Data Link layer; uses MAC addresses to send traffic only to the target port.
- **Router**: Network layer; uses IP addresses to route traffic between different networks.

### Q5: What is the "Silly Window Syndrome" in TCP?
**Model answer**: It occurs when the receiver advertises a very small window size, causing the sender to send tiny packets. This increases overhead. TCP solves this by using **Nagle's Algorithm** (buffering small packets) and the **Clark Solution** (waiting for a larger window).

## Related notes

- [Operating systems](os.md)
- [OOP and Design Basics](oop.md)
- [System Design Fundamentals](../06-system-design/system-design-fundamentals.md)
