---
title: "Event 3"
date: "2026-04-13"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# "AWS Kubernetes, Elixir, and Infrastructure as Code with Terraform"

### Event Objectives

- Introduce container orchestration with Kubernetes and how AWS EKS simplifies running workloads at scale in the cloud.
- Explore Elixir and the BEAM virtual machine as a unified, fault-tolerant solution for DevOps infrastructure.
- Demonstrate Infrastructure as Code (IaC) principles using AWS CloudFormation, AWS CDK, and Terraform.
- Provide practical guidance on tooling, workflows, and best practices for modern cloud-native development.

### Speakers

- **Bao Huynh** – Junior Cloud Native Developer at Endava Vietnam | Founder & Head of ITea Lab | Focus: Architecting for the Cloud with Kubernetes
- **Nguyen Ta Minh Triet** – R&D Member at ITea Lab, Swinburne Vietnam | SAP Developer Intern at Bosch GSV | Focus: Elixir for Highly Concurrent & Fault-Tolerant DevOps Infrastructure
- **Thinh Nguyen (Khanh Phuc Thinh Nguyen)** – FCAJ Cloud Engineer Trainee | ITea Lab Operations Team | Focus: Infrastructure as Code with Terraform on AWS

---

### Key Highlights

#### Session 1: Architecting for the Cloud with Kubernetes

##### Container Orchestration Challenges

- **Docker & Docker Compose** → Package applications into containers for portability; Compose helps run multi-container stacks with a single command.
- **Scaling Problem** → Running a handful of containers manually is manageable, but production workloads span many machines and require automation.
- **What Orchestration Solves**:
  - Self-healing (automatic recovery from failures)
  - Scalability (grow or shrink capacity based on demand)
  - Minimal-downtime updates and rollbacks
- **Popular Orchestrators** → Docker Swarm, Kubernetes (K8s), K3S, and AWS ECS.

##### Introduction to Kubernetes

- **What is Kubernetes?** → An open-source platform (also called K8S) for running containers at scale across a cluster of machines.
- **Core Features** → Scheduling, self-healing, auto-scaling, rolling updates, and deep customizability.

##### Kubernetes Architecture

- **Control Plane (Cluster Brain)**:
  - `etcd` — distributed key-value store holding the entire cluster state.
  - `kube-apiserver` — the single API entry point for all cluster operations.
  - `kube-scheduler` — decides which worker node each Pod runs on.
  - `kube-controller-manager` — continuously reconciles actual state with desired state.
  - `cloud-controller-manager` — handles cloud-provider-specific integrations (e.g., load balancers on AWS).

- **Worker Node**:
  - Runs the actual application containers via a container runtime (e.g., containerd).
  - `kubelet` — agent that manages Pods on each node.
  - `kube-proxy` — handles network routing and traffic forwarding to Pods.

##### Key Kubernetes Objects

- **Pod** → The smallest deployable unit; usually contains one container, with all containers in a Pod sharing the same IP and optionally the same storage volumes.
- **ReplicaSet** → Keeps a specified number of identical Pods running at all times; replaces any that fail (self-healing).
- **Deployment** → The standard way to manage an application in K8S — wraps a ReplicaSet and adds rolling updates and rollback capabilities.
- **ConfigMap** → Stores non-sensitive configuration as key-value pairs, injected into Pods as environment variables or mounted files.
- **Secret** → Stores sensitive values (passwords, tokens) similarly to ConfigMap, but Base64-encoded; access is restricted to only the Pods that need it.
- **Job** → Runs a one-time task (e.g., a database backup or batch processing job); Kubernetes retries the Pod if it fails.

##### Manifests, kubectl & Getting Started

- Kubernetes objects are defined in **YAML manifest files** and applied using `kubectl` — the primary CLI tool for interacting with a cluster.
- **Local Learning Environments**:
  - **Minikube** → Runs a local Kubernetes cluster on a single machine; ideal for beginners.
  - **K3S** → A lightweight Kubernetes distribution, easy to install and resource-efficient.
  - **K3D** → Runs K3S inside Docker; fast cluster creation and deletion, great for testing on a laptop.
