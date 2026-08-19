# 🌐 DevSecOps Engineer Journey — Day 03

> **Focus:** Networking for DevSecOps
> **Level:** Beginner → Professional
> **Goal:** Understand how systems communicate across networks and develop the networking knowledge required for DevSecOps, cloud security, containers, Kubernetes, CI/CD, troubleshooting, and production incident response.

---

# 🎯 Day 03 Objectives

By the end of Day 03, I should understand:

* What a computer network is
* LAN, WAN, Internet
* OSI model
* TCP/IP model
* Encapsulation and decapsulation
* MAC addresses
* IP addresses
* IPv4
* IPv6 fundamentals
* Public vs private IP addresses
* Subnet masks
* CIDR notation
* Default gateway
* ARP
* DNS
* TCP
* UDP
* TCP three-way handshake
* Ports and sockets
* Routing
* NAT
* ICMP
* HTTP
* HTTPS
* TLS fundamentals
* Reverse proxy
* Forward proxy
* Load balancer
* Firewall
* WAF
* Network segmentation
* VPC/VNet fundamentals
* Security groups / network filtering concepts
* Network troubleshooting
* Network security fundamentals
* How networking connects to DevSecOps
* How networking connects to Docker
* How networking connects to Kubernetes
* How networking connects to AWS/Azure
* How attackers abuse network weaknesses
* How defenders detect network attacks

---

# 🧠 Day 03 Core Principle

> **A DevSecOps engineer must understand what happens between the moment an application sends a request and the moment the destination application receives it.**

Do not memorize commands.

Understand the traffic flow.

```text
Application
    │
    ▼
DNS
    │
    ▼
IP Address
    │
    ▼
Routing
    │
    ▼
TCP / UDP
    │
    ▼
Port
    │
    ▼
Firewall
    │
    ▼
Load Balancer / Proxy
    │
    ▼
Web Server
    │
    ▼
Application
    │
    ▼
Database
```

---

# 1. What Is a Computer Network?

A computer network allows systems to communicate and exchange information.

Example:

```text
Laptop
   │
   ▼
Wi-Fi Router
   │
   ▼
Internet
   │
   ▼
Cloud Server
   │
   ▼
Application
```

A network can connect:

* Computers
* Servers
* Containers
* Kubernetes nodes
* Cloud resources
* Databases
* Load balancers
* Network appliances
* IoT devices

---

# 2. Why Networking Matters to DevSecOps

Almost every DevSecOps system depends on networking.

```text
Developer
    │
    ▼
Git Repository
    │
    ▼
CI/CD Runner
    │
    ▼
Container Registry
    │
    ▼
Cloud
    │
    ▼
Kubernetes
    │
    ▼
Application
    │
    ▼
Database
```

Every connection requires networking.

If networking fails:

```text
Application
     X
Database
```

The application may be completely healthy but still unavailable.

This is why:

> **Network problems can look like application problems.**

This principle follows directly from the troubleshooting mindset established on Day 02.

---

# 3. Network Components

A basic enterprise network may contain:

```text
                    INTERNET
                       │
                       ▼
                  ┌─────────┐
                  │ Firewall│
                  └────┬────┘
                       │
                       ▼
                  ┌─────────┐
                  │   WAF   │
                  └────┬────┘
                       │
                       ▼
                ┌──────────────┐
                │Load Balancer │
                └──────┬───────┘
                       │
              ┌────────┴────────┐
              ▼                 ▼
          Web Server         Web Server
              │                 │
              └────────┬────────┘
                       ▼
                  Application
                       │
                       ▼
                    Database
```

Important components:

* Router
* Switch
* Firewall
* Load balancer
* Proxy
* WAF
* DNS server
* DHCP server
* VPN gateway
* Network interface
* Server
* Client

---

# 4. OSI Model

The OSI model provides a conceptual way to understand network communication.

```text
Layer 7 ─ Application
Layer 6 ─ Presentation
Layer 5 ─ Session
Layer 4 ─ Transport
Layer 3 ─ Network
Layer 2 ─ Data Link
Layer 1 ─ Physical
```

---

# 5. OSI Layers

## Layer 7 — Application

Examples:

```text
HTTP
HTTPS
DNS
SMTP
SSH
FTP
```

This is where application-level protocols operate.

---

## Layer 6 — Presentation

Responsible conceptually for:

* Data representation
* Encoding
* Encryption
* Compression

Modern protocol stacks don't always map cleanly to this layer.

---

## Layer 5 — Session

Conceptually manages communication sessions.

Examples include:

* Session establishment
* Session management
* Session termination

---

## Layer 4 — Transport

Main protocols:

```text
TCP
UDP
```

Responsible for transport-level communication.

---

## Layer 3 — Network

Main concepts:

```text
IP
Routing
Packets
```

Routers primarily operate at this layer conceptually.

---

## Layer 2 — Data Link

Main concepts:

```text
MAC addresses
Frames
Ethernet
ARP-related local-network behavior
```

---

## Layer 1 — Physical

Examples:

```text
Ethernet cable
Fiber
Radio
Wi-Fi signals
Network hardware
```

---

# 6. TCP/IP Model

The TCP/IP model is more commonly used in practical networking.

```text
┌─────────────────────────┐
│ Application             │
├─────────────────────────┤
│ Transport               │
├─────────────────────────┤
│ Internet                │
├─────────────────────────┤
│ Network Access          │
└─────────────────────────┘
```

Examples:

```text
Application
    │
HTTP / DNS / SSH
    │
Transport
    │
TCP / UDP
    │
Internet
    │
IP
    │
Network Access
    │
Ethernet / Wi-Fi
```

---

# 7. Encapsulation

When an application sends data, information is added at different layers.

```text
Application Data
       ↓
TCP Header + Data
       ↓
IP Header + TCP Segment
       ↓
Ethernet Header + IP Packet
       ↓
Physical Transmission
```

Conceptually:

