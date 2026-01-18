# OpenTofu Installation on Linux

## 📌 Introduction

This document explains how to install **OpenTofu** on Linux systems using **officially supported methods** as documented by the OpenTofu project.

Supported installation methods:
- Debian / Ubuntu (DEB packages)
- RHEL / Rocky / Alma / CentOS (RPM packages)
- Snap (Universal method)

👉 These steps follow **official OpenTofu documentation** and are safe for production use.

---

## 🛠 Prerequisites

Before installing OpenTofu, ensure:

- Linux system with sudo/root access
- Internet connectivity
- `curl` or `wget` installed

Check OS details:
```bash
cat /etc/os-release
```
---

## 🟢 Method 1: Install OpenTofu on Debian / Ubuntu (DEB)
### Supported Distributions

- Ubuntu 20.04 / 22.04 / 24.04
- Debian 11 / 12

---

### Step 1: Install required packages

```hcl
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
```

---

### Step 2: Add OpenTofu GPG key

```hcl
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://get.opentofu.org/opentofu.gpg | sudo tee /etc/apt/keyrings/opentofu.gpg >/dev/null

curl -fsSL https://packages.opentofu.org/opentofu/tofu/gpgkey | sudo gpg --no-tty --batch --dearmor -o /etc/apt/keyrings/opentofu-repo.gpg >/dev/null

sudo chmod a+r /etc/apt/keyrings/opentofu.gpg /etc/apt/keyrings/opentofu-repo.gpg
```

---

### Step 3: Add OpenTofu APT repository

```hcl
echo \
  "deb [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main
deb-src [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main" | \
  sudo tee /etc/apt/sources.list.d/opentofu.list > /dev/null

sudo chmod a+r /etc/apt/sources.list.d/opentofu.list

```

---

### Step 4: Install OpenTofu

```hcl
sudo apt update
sudo apt install -y tofu

```
---

## 🔵 Method 2: Install OpenTofu on RHEL / Rocky / Alma / CentOS (RPM)
## Supported Distributions

- RHEL 8 / 9
- Rocky Linux 8 / 9
- AlmaLinux 8 / 9
- CentOS Stream 8 / 9

---
### Step 1: Install required tools

```hcl
sudo dnf install -y dnf-plugins-core

```
---

### Step 2: Add OpenTofu RPM repository

```hcl
sudo cat >/etc/yum.repos.d/opentofu.repo <<EOF
[opentofu]
name=opentofu
baseurl=https://packages.opentofu.org/opentofu/tofu/rpm_any/rpm_any/\$basearch
repo_gpgcheck=0
gpgcheck=1
enabled=1
gpgkey=https://get.opentofu.org/opentofu.gpg
       https://packages.opentofu.org/opentofu/tofu/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300

[opentofu-source]
name=opentofu-source
baseurl=https://packages.opentofu.org/opentofu/tofu/rpm_any/rpm_any/SRPMS
repo_gpgcheck=0
gpgcheck=1
enabled=1
gpgkey=https://get.opentofu.org/opentofu.gpg
       https://packages.opentofu.org/opentofu/tofu/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
EOF

```

---
### Step 3: Install OpenTofu

```hcl
sudo dnf install -y opentofu
```

---

## 🟡 Method 3: Install OpenTofu Using Snap (Ubuntu)

#### Snap is useful when:

- Package manager access is restricted
- You want quick installation
- Distribution is not officially listed

---
### Step 1: Ensure snap is installed


```hcl
snap --version

```
If not installed:

```hcl
sudo apt install snapd     # Debian/Ubuntu

```
---
### Step 2: Install OpenTofu via Snap

```hcl
sudo snap install opentofu --classic

```

---

### ✅ Verify Installation

After installation (any method), verify:

```hcl
tofu version

```
Expected output:

```hcl
OpenTofu v1.x.x

```

---

### 🔄 Upgrade OpenTofu
#### Debian / Ubuntu

```hcl
sudo apt update
sudo apt upgrade tofu

```

#### RHEL-based

```hcl
sudo dnf upgrade opentofu

```

#### Snap

```hcl
sudo snap refresh opentofu

```

---

### 🗑 Uninstall OpenTofu
#### Debian / Ubuntu

```hcl
sudo apt remove -y tofu

```
#### RHEL-based

```hcl
sudo dnf remove -y opentofu

```

#### Snap

```hcl
sudo snap remove opentofu

```

---

### ⚠️ Common Issues & Troubleshooting


❌ tofu: command not found

✔ Restart the terminal

✔ Ensure /usr/bin or /snap/bin is in PATH

---

### ❌ Permission issues

Avoid running OpenTofu as root unless required.

---

#### 📌 Best Practices

✔ Use package manager (DEB/RPM) for servers

✔ Use Snap for quick testing

✔ Verify version after install

✔ Keep OpenTofu updated

---

## 📚 Official References

https://opentofu.org/docs/intro/install/deb/

https://opentofu.org/docs/intro/install/rpm/

https://opentofu.org/docs/intro/install/snap/

---
