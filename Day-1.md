# 🚀 DevSecOps Engineer Journey —> Day 01

> **Goal:** Build a strong foundation in DevSecOps from zero, understand how modern software moves from developer code to production, and develop the operational/security mindset required for a professional DevSecOps Engineer.

---

## 📌 Learning Journey

This 30-day journey is designed to progress from:

```text
Beginner
   ↓
DevOps Foundations
   ↓
Security Foundations
   ↓
DevSecOps Practices
   ↓
Cloud & Kubernetes
   ↓
Production Operations
   ↓
Security Automation
   ↓
Professional DevSecOps Engineer
```

The objective is **not** to memorize tools.

The objective is to understand:

> **How software is built, secured, deployed, operated, monitored, attacked, defended, and continuously improved in a real organization.**

---

# 📅 Day 01 — DevSecOps Foundations

## 🎯 Day 01 Objectives

By the end of Day 01, I should understand:

* What DevOps is
* What DevSecOps is
* Why companies adopted DevSecOps
* CI/CD
* Continuous Integration
* Continuous Delivery
* Continuous Deployment
* Shift-left security
* Shift-right security
* DevSecOps lifecycle
* Security throughout the SDLC
* SAST
* SCA
* Secret scanning
* DAST
* IaC security
* Container security
* Runtime security
* Security gates
* DevSecOps culture
* Basic production thinking

---

# 1. What Is DevOps?

## Definition

**DevOps is a combination of practices, culture, automation, and processes that brings software development and IT operations closer together.**

Traditional organizations often separated teams:

```text
┌───────────────┐
│  Developers   │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│      QA       │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│   Operations  │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│    Security   │
└───────────────┘
```

This can create:

* Slow releases
* Communication gaps
* Manual processes
* Deployment failures
* Security discovered too late
* Poor ownership
* Long feedback cycles

DevOps tries to improve this.

---

# 2. DevOps Lifecycle

A simplified DevOps lifecycle:

```text
       ┌─────────────┐
       │     PLAN    │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │     CODE    │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │    BUILD    │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │     TEST    │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │   RELEASE   │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │   DEPLOY    │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │   OPERATE   │
       └──────┬──────┘
              ↓
       ┌─────────────┐
       │   MONITOR   │
       └──────┬──────┘
              │
              └──────────────→ PLAN
```

The feedback loop is extremely important.

Production generates information.

That information should improve the next development cycle.

---

# 3. Why DevSecOps?

DevOps solved many operational problems.

But another problem remained:

> **Security was often introduced too late.**

For example:

```text
Developer writes code
        ↓
Application built
        ↓
Application deployed
        ↓
Security team tests
        ↓
Vulnerability discovered
        ↓
Release stopped
        ↓
Developer fixes issue
        ↓
Build again
        ↓
Deploy again
```

This is expensive and slow.

DevSecOps integrates security throughout the lifecycle.

---

# 4. What Is DevSecOps?

A useful mental model:

```text
DevOps + Security + Automation + Shared Responsibility
                        =
                    DevSecOps
```

DevSecOps means security becomes part of the development and operations lifecycle instead of being a final checkpoint.

---

# 5. Complete DevSecOps Lifecycle

```text
                         DEVSECOPS

                            PLAN
                             │
                             ▼
                     Threat Modeling
                             │
                             ▼
                            CODE
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
            SAST            SCA       Secret Scanning
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                           BUILD
                             │
                             ▼
                    Container Security
                    Dependency Security
                             │
                             ▼
                           TEST
                             │
                             ▼
                            DAST
                             │
                             ▼
                          RELEASE
                             │
                       Policy Gates
                             │
                             ▼
                          DEPLOY
                             │
                             ▼
                        KUBERNETES
                        / CLOUD
                             │
                             ▼
                          RUNTIME
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
            Logs           Metrics        Traces
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                       INCIDENT RESPONSE
                             │
                             ▼
                        ROOT CAUSE
                             │
                             ▼
                         REMEDIATION
                             │
                             ▼
                         FEEDBACK
                             │
                             └────────→ PLAN
```

