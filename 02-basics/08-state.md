# OpenTofu State

## Introduction

In OpenTofu, **state** is how OpenTofu **remembers what infrastructure exists** and **what it manages**.

The state acts like a **memory or record book** for OpenTofu.

👉 **State = Source of truth for your infrastructure**

Without state, OpenTofu would not know:
- What resources already exist
- What needs to be changed
- What should be deleted

---

## State Explained in Simple Words (Layman Example)

Imagine a shopkeeper maintaining a notebook:

| Real Life | OpenTofu |
|---------|---------|
| Notebook of stock | State file |
| Items in shop | Resources |
| Adding/removing stock | Apply / Destroy |
| Checking stock | Plan |

If the notebook is lost:
- The shopkeeper doesn’t know what exists
- Mistakes will happen

Similarly, OpenTofu **depends on state** to work safely.
 

---

## What Exactly Is State?

State is a file that:
- Tracks resources created by OpenTofu
- Stores resource IDs and attributes
- Maps your `.tf` code to real infrastructure
- Helps OpenTofu detect changes

By default, state is stored locally as:
```text
terraform.tfstate
```

> In OpenTofu, the file name is still terraform.tfstate for compatibility.

---

## Why State Is Required
OpenTofu uses state to:

✔ Know what already exists <br/>
✔ Create dependency graph <br/>
✔ Detect configuration changes <br/>
✔ Perform updates safely <br/>
✔ Avoid duplicate resources <br/>

Without state:

❌ Duplicate resource creation <br/>
❌ Accidental deletions <br/>
❌ No change detection <br/>

---

## What Is Stored in the State File?
State file contains:
- Resource type and name
- Provider details
- Resource IDs (cloud IDs)
- Attribute values
- Dependencies between resources

Example (simplified):

```json
{
  "resources": [
    {
      "type": "azurerm_resource_group",
      "name": "rg",
      "instances": [
        {
          "attributes": {
            "name": "rg-demo",
            "location": "Central India"
          }
        }
      ]
    }
  ]
}

```

---

## Local State (Default Behavior)
By default:
- State is stored on your local machine
- File name: terraform.tfstate
- Location: Same folder as .tf files


Pros

✔ Simple <br/>
✔ Good for learning <br/>
✔ No setup required <br/>

Cons

❌ Not safe for teams<br/>
❌ No locking<br/>
❌ Risk of overwrite<br/>

---

## Remote State (High-Level Overview)
Remote state stores the state file in a central location, such as:
- Azure Storage
- AWS S3
- Google Cloud Storage

#### Benefits

✔ Team collaboration<br/>
✔ State locking<br/>
✔ Safer storage<br/>
✔ Avoid conflicts<br/>

👉 You will learn this in 08-remote-state section.

---

## How OpenTofu Uses State (Workflow)
### 1️⃣ tofu init
- Prepares backend
- Downloads providers
- Prepares state handling

---

### 2️⃣ tofu plan
- Reads current state
- Compares with desired configuration
- Shows what will change

---

### 3️⃣ tofu apply
- Applies changes
- Updates state file

---

### 4️⃣ tofu destroy
- Deletes resources
- Updates state file

---

## State and Resource Mapping
Each resource in code maps to one entry in state.

```hcl
resource "azurerm_resource_group" "rg" {
  name = "rg-demo"
}
```

State entry:

```hcl
azurerm_resource_group.rg
```

If you rename the resource in code: 

❌ OpenTofu thinks it’s a new resource <br/>
❌ Old resource may be destroyed<br/>

---

## What Happens If State Is Deleted?
If state file is deleted:
- OpenTofu forgets all managed resources
- Next apply may recreate everything
- Very dangerous in production

👉 Never delete state manually

---

## State Locking (Concept)
State locking prevents:
- Two people running apply at same time
- Corrupt state

Local state ❌ no locking<br/>
Remote state ✔ supports locking<br/>

---

## Importing Existing Resources into State
If a resource exists but not in state:
```bash
tofu import azurerm_resource_group.rg /subscriptions/.../resourceGroups/rg-demo
```

This:
- Adds resource to state
- Does NOT create resource

---

## State vs Configuration (Very Important)


|Configuration |State |
|---------|--------|
|What you want |What exists |
|.tf files |.tfstate file |
|Declarative |Actual reality |
|Version-controlled |Never commit to Git |


---

## State Files and GitHub
🚫 Never commit these files: 

```text
terraform.tfstate
terraform.tfstate.backup

```

✔ Add to .gitignore

---


## Common Beginner Mistakes
❌ Deleting state file <br/>
❌ Editing state manually<br/>
❌ Sharing state over email<br/>
❌ Using local state for team projects<br/>
❌ Ignoring state backups<br/>

## Best Practices for State
✔ Use local state only for learning<br/>
✔ Use remote state for real projects<br/>
✔ Enable state locking<br/>
✔ Restrict access to state<br/>
✔ Backup state regularly<br/>

---

## Summary (In Simple Words)
- State is OpenTofu’s memory
- Tracks what infrastructure exists
- Required for safe changes
- Must be protected carefully
- Local for learning, remote for teams

---

## What’s Next?
🎉 You have completed all OpenTofu basics!
Next step is to start hands-on usage with OpenTofu commands.
👉 Next section to move into:

```text
03-cli-commands/
```
---