```text
Application
    ↓
Segment
    ↓
Packet
    ↓
Frame
    ↓
Bits
```

---

# 8. Decapsulation

The destination reverses the process.

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Application Data
```

Mental model:

```text
Sender

Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
 ↓
Network


Receiver

Frame
 ↓
Packet
 ↓
Segment
 ↓
Data
```

---

# 9. MAC Address

A MAC address identifies a network interface at the local network level.

Example:

```text
00:1A:2B:3C:4D:5E
```

MAC addresses are associated with Layer 2 networking.

Important distinction:

```text
MAC Address
    ↓
Local network identity

IP Address
    ↓
Network-layer addressing
```

Do not confuse MAC addresses with IP addresses.

---

# 10. IP Address

An IP address identifies a network endpoint at the IP layer.

Example IPv4:

```text
192.168.1.10
```

Another:

```text
10.0.0.25
```

An IPv4 address contains 32 bits.

```text
192 . 168 . 1 . 10
```

Each octet ranges from:

```text
0 → 255
```

---

# 11. Private IPv4 Address Ranges

Common private ranges:

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

These are commonly used inside private networks.

Example:

```text
Laptop
192.168.1.10

Router
192.168.1.1
```

---

# 12. Public vs Private IP

Private:

```text
192.168.1.10
```

Public:

```text
Internet-routable address
```

Typical architecture:

```text
Private Server
      │
      ▼
Private IP
      │
      ▼
NAT / Gateway
      │
      ▼
Public Internet
```

---

# 13. IPv4 vs IPv6

IPv4:

```text
32-bit
192.168.1.10
```

IPv6:

```text
128-bit
2001:db8::1
```

IPv6 provides a vastly larger address space.

For DevSecOps, I need to recognize IPv6 even when an environment primarily uses IPv4.

---

# 14. Subnet Mask

A subnet mask determines which portion of an IPv4 address represents the network and which portion represents hosts.

Example:

```text
IP:
192.168.1.10

Mask:
255.255.255.0
```

Equivalent CIDR:

```text
192.168.1.10/24
```

---

# 15. CIDR

CIDR means:

> Classless Inter-Domain Routing

Example:

```text
10.0.0.0/24
```

The `/24` indicates that 24 bits represent the network prefix.

Conceptually:

```text
Network bits | Host bits
-------------+-----------
24 bits      | 8 bits
```

For IPv4:

```text
32 total bits
```

Therefore:

```text
/24
=
24 network bits
+
8 host bits
```

---

# 16. Common CIDR Sizes

Understand these:

```text
/8
/16
/24
/25
/26
/27
/28
/29
/30
/32
```

Example:

```text
192.168.1.0/24
```

Commonly represents a 256-address block, with actual usable host capacity depending on the addressing environment and reserved addresses.

---

# 17. Why Subnetting Matters in DevSecOps

Subnetting allows networks to be separated.

Example:

```text
VPC
│
├── Public Subnet
│
├── Application Subnet
│
└── Database Subnet
```

Security architecture:

```text
Internet
   │
   ▼
Public Subnet
   │
   ▼
Application Subnet
   │
   ▼
Database Subnet
```

The database should generally not be directly exposed to the Internet.

---

# 18. Default Gateway

A default gateway is typically the router a host uses to reach destinations outside its local subnet.

Example:

```text
Host:
192.168.1.10

Gateway:
192.168.1.1
```

Traffic to another network:

```text
192.168.1.10
      │
      ▼
192.168.1.1
      │
      ▼
Other Network
```

---

# 19. ARP

ARP helps IPv4 hosts discover the MAC address associated with an IP address on the local network.

Conceptually:

```text
Host knows:

192.168.1.20

But needs:

MAC Address
```

ARP asks:

> Who has 192.168.1.20?

The appropriate device responds with its MAC address.

---

# 20. ARP Security

ARP has historically been vulnerable to spoofing attacks.

Conceptually:

```text
Victim
   │
   ▼
Attacker sends forged ARP information
   │
   ▼
Victim associates wrong MAC/IP mapping
```

Potential consequence:

```text
Man-in-the-Middle
```

Enterprise defenses can include:

* Dynamic ARP inspection
* Network segmentation
* Secure switching controls
* Monitoring
* Encryption such as TLS

---

# 21. DNS

DNS translates names into network addresses and provides other forms of naming information.

Example:

```text
example.com
     │
     ▼
DNS
     │
     ▼
IP Address
```

Instead of remembering:

```text
203.0.113.10
```

users access:

```text
example.com
```

---

# 22. DNS Resolution

A simplified flow:

```text
Application
    │
    ▼
Local Resolver
    │
    ▼
DNS Infrastructure
    │
    ▼
Authoritative DNS
    │
    ▼
IP Address
```

Then:

```text
Application
    │
    ▼
IP Address
```

---

# 23. DNS Record Types

Know these:

| Record | Purpose                    |
| ------ | -------------------------- |
| A      | IPv4 address               |
| AAAA   | IPv6 address               |
| CNAME  | Alias                      |
| MX     | Mail server                |
| NS     | Name server                |
| TXT    | Text/metadata              |
| PTR    | Reverse DNS                |
| SOA    | Zone authority information |

---

# 24. DNS Troubleshooting

Use:

```bash
dig example.com
```

or:

```bash
nslookup example.com
```

Check:

```text
Name
 ↓
Resolver
 ↓
DNS Response
 ↓
IP
```

If DNS fails:

```text
Application
   ↓
DNS lookup
   X
No IP
```

The application may appear to be "down" even though the application server itself is healthy.

---

# 25. TCP

TCP is a connection-oriented transport protocol.

TCP provides mechanisms for:

* Reliable delivery
* Ordering
* Retransmission
* Flow control
* Congestion control

Typical web traffic uses:

```text
HTTP → TCP
HTTPS → TCP
```

Traditional HTTPS uses TCP underneath TLS.

---

# 26. TCP Three-Way Handshake

The classic TCP connection establishment:

```text
Client                         Server

  SYN
   ───────────────────────────>

                         SYN + ACK
   <───────────────────────────

  ACK
   ───────────────────────────>

       Connection Established
