# OpenTofu Data Sources

## Introduction

In OpenTofu, **data sources** are used to **read or fetch information from existing infrastructure**.

Unlike resources, data sources **do not create anything**.  
They only **retrieve data** so it can be used in your configuration.

👉 **Resources = Create / Manage**
👉 **Data Sources = Read / Fetch**
 
---

## Data Sources Explained in Simple Words (Layman Example)

Imagine visiting a government office:

| Real Life | OpenTofu |
|---------|---------|
| Asking for land record | Data Source |
| Buying new land | Resource |
| Reading Aadhaar details | Data Source |
| Creating Aadhaar | Resource |



You are **reading existing information**, not creating something new.
 
---

## Why Data Sources Are Important

Without data sources:

❌ You must hard-code values  <br/>
❌ Cannot use existing infrastructure  <br/>
❌ Difficult integration with existing systems<br/>

With data sources:

✔ Read existing resources  <br/>
✔ Avoid duplication  <br/>
✔ Integrate with legacy infrastructure  <br/>
✔ Safer for production environments<br/>
 
---

## What Exactly Is a Data Source?

A **data source**:
- Fetches information from a provider
- Reads existing infrastructure
- Returns attributes you can use
- Does not modify anything

Examples:
- Existing resource group
- Existing VNet
- Existing subnet
- Existing image ID
- Existing DNS zone

---

## Data Source Syntax

### Basic Syntax
```hcl
data "data_source_type" "logical_name" {
  # filters / arguments
}
```

---

## Simple Data Source Example (Azure Resource Group)

```hcl
data "azurerm_resource_group" "existing_rg" {
  name = "rg-existing"
}

```
Use it as:


```hcl
data.azurerm_resource_group.existing_rg.location

```

---

## Resource vs Data Source (Very Important)

| Feature | Resource | Data Source |
|--------|-------|--------|
| Purpose|Create / manage |Read only |
| Changes infra |Yes |No |
| State tracking |Yes |Read-only |
| Deletes resource |Yes |No |
| Prefix |resource |data |


---

## When Should You Use Data Sources?
Use data sources when:
- Infrastructure already exists
- Resources are shared
- You don’t want OpenTofu to manage lifecycle
- Working in production environments
- Reading cloud-managed resources

---

## Common Real-World Use Cases

### 1️⃣ Use Existing Resource Group


```hcl
data "azurerm_resource_group" "rg" {
  name = "rg-shared"
}

```

---

### 2️⃣ Use Existing Virtual Network

```hcl
data "azurerm_virtual_network" "vnet" {
  name                = "vnet-prod"
  resource_group_name = data.azurerm_resource_group.rg.name
}

```

---

### 3️⃣ Use Existing Subnet

```hcl
data "azurerm_subnet" "subnet" {
  name                 = "subnet-app"
  virtual_network_name = data.azurerm_virtual_network.vnet.name
  resource_group_name  = data.azurerm_resource_group.rg.name
}

```

---

## Referencing Data Source Values
Syntax:

```hcl
data.data_source_type.logical_name.attribute

```

Example:


```hcl
data.azurerm_subnet.subnet.id

```

---

## Data Sources with Resources (Very Common Pattern)


```hcl
resource "azurerm_network_interface" "nic" {
  name                = "nic-demo"
  location            = data.azurerm_resource_group.rg.location
  resource_group_name = data.azurerm_resource_group.rg.name
 
  ip_configuration {
    name                          = "internal"
    subnet_id                     = data.azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
  }
}

```

---

## Multiple Data Sources Together


```hcl
data "azurerm_resource_group" "rg" {
  name = "rg-shared"
}
 
data "azurerm_virtual_network" "vnet" {
  name                = "vnet-shared"
  resource_group_name = data.azurerm_resource_group.rg.name
}

```

OpenTofu automatically handles dependencies.

---

## Data Sources and State File
- Data sources are recorded in state
- They do not control lifecycle
- Only store fetched information

✔ Safe to use<br/>
✔ No accidental deletion<br/>

---

## Common Beginner Mistakes
❌ Expecting data source to create resources <br/>
❌ Using wrong names (resource vs data)<br/>
❌ Hard-coding values instead of reading<br/>
❌ Assuming data source can delete infra<br/>

---

## Best Practices for Data Sources
✔ Use data sources for shared resources
✔ Prefer data sources in production
✔ Combine with resources carefully
✔ Use meaningful logical names
✔ Avoid duplication of resources

---

## Summary (In Simple Words)
- Data sources read existing infrastructure
- They do not create or delete anything
- Used to integrate with existing systems
- Very important for real-world projects
- Safer than managing everything as resources

---

## What’s Next?
The final core concept is State, which explains how OpenTofu remembers what exists.
👉 Next file to create:

```text
02-basics/08-state.md
```
