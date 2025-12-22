# OpenTofu Installation on macOS

## Introduction

This document explains how to install **OpenTofu** on **macOS** using multiple supported methods.

You will learn:
- How to install OpenTofu using **Homebrew** (recommended)
- How to install OpenTofu manually (binary method)
- How to verify the installation
- How to enable command auto-completion

---

## Prerequisites

Before installing OpenTofu, ensure:

- macOS 12 (Monterey) or later
- Administrator access
- Internet connectivity
- Terminal access

Check macOS version:
```bash
sw_vers
```
---
## Installation Method 1: Using Homebrew (Recommended)
Homebrew is the most common package manager for macOS and the simplest way to install OpenTofu.
### Step 1: Check if Homebrew is installed

Bash
```bash
brew --version
```

If Homebrew is not installed, install it:

Bash
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Restart the terminal after installation.
### Step 2: Install OpenTofu

Bash
```bash
brew update
brew install opentofu
```

### Step 3: Verify installation

Bash
```bash
tofu version
```

Expected output:

Text
> OpenTofu v1.x.x
---
## Installation Method 2: Manual Installation (Binary)
Use this method if:
- Homebrew is not allowed
- You prefer manual installation
- You are in a restricted corporate environment
### Step 1: Download OpenTofu binary
1. Visit the official OpenTofu releases page
2. Download the correct binary for your system:
   - darwin_amd64 → Intel Macs
   - darwin_arm64 → Apple Silicon (M1/M2/M3)
3. Extract the archive

You will get a binary named:

Text
> tofu
### Step 2: Move binary to /usr/local/bin

Bash
```bash
sudo mv tofu /usr/local/bin/
```

Make it executable:

Bash
```bash
sudo chmod +x /usr/local/bin/tofu
```

### Step 3: Verify installation

Bash
```bash
tofu version
```

---
## Enable Auto-Completion (Optional)
### Bash

Bash
```bash
tofu -install-autocomplete
```
Restart terminal:
Bash
```bash
exec bash
```

### Zsh (default shell)

Bash
```bash
tofu -install-autocomplete
exec zsh
```
---
## Upgrade OpenTofu
### Homebrew

Bash
```bash
brew upgrade opentofu
```

### Manual Installation
- Download the latest binary
- Replace the existing tofu binary
- Verify version again

---
## Uninstall OpenTofu
Homebrew

Bash
```bash
brew uninstall opentofu
```

### Manual

Bash
```bash
sudo rm /usr/local/bin/tofu
```
---
## Common Issues & Troubleshooting
### ❌ tofu: command not found
✔ Ensure /usr/local/bin is in your PATH
✔ Restart the terminal
### ❌ Permission denied error

Bash
```bash
zsh: permission denied: tofu
```

✔ Run:

Bash
```bash
chmod +x /usr/local/bin/tofu
```
---
## Recommended Tools for macOS Users
- iTerm2 or Terminal
- Homebrew
- Visual Studio Code
- Git
- Docker Desktop (optional)