```

Mental model:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

---

# 27. Why the TCP Handshake Matters

It helps explain:

* Connection failures
* SYN floods
* Firewall behavior
* Packet captures
* Latency
* TCP troubleshooting

Example:

```text
Client
  │
  │ SYN
  ▼
Firewall
  X
Blocked
```

The application may appear unavailable even though the server process is running.

---

# 28. UDP

UDP is connectionless at the transport layer and does not provide TCP-style delivery guarantees.

UDP is commonly used by protocols/applications such as:

* DNS
* DHCP
* VoIP
* Streaming
* QUIC-based traffic

UDP can provide lower overhead, but the application must handle reliability if required.

---

# 29. TCP vs UDP

| Feature                | TCP       | UDP                                  |
| ---------------------- | --------- | ------------------------------------ |
| Connection-oriented    | Yes       | No                                   |
| Reliability mechanisms | Yes       | No TCP-style reliability             |
| Ordering               | Yes       | No                                   |
| Retransmission         | Yes       | No                                   |
| Overhead               | Higher    | Lower                                |
| Common uses            | HTTP, SSH | DNS, streaming, QUIC-related traffic |

---

# 30. Ports

Ports identify services at the transport layer.

Common examples:

```text
22    SSH
53    DNS
80    HTTP
443   HTTPS
3306  MySQL
5432  PostgreSQL
6379  Redis
8080  Common application port
8443  Common alternate HTTPS
```

Important:

> **A port number does not guarantee what service is actually running there.**

Always verify.

---

# 31. Socket

A socket represents an endpoint for network communication.

Conceptually:

```text
IP Address + Port + Protocol
```

Example:

```text
192.168.1.10:443
```

A network connection can be represented using source and destination information.

```text
Client
192.168.1.20:51542
        │
        ▼
Server
192.168.1.10:443
```

---

# 32. Listening Ports

On Linux:

```bash
ss -tulpn
```

This can help identify listening sockets.

Example:

```text
LISTEN
0.0.0.0:22
0.0.0.0:80
0.0.0.0:443
```

Remember from Day 02:

> Network problems often require checking whether the expected service is actually listening.

---

# 33. Routing

Routing determines how packets reach other networks.

Example:

```text
Host
 │
 ▼
Default Gateway
 │
 ▼
Router
 │
 ▼
Internet
```

Check routes on Linux:

```bash
ip route
```

On macOS:

```bash
netstat -rn
```

---

# 34. Routing Table

Conceptually:

```text
Destination
    │
    ▼
Route
    │
    ▼
Next Hop
    │
    ▼
Interface
```

Example:

```text
default
192.168.1.1
```

means traffic without a more specific route can use the default route.

---

# 35. NAT

NAT means:

> Network Address Translation

Common home/enterprise scenario:

```text
Private Host
192.168.1.10
      │
      ▼
NAT Gateway
      │
      ▼
Public Internet
```

NAT allows private address space to communicate externally using translated addresses.

---

# 36. ICMP

ICMP is used for network control and diagnostic messaging.

A familiar example:

```bash
ping example.com
```

Ping commonly uses ICMP Echo Request and Echo Reply for IPv4.

Important:

> Ping failure does not automatically prove that the target is down.

ICMP may be blocked.

---

# 37. HTTP

HTTP is an application-layer protocol used for web communication.

Simplified:

```text
Client
  │
  │ HTTP Request
  ▼
Server
  │
  │ HTTP Response
  ▼
Client
```

Example:

```http
GET / HTTP/1.1
Host: example.com
```

Response:

```http
HTTP/1.1 200 OK
```

---

# 38. HTTP Methods

Know the common methods:

```text
GET
POST
PUT
PATCH
DELETE
HEAD
OPTIONS
```

Examples:

```text
GET
→ Retrieve resource

POST
→ Submit/create data

PUT
→ Replace resource

PATCH
→ Partially modify resource

DELETE
→ Delete resource
```

---

# 39. HTTP Status Codes

Important categories:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client-side error
5xx → Server-side error
```

Important examples:

```text
200 OK
201 Created
204 No Content

301 Moved Permanently
302 Found
304 Not Modified

400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
429 Too Many Requests

500 Internal Server Error
502 Bad Gateway
503 Service Unavailable
504 Gateway Timeout
```

---

# 40. HTTP vs HTTPS

HTTP:

```text
Client
  │
  │ HTTP
  ▼
Server
```

HTTPS:

```text
Client
  │
  │ TLS
  │
  ▼
Server
```

HTTPS provides encryption and authentication through TLS.

---

# 41. TLS

TLS provides cryptographic protection for network communication.

Conceptually:

```text
Client
   │
   │ TLS Handshake
   ▼
Server
   │
   ▼
Encrypted Application Traffic
```

TLS helps provide:

* Confidentiality
* Integrity
* Server authentication

---

# 42. HTTPS Mental Model

```text
HTTP Application Data
        │
        ▼
       TLS
        │
        ▼
      TCP
        │
        ▼
       IP
        │
        ▼
    Ethernet/Wi-Fi
```

This layered model is extremely important for troubleshooting.

---

# 43. TLS Certificate

When accessing:

```text
https://example.com
```

the server presents a certificate.

The certificate helps establish the server's identity.

Important concepts:

* Certificate
* Public key
* Private key
* Certificate Authority
* Certificate chain
* Expiration
* Hostname validation
* TLS versions
* Cipher suites

---

# 44. Reverse Proxy

A reverse proxy sits in front of backend servers.

```text
Internet
    │
    ▼
Reverse Proxy
    │
    ├──────────► Application 1
    │
    ├──────────► Application 2
    │
    └──────────► Application 3
```

Examples:

