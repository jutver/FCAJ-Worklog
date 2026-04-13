---
title: "Event 4"
date: "2025-11-17"
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# "AWS Networking, IAM, and Security"

### Event Objectives

- Introduce the foundational concepts of AWS Networking and how Virtual Private Clouds are structured and secured.
- Explain Identity and Access Management (IAM) as the backbone of secure, least-privilege access control on AWS.
- Demonstrate practical AWS network and application protection tools including WAF, Shield, and Network Firewall.
- Provide actionable guidance for building secure, well-architected cloud infrastructure on AWS.

### Speakers

- **Lam An Thinh** – DataXight Security Engineer Intern | ITea Lab President | Focus: AWS Networking
- **Nguyen Phan Quoc Viet** – Focus: AWS Networking
- **Huynh Hoang Long** – FCAJ Cloud Engineer Ambassador | Focus: Identity & Access Management
- **Dang Thi Minh Thu** – FCAJ Cloud Engineer Ambassador | Focus: Identity & Access Management
- **Lam Tuan Kiet** – DevOps Engineer | Focus: AWS Network & Application Protection

---

### Key Highlights

#### Session 1: AWS Networking

##### VPC & Core Network Architecture

- **VPC (Virtual Private Cloud)** → An isolated private network within AWS where all cloud resources reside.
- **CIDR (Classless Inter-Domain Routing)** → Defines the IP address range for your VPC, controlling the total pool of available addresses.
- **Blast Radius Concept** → Poor network segmentation means a single misconfiguration (e.g., opening port 22 to `0.0.0.0/0`) can expose the entire environment.

##### Subnets, Route Tables & Internet Gateway

- **Subnets** → Subdivisions of a VPC that partition resources into logical groups (public vs. private).
- **Elastic IP** → A static public IPv4 address associated with an EC2 instance for consistent external access.
- **Route Tables** → Define how traffic is directed within the VPC and to/from the outside world.
- **Internet Gateway (IGW)** → Connects a VPC to the public internet; attached at the VPC level for public subnet routing.
- **Egress Routing** → Controls outbound-only traffic paths for private resources.

##### NAT Gateway

- **Purpose** → Allows resources in private subnets to reach the internet (e.g., for software updates) while preventing unsolicited inbound connections.
- **Mechanism**:
  - **SNAT (Source NAT)**: Replaces the EC2 instance's private IP with the NAT Gateway's public IP for outbound traffic.
  - **PAT (Port Address Translation)**: Uses unique source ports to differentiate sessions from multiple EC2 instances.
  - **State Table**: Tracks active sessions and drops any inbound packets not matching an existing entry.
- **Deployment Options** → Zonal vs. Regional NAT Gateway — balancing availability against cost and performance.

##### Security Group

- **Role** → The primary defense layer for individual AWS resources, operating at the ENI (Elastic Network Interface) level.
- **Stateful Mechanism** → Automatically allows return traffic for any permitted inbound connection; no need to configure outbound rules separately.
- **Zero Trust Philosophy** → All inbound traffic is implicitly denied by default; only explicit "Allow" rules are supported — there are no "Deny" rules.
- **Micro-segmentation** → Security policies follow the instance regardless of its subnet, enabling fine-grained access control.

##### Network ACL (NACL)

- **Role** → A subnet-level firewall acting as the second layer of defense, complementing Security Groups.
- **Stateless Mechanism** → NACL evaluates each packet independently; both inbound and outbound rules must be configured explicitly, including ephemeral ports (1024–65535).
- **Rule Evaluation** → Rules are processed in numerical order (lowest first); the first matching rule wins, and a default "Deny All" asterisk (`*`) rule closes every NACL.
- **Key Advantage over Security Groups** → Supports explicit **DENY** rules, enabling proactive blocking of specific IP ranges or traffic patterns.

---

#### Session 2: AWS IAM — Identity & Access Management

##### What is IAM?

- **Core Function** → An AWS service for managing authentication (who you are) and authorization (what you can do) across all cloud resources.
- **Manages** → Users, groups, roles, and policies in a unified access control framework.
- **IAM Groups** → Simplify permission management by assigning policies to a group rather than individual users.

##### Best Practices with IAM

- Apply the **Least Privilege Principle** — grant only the permissions needed, never more.
- **Delete root access keys** immediately after account creation; use IAM users or roles for all day-to-day operations.
- Avoid using `"*"` in `Actions` or `Resources` in IAM policies, as this grants overly broad permissions.
- **Enable MFA** for all users, especially those with elevated privileges.
- **Rotate passwords and credentials** on a regular schedule to minimize exposure from compromised keys.

##### SSO — Single Sign-On

- **Concept** → One login credential grants access to multiple AWS accounts and applications, simplifying the user experience.
- **Multi-account Integration** → Integrates with AWS Organizations to centrally manage access across Finance, Legal, Production, Test, and other departments under a single root account.
- **Centralized Access Management** → Policies and permissions are governed from one place, reducing administrative overhead and risk of misconfiguration.

##### SCPs & Permission Boundaries

- **Service Control Policies (SCPs)**:
  - An organizational-level policy type attached via AWS Organizations.
  - Controls the **maximum available permissions** across all accounts in the organization.
  - SCPs never grant permissions — they only filter or restrict what is already allowed.

- **Permission Boundaries**:
  - An advanced IAM feature that sets the **maximum permissions** an identity-based policy can grant to a specific IAM User or Role.
  - Unlike SCPs (which apply organization-wide), Permission Boundaries are scoped to individual users or roles within a single account.
  - Useful for delegating IAM management safely without allowing privilege escalation.

