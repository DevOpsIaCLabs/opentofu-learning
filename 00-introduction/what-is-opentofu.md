# What is OpenTofu?

## Introduction

**OpenTofu** is an open-source **Infrastructure as Code (IaC)** tool that allows you to define, provision, and manage infrastructure using code instead of manual processes.

With OpenTofu, you can create and manage cloud resources such as virtual machines, networks, storage, Kubernetes clusters, and more in a **repeatable, consistent, and automated way**.
 
---

## Why Infrastructure as Code (IaC)?

Traditional infrastructure management involves:
- Manual creation of resources
- Human errors
- No version control
- Difficult rollback and auditing

Infrastructure as Code solves these problems by:
- Treating infrastructure like application code
- Storing configurations in version control (Git)
- Enabling automation and repeatability
- Allowing review, rollback, and collaboration

---

## What is OpenTofu?

**OpenTofu** is a community-driven, open-source fork of Terraform, created to ensure:
- **Open governance**
- **Permissive open-source licensing**
- **Long-term stability without vendor lock-in**

OpenTofu uses the same declarative configuration language (HCL) and workflow that Terraform users are familiar with.

> 💡 If you know Terraform, you already know most of OpenTofu.
 
---

## Key Features of OpenTofu

- 🧾 Declarative configuration language (HCL)
- ☁️ Supports multiple cloud providers (Azure, AWS, GCP, etc.)
- 🔁 Reusable modules
- 🗂 State management to track infrastructure
- 🔒 Remote state & state locking support
- 🤝 Community-governed under the Linux Foundation
- 🆓 100% open-source (MPL 2.0 license)

---

## OpenTofu vs Terraform

| Feature | OpenTofu | Terraform |
|------|--------|----------|
| License | MPL 2.0 (Open Source) | Business Source License (BSL) |
| Governance | Community-led | Vendor-led |
| Cost | Free | Free + Commercial restrictions |
| Compatibility | Terraform-compatible | Native |
| Future Risk | Low | License-dependent |
 
---

## Where Can OpenTofu Be Used?

OpenTofu can be used to manage infrastructure across:

### Cloud Providers
- Microsoft Azure
- Amazon Web Services (AWS)
- Google Cloud Platform (GCP)
- Oracle Cloud
- DigitalOcean

### Other Platforms
- Kubernetes
- GitHub / GitLab
- Databases
- Monitoring & Observability tools
- SaaS platforms

---

## Who Should Learn OpenTofu?

OpenTofu is useful for:
- DevOps Engineers
- Platform Engineers
- Site Reliability Engineers (SRE)
- Cloud Engineers
- System Administrators moving to DevOps
- Students learning cloud & automation

---

## How OpenTofu Works (High-Level)

1. You write infrastructure code in `.tf` files
2. OpenTofu reads the configuration
3. It compares desired state vs current state
4. It creates an execution plan
5. Resources are created/updated/destroyed accordingly

---

## Example: Simple OpenTofu Configuration

```
provider "azurerm" {
  features {}
}
 
resource "azurerm_resource_group" "example" {
  name     = "rg-opentofu-demo"
  location = "East US"
}
```
---

## Benefit of Using OpenTofu

1. ✔ Repeatable and consistent infrastructure
2. ✔ Version-controlled infrastructure changes
3. ✔ Faster provisioning and updates
4. ✔ Reduced human error
5. ✔ Cloud-agnostic approach
6. ✔ No licensing surprises

---
## When Should You Choose OpenTofu?
Choose OpenTofu if you:
- Want a fully open-source IaC tool
- Need long-term stability without licensing risk
- Are building public or internal reusable modules
- Want community-driven innovation
- Are migrating from Terraform safely
---