This is the mental model for the entire course.

---

# 6. Secure SDLC

Security should exist throughout the Software Development Life Cycle.

```text
PLAN
 │
 ├── Security requirements
 └── Threat modeling
      ↓
DESIGN
 │
 ├── Architecture review
 └── Security controls
      ↓
DEVELOP
 │
 ├── Secure coding
 ├── SAST
 ├── SCA
 └── Secret scanning
      ↓
BUILD
 │
 ├── Dependency checks
 ├── Container scanning
 └── SBOM
      ↓
TEST
 │
 ├── DAST
 ├── Integration testing
 └── Security testing
      ↓
DEPLOY
 │
 ├── IaC validation
 ├── Policy enforcement
 └── Security gates
      ↓
OPERATE
 │
 ├── Monitoring
 ├── Logging
 ├── Detection
 └── Incident response
      ↓
IMPROVE
 │
 └──────────────→ PLAN
```

---

# 7. Shift Left

## What does Shift Left mean?

Security testing is moved earlier in the development lifecycle.

Traditional:

```text
CODE
 ↓
BUILD
 ↓
DEPLOY
 ↓
SECURITY TEST
 ↓
VULNERABILITY
```

Shift-left:

```text
CODE
 ↓
SECURITY CHECK
 ↓
BUILD
 ↓
SECURITY CHECK
 ↓
DEPLOY
```

The objective is:

> **Find problems as early as practical.**

---

# 8. Example of Shift Left

Developer writes:

```python
query = "SELECT * FROM users WHERE id=" + user_id
```

A security scanner may identify a potential SQL injection.

Instead of waiting for production penetration testing:

```text
Developer
    ↓
Git commit
    ↓
SAST
    ↓
Finding
    ↓
Developer fixes code
    ↓
Pipeline continues
```

This creates a much shorter feedback loop.

---

# 9. Shift Right

Shift-left does not mean production security is unnecessary.

We also need security after deployment.

```text
                  SECURITY

             ┌──── SHIFT LEFT ────┐
             │                     │
             ▼                     │
        Before Production          │
             │                     │
             └────────┐            │
                      │            │
                      ▼            │
                   DEPLOY          │
                      │            │
                      ▼            │
               SHIFT RIGHT        │
                      │            │
                      ▼            │
                 Production       │
                      │            │
             ┌────────┼────────┐   │
             ▼        ▼        ▼   │
           Logs     Metrics   WAF  │
             │        │        │   │
             └────────┼────────┘   │
                      ▼            │
               Incident Response   │
                      │            │
                      └────────────┘
```

### Shift Left

Examples:

* SAST
* SCA
* Secret scanning
* IaC scanning
* Container scanning
* Threat modeling

### Shift Right

Examples:

* Runtime monitoring
* WAF
* SIEM
* EDR
* Cloud detection
* Runtime security
* Incident response

---

# 10. CI — Continuous Integration

Continuous Integration means developers frequently integrate code changes into a shared repository and automated processes validate those changes.

Example:

```text
Developer
    ↓
git push
    ↓
Pull Request
    ↓
CI Pipeline
    ↓
Tests
    ↓
Security Checks
    ↓
Build
    ↓
Result
```

A CI pipeline might execute:

```text
Checkout Code
      ↓
Install Dependencies
      ↓
Lint
      ↓
Unit Tests
      ↓
SAST
      ↓
SCA
      ↓
Secret Scan
      ↓
Build
```

---

# 11. Continuous Delivery

Continuous Delivery means the software is kept in a state where it can be released reliably.

Example:

```text
Git
 ↓
CI
 ↓
Build
 ↓
Test
 ↓
Security
 ↓
Artifact
 ↓
Staging
 ↓
Ready for Production
```

Production deployment may still require an approval.

---

# 12. Continuous Deployment

Continuous Deployment goes one step further.

Successful changes can automatically reach production.