- **Recommended Learning Resources** → LFS158 (Introduction to Kubernetes), the official Kubernetes.io documentation, and *Kubernetes the Hard Way* by Kelsey Hightower for deeper understanding.

##### EKS — Kubernetes on AWS

- **What is EKS?** → Amazon Elastic Kubernetes Service; AWS manages the control plane so teams focus on applications rather than cluster infrastructure.
- **Why EKS?** → Reduces manual setup, integrates natively with AWS services (IAM, VPC, Load Balancers, ECR), and simplifies running production-grade Kubernetes in the cloud.

##### Additional Tools

- **Helm** → The package manager for Kubernetes; packages applications as reusable, versioned Charts with configurable `values.yaml` files for dev, staging, and production environments.
- **K9S** → A terminal-based UI that makes it easy to visualize pods, services, and logs across a cluster without memorizing kubectl commands.

---

#### Session 2: Elixir as a Unified Solution for Highly Concurrent & Fault-Tolerant DevOps Infrastructure

##### Introduction to Elixir

- **What is Elixir?** → A functional, concurrent programming language that runs on the BEAM virtual machine — the same runtime originally built for Erlang.
- **Language Lineage**:
  - Based on Erlang; runs on the same BEAM VM.
  - Syntax inspired by Ruby (familiar and readable).
  - Compiled to BEAM bytecode, similar to how Java targets the JVM.
  - Functional paradigm (like Haskell) with immutable data and pattern matching.

##### BEAM Processes & Concurrency

- **BEAM Process Model** → Every Elixir program runs as a single OS process, but the BEAM runtime spawns thousands of lightweight internal processes — each isolated with no shared memory.
- **Two Process Types**:
  - **Worker** → Performs a specific task.
  - **Supervisor** → Monitors and restarts workers when they fail.
- **Scale** → The Phoenix Framework benchmarked **2 million simultaneous WebSocket connections** on a single server — a testament to BEAM's concurrency model.

##### Achieving Fault-Tolerance with OTP

- **Lightweight Processes** → BEAM can sustain millions of concurrent processes, each handling a small, isolated unit of work.
- **Process Supervision** → Rather than defensive `try/catch` programming, supervised processes are simply allowed to crash and be automatically restarted by their supervisor — making error handling more consistent and predictable.
- **"Let It Crash" Philosophy** → Embraces failure as a normal event; the supervision tree ensures the system recovers gracefully without manual intervention.
- **Hot Code Upgrades** → The BEAM (inherited from Erlang) supports upgrading running systems without downtime, though modern blue-green deployments are now often preferred in practice.

##### Elixir in DevOps Pipelines

- **Integrated Tooling** → Elixir's built-in tools (`Mix` for build/test/dependency management, `IEx` for interactive development) reduce the need for external tooling sprawl.
- **Unified Solution** → A single BEAM-based stack can handle web serving, background jobs, real-time communication, data pipelines, and monitoring — removing the friction of integrating multiple languages and runtimes.
- **Benefits for Dev & Ops Teams** → Fewer moving parts, consistent deployment artifacts, and a shared language for application and infrastructure logic.

##### Real-World Case Study — From Serverless to Elixir

- A service originally built on **AWS API Gateway + Lambda (Node.js)** for collecting browser event streams was rewritten in Elixir.
- **Cost comparison**:
  - API Gateway at 5M requests/hour → **$12,600/month**
  - Elixir at low-end (0.5 CPUs) → **$59/month**
  - Elixir at high-end (2 CPUs) → **$397/month**
- The rewrite demonstrated that for high-throughput, long-lived connections, a well-tuned BEAM application dramatically outperforms a serverless architecture on both cost and operational complexity.

---