* Nginx
* HAProxy
* Apache HTTP Server
* Cloud-based reverse proxies

---

# 45. Why Use a Reverse Proxy?

Possible responsibilities:

* TLS termination
* Routing
* Load balancing
* Header manipulation
* Authentication integration
* Caching
* Rate limiting
* Access control

---

# 46. Forward Proxy

A forward proxy represents clients when accessing external destinations.

```text
Client
  │
  ▼
Forward Proxy
  │
  ▼
Internet
  │
  ▼
Destination
```

Difference:

```text
Forward Proxy
→ protects/represents clients

Reverse Proxy
→ protects/represents servers
```

---

# 47. Load Balancer

A load balancer distributes traffic across multiple backend systems.

```text
                 Load Balancer
                /      |      \
               /       |       \
              ▼        ▼        ▼
           Server 1 Server 2 Server 3
```

Benefits can include:

* Availability
* Scalability
* Traffic distribution
* Health checking
* Failover

---

# 48. Health Checks

A load balancer may check:

```text
GET /health
```

If:

```text
Server 1 → Healthy
Server 2 → Healthy
Server 3 → Unhealthy
```

traffic can be directed away from the unhealthy server depending on configuration.

---

# 49. Firewall

A firewall controls network traffic according to defined rules.

Example:

```text
Internet
   │
   ▼
Firewall
   │
   ├── Allow HTTPS
   ├── Allow SSH from trusted network
   └── Block everything else
```

A mature rule should consider:

* Source
* Destination
* Port
* Protocol
* Direction
* Environment
* Business requirement

---

# 50. Network Segmentation

Segmentation separates systems into security boundaries.

Example:

```text
                 Network
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      Web          App         DB
     Network      Network     Network
```

Potential policy:

```text
Internet → Web
Web → App
App → DB
Internet → DB ❌
```

This reduces attack surface and limits lateral movement.

---

# 51. WAF

WAF means:

> Web Application Firewall

A WAF focuses on HTTP/HTTPS application traffic.

Conceptually:

```text
Internet
    │
    ▼
   WAF
    │
    ▼
Load Balancer
    │
    ▼
Application
```

A WAF may help detect/block patterns associated with:

* SQL injection
* XSS
* Malicious requests
* Application-layer attacks
* Protocol anomalies

A WAF is not a replacement for secure coding.

---

# 52. Firewall vs WAF

| Control          | Primary Focus                 |
| ---------------- | ----------------------------- |
| Network Firewall | Network traffic               |
| WAF              | Web/application-layer traffic |

Example:

```text
Firewall
→ Should TCP/443 be allowed?

WAF
→ Is this HTTP request malicious?
```

---

# 53. VPC / Virtual Network Concept

Cloud networking builds isolated logical networks.

Generic model:

```text
Cloud
 │
 ▼
VPC / Virtual Network
 │
 ├── Public Subnet
 │
 ├── Private Application Subnet
 │
 └── Private Database Subnet
```

This becomes important when we reach AWS and Azure.

---

# 54. Security Groups / Network Rules

Cloud environments commonly provide network-level controls.

Conceptually:

```text
Application Server
       │
       ▼
Security Rule
       │
       ├── Allow 443
       ├── Allow App → DB
       └── Deny unnecessary traffic
```

Security should follow least privilege.

---

# 55. Complete Enterprise Traffic Flow

A typical web application may look like:

```text
                         INTERNET
                            │
                            ▼
                          DNS
                            │
                            ▼
                         CDN
                            │
                            ▼
                          WAF
                            │
                            ▼
                    Load Balancer
                            │
                            ▼
                     Reverse Proxy
                            │
                 ┌──────────┴──────────┐
                 ▼                     ▼
             App Server 1          App Server 2
                 │                     │
                 └──────────┬──────────┘
                            ▼
                       Application
                            │
                            ▼
                         Database
```

Every arrow represents a networking dependency.

---

# 56. What Happens When I Open HTTPS?

Suppose I open:

```text
https://example.com
```

The simplified sequence is:

```text
1. Application needs IP
        ↓
2. DNS resolution
        ↓
3. Route selected
        ↓
4. TCP connection established
        ↓
5. TLS handshake
        ↓
6. HTTP request
        ↓
7. Server processes request
        ↓
8. HTTP response
        ↓
9. TLS decrypts response
        ↓
10. Application displays result
```

This is one of the most important mental models of Day 03.

---

# 57. Troubleshooting by Layer

When an application is unavailable, don't randomly restart it.

Use a layered approach.

```text
Application Problem
       │
       ▼
DNS?
       │
       ▼
Routing?
       │
       ▼
TCP connectivity?
       │
       ▼
Port listening?
       │
       ▼
Firewall?
       │
       ▼
TLS?
       │
       ▼
HTTP?
       │
       ▼
Application?
       │
       ▼
Database?
```

---

# 58. DNS Troubleshooting

```bash
dig example.com
```

or:

```bash
nslookup example.com
```

Ask:

```text
Does DNS resolve?
      ↓
What IP was returned?
      ↓
Is it the expected IP?
```

---

# 59. Connectivity Troubleshooting

Test HTTP:

```bash
curl -I https://example.com
```

Verbose:

```bash
curl -v https://example.com
```

Test TCP:

```bash
nc -vz example.com 443
```

---

# 60. Route Troubleshooting

Linux:

```bash
ip route
```

macOS:

```bash
netstat -rn
```

Ask:

```text
Do I have a route?
       ↓
What is my gateway?
       ↓
Is traffic leaving through the expected interface?
```

---

# 61. Local Port Investigation

Linux:

```bash
ss -tulpn
```

macOS:

```bash
lsof -nP -iTCP -sTCP:LISTEN
```

Ask:

```text
Is the application listening?
       ↓
Which IP?
       ↓
Which port?
       ↓
Which process?
```

---

# 62. HTTP Troubleshooting

Use:

```bash
curl -v https://example.com
```

Look at:

```text
DNS
TCP
TLS
HTTP status
Headers
Redirects
Response
```

Example:

```text
DNS → SUCCESS
TCP → SUCCESS
TLS → SUCCESS
HTTP → 502
```

This immediately tells me that the problem is probably above basic network connectivity.

---

# 63. Network Troubleshooting Framework

Use:

```text
                 INCIDENT
                    │
                    ▼
                 CONFIRM
                    │
                    ▼
                  SCOPE
                    │
                    ▼
                  DNS
                    │
                    ▼
                 ROUTING
                    │
                    ▼
                  TCP
                    │
                    ▼
                 PORT
                    │
                    ▼
                FIREWALL
                    │
                    ▼
                  TLS
                    │
                    ▼
                  HTTP
                    │
                    ▼
              APPLICATION
                    │
                    ▼
               DEPENDENCIES
                    │
                    ▼
                ROOT CAUSE
```

This extends the Day 02 principle of **observe → collect evidence → form a hypothesis → test → validate**.

---

# 64. Network Security Threats

A DevSecOps engineer should recognize:

* Port exposure
* Unnecessary services
* Weak firewall rules
* Open management ports
* DNS abuse
* DNS spoofing
* ARP spoofing
* Man-in-the-middle attacks
* Network reconnaissance
* DDoS
* SYN floods
* Lateral movement
* Network segmentation failures
* Insecure protocols
* TLS misconfiguration
* Exposed databases
* Exposed Redis
* Exposed administrative interfaces

---

# 65. Attack Surface

Consider:

```text
Internet
   │
   ├── 22 SSH
   ├── 80 HTTP
   ├── 443 HTTPS
   ├── 3306 MySQL
   ├── 6379 Redis
   └── 8080 Application
```

The question is not:

> "Are the ports open?"

The professional question is:

> **"Which services need to be reachable, from where, and why?"**

---

# 66. Least Network Privilege

Bad:

```text
Internet
   │
   ▼
Database
   │
   └── 3306 OPEN TO WORLD
```

Better:

```text
Internet
   │
   ▼
Web
   │
   ▼
Application
   │
   ▼
Database
```

Only required communication should be allowed.

---

# 67. Network Reconnaissance

Authorized security testing may involve identifying:

```text
Hosts
 ↓
Open Ports
 ↓
Services
 ↓
Versions
 ↓
Network Relationships
 ↓
Attack Surface
```

Common defensive/security tools include:

```text
Nmap
Wireshark
tcpdump
curl
dig
ss
netcat
```

Use scanning only against systems you are authorized to test.

---

# 68. Packet Capture

Packet captures allow engineers to inspect network traffic.

Common tools:

```text
Wireshark
tcpdump
```

Conceptually:

```text
Application
    │
    ▼
Network Interface
    │
    ▼
Packet Capture
    │
    ▼
Analysis
```

Useful for troubleshooting:

* DNS failures
* TCP handshakes
* Retransmissions
* TLS negotiation
* HTTP traffic
* Unexpected connections

---

# 69. DevSecOps + Networking

Networking connects directly to everything learned so far.

```text
DevSecOps
    │
    ├── Linux
    │     ↓
    │   Network Interfaces
    │
    ├── CI/CD
    │     ↓
    │   Git / Registry Connections
    │
    ├── Containers
    │     ↓
    │   Container Networks
    │
    ├── Cloud
    │     ↓
    │   VPC / VNet
    │
    ├── Kubernetes
    │     ↓
    │   Services / Network Policies
    │
    └── Security
          ↓
      Firewall / WAF / Detection
```

---

# 70. Docker Networking Preview

Docker introduces virtual networking.

Conceptually:

```text
Host
 │
 ▼
Docker Network
 │
 ├── Container A
 ├── Container B
 └── Container C
```

Containers may communicate using:

* Bridge networks
* Host networking
* User-defined networks
* Port publishing

This will become important on Day 05.

---

# 71. Kubernetes Networking Preview

Kubernetes networking introduces concepts such as:

```text
Pod
 ↓
Pod IP
 ↓
Service
 ↓
Ingress
 ↓
Load Balancer
```

Later we will study:

* Cluster networking
* Services
* ClusterIP
* NodePort
* LoadBalancer
* Ingress
* NetworkPolicy
* DNS
* CNI

Day 03 gives the foundation required to understand them.

---

# 72. Cloud Networking Preview

Later:

```text
Cloud
 │
 ▼
VPC / VNet
 │
 ├── Subnets
 ├── Route Tables
 ├── Gateways
 ├── NAT
 ├── Security Controls
 └── Load Balancers
```

Without networking fundamentals, cloud networking becomes memorization.

With networking fundamentals, it becomes logical.

---

# 73. Production Scenario — Website Down

## Situation

Production reports:

```text
Website: DOWN
Server: UP
CPU: 25%
RAM: 40%
Disk: 30%
```

Do not immediately restart.

Investigate:

```text
DNS
 ↓
IP
 ↓
Route
 ↓
TCP 443
 ↓
Firewall
 ↓
TLS
 ↓
HTTP
 ↓
Load Balancer
 ↓
Application
```

---

# 74. Production Scenario — DNS Failure

Symptoms:

```text
Application
    │
    ▼
DNS Lookup
    X
Resolution failed
```

Investigate:

```bash
dig application.example.com
```

Then:

```text
Resolver
DNS record
Authoritative server
TTL
Network connectivity
Configuration
```

---

# 75. Production Scenario — Port Not Listening

Suppose:

```text
Application expected:
443
```

But:

```text
ss -tulpn
```

shows:

```text
8080
```

Possible issue:

```text
Application
   ↓
Listening on 8080
   X
Expected 443
```

Potential causes:

* Configuration change
* Deployment problem
* Reverse proxy issue
* Service startup failure
* Incorrect binding

---

# 76. Production Scenario — 502 Bad Gateway

Architecture:

```text
Client
  ↓
Load Balancer
  ↓
Reverse Proxy
  ↓
Application
```

Response:

```text
502 Bad Gateway
```

Do not immediately blame the application.

Investigate:

```text
Load Balancer
      ↓
Backend health
      ↓
Network connectivity
      ↓
Application port
      ↓
Application process
      ↓
Application logs
```

---

# 77. Production Scenario — 504 Gateway Timeout

A 504 may indicate that an intermediary did not receive a timely response from an upstream service.

Possible areas:

```text
Client
 ↓
Proxy
 ↓
Load Balancer
 ↓
Application
 ↓
Database
```

Investigate latency at every layer.

---

# 78. Security Scenario — Database Exposed

Suppose:

```text
Internet
   │
   ▼
203.0.113.x
   │
   ▼
TCP/3306
   │
   ▼
MySQL
```

Questions:

1. Why is the database Internet-accessible?
2. Is this required?
3. Can it be placed in a private subnet?
4. Which systems need access?
5. Are firewall rules restrictive?
6. Is authentication strong?
7. Is encryption enabled?
8. Is monitoring configured?

---

# 79. Security Scenario — SSH Exposed

Suppose:

```text
Internet
   │
   ▼
TCP/22
   │
   ▼
Production Server
```

A professional assessment asks:

```text
Is SSH publicly required?
        ↓
Can access be restricted?
        ↓
Can a bastion be used?
        ↓
Are keys used?
        ↓
Is MFA available?
        ↓
Are root logins disabled?
        ↓
Are logs monitored?
```

---

# 80. Day 03 Hands-On Lab

> Perform these exercises only on systems you own or are explicitly authorized to test.

Create a workspace:

```bash
mkdir -p ~/devsecops-lab/day03
cd ~/devsecops-lab/day03
```

---

# 81. Lab 1 — Identify Network Interfaces

### Linux

```bash
ip addr
```

### macOS

```bash
ifconfig
```

Record:

```text
Interface:
IP:
MAC:
Status:
```

---

# 82. Lab 2 — Routing Table

### Linux

```bash
ip route
```

### macOS

```bash
netstat -rn
```

Identify:

```text
Default route
Gateway
Interface
Local networks
```

---

# 83. Lab 3 — DNS

Run:

```bash
nslookup example.com
```

Then:

```bash
dig example.com
```

Record:

```text
Domain:
Resolver:
Returned IP:
```

Compare the results.

---

# 84. Lab 4 — HTTP

Run:

```bash
curl -I https://example.com
```

Observe:

```text
HTTP status
Server headers
Cache headers
Location
Security headers
```

Then:

```bash
curl -v https://example.com
```

Observe the connection stages.

---

# 85. Lab 5 — TCP Connectivity

Use:

```bash
nc -vz example.com 443
```

Understand:

```text
DNS
 ↓
IP
 ↓
TCP
 ↓
Port 443
```

Do not interpret a successful TCP connection as proof that the application itself is healthy.

---

# 86. Lab 6 — Local Listening Ports

### Linux

```bash
ss -tulpn
```

### macOS

```bash
lsof -nP -iTCP -sTCP:LISTEN
```

Record:

```text
Process
IP
Port
Protocol
```

Ask:

> Which services are actually exposed?

---

# 87. Lab 7 — HTTP Status Investigation

Run:

```bash
curl -I https://example.com
```

Identify:

```text
Status code
```

Then explain:

```text
What does the status mean?
```

Repeat against an authorized test application if available.

---

# 88. Lab 8 — DNS → TCP → TLS → HTTP

Use:

```bash
dig example.com
```

Then:

```bash
nc -vz example.com 443
```

Then:

```bash
curl -v https://example.com
```

Build this mental chain:

```text
DNS
 ↓
IP
 ↓
TCP 443
 ↓
TLS
 ↓
HTTP
 ↓
Response
```

---

# 89. Lab 9 — Packet Capture Introduction

If available on your system:

```bash
sudo tcpdump -i any
```

On macOS, identify the correct interface first:

```bash
ifconfig
```

Then capture traffic on the appropriate interface.

Stop with:

```text
CTRL+C
```

Do not capture traffic you are not authorized to inspect.

---

# 90. Lab 10 — Authorized Service Enumeration

On your own lab machine, identify listening services.

Linux:

```bash
ss -tulpn
```

Then optionally validate a known local service using a scanner.

For example, against your own host:

```bash
nmap 127.0.0.1
```

The objective is not aggressive exploitation.

The objective is:

```text
Discover
 ↓
Understand
 ↓
Verify
 ↓
Document
```

---

# 91. Lab 11 — Build a Network Diagram

Create:

```text
Internet
   │
   ▼
Router
   │
   ▼
Your Machine
   │
   ├── DNS
   ├── HTTP
   ├── HTTPS
   └── Local Services
```

Then document your actual environment.

---

# 92. Lab 12 — Troubleshooting Exercise

Simulate the following thought process:

```text
Website unavailable
       ↓
DNS works?
       ↓
TCP 443 reachable?
       ↓
TLS succeeds?
       ↓
HTTP response?
       ↓
Application healthy?
```

For every stage, record:

```text
Command
Expected result
Actual result
Conclusion
```

---

# 93. Network Troubleshooting Command Cheat Sheet

```bash
# Interfaces
ip addr
ifconfig

# Routing
ip route
netstat -rn

# DNS
dig example.com
nslookup example.com

# HTTP
curl -I https://example.com
curl -v https://example.com

# TCP
nc -vz example.com 443

# Listening services
ss -tulpn

# Packet capture
tcpdump

# Local connections - macOS
lsof -nP -i
```

---

# 94. Day 03 Security Checklist