##### Credential Management & Access Analyzer

- **Credentials Spectrum**:
  - **Long-term**: IAM User Access Keys — do not expire by default; should be avoided.
  - **Short-term**: Generated by AWS STS (Security Token Service) — auto-expire between 15 minutes and 36 hours.
- **Recommendation** → Use AWS IAM Identity Center for logins, as it provides short-term credentials behind the scenes.
- **IAM Access Analyzer** → Automatically flags policies with overly permissive configurations such as `"Principal: *"`, helping identify unintended public access.

---

#### Session 3: AWS Security — Network & Application Protection

##### AWS WAF (Web Application Firewall)

- **Purpose** → Protects web applications from common exploits by filtering and monitoring HTTP/HTTPS requests.
- **Prevents** → SQL injection, cross-site scripting (XSS), and other OWASP Top 10 threats.
- **Integration** → Deployed in front of CloudFront, ALB, API Gateway, or AppSync to inspect requests before they reach the application.

##### AWS Shield

- **Purpose** → Provides managed DDoS (Distributed Denial of Service) protection for AWS workloads.
- **Two Tiers**:
  - **Standard** → Automatically applied to all AWS customers at no extra cost; protects against common volumetric attacks.
  - **Advanced** → Paid tier offering enhanced protection, real-time attack visibility, 24/7 DDoS response team support, and cost protection.

##### AWS Network Firewall

- **Purpose** → A managed service that deploys security boundaries within VPCs for deep traffic inspection.
- **Capabilities**:
  - Stateful and stateless traffic filtering.
  - Intrusion detection and prevention (IDS/IPS).
  - Domain-based filtering and TLS inspection.
- **Use Case** → Enforces granular, consistent network security policies across all traffic flowing through a VPC.

##### AWS Firewall Manager

- **Purpose** → Centralized security management across multiple AWS accounts and regions.
- **Automates** → Rule deployment for WAF, Shield Advanced, Network Firewall, and Security Groups at scale.
- **Best Suited For** → Organizations using AWS Organizations who need consistent policy enforcement across dozens or hundreds of accounts.

---

### Key Takeaways

#### Layered Security is Essential

- AWS networking is built around a layered defense model: Security Groups protect individual resources, NACLs guard subnets, and NAT Gateways control internet access for private workloads.
- Understanding how these layers interact — especially the stateful vs. stateless distinction — is critical for designing secure architectures.

#### IAM is the Foundation of Cloud Security

- Every cloud security problem can eventually be traced back to permissions. IAM done right — with least privilege, MFA, short-term credentials, and SCPs — dramatically reduces the attack surface.
- The shift from long-term IAM keys to identity-center-based short-term credentials is one of the most impactful security improvements an organization can make.

#### Application-Layer Protection Completes the Picture

- Network-level controls alone are not enough. AWS WAF and Shield provide protection against application-layer threats and volumetric attacks that bypass traditional firewall rules.
- AWS Firewall Manager makes it operationally feasible to enforce security standards consistently at scale, especially in multi-account environments.

---

### Applying to Work

- **Networking Design**:
  - Always separate public and private subnets; route internet-bound traffic from private resources through NAT Gateways.
  - Use Security Groups as the primary access control mechanism and layer NACLs for subnet-wide deny rules when needed.

- **IAM Hygiene**:
  - Audit existing IAM policies for `"*"` wildcards and replace with scoped permissions.
  - Enforce MFA organization-wide and migrate to short-term credential workflows.

- **Application & Network Protection**:
  - Deploy AWS WAF on all internet-facing endpoints to guard against common web exploits.
  - Use AWS Firewall Manager to centralize security policy enforcement if managing multiple AWS accounts.

---

### Event Experience

Attending the **AWS Networking, IAM, and Security** sessions offered a comprehensive deep dive into the security building blocks of the AWS platform — from physical network architecture all the way up to application-layer protection.

#### Building a Mental Model of AWS Security

- The sessions flowed naturally from network infrastructure (VPC, subnets, gateways) to access control (IAM) and finally to threat protection (WAF, Shield, Network Firewall), painting a complete picture of secure cloud architecture.
- The contrast between stateful Security Groups and stateless NACLs — demonstrated through step-by-step packet flow diagrams — made an often-confusing topic intuitive and memorable.

#### Practical IAM Concepts Made Clear

- The distinction between SCPs (organization-wide ceiling) and Permission Boundaries (per-user/role ceiling) clarified a common point of confusion in multi-account AWS environments.
- The emphasis on credential hygiene — avoiding long-term keys, rotating regularly, and using IAM Identity Center — provided immediately actionable guidance.

#### Understanding Threat Protection at Scale

- The progression from WAF (request filtering) → Shield (DDoS protection) → Network Firewall (deep packet inspection) → Firewall Manager (centralized governance) illustrated how AWS protection services stack on top of each other.
- Seeing how Firewall Manager can automate policy rollout across an entire AWS Organization highlighted the importance of security-as-code thinking at the enterprise level.

#### Lessons Learned

- Security on AWS is not a single toggle — it is a series of deliberate, layered decisions made at the network, identity, and application levels.
- The difference between a secure and an insecure architecture often comes down to small defaults: an open security group rule, a missing MFA policy, or an overly permissive IAM action.
- Investing time in understanding the fundamentals — CIDR, stateful vs. stateless filtering, least privilege — pays dividends when debugging real-world incidents or designing new systems.