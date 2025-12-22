# OpenTofu Installation on Linux

## Introduction

This document explains how to install **OpenTofu** on major Linux distributions:

- Ubuntu (APT-based)
- Debian (APT-based)
- RHEL / CentOS / Rocky / AlmaLinux (DNF/YUM-based)

OpenTofu provides official packages for Linux, making installation simple and reliable.

---

## Prerequisites

Before installing OpenTofu, ensure:

- You have **root or sudo access**
- Your system is updated
- Internet connectivity is available

Check OS version:
```bash
cat /etc/os-release
```
---
## Install OpenTofu on Ubuntu
### Supported Versions
- Ubuntu 20.04
- Ubuntu 22.04
- Ubuntu 24.04
### Step 1: Update system packages
Bash
```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install required dependencies
Bash
```bash
sudo apt install -y wget gnupg lsb-release
```


### Step 3: Add OpenTofu GPG key

Bash
```bash

wget -O- https://packages.opentofu.org/opentofu.gpg | \
gpg --dearmor | sudo tee /usr/share/keyrings/opentofu.gpg > /dev/null
```
### Step 4: Add OpenTofu repository

Bash
```bash
echo "deb [signed-by=/usr/share/keyrings/opentofu.gpg] \
https://packages.opentofu.org/opentofu/$(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/opentofu.list
```

### Step 5: Install OpenTofu
Bash
```bash
sudo apt update
sudo apt install -y opentofu
```

---
## Install OpenTofu on Debian
### Supported Versions
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
### Step 1: Update system packages

Bash
```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install dependencies
Bash
```bash
sudo apt install -y wget gnupg lsb-release
```

### Step 3: Add OpenTofu GPG key

Bash
```bash
wget -O- https://packages.opentofu.org/opentofu.gpg | \
gpg --dearmor | sudo tee /usr/share/keyrings/opentofu.gpg > /dev/null
```
### Step 4: Add OpenTofu repository

Bash
```bash
echo "deb [signed-by=/usr/share/keyrings/opentofu.gpg] \
https://packages.opentofu.org/opentofu/$(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/opentofu.list
```

### Step 5: Install OpenTofu
Bash
```bash
sudo apt update
sudo apt install -y opentofu
```


---
## Install OpenTofu on RHEL / CentOS / Rocky / AlmaLinux
### Supported Versions
- RHEL 8 / 9
- CentOS Stream 8 / 9
- Rocky Linux 8 / 9
- AlmaLinux 8 / 9

### Step 1: Update system packages

Bash
```bash
sudo dnf update -y
```

### Step 2: Add OpenTofu repository

Bash
```bash
sudo dnf config-manager --add-repo \
https://packages.opentofu.org/opentofu.repo
```

If dnf config-manager is missing:

Bash
```bash
sudo dnf install -y dnf-plugins-core
```

### Step 3: Install OpenTofu

Bash
```bash
sudo dnf install -y opentofu
```

## Verify Installation
### Check OpenTofu version:

Bash
```bash
tofu version
```
### Expected output:

Text
> OpenTofu v1.x.x

---
## Enable Command Auto-Completion (Optional)
### Bash

Bash
```bash
tofu -install-autocomplete
```

### Restart shell:

Bash
```bash
exec bash
```
---
## Upgrade OpenTofu
### Ubuntu / Debian

Bash
```bash
sudo apt update
sudo apt upgrade opentofu
```

### RHEL-based

Bash
```bash
sudo dnf upgrade opentofu
```
---
## Uninstall OpenTofu
### Ubuntu / Debian

Bash
```bash
sudo apt remove -y opentofu
```

### RHEL-based

Bash
```bash
sudo dnf remove -y opentofu
```
---
## Common Installation Issues
### ❌ Command not found

Bash
```bash
tofu: command not found
```

✔ Ensure /usr/bin is in your PATH
✔ Re-login or restart shell

---
