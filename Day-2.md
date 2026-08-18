# 🐧 DevSecOps Engineer Journey — Day 02

> **Focus:** Linux for DevSecOps
> **Level:** Beginner → Professional
> **Goal:** Learn enough Linux to confidently operate, troubleshoot, secure, and automate production systems.

---

# 🎯 Day 02 Objectives

By the end of Day 02, I should understand:

* What Linux is and why DevSecOps engineers use it
* Linux filesystem
* Users and groups
* File permissions
* Processes
* Services
* systemd
* Logs
* Networking commands
* Ports and sockets
* Disk and memory
* Environment variables
* SSH
* Package management
* Bash fundamentals
* Linux security fundamentals
* Basic troubleshooting methodology
* How Linux fits into DevSecOps

Most importantly:

> **I should be able to investigate a Linux production problem without randomly restarting things.**

---

# 1. Why Linux Matters to DevSecOps

A huge amount of modern infrastructure runs on Linux.

A typical production architecture might look like:

```text
                         INTERNET
                            │
                            ▼
                    ┌───────────────┐
                    │      CDN      │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────┐
                    │ Load Balancer │
                    └───────┬───────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     Linux Server    │
                 │                     │
                 │ ┌─────────────────┐ │
                 │ │   Application   │ │
                 │ └─────────────────┘ │
                 │                     │
                 │ ┌─────────────────┐ │
                 │ │     Nginx       │ │
                 │ └─────────────────┘ │
                 │                     │
                 │ ┌─────────────────┐ │
                 │ │ Docker/K8s      │ │
                 │ └─────────────────┘ │
                 └─────────────────────┘
                            │
                            ▼
                         Database
```

Even if you eventually work heavily with:

* AWS
* Azure
* Kubernetes
* Terraform
* Docker
* Jenkins
* GitHub Actions

you will still encounter Linux concepts.

---

# 2. Linux Mental Model

Think about Linux as several layers:

```text
┌─────────────────────────────┐
│        Applications         │
├─────────────────────────────┤
│        Shell / CLI          │
├─────────────────────────────┤
│       System Libraries      │
├─────────────────────────────┤
│           Kernel            │
├─────────────────────────────┤
│          Hardware           │
└─────────────────────────────┘
```

The **kernel** manages resources such as:

* CPU
* Memory
* Processes
* Devices
* Networking
* Filesystems

---

# 3. Linux Distribution

Linux itself is the kernel.

A distribution combines Linux with additional software.

Examples:

```text
Ubuntu
Debian
Fedora
RHEL
Rocky Linux
AlmaLinux
Amazon Linux
Arch Linux
```

In enterprise DevSecOps environments, you will frequently encounter distributions such as:

```text
Ubuntu
RHEL
Amazon Linux
Debian
```

---

# 4. Terminal and Shell

When you open a terminal, you're interacting with a shell.

Common shells:

```text
bash
zsh
fish
sh
```

Your Mac commonly uses `zsh`.

Linux servers frequently use:

```bash
bash
```

The shell allows you to interact with the operating system.

Example:

```bash
pwd
```

```bash
ls
```

```bash
cd /tmp
```

---

# 5. Current Directory

Check where you are:

```bash
pwd
```

Example:

```text
/home/amit
```

`pwd` means:

> **Print Working Directory**

---

# 6. Listing Files

Basic:

```bash
ls
```

Detailed:

```bash
ls -l
```

Including hidden files:

```bash
ls -la
```

Human-readable:

```bash
ls -lah
```

You'll frequently use:

```bash
ls -lah
```

---

# 7. Linux Filesystem

Unlike Windows, Linux doesn't primarily use:

```text
C:
D:
E:
```

Linux starts from:

```text
/
```

This is called the **root filesystem**.

A simplified filesystem:

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

---

# 8. Important Linux Directories

## `/etc`

Configuration.

Examples:

```text
/etc/ssh/
/etc/nginx/
/etc/hosts
/etc/passwd
/etc/group
```

Think:

> **Configuration lives here.**

---

## `/var`

Variable data.

Common examples:

```text
/var/log
/var/lib
/var/cache
```

Logs frequently live under:

```text
/var/log
```

---

## `/home`

Normal users' home directories.

Example:

```text
/home/amit
/home/bob
```

---

## `/root`

Home directory of the root user.

Important:

```text
/root
```

is different from:

```text
/
```

---

## `/tmp`

Temporary files.

Applications often use it for temporary data.

Do not assume everything inside `/tmp` is harmless.

---

## `/usr`

Userland programs and libraries.

You'll often see:

```text
/usr/bin
/usr/sbin
/usr/lib
```

---

## `/proc`

A virtual filesystem exposing kernel/process information.

For example:

```bash
cat /proc/cpuinfo
```

```bash
cat /proc/meminfo
```

You can investigate a process:

```bash
ls /proc/<PID>
```

This becomes extremely useful during troubleshooting.

---

# 9. Absolute vs Relative Paths

Absolute:

```text
/etc/nginx/nginx.conf
```

Starts from `/`.

Relative:

```text
./config/nginx.conf
```

Relative to the current directory.

Special paths:

```text
.
..
~
/
```

Meaning:

```text
.   = current directory
..  = parent directory
~   = home directory
/   = filesystem root
```

---

# 10. Creating Files and Directories

Directory:

```bash
mkdir test
```

Nested directories:

```bash
mkdir -p project/logs/app
```

Create file:

```bash
touch test.txt
```

---

# 11. Copying Files

```bash
cp source.txt destination.txt
```

Directory:

```bash
cp -r source_dir destination_dir
```

---

# 12. Moving and Renaming

```bash
mv old.txt new.txt
```

Move:

```bash
mv file.txt /tmp/
```

---

# 13. Removing

File:

```bash
rm file.txt
```

Directory:

```bash
rm -r directory
```

Be extremely careful with:

```bash
rm -rf
```

Especially as root.

A command like:

```bash
rm -rf /
```

can be catastrophic on systems where protections don't stop it.

Professional rule:

> **Never run destructive commands you don't fully understand.**

---

# 14. Reading Files

```bash
cat file.txt
```

For large files:

```bash
less file.txt
```

First lines:

```bash
head file.txt
```

Last lines:

```bash
tail file.txt
```

Last 100:

```bash
tail -n 100 file.txt
```

Follow a changing log:

```bash
tail -f application.log
```

This is extremely useful in operations.

---

# 15. Searching Files

Find files:

```bash
find /var/log -type f
```

Find a specific filename:

```bash
find /var/log -name "*.log"
```

Search text:

```bash
grep "ERROR" application.log
```

Case-insensitive:

```bash
grep -i "error" application.log
```

Recursive:

```bash
grep -R "password" /etc
```

Be careful with recursive searches over sensitive files.

---

# 16. Pipes

One of the most important Linux concepts.

Example:

```bash
ps aux | grep nginx
```

The output of one command becomes the input of another.

Mental model:

```text
Command A
    │
    ▼
   pipe
    │
    ▼
Command B
```

Example:

```bash
cat access.log | grep "500"
```

Better:

```bash
grep "500" access.log
```

Avoid unnecessary pipelines.

---

# 17. Redirection

Output to a file:

```bash
command > output.txt
```

Append:

```bash
command >> output.txt
```

Redirect errors:

```bash
command 2> errors.txt
```

Both output and errors:

```bash
command > output.txt 2>&1
```

---

# 18. Users

Linux is multi-user.

View current user:

```bash
whoami
```

View user identity:

```bash
id
```

Example:

```text
uid=1000(amit) gid=1000(amit) groups=1000(amit)
```

---

# 19. Root

`root` is the superuser.

```text
root
UID 0
```

Root has extensive privileges.

Professional DevSecOps principle:

> **Don't use root when you don't need root.**

This is the principle of **least privilege**.

---

# 20. Users and Groups

List users:

```bash
cat /etc/passwd
```

Groups:

```bash
cat /etc/group
```

Current user's groups:

```bash
groups
```

Why groups matter:

```text
Developer
   │
   ├── docker
   ├── developers
   └── monitoring
```

Group membership determines access to resources.

---

# 21. File Permissions

Run:

```bash
ls -l
```

Example:

```text
-rwxr-xr--
```

Break it down:

```text
- rwx r-x r--
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── Owner
└──────────── File type
```

Permissions:

```text
r = read
w = write
x = execute
```

---

# 22. Permission Numbers