* [ ] Understand OSI model
* [ ] Understand TCP/IP model
* [ ] Understand encapsulation
* [ ] Understand MAC addresses
* [ ] Understand IPv4
* [ ] Understand IPv6 basics
* [ ] Understand private IP ranges
* [ ] Understand public IPs
* [ ] Understand subnet masks
* [ ] Understand CIDR
* [ ] Understand default gateways
* [ ] Understand ARP
* [ ] Understand DNS
* [ ] Understand DNS records
* [ ] Understand TCP
* [ ] Understand UDP
* [ ] Understand TCP handshake
* [ ] Understand ports
* [ ] Understand sockets
* [ ] Understand routing
* [ ] Understand NAT
* [ ] Understand ICMP
* [ ] Understand HTTP
* [ ] Understand HTTPS
* [ ] Understand TLS
* [ ] Understand reverse proxies
* [ ] Understand forward proxies
* [ ] Understand load balancers
* [ ] Understand firewalls
* [ ] Understand WAF
* [ ] Understand network segmentation
* [ ] Understand cloud networking fundamentals
* [ ] Understand Docker networking basics
* [ ] Understand Kubernetes networking basics
* [ ] Complete DNS lab
* [ ] Complete TCP lab
* [ ] Complete HTTP lab
* [ ] Complete listening-port lab
* [ ] Complete troubleshooting exercise
* [ ] Build a network diagram
* [ ] Answer interview questions
* [ ] Solve production scenarios

---

# 🔥 Day 03 Interview Grill

Answer these **without searching first**.

## Beginner

1. What is a computer network?
2. What is the OSI model?
3. What is the TCP/IP model?
4. What is an IP address?
5. What is a MAC address?
6. What is a subnet mask?
7. What is CIDR?
8. What is a default gateway?
9. What is DNS?
10. What is a port?

---

## Intermediate

11. Explain TCP vs UDP.
12. Explain the TCP three-way handshake.
13. What is ARP?
14. What is routing?
15. What is NAT?
16. What is ICMP?
17. What is a socket?
18. What happens when you access `https://example.com`?
19. What is TLS?
20. What is the difference between HTTP and HTTPS?

---

## DevSecOps

21. Why does a DevSecOps engineer need networking knowledge?
22. What is the difference between a firewall and WAF?
23. What is a reverse proxy?
24. What is a load balancer?
25. Why is network segmentation important?
26. Why should databases generally not be Internet-facing?
27. How would you troubleshoot a 502?
28. How would you troubleshoot a 504?
29. How would you investigate an application that cannot connect to its database?
30. How can network configuration become a security vulnerability?

---

## Senior-Level Grill

31. A server is healthy but the application is unreachable. How do you investigate?

32. DNS resolves correctly, but TCP/443 fails. What possibilities do you investigate?

33. TCP/443 works, TLS fails. What could be wrong?

34. TLS works, but the server returns HTTP 502. Where do you investigate?

35. The application returns HTTP 200, but users report severe latency. What networking data would you investigate?

36. A database is reachable from the Internet. What risks exist?

37. A Kubernetes application cannot communicate with another service. What networking layers would you investigate?

38. A CI/CD runner cannot reach the container registry. What would you investigate?

39. A cloud application can access the Internet but cannot reach a private database. What networking components could be involved?

40. How would you design network segmentation for a production web application?

---

# 🧠 Day 03 Production Grill

## Scenario 1 — DNS Failure

Production:

```text
Application: DOWN
Server: UP
CPU: 30%
RAM: 45%
Disk: 25%
```

DNS lookup fails.

Think:

```text
Application
     ↓
DNS
     X
Resolution failure
```

Investigate:

```text
Resolver
DNS records
Authoritative DNS
Network connectivity
Configuration
```

---

# Scenario 2 — TCP Failure

```text
DNS: SUCCESS
TCP 443: FAILED
```

Think:

```text
DNS
 ↓
IP
 ↓
TCP
 X
```

Investigate:

```text
Firewall
Security group
Network ACL
Routing
Server listener
Network path
```

---

# Scenario 3 — TLS Failure

```text
DNS: SUCCESS
TCP 443: SUCCESS
TLS: FAILED
```

Investigate:

```text
Certificate
Certificate chain
Hostname
TLS version
Cipher compatibility
Proxy
Load balancer
Server configuration
```

---

# Scenario 4 — HTTP 502

```text
DNS: SUCCESS
TCP: SUCCESS
TLS: SUCCESS
HTTP: 502
```

Think:

```text
Network connectivity works.

Now investigate:

Load Balancer
     ↓
Reverse Proxy
     ↓
Backend
     ↓
Application
```

---

# Scenario 5 — Database Exposure

You discover:

```text
Internet
   │
   ▼
TCP/5432
   │
   ▼
PostgreSQL
```

Your task:

```text
Why is it exposed?
       ↓
Who needs access?
       ↓
Can it be private?
       ↓
Restrict source networks
       ↓
Authentication
       ↓
Encryption
       ↓
Logging
       ↓
Monitoring
```

---

# Scenario 6 — CI/CD Network Failure

A CI runner reports:

```text
Unable to connect to container registry
```

Investigate:

```text
DNS
 ↓
Route
 ↓
Firewall
 ↓
Proxy
 ↓
TLS
 ↓
Authentication
 ↓
Registry
```

Do not assume the registry is down.

---

# 🏗️ Day 03 Enterprise Architecture

Understand this diagram:

```text
                              INTERNET
                                  │
                                  ▼
                                DNS
                                  │
                                  ▼
                                CDN
                                  │
                                  ▼
                                WAF
                                  │
                                  ▼
                           LOAD BALANCER
                                  │
                                  ▼
                          REVERSE PROXY
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
               APP SERVER 1               APP SERVER 2
                    │                           │
                    └─────────────┬─────────────┘
                                  ▼
                             APPLICATION
                                  │
                         ┌────────┴────────┐
                         ▼                 ▼
                      CACHE             DATABASE
                         │                 │
                         └────────┬────────┘
                                  ▼
                              MONITORING
                                  │
                                  ▼
                                 SIEM
                                  │
                                  ▼
                              SECURITY
```

This is the networking foundation for the rest of the journey.