#### Session 3: Infrastructure as Code with Terraform on AWS

##### Why IaC? The Problem with ClickOps

- **ClickOps** → Manually provisioning infrastructure through the AWS Console; great for learning, but problematic at scale.
- **Limitations of ClickOps**:
  - **Slow** — repetitive manual steps for every environment.
  - **Human Error** — inconsistent configurations across deployments.
  - **Inconsistency** — no guaranteed parity between dev, staging, and production.
  - **Collaboration Problems** — no version history or peer review for infrastructure changes.
- **IaC Solution** → Use code (not clicks) to automatically create, update, and delete infrastructure; enables automation, reproducibility, scalability, and collaboration.

##### AWS CloudFormation

- **What is it?** → AWS's native IaC tool; infrastructure is described in YAML or JSON templates that CloudFormation provisions automatically.
- **CloudFormation Stack** → A named collection of AWS resources managed as a single unit; deploy, update, or delete all resources together from one template.
- **Template Anatomy** → A YAML/JSON file defining the desired state of infrastructure — resources, parameters, outputs, and conditions.
- **Workflow** → Author a template → store in S3 or locally → create a stack → CloudFormation provisions all specified resources.
- **Configuration Drift** → When resources are manually changed outside CloudFormation, they diverge from the template. CloudFormation's drift detection identifies what changed, though it does not auto-fix; the operator must update the stack or revert the change.

##### AWS Cloud Development Kit (CDK)

- **What is it?** → An open-source framework that lets developers define AWS infrastructure using real programming languages: TypeScript, JavaScript, Python, Java, C#, and Go — which then synthesizes to CloudFormation templates under the hood.
- **Constructs** → The fundamental building blocks of CDK, with three abstraction levels:
  - **L1 (CfnXxx)** → Direct 1:1 mapping to CloudFormation resources; full manual control, lowest abstraction.
  - **L2** → Higher-level, developer-friendly API with sensible defaults and helper methods; the most commonly used level.
  - **L3** → Complete architecture patterns (multiple resources working together); fastest path to deploying common scenarios.
- **CDK Hierarchy** → `App` (top-level) → `Stack` (unit of deployment) → `Construct` (individual resources or patterns).
- **Key CLI Commands** → `cdk init`, `cdk bootstrap`, `cdk synth`, `cdk deploy`, `cdk diff`, `cdk destroy`, `cdk drift`, and `cdk doctor`.

##### Terraform

- **What is it?** → An open-source IaC tool by HashiCorp that uses **HCL (HashiCorp Configuration Language)** to provision infrastructure across AWS, Azure, Google Cloud, and more — all from one tool.
- **Core Strengths**:
  - **Multi-Cloud Support** → Works across all major providers with a consistent workflow.
  - **State Tracking** → Maintains a `terraform.tfstate` file that records the real-world state of all managed resources.
  - **Simple Configuration** → HCL is readable and declarative, reducing the learning curve.
- **Folder Structure**:
  - Basic: `main.tf`, `variables.tf`, `outputs.tf`, `providers.tf`, `.tfvars`
  - Advanced: Organized into `bootstrap/`, `environment/` (dev/staging/prod), and reusable `modules/` (networking, ec2, s3).
- **Key CLI Workflow**:
  - `terraform init` → Initialize the project and download providers.
  - `terraform validate` → Check syntax and configuration errors.
  - `terraform plan` → Preview what will be created (+), modified (~), or destroyed (-).
  - `terraform apply` → Execute the planned changes.
  - `terraform destroy` → Remove all managed infrastructure.
  - `terraform state` → Inspect and manage the state file.

##### Choosing the Right IaC Tool

Three questions to guide the decision:
1. **One Cloud or Many?** → Terraform excels for multi-cloud; CloudFormation/CDK are optimal for AWS-only setups.
2. **Developers or Ops?** → CDK suits developer teams comfortable with code; CloudFormation and Terraform are more Ops-friendly.
3. **Cloud & Ecosystem Support** → Consider what existing tooling, modules, and community resources are available.
- **Other notable tools** → OpenTofu (open-source Terraform fork) and Pulumi (multi-language, multi-cloud IaC).

