# OpenTofu Locals

## Introduction

In OpenTofu, **locals** are used to define **temporary values** that can be reused **inside the same configuration**.

Locals help you:
- Avoid repeating the same value again and again
- Keep code clean and readable
- Simplify complex expressions

👉 **Locals = Internal helper values**
 
---

## Locals Explained in Simple Words (Layman Example)

Imagine cooking at home:

| Real Life | OpenTofu |
|---------|---------|
| Ingredients kept on the table | Locals |
| Recipe steps | Resources |
| Final dish | Infrastructure |

You keep commonly used items ready instead of searching again and again.

Similarly:
- Locals store reusable values
- Used by resources, outputs, and modules

---

## Why Locals Are Important

Without locals:
❌ Repeated values everywhere  
❌ Hard to read code  
❌ Difficult updates

With locals:
✔ Centralized values  
✔ Cleaner configuration  
✔ Easy maintenance  
✔ Fewer mistakes
 
---

## Basic Local Syntax

```hcl
locals {
  key = value
}
```

---

## Simple Local Example

```hcl
locals {
  environment = "dev"
}

```

Use it as:

```hcl
local.environment

```
---

## Locals vs Variables (Very Important)


| Variables | Locals |
|---------|---------|
| Inputs to configuration | Internal values |
| Values come from user | Values defined in code |
| Can be overridden | Cannot be overridden |
| Used for customization | Used for logic & reuse |


👉 Rule of thumb:
- User input → Variable
- Calculated/internal value → Local

---

## Using Locals with Resources

```hcl
locals {
  location = "Central India"
}

resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = local.location
}

```
---

## Using Locals to Build Names (Common Use Case)

```hcl
locals {
  project     = "opentofu"
  environment = "dev"
}
resource "azurerm_resource_group" "rg" {
  name     = "${local.project}-${local.environment}-rg"
  location = "Central India"
}
```
Result:

```hcl

opentofu-dev-rg
```

---

## Locals with Expressions
Locals can use expressions and functions.


```hcl
locals {
  is_production = var.environment == "prod"
}

```

---

### Locals with Maps


```hcl
locals {
  common_tags = {
    environment = var.environment
    owner       = "devops-team"
  }
}

```

Usage:


```hcl
tags = local.common_tags

```

---

## Multiple Local Blocks
You can define locals in multiple blocks

```hcl

locals {
  env = "dev"
}
 
locals {
  region = "Central India"
}
```
OpenTofu merges them automatically.

---

### Where to Define Locals
Best practice:

```hcl

locals.tf
```
---

But locals can be defined in any .tf file.

## Locals Scope
- Locals are module-scoped
- Cannot be accessed outside the module
- Not exposed unless passed via outputs

---

## Common Beginner Mistakes
❌ Using locals for user input<br/>
❌ Trying to override locals<br/>
❌ Confusing local with var<br/>
❌ Overusing locals unnecessarily<br/>

---

## Best Practices for Locals
✔ Use locals for repeated values<br/>
✔ Use meaningful skilled names<br/>
✔ Combine locals with variables<br/>
✔ Keep locals simple<br/>
✔ Avoid putting secrets in locals<br/>

---

## Summary (In Simple Words)
- Locals store internal reusable values
- They simplify OpenTofu code
- Used only inside the same module
- Improve readability and maintainability
- Do not accept user input

---

## What’s Next?
Next, you should learn about Data Sources, which allow OpenTofu to read existing infrastructure.
👉 Next file to create:

```text
02-basics/07-data-sources.md
```
