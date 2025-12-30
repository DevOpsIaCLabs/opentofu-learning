# OpenTofu Variables

## Introduction

In OpenTofu, **variables** are used to make configurations **flexible, reusable, and easy to manage**.

Instead of hard-coding values (like region, resource names, or sizes), we use variables so the same code can work in:
- Development
- Testing
- Production

👉 **Variables = Inputs to your OpenTofu configuration**
 
---

## Variables Explained in Simple Words (Layman Example)

Think about a **mobile phone order form**:

| Real Life | OpenTofu |
|---------|---------|
| Customer name | Variable |
| Phone model | Variable |
| Color | Variable |
| Delivery address | Variable |
| Price | Output |

The form (code) stays the same, but values change.

Similarly:
- Code remains same
- Variable values change

---

## Why Variables Are Important

Without variables:

❌ Code duplication  
❌ Hard-coded values  
❌ Difficult environment changes

With variables:

✔ Reusable code  
✔ Easy updates  
✔ Cleaner configuration  
✔ Environment-specific values

---
## Basic Variable Syntax

### Variable Block
```hcl
variable "variable_name" {
  type        = string
  description = "Description of variable"
}
```

---

## Simple Variable Example

#### variables.tf
```hcl
variable "location" {
  type        = string
  description = "Azure region"
}
```
#### main.tf

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = var.location
}
```

---

### How to Use a Variable
#### Variables are referenced using:

```hcl
var.variable_name
```
Example:

```hcl
var.location
```

---

### Variable Types (Very Important)
#### 1️⃣ String

```hcl
variable "environment" {
  type    = string
  default = "dev"
}
```

---

#### 2️⃣ Number

```hcl
variable "vm_count" {
  type    = number
  default = 2
}

```

---

#### 3️⃣ Boolean

```hcl
variable "enable_monitoring" {
  type    = bool
  default = true
}

```

---

#### 4️⃣ List
```hcl
variable "subnet_names" {
  type    = list(string)
  default = ["subnet1", "subnet2"]
}

```

---

#### 5️⃣ Map

```hcl
variable "tags" {
  type = map(string)
  default = {
    environment = "dev"
    owner       = "team-a"
  }
}

```

---

### Default Values
If a variable has a default value, it becomes optional.

```hcl
variable "location" {
  type    = string
  default = "Central India"
}

```

---

### Required Variables
If no default value is provided, OpenTofu will ask for input.

```hcl
variable "resource_group_name" {
  type = string
}

```

---

### How to Pass Variable Values

#### Method 1️⃣: Command Line

```hcl
tofu apply -var="location=Central India"
```

---

#### Method 2️⃣: .tfvars File (Recommended)

#### terraform.tfvars

```hcl
location = "Central India"
```
OpenTofu automatically loads:
- terraform.tfvars
- *.auto.tfvars

---

#### Method 3️⃣: Environment Variables
```hcl
setx TF_VAR_location "Central India"
```

---

#### Method 4️⃣: Interactive Prompt

```hcl
tofu apply

```
OpenTofu will ask:

```hcl
var.location
  Enter a value:

```

---

### Variable Validation (Beginner Friendly)
Validation ensures correct input.

```hcl
variable "environment" {
  type = string
 
  validation {
    condition     = contains(["dev", "test", "prod"], var.environment)
    error_message = "Environment must be dev, test, or prod"
  }
}

```

---

### Sensitive Variables
Used for secrets like passwords.

```hcl
variable "admin_password" {
  type      = string
  sensitive = true
}

```
> Sensitive values are hidden from output.

---

### Best Practices for Variables
✔ Define variables in variables.tf

✔ Use meaningful names

✔ Add descriptions

✔ Use defaults where possible

✔ Use .tfvars for environment values

✔ Never hard-code secrets

---

### Common Beginner Mistakes

❌ Hard-coding values

❌ Using wrong variable types

❌ Forgetting var. prefix

❌ Committing secrets to GitHub

❌ Not using validation

---

### Summary (In Simple Words)

- Variables are inputs to OpenTofu
- They make code reusable
- Values can change without changing code
- Variables support multiple data types
- .tfvars files are best for values

---

### What’s Next?
Next, you should learn about Outputs, which show values after OpenTofu creates resources.
#### 👉 Next file to create:

```hcl
02-basics/05-outputs.md
```
