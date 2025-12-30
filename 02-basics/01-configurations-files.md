# OpenTofu Configuration Files

## Introduction

OpenTofu uses **configuration files** to define infrastructure in a **declarative way**.  
These files describe **what infrastructure you want**, and OpenTofu figures out **how to create or update it**.

All OpenTofu configuration files use the **`.tf` extension** and are written in **HashiCorp Configuration Language (HCL)**.

---

## What is a Configuration File?

A configuration file:
- Is a plain text file
- Has a `.tf` extension
- Describes infrastructure resources
- Can be version-controlled using Git

Example file name:
```text
main.tf
```

### File Extensions Used in OpenTofu

| File Type         | Purpose                     |
| ----------------- | --------------------------- |
| `.tf`             | Main configuration files    |
| `.tfvars`         | Variable values             |
| `.tfstate`        | State file (auto-generated) |
| `.tfstate.backup` | Backup of state file        |

> ⚠️ Never commit .tfstate files to GitHub

## Common Configuration File Names (Best Practice)

OpenTofu does not enforce file names, but these are industry best practices:

| File Name      | Purpose                      |
| -------------- | ---------------------------- |
| `main.tf`      | Main configuration           |
| `providers.tf` | Provider configuration       |
| `variables.tf` | Input variables              |
| `outputs.tf`   | Output values                |
| `locals.tf`    | Local values                 |
| `versions.tf`  | OpenTofu & provider versions |

### What is HCL (HashiCorp Configuration Language)?

HCL is:

- Human-readable
- Declarative
- Easy to learn
- Designed for infrastructure definitions

#### Key Characteristics

- Uses blocks
- Uses key-value pairs
- Supports comments
- Supports expressions

---
### Basic Syntax of a .tf File

```hcl
block_type "label" "name" {
  key = "value"
}
```
#### Example:
```hcl
resource "azurerm_resource_group" "example" {
  name     = "rg-demo"
  location = "East US"
}

```
### Types of Blocks in OpenTofu
#### 1️⃣ Provider Block
Defines which platform OpenTofu will interact with.

```hcl
provider "azurerm" {
  features {}
}
```
---
#### 2️⃣ Resource Block

Defines actual infrastructure resources.
```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-example"
  location = "Central India"
}
```
---
#### 3️⃣ Variable Block
Defines input values.
```hcl
variable "location" {
  type        = string
  description = "Azure region"
}
```
---
#### 4️⃣ Output Block
Defines values returned after execution.
```hcl
output "resource_group_name" {
  value = azurerm_resource_group.rg.name
}
```
---
#### 5️⃣ Local Block
Defines reusable local values.

```hcl
locals {
  environment = "dev"
}
```
### Comments in Configuration Files
#### Single-line comment

```hcl
# This is a comment
```
#### Alternative comment style

```hcl
// This is also a comment
```
### How OpenTofu Reads Configuration Files

- OpenTofu automatically loads all .tf files in a directory
- File order does not matter
- Blocks can be split across files
Example:


```text
providers.tf
resources.tf
variables.tf
```
All are treated as one configuration.

---
### Folder-Based Configuration
Each folder represents one OpenTofu project.

Example:


```text
my-opentofu-project/
├── main.tf
├── variables.tf
├── outputs.tf
```
You must run OpenTofu commands inside the folder.

---
#### Example: Minimal Valid OpenTofu Configuration

```hcl
terraform {
  required_version = ">= 1.0.0"
}

provider "azurerm" {
  features {}
}
```
This configuration:

- Has no resources
- Is still valid
- Can be initialized using tofu init

---

### Common Beginner Mistakes

❌ Forgetting .tf extension

❌ Syntax errors (missing braces {})

❌ Mixing tabs and spaces inconsistently

❌ Committing .tfstate to GitHub

❌ Running OpenTofu from the wrong directory

### Best Practices

✔ Use separate files (main.tf, variables.tf)

✔ Keep one project per folder

✔ Use meaningful names

✔ Add comments for clarity

✔ Use version control

### Summary

- OpenTofu uses .tf configuration files
- Files are written in HCL
- File names are flexible but best practices exist
- All .tf files in a folder are loaded together
- Configuration files define the desired state

### What’s Next?

Next, you should learn about Providers, which tell OpenTofu where to create infrastructure.


#### 👉 Next file to create:

```text
02-basics/02-providers.md
```