```text
Developer
    ↓
Git
    ↓
CI
    ↓
Tests
    ↓
Security
    ↓
Build
    ↓
Deploy
    ↓
Production
```

No manual production approval is necessarily required for every change.

---

# 13. Continuous Delivery vs Continuous Deployment

| Concept                | Meaning                                              |
| ---------------------- | ---------------------------------------------------- |
| Continuous Integration | Frequently integrate and automatically validate code |
| Continuous Delivery    | Keep software ready for release                      |
| Continuous Deployment  | Automatically deploy validated changes to production |

Remember:

```text
CI
 ↓
CD
 ↓
Production
```

But **Delivery ≠ Deployment**.

---

# 14. What Is a CI/CD Pipeline?

A pipeline is an automated sequence of activities that takes source code toward a deployable application.

Example:

```text
┌─────────────┐
│    Git      │
└──────┬──────┘
       ↓
┌─────────────┐
│   Checkout  │
└──────┬──────┘
       ↓
┌─────────────┐
│     Test    │
└──────┬──────┘
       ↓
┌─────────────┐
│     SAST    │
└──────┬──────┘
       ↓
┌─────────────┐
│     SCA     │
└──────┬──────┘
       ↓
┌─────────────┐
│ Secret Scan │
└──────┬──────┘
       ↓
┌─────────────┐
│    Build    │
└──────┬──────┘
       ↓
┌─────────────┐
│Image Scanner│
└──────┬──────┘
       ↓
┌─────────────┐
│   Registry  │
└──────┬──────┘
       ↓
┌─────────────┐
│   Staging   │
└──────┬──────┘
       ↓
┌─────────────┐
│    DAST     │
└──────┬──────┘
       ↓
┌─────────────┐
│ Production  │
└─────────────┘
```

---

# 15. Security Gates

A security gate determines whether a pipeline should continue.

Example:

```text
Build
  ↓
SAST
  ↓
Critical finding?
  │
 ┌┴──────────────┐
 │               │
YES              NO
 │               │
 ▼               ▼
BLOCK           Continue
Pipeline          │
                  ▼
                Build
```

But blindly blocking everything is not mature DevSecOps.

---

# 16. Risk-Based Security Gates

Suppose a scanner reports:

```text
Critical: 2
High: 10
Medium: 500
Low: 2,000
```

A mature DevSecOps engineer asks:

* Are the findings real?
* Are they exploitable?
* Is the application internet-facing?
* Is sensitive data involved?
* Is there a known exploit?
* Is the vulnerable component actually used?
* Is there a compensating control?
* What is the business impact?
* What is the remediation SLA?

Security decisions should be **risk-based**, not merely tool-output-based.

---

# 17. SAST

## Static Application Security Testing

SAST analyzes application source code or related representations without executing the application in the normal way.

Typical use:

```text
Source Code
    ↓
SAST
    ↓
Potential Vulnerability
```

Examples of tools:

```text
Semgrep
SonarQube
CodeQL
Checkmarx
```

Potential findings:

* Injection
* Unsafe APIs
* Hardcoded secrets
* Insecure coding patterns
* Authentication weaknesses
* Data flow issues

---

# 18. SCA

## Software Composition Analysis

Modern applications depend heavily on third-party libraries.

Example:

```text
My Application
      │
      ├── React
      ├── Express
      ├── OpenSSL
      ├── Log4j
      └── Other Libraries
```

SCA helps identify:

```text
Library
   ↓
Version
   ↓
Known Vulnerability
   ↓
Risk
   ↓
Upgrade / Remediation
```

Examples:

```text
Dependabot
Snyk
OWASP Dependency-Check
Trivy
```

---

# 19. Secret Scanning

Secrets can accidentally enter source code.

Examples:

```text
AWS keys
API tokens
Private keys
Database passwords
OAuth secrets
Cloud credentials
```

Bad:

```python
AWS_SECRET = "real-secret-value"
```

Secret scanning attempts to detect such exposures.

