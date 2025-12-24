# OpenTofu Resources

## Introduction

In OpenTofu, a **resource** represents a **real infrastructure object** that you want to create, update, or delete.

Examples of resources:
- A cloud server (VM)
- A network (VNet / VPC)
- A storage account
- A database
- A Kubernetes cluster

👉 If **providers are the connectors**, then **resources are the actual things you create**.

---

## Resource Explained in Simple Words (Layman Example)

Think about building a house:

| Real Life | OpenTofu |
|---------|---------|
| Builder | Provider |
| Blueprint | `.tf` configuration |
| House / Room | Resource |
| Address | Resource name |

You tell the builder **what you want to build**, not **how to build it**.

Similarly, in OpenTofu:
- You declare resources
- OpenTofu creates them automatically

---

## What Exactly Is a Resource?

A **resource**:
- Defines a single infrastructure object
- Is declared in a `.tf` file
- Belongs to a provider
- Has properties (arguments)
- Has an internal state

Each resource maps to **one real-world object**.

---

## Resource Block Syntax

### Basic Syntax
```hcl
resource "resource_type" "resource_name" {
  argument1 = "value"
  argument2 = "value"
}
```
#### Example

```hcl
resource "azurerm_resource_group" "example" {
  name     = "rg-demo"
  location = "Central India"
}
```

---
### Understanding Resource Components
#### 1️⃣ Resource Type
```hcl
azurerm_resource_group

```
- Comes from provider
- Defines what kind of resource it is
- Format: ``` provider_resource ```
---

#### 2️⃣ Resource Name (Logical Name)
```hcl
example

```
- Used only inside OpenTofu
- Must be unique within a module
- Not the actual cloud name

Example reference:
```hcl
azurerm_resource_group.example.name

```

---
#### 3️⃣ Resource Arguments

Arguments define properties of the resource.

Example:

```hcl
name     = "rg-demo"
location = "Central India"

```
These values are sent to the cloud API.

---
### Resource Naming: Logical vs Real Name

```hcl
resource "azurerm_resource_group" "rg1" {
  name = "rg-production"
}

```
- ```rg1``` → OpenTofu internal name
- ```rg-production``` → Azure resource name

---

### Resource Lifecycle (Create → Update → Delete)

OpenTofu manages resource lifecycle automatically.
#### Create

```hcl
tofu apply
```

#### Update

- Change value in .tf file
- Run tofu apply
- OpenTofu updates only changed fields

#### Delete
```hcl
tofu destroy

```
---
### How OpenTofu Knows What Exists (State)

OpenTofu tracks resources using a state file.

State contains:

- Resource IDs
- Attributes
- Dependencies

Example reference:

```hcl
azurerm_resource_group.example.id
```

> ⚠️ State file is critical — never delete it accidentally.

---

### Resource Dependencies (Very Important)

Resources often depend on each other.

#### Example

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = "Central India"
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vnet-demo"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}

```
OpenTofu automatically:

- Creates Resource Group first
- Then creates VNet

---
### Explicit Dependency (depends_on)

Used when dependency is not obvious.
```hcl
resource "azurerm_virtual_network" "vnet" {
  depends_on = [azurerm_resource_group.rg]
}
```
---
### Resource Meta-Arguments

Meta-arguments control how OpenTofu manages resources.

### Common Meta-Arguments

| Meta-Argument | Purpose                        |
| ------------- | ------------------------------ |
| `depends_on`  | Explicit dependency            |
| `count`       | Create multiple copies         |
| `for_each`    | Loop over map/set              |
| `lifecycle`   | Control create/delete behavior |
| `provider`    | Specify provider alias         |


#### Example: ``` count ```

```hcl
resource "azurerm_resource_group" "rg" {
  count    = 2
  name     = "rg-${count.index}"
  location = "Central India"
}
```
#### Example: ```lifecycle```

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-critical"
  location = "Central India"

  lifecycle {
    prevent_destroy = true
  }
}
```
---
### Multiple Resources in One File

You can define multiple resources in one file.

```hcl
resource "azurerm_resource_group" "rg" { ... }
resource "azurerm_storage_account" "sa" { ... }
```
File order does not matter.

---

### Common Beginner Mistakes

❌ Confusing logical name with real name <br>
❌ Hardcoding values everywhere<br>
❌ Ignoring dependencies<br>
❌ Accidentally destroying resources<br>
❌ Not checking tofu plan<br>
---

### Best Practices for Resources

✔ One resource = one purpose<br>
✔ Use meaningful logical names<br>
✔ Use variables for values<br>
✔ Use tofu plan before apply<br>
✔ Use lifecycle rules carefully<br>

---

### Summary (In Simple Words)

- Resources are actual infrastructure
- Defined using ```resource``` blocks
- Belong to a provider
- Have arguments and dependencies
- Managed automatically by OpenTofu

---

### What’s Next?

Now that you understand resources, the next step is learning Variables, which make configurations reusable and flexible.

