# DevOpsTheWay (DOTW, pronounced “dot-wuh”)

**DOTW** is a modular DevOps platform and learning ecosystem designed to **bootstrap a complete DevOps environment quickly and reproducibly** on new machines, while also providing **structured labs for training, experimentation, and platform engineering practice**.

It combines infrastructure provisioning, configuration management, CI/CD, container platforms, and observability into a cohesive stack that can run locally or in the cloud.

**dotw-integration** is the **integration repository** (Git superproject) for the DOTW ecosystem.

It integrates all `dotw` repositories via **git submodules**, pinning each repo to a known-good **release tag** (e.g. `v0.1.0`) so the ecosystem can be cloned and reproduced consistently.

---

## What you get here

- One repo to clone that pulls the entire DOTW ecosystem
- Explicit version pinning per module (submodule commit pointers)
- A clean workflow that allows each module repo to evolve independently

---

## Clone the full ecosystem

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/tosshs/dotw-integration.git
```

---

<details>
<summary>Platform Architecture (click to expand)</summary>
  
```text
                               developer
                                   |
                                   v
                           dotw-integration
                        (project distribution)
                                   |
                                   v
                      dotw-workstation-setup
                     (bootstrap dev workstation)
                                   |
                                   v
                           dotw-platformctl
                        (platform control plane)
                                   |
    +------------------------------+-----------------------------------+
    |                              |                                   |
    v                              v                                   v
dotw-almalinux10wsl            dotw-vagrant                      dotw-terraform
(automation host)              (local infra)                     (cloud infra)
    |                              |                                   |
    |                              v                                   v
    |                        local lab nodes                      AWS lab infra
    |                         (VMs/clusters)                     (VPC/EC2/etc)
    |                              |
    +--> dotw-ansible              |
    |   (configuration mgmt)       |
    |                              |
    +-----> Harbor                 |
    |   (container registry)       |
    |                              |
    |       +----------------------+----------------------------------+
    |       |                      |                                  |
    |       v                      v                                  v
    |      OKD              SharedServices VM                  Kubernetes
    |   (dotw-okd)         (single always-on VM)              (dotw-kubernetes)
    |       |                      |                                  |
    |       |                      v                                  |
    |       |              Prometheus/Grafana/Loki                    |
    |       |             (central monitoring/logging)                |
    |       |                      |                                  |
    |       |                      v                                  |
    |       |                 TeamCity (CI)                           |
    |       |             build / test / images                       |
    |       |                                                         |
    |       v                                                         v
    |   ArgoCD (CD)                                              ArgoCD (CD)
    | GitOps deployment                                         GitOps deployment
    |       ^                                                         ^
    |       |                                                         |
    +-------+-------------------- Helm Charts ------------------------+
                          (application packaging)
                                   |
                                   v
                          Application Layer
                     +--------------------------------+
                     | Java | Python | Platform Apps  |
                     +--------------------------------+

Per-environment minimum (in each k8s/okd env):
  - login/SSO (optional: Keycloak / OAuth provider)
  - basic monitoring (minimal, optional; heavy stack centralized)

Central observability:
  - Prometheus / Grafana / Loki on SharedServices VM


Knowledge / Documentation Layer
    dotw-ai


CI            → TeamCity
CD            → ArgoCD
Packaging     → Helm
Registry      → Harbor (on AlmaLinux10 WSL disk)
Platform      → Kubernetes / OKD
Config        → Ansible (on AlmaLinux10 WSL)
Infra         → Terraform / Vagrant
Control       → platformctl
Observability → SharedServices VM (Prom/Graf/Loki)
Optional      → per-env login + minimal monitoring
```

</details>

---

# Core Concept

DOTW is built as a **set of specialized repositories**, each responsible for one part of the DevOps lifecycle.  
The **`dotw-integration`** repository acts as the **superproject**, pinning versions of all components so the entire ecosystem can be cloned and reproduced consistently.

dotw-integration  
↓  
pins versions of all DOTW modules  
↓  
provides reproducible DevOps platform environments  

This ensures:

- reproducible environments  
- controlled upgrades  
- modular architecture  
- easy onboarding for new machines  

---

# Platform Planes

DOTW organizes its system into **three main operational planes**.

## 1. Control Plane

Responsible for orchestrating the platform and automation tooling.

Key components:

- dotw-platformctl  
- dotw-almalinux10wsl  
- dotw-ansible  

Responsibilities:

- orchestration commands  
- environment provisioning workflows  
- configuration management  
- developer control interface  

---

## 2. Infrastructure Plane

Responsible for **creating and managing infrastructure environments**.

Providers:

- dotw-vagrant → local infrastructure  
- dotw-terraform → cloud infrastructure  

Targets:

- local lab clusters  
- Kubernetes environments  
- OKD / OpenShift environments  
- AWS infrastructure  

---

## 3. Platform & Delivery Plane

Responsible for **building, delivering, and operating workloads**.

Core services:

- TeamCity → CI pipeline  
- ArgoCD → GitOps CD  
- Helm → application packaging  
- Harbor → container registry  
- Prometheus → metrics  
- Grafana → visualization  
- Loki → logging  

Application environments:

- Kubernetes lab  
- OKD lab  
- cloud environments  

---

# Shared Services

A dedicated **SharedServices environment** hosts platform services used across clusters.

Examples:

- TeamCity  
- Prometheus  
- Grafana  
- Loki  

This allows:

- centralized monitoring  
- independent CI infrastructure  
- reusable services for multiple clusters  

---

# Observability Model

DOTW uses **centralized observability** with optional lightweight monitoring per environment.

Central:

Prometheus / Grafana / Loki (SharedServices)

Per cluster (optional):

- minimal monitoring  
- authentication / SSO  

---

# DevOps Workflow

The platform follows a modern **GitOps delivery flow**.

Developer  
↓  
TeamCity (CI)  
↓  
build container image  
↓  
push to Harbor  
↓  
Helm charts define deployment  
↓  
ArgoCD syncs clusters  
↓  
Applications run on Kubernetes / OKD  

---

# Key Goals of DOTW

DOTW aims to:

- bootstrap a full DevOps environment on new machines quickly  
- provide reproducible infrastructure and platform setups  
- enable hands-on training with real DevOps tooling  
- support experimentation with Kubernetes and OpenShift  
- unify local labs and cloud environments  
- model real-world platform engineering architectures  

---

# Architectural Philosophy

DOTW follows several principles:

- modular repositories  
- reproducible environments  
- infrastructure-as-code  
- GitOps delivery  
- local + cloud parity  
- training-oriented platform design  

---

# In Short

DOTW is both:

- a reproducible DevOps platform  
- a learning and experimentation environment  

It enables developers and engineers to **bootstrap, operate, and study a complete DevOps ecosystem** spanning infrastructure, CI/CD, observability, and cloud-native platforms.