Examples:

```text
Gitleaks
TruffleHog
GitHub Secret Scanning
```

Important:

> Removing a secret from the latest file does not automatically mean the secret is safe.

If the credential was exposed:

```text
1. Revoke
2. Rotate
3. Investigate
4. Remove exposure
5. Search history
6. Improve controls
```

---

# 20. DAST

## Dynamic Application Security Testing

DAST tests an application while it is running.

Conceptually:

```text
Running Application
        ↑
        │
       DAST
        │
        ▼
Security Testing
```

It can help identify issues such as:

* Injection
* Authentication problems
* Misconfiguration
* Security headers
* Some access-control issues
* Runtime application vulnerabilities

Examples:

```text
OWASP ZAP
Burp Suite
```

---

# 21. SAST vs SCA vs DAST

| Technology         | Primary Target             |
| ------------------ | -------------------------- |
| SAST               | Application code           |
| SCA                | Third-party dependencies   |
| Secret scanning    | Credentials/secrets        |
| DAST               | Running application        |
| IaC scanning       | Infrastructure definitions |
| Container scanning | Container images           |

A professional DevSecOps pipeline commonly uses multiple layers.

---

# 22. Infrastructure as Code

Infrastructure can also be represented as code.

Example:

```text
Terraform
CloudFormation
Kubernetes YAML
Helm
Ansible
```

Instead of manually creating infrastructure:

```text
Engineer
   ↓
AWS Console
   ↓
Click buttons
   ↓
Infrastructure
```

IaC allows:

```text
Code
 ↓
Review
 ↓
Test
 ↓
Plan
 ↓
Apply
 ↓
Infrastructure
```

---

# 23. IaC Security

Example of a dangerous configuration:

```text
Internet
   ↓
Security Group
   ↓
Port 22
   ↓
0.0.0.0/0
```

An IaC security scanner can identify risky configurations before deployment.

Tools include:

```text
Checkov
KICS
tfsec
```

---

# 24. Container Security

Modern applications are often packaged into containers.

Simplified architecture:

```text
Application
     ↓
Dockerfile
     ↓
Container Image
     ↓
Registry
     ↓
Deployment
     ↓
Container Runtime
```

Security should exist at multiple stages:

```text
Dockerfile
    ↓
Build
    ↓
Image Scan
    ↓
SBOM
    ↓
Registry
    ↓
Admission Policy
    ↓
Runtime Security
```

---

# 25. Runtime Security

Deployment is not the end.

After deployment:

```text
Application
    ↓
Production
    ↓
Monitoring
    ↓
Detection
    ↓
Alert
    ↓
Investigation
    ↓
Response
```

Possible monitoring areas:

```text
CPU
Memory
Network
HTTP
Authentication
Errors
Logs
Processes
Containers
Cloud activity
Kubernetes events
```

---

# 26. DevSecOps Shared Responsibility

Security should not be:

```text
"Security team's problem."
```

Instead:

```text
             SECURITY

Developer ──────────────┐
                        │
DevOps ─────────────────┤
                        │
Security ───────────────┤
                        │
Cloud ──────────────────┤
                        │
Operations ──────────────┘
                        │
                        ▼
                 Shared Security
```

Everyone has responsibilities.

---

# 27. DevSecOps Engineer Responsibilities

A DevSecOps Engineer may work on:

### CI/CD

```text
Pipeline design
Pipeline security
Build automation
Deployment automation
```

### Security

```text
SAST
SCA
DAST
Secret scanning
IaC security
Container security
Vulnerability management
```

### Cloud

```text
IAM
Network security
Logging
Monitoring
Security controls
```

### Infrastructure

```text
Linux
Docker
Kubernetes
Terraform
```

### Operations

```text
Monitoring
Alerting
Incident response
Troubleshooting
Reliability
```

---

# 28. Complete Industry-Level Mental Model

This is the diagram I want to remember throughout the entire journey:

```text
                          BUSINESS
                             │
                             ▼
                       REQUIREMENTS
                             │
                             ▼
                           DESIGN
                             │
                    ┌────────┴────────┐
                    │ Threat Modeling │
                    └────────┬────────┘
                             ▼
                            CODE
                             │
                             ▼
                       SOURCE CONTROL
                             │
                             ▼
                          CI PIPELINE
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
         SAST                SCA          SECRET SCANNING
          │                  │                  │
          └──────────────────┼──────────────────┘
                             ▼
                           BUILD
                             │
                             ▼
                     CONTAINER IMAGE
                             │
                    ┌────────┴────────┐
                    │ Image Scanning  │
                    │      SBOM       │
                    └────────┬────────┘
                             ▼
                       ARTIFACT REGISTRY
                             │
                             ▼
                           IaC
                             │
                      IaC Security Scan
                             │
                             ▼
                         DEPLOYMENT
                             │
                             ▼
                     CLOUD / KUBERNETES
                             │
                             ▼
                          RUNTIME
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
         LOGS              METRICS            TRACES
          │                  │                  │
          └──────────────────┼──────────────────┘
                             ▼
                       DETECTION / ALERT
                             │
                             ▼
                    INCIDENT RESPONSE
                             │
                             ▼
                       ROOT CAUSE
                             │
                             ▼
                        REMEDIATION
                             │
                             ▼
                       POSTMORTEM
                             │
                             ▼
                         FEEDBACK
                             │
                             └──────────────→ DESIGN
```

---

# 29. Day 01 Hands-On Lab

The objective today is **environment discovery**, not installing everything.

Run:

```bash
uname -a
```

```bash
sw_vers
```

```bash
git --version
```

```bash
docker --version
```

```bash
python3 --version
```

```bash
node --version
```

```bash
kubectl version --client
```

```bash
terraform version
```

Also check:

```bash
which git
which docker
which kubectl
which terraform
```

Record which tools are available.

---

# 30. Create Your DevSecOps Learning Repository

Recommended structure:

```text
devsecops-engineer-journey/
│
├── README.md
│
├── Day-01-DevSecOps-Foundations/
│   ├── README.md
│   ├── diagrams/
│   ├── notes/
│   ├── labs/
│   └── answers/
│
├── Day-02-Linux/
├── Day-03-Networking/
├── Day-04-Git/
├── Day-05-Docker/
├── Day-06-Docker-Security/
├── Day-07-CI-CD/
│
├── Day-08-CI-CD-Security/
├── Day-09-SAST/
├── Day-10-SCA/
│
├── Day-11-Secrets/
├── Day-12-DAST/
├── Day-13-Terraform/
├── Day-14-IaC-Security/
│
├── Day-15-Container-Security/
├── Day-16-AWS/
├── Day-17-AWS-IAM/
├── Day-18-AWS-Networking/
│
├── Day-19-Kubernetes/
├── Day-20-Kubernetes-Security/
├── Day-21-Kubernetes-Networking/
│
├── Day-22-Cloud-Runtime-Security/
├── Day-23-Observability/
├── Day-24-Vulnerability-Management/
├── Day-25-Supply-Chain-Security/
│
├── Day-26-Incident-Response/
├── Day-27-Architecture/
├── Day-28-Full-DevSecOps-Pipeline/
├── Day-29-Interview/
└── Day-30-Final-Assessment/
```

---

# 31. Day 01 Interview Questions

Answer these without searching first.

### Beginner

1. What is DevOps?
2. What is DevSecOps?
3. Why do we need DevSecOps?
4. What is CI?
5. What is CD?
6. What is a CI/CD pipeline?
7. What is Shift Left?
8. What is Shift Right?

### Security

9. What is SAST?
10. What is SCA?
11. What is DAST?
12. What is secret scanning?
13. What is IaC security?
14. What is container security?
15. What is runtime security?

### Professional

16. Why shouldn't security testing happen only after deployment?
17. Should every security finding block production?
18. How should security risk be prioritized?
19. Who owns security in DevSecOps?
20. How does DevSecOps improve developer feedback?