Linux permissions can be represented numerically.

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
rwx = 7
rw- = 6
r-x = 5
r-- = 4
```

Example:

```bash
chmod 755 script.sh
```

Means:

```text
Owner  = rwx = 7
Group  = r-x = 5
Others = r-x = 5
```

---

# 23. Security Importance of Permissions

Bad:

```bash
chmod 777 secret.txt
```

This potentially gives:

```text
Everyone:
read
write
execute
```

That's usually dangerous.

Better:

```text
Least privilege
```

For sensitive files, permissions should be deliberately restricted.

---

# 24. Ownership

Check:

```bash
ls -l
```

Example:

```text
-rw-------  1 amit  staff  secret.txt
```

The owner and group matter.

Change owner:

```bash
chown user:group file
```

Change group:

```bash
chgrp group file
```

These operations typically require elevated privileges when changing ownership to another user.

---

# 25. Processes

A running program becomes a process.

View processes:

```bash
ps aux
```

Interactive:

```bash
top
```

On many Linux systems:

```bash
htop
```

Process IDs are called:

```text
PID
```

---

# 26. Process Tree

Processes can have parent-child relationships.

Example:

```text
systemd
   │
   ├── nginx
   │    ├── worker
   │    └── worker
   │
   ├── sshd
   │    └── bash
   │
   └── application
```

Useful command:

```bash
pstree
```

---

# 27. Killing Processes

Find PID:

```bash
ps aux | grep application
```

Then:

```bash
kill <PID>
```

A stronger signal:

```bash
kill -9 <PID>
```

Do **not** make `kill -9` your first choice.

Preferred approach:

```text
Graceful termination
       ↓
Observe
       ↓
Force kill only if necessary
```

Why?

Applications may need time to:

* Finish requests
* Close connections
* Flush buffers
* Save state
* Release resources

---

# 28. CPU Troubleshooting

Check:

```bash
top
```

Look for:

```text
CPU utilization
Load average
Memory
Processes
```

If CPU is high:

```text
Which process?
        ↓
Why is it consuming CPU?
        ↓
Application issue?
        ↓
Infinite loop?
        ↓
High traffic?
        ↓
Cryptominer?
        ↓
Compression?
        ↓