---

# 🔐 Day 03 Security Mental Model

Think:

```text
                  NETWORK SECURITY
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
     Identity          Traffic         Segmentation
        │                │                │
        ▼                ▼                ▼
      Access          Firewall          Subnets
                         │                │
                         ▼                ▼
                        WAF            Security Rules
                         │
                         ▼
                     Monitoring
                         │
                         ▼
                       SIEM
```

---

# 🔥 Day 03 Golden Rules

### Rule 1

> **DNS failure can look like an application failure.**

### Rule 2

> **A running process does not prove network reachability.**

### Rule 3

> **An open port does not prove an application is healthy.**

### Rule 4

> **A successful TCP connection does not prove HTTP is working.**

### Rule 5

> **A successful TLS handshake does not prove the backend application is healthy.**

### Rule 6

> **Never assume a port number identifies the service. Verify it.**

### Rule 7

> **Network access should follow least privilege.**

### Rule 8

> **Databases should not be unnecessarily exposed to untrusted networks.**

### Rule 9

> **Network segmentation limits blast radius.**

### Rule 10

> **Troubleshoot from evidence, not assumptions.**

---

# 🧩 Day 03 DevSecOps Connection

Today's concepts connect directly to future days:

```text
NETWORKING
    │
    ├── Linux
    │     ↓
    │   Interfaces / Routes / Sockets
    │
    ├── Git
    │     ↓
    │   Remote Repository Communication
    │
    ├── Docker
    │     ↓
    │   Container Networking
    │
    ├── CI/CD
    │     ↓
    │   Runners / Registries / APIs
    │
    ├── AWS
    │     ↓
    │   VPC / Subnets / Routing
    │
    ├── Kubernetes
    │     ↓
    │   Pods / Services / Ingress
    │
    ├── Security
    │     ↓
    │   Firewall / WAF / Segmentation
    │
    └── Observability
          ↓
       Network Logs
```

Day 02 established Linux networking commands such as `ip addr`, `ip route`, `ss`, `curl`, `dig`, and `nslookup`; Day 03 now explains **what those commands are actually inspecting**.

---

# 📊 Day 03 Deliverables

By the end of Day 03, I should have:

* [ ] Understood networking fundamentals
* [ ] Understood OSI
* [ ] Understood TCP/IP
* [ ] Understood IP addressing
* [ ] Understood private/public IPs
* [ ] Understood CIDR
* [ ] Understood subnetting fundamentals
* [ ] Understood MAC addresses
* [ ] Understood ARP
* [ ] Understood DNS
* [ ] Understood TCP
* [ ] Understood UDP
* [ ] Understood TCP handshake
* [ ] Understood ports
* [ ] Understood sockets
* [ ] Understood routing
* [ ] Understood NAT
* [ ] Understood ICMP
* [ ] Understood HTTP
* [ ] Understood HTTPS
* [ ] Understood TLS
* [ ] Understood reverse proxy
* [ ] Understood forward proxy
* [ ] Understood load balancer
* [ ] Understood firewall
* [ ] Understood WAF
* [ ] Understood network segmentation
* [ ] Understood cloud networking fundamentals
* [ ] Understood Docker networking basics
* [ ] Understood Kubernetes networking basics
* [ ] Completed DNS lab
* [ ] Completed TCP connectivity lab
* [ ] Completed HTTP/TLS lab
* [ ] Investigated local listening ports
* [ ] Performed basic packet capture
* [ ] Built network architecture diagram
* [ ] Solved production troubleshooting scenarios
* [ ] Answered interview questions

---

# 🏆 Day 03 Final Mental Model

```text
                         NETWORKING
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
             DNS             IP              MAC
              │               │               │
              └───────────────┼───────────────┘
                              ▼
                           ROUTING
                              │
                              ▼
                           TCP/UDP
                              │
                              ▼
                            PORT
                              │
                              ▼
                          FIREWALL
                              │
                              ▼
                             WAF
                              │
                              ▼
                       LOAD BALANCER
                              │
                              ▼
                        REVERSE PROXY
                              │
                              ▼
                         APPLICATION
                              │
                              ▼
                           DATABASE
                              │
                              ▼
                        MONITORING
                              │
                              ▼
                            SIEM
                              │
                              ▼
                       DEVSECOPS
```

---

# 🎯 Day 03 Final Challenge

Without searching, explain this complete request:

```text
I open:

https://example.com
```

Explain what happens from:

```text
1. Application
      ↓
2. DNS
      ↓
3. IP
      ↓
4. Routing
      ↓
5. TCP
      ↓
6. TLS
      ↓
7. HTTP
      ↓
8. Load Balancer
      ↓
9. Reverse Proxy
      ↓
10. Application
      ↓
11. Database
      ↓
12. Response
```

Then answer:

> **If the website is down, at which exact layer would you start investigating, and why?**

If I can explain this correctly, I have started developing the **networking mental model required for professional DevSecOps engineering**.

---

# 📈 Progress

**Day:** 03 / 30

**Topic:** Networking for DevSecOps

**Status:** 🟡 In Progress

**Theory:** ⬜

**Hands-on:** ⬜

**Troubleshooting:** ⬜

**Security Analysis:** ⬜

**Interview Grill:** ⬜

**Production Scenarios:** ⬜

**Documentation:** ⬜

---

# 🚀 Next — Day 04

> **Git & Version Control for DevSecOps**

We will move from:

```text
Day 01 → DevSecOps
Day 02 → Linux
Day 03 → Networking
                 ↓
Day 04 → Git
```

And connect Git to:

```text
Developer
    ↓
Git
    ↓
Branch
    ↓
Commit
    ↓
Pull Request
    ↓
Code Review
    ↓
CI/CD
    ↓
Security Scanning
    ↓
Build
    ↓
Deployment
```

The goal is to understand **Git not merely as a version-control tool, but as the security and change-management foundation of a modern DevSecOps pipeline.**