---

# 32. Day 01 Production Scenario

## Scenario

A developer pushes a new application.

The application contains:

```text
1 Critical vulnerability
3 High vulnerabilities
10 Medium vulnerabilities
```

The developer says:

> "The release is urgent. Just deploy it."

### Your job

Think like a DevSecOps Engineer.

Ask:

```text
Is the critical vulnerability real?
        ↓
Is it exploitable?
        ↓
Is the affected code actually used?
        ↓
Is the application internet-facing?
        ↓
Does sensitive data exist?
        ↓
Is there a known exploit?
        ↓
Are compensating controls present?
        ↓
Can the vulnerability be fixed immediately?
        ↓
Can the release be safely mitigated?
        ↓
Who accepts the risk?
```

This is **risk-based DevSecOps thinking**.

---

# 33. Day 01 Deliverables

By the end of Day 01, I should have:

* [ ] Understood DevOps
* [ ] Understood DevSecOps
* [ ] Understood CI
* [ ] Understood Continuous Delivery
* [ ] Understood Continuous Deployment
* [ ] Understood Shift Left
* [ ] Understood Shift Right
* [ ] Understood SAST
* [ ] Understood SCA
* [ ] Understood Secret Scanning
* [ ] Understood DAST
* [ ] Understood IaC Security
* [ ] Understood Container Security
* [ ] Understood Runtime Security
* [ ] Understood Security Gates
* [ ] Understood Risk-Based Security
* [ ] Created the GitHub learning repository
* [ ] Checked local DevSecOps tooling
* [ ] Answered the 20 interview questions
* [ ] Completed the production scenario

---

# 🧠 Day 01 Golden Rules

Remember these.

### Rule 1

> **DevSecOps is not a collection of security tools.**

### Rule 2

> **Automation is important, but understanding the system is more important.**

### Rule 3

> **Security should be integrated throughout the SDLC.**

### Rule 4

> **Shift Left does not eliminate runtime security.**

### Rule 5

> **Not every vulnerability has the same business risk.**

### Rule 6

> **DevSecOps is shared responsibility.**

### Rule 7

> **A production system is more than code.**

Think:

```text
Code
 ↓
Dependencies
 ↓
Build
 ↓
Artifact
 ↓
Infrastructure
 ↓
Cloud
 ↓
Network
 ↓
Runtime
 ↓
Users
 ↓
Business
```

### Rule 8

> **A good DevSecOps Engineer understands both security and operations.**

### Rule 9

> **Don't learn tools first. Learn the problem each tool solves.**

### Rule 10

> **The ultimate goal is secure, reliable, repeatable, observable delivery.**

---

# 🏁 Day 01 Final Mental Model

If I remember only one thing from today, it should be this:

```text
                     ┌───────────────┐
                     │    BUSINESS   │
                     └───────┬───────┘
                             │
                             ▼
                     ┌───────────────┐
                     │  APPLICATION  │
                     └───────┬───────┘
                             │
                             ▼
                     ┌───────────────┐
                     │     CODE      │
                     └───────┬───────┘
                             │
                             ▼
                     ┌───────────────┐
                     │      CI       │
                     └───────┬───────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
            SAST            SCA          SECRETS
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                         BUILD
                             │
                             ▼
                       CONTAINER
                             │
                             ▼
                        IaC / CLOUD
                             │
                             ▼
                        KUBERNETES
                             │
                             ▼
                         RUNTIME
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
            LOGS           METRICS        TRACES
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                       DETECTION
                             │
                             ▼
                    INCIDENT RESPONSE
                             │
                             ▼
                       REMEDIATION
                             │
                             ▼
                        FEEDBACK
                             │
                             └──────────→ CODE
```

**Day 01 complete.**

The next step in this journey is **Day 02 — Linux for DevSecOps**, where we move from concepts into the operating-system layer that almost every production DevSecOps engineer eventually has to troubleshoot.
