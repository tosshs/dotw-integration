# DevOpsTheWay (DOTW)

**DevOpsTheWay (DOTW, pronounced “dot-wuh”)** — a modular platform engineering ecosystem designed to bootstrap reproducible DevOps environments and support experimentation, learning, and platform development.

---

## dotw-integration

**dotw-integration** is the platform distribution and integration point for the DOTW ecosystem.

It aggregates all `dotw` repositories using git submodules, ensuring consistent versions and reproducible environments.

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/tmilkotev/dotw-integration.git
```

---

## 🧭 Platform
<details>
<summary><strong>Platform Architecture (click to expand)</strong></summary>
  
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
```

</details>

DOTW is organized around a modular architecture:
- **Control** → platform orchestration and environment lifecycle  
- **Infrastructure** → local and cloud environments  
- **Platform** → application runtime and delivery tooling  
- **Observability** → monitoring, logging, and platform visibility  
- **Knowledge** → documentation, reasoning, and learning systems

---

## 🏗 Goals

DOTW aims to:

- bootstrap complete DevOps environments quickly
- provide reproducible platform setups
- enable hands-on experimentation with modern tooling
- unify local labs and cloud environments
- model real-world platform engineering architectures

---

## 🧭 Platform Stack

🐧 Linux · 🖥️ Vagrant · 🏗 Terraform · ⚙️ Ansible · 🎛 platformctl · ⎈ Kubernetes / OKD · 📦 Helm · 📚 Harbor · 🔵 TeamCity · 🚀 ArgoCD · 📊 Prometheus · 📈 Grafana · 🪵 Loki