Database?
```

Never jump directly to:

```bash
kill -9
```

---

# 29. Memory

Check:

```bash
free -h
```

You want to understand:

```text
Total
Used
Free
Available
Swap
```

High memory usage doesn't automatically mean something is wrong.

Linux intentionally uses memory for caching.

The important question is:

> **Is the system under memory pressure?**

---

# 30. Disk Space

Check:

```bash
df -h
```

Example:

```text
Filesystem
Size
Used
Available
Use%
```

Find large directories:

```bash
du -sh *
```

Or:

```bash
du -sh /var/*
```

Production issue:

```text
Disk = 100%
```

Possible consequences:

```text
Logs cannot be written
Database cannot write
Application crashes
Package installations fail
Containers fail
```

---

# 31. Inodes

Sometimes:

```text
Disk space = available
```

but the filesystem still cannot create files.

Check:

```bash
df -i
```

Why?

You may have exhausted **inodes**.

Think:

```text
Disk capacity
+
File/inode capacity
```

Both matter.

---

# 32. Services

Modern Linux distributions commonly use `systemd`.

Check service:

```bash
systemctl status nginx
```

Start:

```bash
sudo systemctl start nginx
```

Stop:

```bash
sudo systemctl stop nginx
```

Restart:

```bash
sudo systemctl restart nginx
```

Enable on boot:

```bash
sudo systemctl enable nginx
```

---

# 33. systemd Mental Model

```text
                    systemd
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
      nginx           ssh           app.service
        │              │              │
        ▼              ▼              ▼
     Process        Process        Process
```

systemd manages services and their lifecycle.

---

# 34. Logs

Logs are one of your most important operational tools.

Traditional logs may exist under:

```text
/var/log
```

With systemd:

```bash
journalctl
```

Service logs:

```bash
journalctl -u nginx
```

Follow logs:

```bash
journalctl -u nginx -f
```

Recent logs:

```bash
journalctl -u nginx --since "1 hour ago"
```

---

# 35. Production Troubleshooting Pattern

Suppose:

> Application is returning HTTP 500.

Don't randomly restart.

Use:

```text
                  HTTP 500
                     │
                     ▼
                Application?
                     │
              ┌──────┴──────┐
              │             │
             YES            NO
              │             │
              ▼             ▼
          Check logs    Check upstream
              │             │
              ▼             ▼
          Process?       Network?
              │             │
              ▼             ▼
           Memory?       Database?
              │             │
              ▼             ▼
            Disk?        DNS?
              │             │
              └──────┬──────┘
                     ▼
                  Root Cause
```

---

# 36. Networking Fundamentals

Check interfaces:

```bash
ip addr
```

Routes:

```bash
ip route
```

Connections:

```bash
ss -tulpn
```

This is extremely useful.

Example:

```text
LISTEN
0.0.0.0:22
0.0.0.0:80
0.0.0.0:443
```

You can determine what services are listening.

---

# 37. Ports

Common ports:

| Port | Protocol / Service      |
| ---: | ----------------------- |
|   22 | SSH                     |
|   53 | DNS                     |
|   80 | HTTP                    |
|  443 | HTTPS                   |
| 3306 | MySQL                   |
| 5432 | PostgreSQL              |
| 6379 | Redis                   |
| 8080 | Common application port |
| 8443 | Common alternate HTTPS  |

Do not assume a port guarantees a particular service.

Always verify.

---

# 38. Test Connectivity

DNS:

```bash
dig example.com
```

or:

```bash
nslookup example.com
```

HTTP:

```bash
curl -I https://example.com
```

Verbose HTTP:

```bash
curl -v https://example.com
```

Test TCP connectivity:

```bash
nc -vz example.com 443
```

---

# 39. DNS Troubleshooting

Imagine:

```text
Application
    ↓
Database hostname
    ↓
DNS
    X
Resolution fails
```

Check:

```bash
dig database.internal
```

Then investigate:

```text
DNS record
DNS server
Resolver
Network
Firewall
Search domain
TTL
```

---

# 40. SSH

SSH is fundamental to Linux operations.

Basic:

```bash
ssh user@server
```

Private key:

```bash
ssh -i key.pem user@server
```

Copy file:

```bash
scp file.txt user@server:/tmp/
```

SSH architecture:

```text
Your Machine
     │
     │ SSH
     ▼
┌───────────────┐
│ Linux Server  │
│               │
│ sshd          │
└───────────────┘
```

---

# 41. SSH Security

Avoid weak practices such as:

```text
root login from anywhere
password authentication
shared accounts
weak passwords
permanent credentials
```

Prefer:

```text
SSH keys
Least privilege
MFA where supported
Restricted access
Bastion / controlled access
Logging
Credential rotation
```

---

# 42. Environment Variables

Check:

```bash
env
```

or:

```bash
printenv
```

Example:

```bash
export APP_ENV=development
```

Read:

```bash
echo "$APP_ENV"
```

Environment variables are commonly used for application configuration.

But:

> **Do not treat environment variables as automatically secure secret storage.**

Secrets need appropriate management.

---

# 43. PATH

Check:

```bash
echo "$PATH"
```

Example:

```text
/usr/local/bin:/usr/bin:/bin
```

When you run:

```bash
python
```

the shell searches directories in `PATH`.

Find executable:

```bash
which python
```

or:

```bash
command -v python
```

---

# 44. Package Management

Ubuntu/Debian:

```bash
apt
```

Example:

```bash
sudo apt update
```

RHEL-based systems:

```bash
dnf
```

or historically:

```bash
yum
```

Package management matters for security because vulnerable packages must be updated.

---

# 45. Linux Security Model

Important security concepts:

```text
Users
Groups
Permissions
Processes
Capabilities
Namespaces
SELinux/AppArmor
Firewall
SSH
Logging
Updates
Least privilege
```

Linux security is much deeper than file permissions.

---

# 46. Firewall

Depending on the distribution/environment, you may encounter:

```text
iptables
nftables
ufw
firewalld
```

Conceptually:

```text
Internet
   │
   ▼
Firewall
   │
   ├── Allow 443
   ├── Allow 22 from trusted network
   └── Block everything else
```

Don't blindly disable firewalls during troubleshooting.

---

# 47. Linux Capabilities

Linux can divide some root privileges into capabilities.

Examples include:

```text
CAP_NET_ADMIN
CAP_NET_RAW
CAP_SYS_ADMIN
```

This matters heavily for containers.

Instead of:

```text
Container = root with everything
```

we want:

```text
Container
   ↓
Minimum required privileges
```

This is a major DevSecOps security concept.

---

# 48. Bash Basics

A DevSecOps engineer should be comfortable writing basic shell scripts.

Example:

```bash
#!/usr/bin/env bash

echo "DevSecOps"
```

Variables:

```bash
NAME="Amit"

echo "$NAME"
```

Condition:

```bash
if [ -f "config.yaml" ]; then
    echo "Config exists"
fi
```

Loop:

```bash
for file in *.log; do
    echo "$file"
done
```

Exit status:

```bash
echo $?
```

---

# 49. Why Exit Codes Matter

Linux commands return exit codes.

Usually:

```text
0 = success
non-zero = failure
```

Example:

```bash
mkdir test
echo $?
```

CI/CD pipelines depend heavily on exit codes.

For example:

```text
Security Scanner
       │
       ▼
Exit 0 → Pipeline continues

Exit non-zero → Pipeline may fail
```

This is one of the bridges between Linux and DevSecOps.

---

# 50. Command Chaining

AND:

```bash
command1 && command2
```

Meaning:

> Run command2 only if command1 succeeds.

OR:

```bash
command1 || command2
```

Meaning:

> Run command2 if command1 fails.

Example:

```bash
docker build . && docker run app
```

---

# 51. Production Incident Example

## Situation

You receive an alert:

```text
Application unavailable
```

Do NOT immediately restart.

Start with:

```bash
uptime
```

Then:

```bash
df -h
```

Then:

```bash
free -h
```

Then:

```bash
ps aux
```

Then:

```bash
ss -tulpn
```

Then inspect service:

```bash
systemctl status <service>
```

Then logs:

```bash
journalctl -u <service> --since "30 minutes ago"
```

Then application logs.

Then network:

```bash
curl -v http://localhost:<port>
```

Now you can start building a hypothesis.

---

# 52. Troubleshooting Framework

Use this methodology:

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
                  COLLECT DATA
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
      CPU            Memory          Disk
        │              │              │
        └──────────────┼──────────────┘
                       ▼
                    Network
                       │
                       ▼
                    Process
                       │
                       ▼
                    Service
                       │
                       ▼
                     Logs
                       │
                       ▼
                  Dependencies
                       │
                       ▼
                  ROOT CAUSE
                       │
                       ▼
                   MITIGATION
                       │
                       ▼
                   VALIDATION
                       │
                       ▼
                 DOCUMENTATION
```

---

# 53. Never Troubleshoot by Guessing

Weak operational approach:

```text
Website broken
 ↓
Restart server
 ↓
Still broken
 ↓
Restart database
 ↓
Still broken
 ↓
Restart Kubernetes
```

This can make incidents worse.

Professional approach:

```text
Observe
 ↓
Hypothesis
 ↓
Test
 ↓
Evidence
 ↓
Change
 ↓
Observe
```

---

# 54. Day 02 Hands-On Lab

Create a workspace:

```bash
mkdir -p ~/devsecops-lab/day02
cd ~/devsecops-lab/day02
```

Create files:

```bash
touch app.log
touch secrets.txt
mkdir logs
mkdir config
```

Check:

```bash
ls -lah
```

Create sample log data:

```bash
printf '%s\n' \
'INFO application started' \
'INFO listening on port 8080' \
'WARN database latency high' \
'ERROR database connection failed' \
'INFO retrying connection' \
'ERROR request returned 500' \
> app.log
```

Search:

```bash
grep "ERROR" app.log
```

Count errors:

```bash
grep -c "ERROR" app.log
```

Follow the log:

```bash
tail -f app.log
```

Press:

```text
CTRL+C
```

to stop.

---

# 55. Process Lab

Run:

```bash
sleep 300 &
```

Find it:

```bash
ps aux | grep sleep
```

Find the PID.

Then terminate it gracefully:

```bash
kill <PID>
```

Verify:

```bash
ps aux | grep sleep
```

---

# 56. Disk Lab

Run:

```bash
df -h
```

Then:

```bash
df -i
```

Then:

```bash
du -sh ~/devsecops-lab
```

Understand the difference between:

```text
Disk capacity
```

and:

```text
Inode availability
```

---

# 57. Network Lab

Run:

```bash
ip addr
```

On macOS, if `ip` isn't available, use:

```bash
ifconfig
```

Check routes:

```bash
netstat -rn
```

Check DNS:

```bash
nslookup example.com
```

Check HTTPS:

```bash
curl -I https://example.com
```

Check detailed connection:

```bash
curl -v https://example.com
```

---

# 58. Service Investigation Lab

On Linux:

```bash
systemctl --type=service
```

Check SSH:

```bash
systemctl status ssh
```

Depending on the distribution, the service may be:

```bash
systemctl status sshd
```

On macOS, don't expect `systemctl` to work because macOS uses a different service-management architecture.

This distinction is important.

> **Don't blindly copy Linux commands onto macOS.**

---

# 59. Security Lab

Create:

```bash
echo "demo-secret" > secrets.txt
```

Check permissions:

```bash
ls -l secrets.txt
```

Change to owner-only:

```bash
chmod 600 secrets.txt
```

Check again:

```bash
ls -l secrets.txt
```

Understand:

```text
600

Owner  = rw-
Group  = ---
Others = ---
```

---

# 60. Bash Lab

Create:

```bash
nano check.sh
```

Add:

```bash
#!/usr/bin/env bash

echo "DevSecOps Linux Check"

echo "User: $(whoami)"
echo "Hostname: $(hostname)"
echo "Kernel:"
uname -a

echo "Disk:"
df -h

echo "Memory:"
free -h 2>/dev/null || echo "free command unavailable on this OS"
```

Make executable:

```bash
chmod +x check.sh
```

Run:

```bash
./check.sh
```

---

# 61. Day 02 DevSecOps Connection

Everything learned today connects to later topics.

```text
Linux
 │
 ├── Processes
 │      ↓
 │   Containers
 │
 ├── Networking
 │      ↓
 │   Kubernetes
 │
 ├── Permissions
 │      ↓
 │   IAM / RBAC
 │
 ├── Filesystems
 │      ↓
 │   Container Storage
 │
 ├── Services
 │      ↓
 │   systemd / Kubernetes
 │
 ├── Logs
 │      ↓
 │   Observability / SIEM
 │
 ├── Shell
 │      ↓
 │   CI/CD Automation
 │
 └── Security
        ↓
     Runtime Security
```

---

# 🔥 Day 02 Interview Grill

Answer these **without searching first**.

## Beginner

1. What is Linux?
2. What is the Linux kernel?
3. What is a shell?
4. What does `pwd` do?
5. What is `/etc` used for?
6. What is `/var/log` used for?
7. What is `/proc`?
8. What is the difference between `/` and `/root`?
9. What does `sudo` do?
10. What is root?

---

## Intermediate

11. Explain Linux file permissions.

12. What does `chmod 755` mean?

13. What does `chmod 600` mean?

14. What is a PID?

15. What's the difference between a process and a service?

16. What is systemd?

17. What is `journalctl`?

18. What is the difference between `df` and `du`?

19. What are inodes?

20. What does `ss -tulpn` show?

---

## DevSecOps

21. Why does a DevSecOps engineer need Linux?

22. Why are file permissions important for security?

23. Why is running applications as root dangerous?

24. Why do CI/CD pipelines care about exit codes?

25. Why is log analysis important in DevSecOps?

26. Why is process monitoring important?

27. Why does network troubleshooting matter to DevSecOps?

28. Why are Linux capabilities important for container security?

---

# 🧠 Day 02 Production Grill

## Scenario 1 — Disk Full

Production server:

```text
CPU:       25%
RAM:       40%
Disk:     100%
Application: DOWN
```

What do you investigate?

Expected thought process:

```text
df -h
   ↓
Which filesystem?
   ↓
du
   ↓
Which directory?
   ↓
Logs?
Temporary files?
Container data?
Database?
Core dumps?
   ↓
Can space be safely reclaimed?
   ↓
Why did it happen?
   ↓
Prevent recurrence
```

---

# Scenario 2 — High CPU

```text
CPU: 98%
RAM: 40%
Disk: 20%
```

Don't immediately kill processes.

Investigate:

```text
top
 ↓
Which PID?
 ↓
Which process?
 ↓
What application?
 ↓
What changed?
 ↓
Traffic increase?
 ↓
Infinite loop?
 ↓
Crypto miner?
 ↓
Database query?
 ↓
Deployment?
```

---

# Scenario 3 — Application Down

```text
Application: DOWN
Server: UP
CPU: Normal
RAM: Normal
Disk: Normal
```

Investigate:

```text
systemctl status
        ↓
Process exists?
        ↓
Port listening?
        ↓
ss -tulpn
        ↓
Logs
        ↓
Dependencies
        ↓
Network
        ↓
Configuration
```

---

# Scenario 4 — Security Incident

You discover:

```text
Unknown process
CPU: 95%
Network connections: active
```

Possible causes include:

```text
Legitimate workload
Bug
Unexpected process
Compromised host
Cryptominer
Malware
```

Your first objective is:

> **Collect evidence and understand the situation before destroying evidence.**

In a real incident, response procedures and authorization matter.

---

# 🧩 Day 02 Command Cheat Sheet

```bash
# System
uname -a
hostname
uptime

# User
whoami
id
groups

# Files
pwd
ls -lah
cd
mkdir
touch
cp
mv
rm

# File inspection
cat
less
head
tail
grep
find

# Processes
ps aux
top
htop
pstree
kill

# Disk
df -h
df -i
du -sh

# Memory
free -h

# Networking
ip addr
ip route
ss -tulpn
curl
dig
nslookup
nc

# Services
systemctl
journalctl

# Permissions
ls -l
chmod
chown
chgrp

# Environment
env
printenv
echo "$PATH"

# Identity
sudo

# Shell
bash
echo
export
```

---

# 📋 Day 02 Deliverables

* [ ] Understand Linux architecture
* [ ] Understand Linux filesystem
* [ ] Understand `/etc`
* [ ] Understand `/var`
* [ ] Understand `/proc`
* [ ] Understand `/tmp`
* [ ] Understand users
* [ ] Understand groups
* [ ] Understand root
* [ ] Understand permissions
* [ ] Understand `chmod`
* [ ] Understand `chown`
* [ ] Understand processes
* [ ] Understand PIDs
* [ ] Understand services
* [ ] Understand systemd
* [ ] Understand logs
* [ ] Understand `journalctl`
* [ ] Understand CPU troubleshooting
* [ ] Understand memory troubleshooting
* [ ] Understand disk troubleshooting
* [ ] Understand inodes
* [ ] Understand basic networking
* [ ] Understand SSH
* [ ] Understand environment variables
* [ ] Understand exit codes
* [ ] Complete Linux lab
* [ ] Complete security lab
* [ ] Answer interview questions
* [ ] Solve production scenarios

---

# 🏆 Day 02 Golden Rules

### 1.

> **Observe before changing production.**

### 2.

> **Don't use root unnecessarily.**

### 3.

> **Don't blindly use `kill -9`.**

### 4.

> **Disk space and inode exhaustion are different problems.**

### 5.

> **A running process is not necessarily a healthy application.**

### 6.

> **A healthy server does not necessarily mean a healthy application.**

### 7.

> **Logs are evidence, not just text.**

### 8.

> **Network problems often look like application problems.**

### 9.

> **Exit codes are fundamental to automation.**

### 10.

> **Security starts at the operating-system level.**

---

# 🧠 Day 02 Final Mental Model

```text
                         LINUX

                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
       USERS           PROCESSES         FILESYSTEM
          │                │                │
          ▼                ▼                ▼
     PERMISSIONS        SERVICES          /etc
          │                │               /var
          ▼                ▼               /proc
       SECURITY         systemd             /tmp
          │                │                │
          └────────────────┼────────────────┘
                           │
                           ▼
                        NETWORK
                           │
                  ┌────────┼────────┐
                  ▼        ▼        ▼
                 DNS      TCP      HTTP
                  │        │        │
                  └────────┼────────┘
                           ▼
                        LOGGING
                           │
                           ▼
                    TROUBLESHOOTING
                           │
                           ▼
                    DEVSECOPS ENGINEER
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
       Docker          Kubernetes          CI/CD
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                       PRODUCTION
```

---

# 🚀 What Comes Next

**Day 01:** DevSecOps foundations ✅

**Day 02:** Linux fundamentals ← **You are here**

**Day 03:** Networking for DevSecOps

On Day 03, we'll build the networking foundation needed to understand:

```text
DNS
 ↓
TCP/IP
 ↓
Ports
 ↓
HTTP/HTTPS
 ↓
TLS
 ↓
Reverse Proxy
 ↓
Load Balancer
 ↓
Firewall
 ↓
WAF
 ↓
VPC
 ↓
Kubernetes Networking
```

That day will be especially important because later, when we reach **AWS, Kubernetes, cloud security, CI/CD, and production incident response**, you'll already understand what's actually happening underneath.
