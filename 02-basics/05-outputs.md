# OpenTofu Outputs

## Introduction

In OpenTofu, **outputs** are used to **display information after infrastructure is created**.

Think of outputs as the **final result or response** that OpenTofu shows once it finishes its work.

👉 **Outputs = What OpenTofu gives back to you**
 
---

## Outputs Explained in Simple Words (Layman Example)

Imagine ordering food online:

| Real Life | OpenTofu |
|---------|---------|
| Order confirmation | Output |
| Order ID | Output |
| Delivery address | Output |
| Total bill | Output |

You place the order → system responds with details.

Similarly:
- You run `tofu apply`
- OpenTofu creates resources
- OpenTofu shows outputs

---

## Why Outputs Are Important

Without outputs:
❌ You don’t know resource IDs  
❌ Hard to debug  
❌ Hard to connect modules  
❌ Hard to reuse values

With outputs:
✔ See created resource details  
✔ Share values between modules  
✔ Use values in other projects  
✔ Easier troubleshooting
 
---

## Basic Output Syntax

```hcl
output "output_name" {
  value = expression
}
```

---

### Simple Output Example
#### Resource

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = "Central India"
}
```
#### Output

```hcl
output "resource_group_name" {
  value = azurerm_resource_group.rg.name
}

```

After tofu apply:

```hcl
resource_group_name = "rg-demo"

```

---

### How to Reference Resource Values
Syntax:

```hcl
resource_type.resource_name.attribute

```
Example:

```hcl
azurerm_resource_group.rg.location

```

---

### Common Output Use Cases
#### 1️⃣ Display Resource Information


```hcl
output "rg_location" {
  value = azurerm_resource_group.rg.location
}

```


---

#### 2️⃣ Share Values Between Modules
Outputs from one module become inputs to another.
Example:


```hcl
output "rg_id" {
  value = azurerm_resource_group.rg.id
}

```

---

#### 3️⃣ Debugging & Learning
Outputs help beginners understand:
- What got created
- What values exist


---

### Sensitive Outputs
Used for secrets like passwords.

```hcl
output "admin_password" {
  value     = var.admin_password
  sensitive = true
}

```

Sensitive outputs:
- Are hidden in CLI output
- Are still stored in state file
> ⚠️ Never output secrets unless required.


---

### Output Data Types
Outputs automatically inherit type from value:
- string
- number
- bool
- list
- map

Example:

```hcl
output "subnet_names" {
  value = var.subnet_names
}

```

---


### Conditional Outputs (Advanced)


```hcl
output "vm_public_ip" {
  value = azurerm_public_ip.vm.ip_address != "" ? azurerm_public_ip.vm.ip_address : "No Public IP"
}

```

---


### Viewing Outputs
#### After Apply


```hcl
tofu apply

```
#### Anytime Later

```hcl
tofu output

```

#### Single Output

```hcl
tofu output resource_group_name

```


---


### Outputs in Modules (Very Important)
#### Inside module


```hcl
output "rg_name" {
  value = azurerm_resource_group.rg.name
}

```
#### In root module

```hcl
module "rg" {
  source = "./rg-module"
}
 
output "rg_name" {
  value = module.rg.rg_name
}

```


---

## Common Beginner Mistakes

❌ Outputting wrong attribute

❌ Outputting sensitive data

❌ Forgetting resource reference syntax

❌ Expecting output without apply

❌ Confusing variables with outputs


---

## Best Practices for Outputs

✔ Output only useful values

✔ Use clear output names

✔ Avoid secrets

✔ Use outputs to connect modules

✔ Keep outputs in outputs.tf


---

## Summary (In Simple Words)
- Outputs show results after OpenTofu runs
- They help you understand what was created
- Outputs are essential for modules
- Sensitive outputs should be handled carefully
- Outputs improve debugging and reuse

---

### What’s Next?
Now that you understand outputs, the next concept is Locals, which help you avoid repeating values inside code.
#### 👉 Next file to create:


```hcl
02-basics/06-locals.md
```