---

### Key Takeaways

#### Kubernetes is the Industry Standard for Container Orchestration

- Understanding Kubernetes' layered architecture — Control Plane, Worker Nodes, Pods, Deployments, Services — is essential for anyone working in cloud-native infrastructure.
- EKS removes the operational burden of managing the control plane, letting teams focus on application delivery rather than cluster maintenance.

#### Elixir Offers a Compelling Alternative for High-Throughput Infrastructure

- The BEAM's lightweight process model and "Let It Crash" supervision philosophy make Elixir genuinely suitable for building resilient, high-concurrency DevOps tooling.
- The cost case study illustrates that the right language and runtime choice can yield an order-of-magnitude reduction in infrastructure spend.

#### IaC is a Non-Negotiable Practice for Scalable Cloud Operations

- Manual infrastructure management does not scale; IaC brings versioning, repeatability, and collaboration to cloud resource provisioning.
- CloudFormation and CDK are excellent for AWS-native projects; Terraform is the go-to for multi-cloud or organization-wide standardization.

---

### Applying to Work

- **Kubernetes**:
  - Start with Minikube or K3D locally to build hands-on familiarity before moving to EKS.
  - Adopt Helm for packaging and deploying applications across environments, and K9S for day-to-day cluster visibility.

- **Elixir**:
  - Evaluate BEAM-based solutions for services that require high concurrency, persistent connections, or complex background processing.
  - Consider the "Let It Crash" philosophy as an alternative to verbose error-handling patterns in existing systems.

- **IaC & Terraform**:
  - Commit all infrastructure definitions to version control and enforce peer review via pull requests — treat infrastructure exactly like application code.
  - Use the `plan → apply` workflow as a safety gate before any production changes, and leverage modules for reusable, environment-specific configurations.

---

### Event Experience

Attending the **AWS Kubernetes, Elixir, and IaC with Terraform** sessions offered a rich overview of the modern DevOps toolchain — from container orchestration and programming language selection through to infrastructure automation at scale.

#### Building Cloud-Native Intuition

- The Kubernetes session established a clear mental model of how containerized workloads are managed in production, progressing naturally from Docker basics all the way to EKS architecture.
- The breakdown of Pods, ReplicaSets, Deployments, ConfigMaps, and Secrets — and how they compose together — gave the conceptual foundation needed to read and write real Kubernetes manifests.

#### An Unexpected Perspective on DevOps Languages

- The Elixir session was a standout for its fresh angle: rather than presenting yet another cloud service, it made a compelling argument for rethinking the runtime and language itself as part of the infrastructure strategy.
- The real-world cost comparison — from thousands of dollars per month on serverless Lambda to under $400 on a single Elixir server — made an abstract technical argument concrete and memorable.

#### Demystifying Infrastructure as Code

- Seeing CloudFormation, CDK, and Terraform presented side by side in the same session made it easy to understand where each tool fits rather than treating them as competing alternatives.
- The practical CDK construct levels (L1/L2/L3) and Terraform's `plan → apply` workflow gave immediately actionable patterns for anyone starting their IaC journey.

#### Connecting the Dots Across Sessions

- The three sessions complemented each other well: Kubernetes handles *how applications run*, Elixir shapes *how services are built*, and Terraform governs *how infrastructure is provisioned* — together forming a coherent picture of a modern, cloud-native engineering culture.

#### Lessons Learned

- Container orchestration is not just about Kubernetes syntax — it is about understanding the self-healing, declarative philosophy that underpins the entire system.
- Choosing a programming language for infrastructure tooling is a legitimate architectural decision, not an afterthought.
- The best IaC tool is not always the most feature-rich one; it is the one that best fits the team's skills, cloud strategy, and operational context.