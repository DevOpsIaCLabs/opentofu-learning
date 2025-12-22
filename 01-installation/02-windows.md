# OpenTofu Installation on Windows

## Introduction

This document explains how to install **OpenTofu** on **Microsoft Windows** using different supported methods.

You will learn:
- How to install OpenTofu using **Chocolatey** (recommended)
- How to install OpenTofu manually (ZIP method)
- How to verify the installation
- How to enable command auto-completion

---

## Prerequisites

Before installing OpenTofu, ensure:

- Windows 10 or Windows 11 (64-bit)
- Administrator access
- Internet connectivity
- PowerShell or Command Prompt available

Check Windows version:
```powershell
winver
```

## Installation Method 1: Using Chocolatey (Recommended)
Chocolatey is a popular Windows package manager and the simplest way to install OpenTofu.
### Step 1: Check if Chocolatey is installed

Powershell
```powershell
choco --version
```

If Chocolatey is not installed, install it using PowerShell (Run as Administrator):

Powershell
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; `
[System.Net.ServicePointManager]::SecurityProtocol = `
[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Restart PowerShell after installation.
### Step 2: Install OpenTofu

Powershell
```powershell
choco install opentofu -y
```

### Step 3: Verify installation

Powershell
```powershell
tofu version
```

Expected output:
Text
> OpenTofu v1.x.x
 

---
## Installation Method 2: Manual Installation (ZIP File)
Use this method if you do not want Chocolatey or are in a restricted environment.
### Step 1: Download OpenTofu binary
1. Go to the official OpenTofu releases page
2. Download the Windows (amd64) ZIP file
3. Extract the ZIP file

You will find:

Text
> tofu.exe

### Step 2: Move binary to a directory
Create a directory:

Text
>Copy tofu.exe into:

Text
> C:\opentofu


---
### Step 3: Add OpenTofu to PATH
1. Open System Properties
2. Click Environment Variables
3. Under System variables, select Path
4. Click Edit
5. Add:

Text
>C:\opentofu

Click OK and close all windows

### Step 4: Verify installation
Open a new PowerShell window and run:

Powershell
```powershell
tofu version
```

---
## Enable Auto-Completion (Optional)

PowerShell
```powershell
tofu -install-autocomplete
```

Restart PowerShell:

Powershell
```powershell
powershell
```
--- 
### Upgrade OpenTofu
#### Using Chocolatey

Powershell
```powershell
choco upgrade opentofu -y
```

### Manual Installation
- Download the latest ZIP
- Replace the existing tofu.exe
- Verify version again
---
## Uninstall OpenTofu
### Chocolatey

Powershell
```powershell
choco uninstall opentofu -y
```

### Manual
1. Delete C:\opentofu\tofu.exe
2. Remove C:\opentofu from PATH
---
## Common Issues & Troubleshooting
### ❌ tofu command not found
✔ Ensure the installation directory is added to PATH

✔ Restart PowerShell or Command Prompt
### ❌ PowerShell execution policy error
Run PowerShell as Administrator:

Powershell
```powershell
Set-ExecutionPolicy RemoteSigned
```

### Recommended Tools for Windows Users
1. Windows Terminal
2. PowerShell 7+
3. Git for Windows
4. VS Code

