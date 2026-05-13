# Azure CLI Installation and Usage Guide

Version 1.0, May 2026
Created by Alexandros Karales

**Current Azure CLI Version:** 2.86.0
**Official Documentation:** [Microsoft Learn - Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)

---

## Table of Contents

- [Installation](#installation)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Linux (Ubuntu/Debian)](#linux-ubuntudebian)
  - [Linux (RHEL/CentOS/Fedora)](#linux-rhelcentosfedora)
  - [Azure Cloud Shell (No Install)](#azure-cloud-shell-no-install-needed)
- [Getting Started](#getting-started)
- [Most Common Commands](#most-common-commands)
- [Resource Group Commands](#resource-group-commands)
- [Virtual Machine Commands](#virtual-machine-commands)
- [Storage Account Commands](#storage-account-commands)
- [Azure AI Services Commands](#azure-ai-services-commands)
- [Networking Commands](#networking-commands)
- [App Service Commands](#app-service-commands)
- [Tips and Tricks](#tips-and-tricks)
- [Troubleshooting](#troubleshooting)

---

## Installation

### Windows

#### Option 1: WinGet (Recommended)

Open **PowerShell** or **Command Prompt** as Administrator:

```powershell
winget install -e --id Microsoft.AzureCLI
```

#### Option 2: MSI Installer

1. Download the MSI installer from: [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)
2. Run the `.msi` file and follow the installation wizard.
3. Restart your terminal after installation.

#### Option 3: PowerShell (Silent Install)

```powershell
$ProgressPreference = 'SilentlyContinue'
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi
Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'
Remove-Item .\AzureCLI.msi
```

#### Verify Installation (Windows)

```powershell
az version
```

---

### macOS

#### Option 1: Homebrew (Recommended)

```bash
brew update && brew install azure-cli
```

#### Option 2: Manual Script

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

#### Update (macOS)

```bash
brew upgrade azure-cli
```

#### Verify Installation (macOS)

```bash
az version
```

---

### Linux (Ubuntu/Debian)

#### One-Line Install (Recommended)

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

#### Manual Steps

```bash
# 1. Install prerequisites
sudo apt-get update
sudo apt-get install -y ca-certificates curl apt-transport-https lsb-release gnupg

# 2. Download and install the Microsoft signing key
sudo mkdir -p /etc/apt/keyrings
curl -sLS https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/microsoft.gpg

# 3. Add the Azure CLI software repository
AZ_DIST=$(lsb_release -cs)
echo "Types: deb
URIs: https://packages.microsoft.com/repos/azure-cli/
Suites: ${AZ_DIST}
Components: main
Architectures: $(dpkg --print-architecture)
Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources

# 4. Update and install
sudo apt-get update
sudo apt-get install -y azure-cli
```

#### Verify Installation (Linux)

```bash
az version
```

---

### Linux (RHEL/CentOS/Fedora)

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Azure CLI repository
sudo dnf install -y https://packages.microsoft.com/config/rhel/9.0/packages-microsoft-prod.rpm

# Install Azure CLI
sudo dnf install -y azure-cli
```

---

### Azure Cloud Shell (No Install Needed)

Azure Cloud Shell is a browser-based shell with the Azure CLI pre-installed.

1. Go to [https://shell.azure.com](https://shell.azure.com)
2. Sign in with your Azure account.
3. Choose **Bash** or **PowerShell**.
4. The CLI is already available, just start typing `az` commands.

This is the easiest option for learners who do not want to install anything locally.

---

## Getting Started

### Login

```bash
# Interactive browser login (most common)
az login

# Login with a specific tenant
az login --tenant YOUR_TENANT_ID

# Login with a service principal (for automation)
az login --service-principal -u APP_ID -p PASSWORD --tenant TENANT_ID

# Check who you are logged in as
az account show
```

### Set Your Subscription

```bash
# List all subscriptions
az account list --output table

# Set the active subscription
az account set --subscription "Your Subscription Name"
# or by ID
az account set --subscription "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

### Configure Defaults

```bash
# Set default location (saves typing --location every time)
az configure --defaults location=eastus

# Set default resource group
az configure --defaults group=myResourceGroup

# View current defaults
az configure --list-defaults
```

---

## Most Common Commands

### General

| Command | Description |
|---------|-------------|
| `az login` | Sign in to Azure |
| `az logout` | Sign out |
| `az account show` | Show current subscription |
| `az account list --output table` | List all subscriptions |
| `az version` | Show Azure CLI version |
| `az upgrade` | Upgrade Azure CLI to latest version |
| `az interactive` | Launch interactive mode (autocomplete) |
| `az find "search term"` | Search for commands |
| `az --help` | Show help |

### Output Formats

```bash
# Table format (human readable)
az account list --output table

# JSON format (default, for scripting)
az account list --output json

# Tab-separated values
az account list --output tsv

# YAML format
az account list --output yaml

# Query specific fields with JMESPath
az account show --query "{name:name, id:id}" --output table
```

---

## Resource Group Commands

Resource groups are containers that hold related Azure resources.

```bash
# Create a resource group
az group create --name myResourceGroup --location eastus

# List all resource groups
az group list --output table

# Show details of a specific resource group
az group show --name myResourceGroup

# Delete a resource group (and ALL resources in it)
az group delete --name myResourceGroup --yes --no-wait

# List resources in a resource group
az resource list --resource-group myResourceGroup --output table
```

---

## Virtual Machine Commands

```bash
# Create a VM (Ubuntu, Standard_B1s - free tier eligible)
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Ubuntu2204 \
    --size Standard_B1s \
    --admin-username azureuser \
    --generate-ssh-keys

# List all VMs
az vm list --output table

# Show VM details
az vm show --resource-group myResourceGroup --name myVM --output table

# Start a VM
az vm start --resource-group myResourceGroup --name myVM

# Stop a VM (deallocate to stop billing)
az vm deallocate --resource-group myResourceGroup --name myVM

# Restart a VM
az vm restart --resource-group myResourceGroup --name myVM

# Delete a VM
az vm delete --resource-group myResourceGroup --name myVM --yes

# Get public IP of a VM
az vm show --resource-group myResourceGroup --name myVM \
    --show-details --query publicIps --output tsv

# Open a port on a VM
az vm open-port --resource-group myResourceGroup --name myVM --port 80

# List available VM sizes in a region
az vm list-sizes --location eastus --output table

# List available VM images
az vm image list --output table
az vm image list --offer Ubuntu --all --output table
```

---

## Storage Account Commands

```bash
# Create a storage account
az storage account create \
    --name mystorageaccount123 \
    --resource-group myResourceGroup \
    --location eastus \
    --sku Standard_LRS

# List storage accounts
az storage account list --output table

# Get storage account keys
az storage account keys list \
    --account-name mystorageaccount123 \
    --resource-group myResourceGroup \
    --output table

# Create a blob container
az storage container create \
    --name mycontainer \
    --account-name mystorageaccount123

# Upload a file to blob storage
az storage blob upload \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --name myfile.txt \
    --file ./localfile.txt

# List blobs in a container
az storage blob list \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --output table

# Download a blob
az storage blob download \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --name myfile.txt \
    --file ./downloaded.txt

# Delete a storage account
az storage account delete \
    --name mystorageaccount123 \
    --resource-group myResourceGroup --yes
```

---

## Azure AI Services Commands

These commands are relevant for the AI-900 and AI Solutions Developer courses.

```bash
# Create an Azure AI Services (Cognitive Services) account
az cognitiveservices account create \
    --name myAIService \
    --resource-group myResourceGroup \
    --kind CognitiveServices \
    --sku S0 \
    --location eastus \
    --yes

# List AI service accounts
az cognitiveservices account list --output table

# Get the endpoint and keys
az cognitiveservices account show \
    --name myAIService \
    --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv

az cognitiveservices account keys list \
    --name myAIService \
    --resource-group myResourceGroup \
    --output table

# Create a specific AI service (e.g., Language)
az cognitiveservices account create \
    --name myLanguageService \
    --resource-group myResourceGroup \
    --kind TextAnalytics \
    --sku F0 \
    --location eastus \
    --yes

# Create an OpenAI service
az cognitiveservices account create \
    --name myOpenAIService \
    --resource-group myResourceGroup \
    --kind OpenAI \
    --sku S0 \
    --location eastus \
    --yes

# Deploy a model to Azure OpenAI
az cognitiveservices account deployment create \
    --name myOpenAIService \
    --resource-group myResourceGroup \
    --deployment-name gpt-4o-mini \
    --model-name gpt-4o-mini \
    --model-version "2024-07-18" \
    --model-format OpenAI \
    --sku-capacity 10 \
    --sku-name Standard

# Delete an AI service
az cognitiveservices account delete \
    --name myAIService \
    --resource-group myResourceGroup
```

---

## Networking Commands

```bash
# Create a virtual network
az network vnet create \
    --resource-group myResourceGroup \
    --name myVNet \
    --address-prefix 10.0.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.0.0.0/24

# List virtual networks
az network vnet list --output table

# Create a Network Security Group (NSG)
az network nsg create \
    --resource-group myResourceGroup \
    --name myNSG

# Add a rule to allow SSH
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --name AllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --destination-port-range 22 \
    --access allow

# Create a public IP
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --sku Standard

# List public IPs
az network public-ip list --resource-group myResourceGroup --output table
```

---

## App Service Commands

```bash
# Create an App Service Plan
az appservice plan create \
    --name myAppPlan \
    --resource-group myResourceGroup \
    --sku F1 \
    --is-linux

# Create a Web App
az webapp create \
    --resource-group myResourceGroup \
    --plan myAppPlan \
    --name myWebApp123 \
    --runtime "PYTHON:3.11"

# List web apps
az webapp list --output table

# Deploy code from GitHub
az webapp deployment source config \
    --name myWebApp123 \
    --resource-group myResourceGroup \
    --repo-url https://github.com/user/repo \
    --branch main \
    --manual-integration

# View web app logs
az webapp log tail --name myWebApp123 --resource-group myResourceGroup

# Restart a web app
az webapp restart --name myWebApp123 --resource-group myResourceGroup

# Delete a web app
az webapp delete --name myWebApp123 --resource-group myResourceGroup
```

---

## Tips and Tricks

### 1. Use Interactive Mode

```bash
az interactive
```

This launches an auto-complete shell with inline documentation. Great for learning.

### 2. Use JMESPath Queries

```bash
# Get just the name of your subscription
az account show --query name --output tsv

# Get VM names and their power states
az vm list --query "[].{Name:name, State:powerState}" --output table

# Filter results
az vm list --query "[?location=='eastus']" --output table
```

### 3. Use `--no-wait` for Long Operations

```bash
# Start a delete without waiting for it to complete
az group delete --name myResourceGroup --yes --no-wait
```

### 4. Use `--debug` for Troubleshooting

```bash
az vm list --debug
```

### 5. Create Aliases

```bash
# Create custom shortcuts
az alias create --name rg --command "group"
az alias create --name ls-rg --command "group list --output table"

# Now you can use:
az ls-rg
```

### 6. Export as ARM Template

```bash
# Export a resource group as a template (Infrastructure as Code)
az group export --name myResourceGroup > template.json
```

### 7. Use Environment Variables for Auth

```bash
export AZURE_SUBSCRIPTION_ID="your-sub-id"
export AZURE_TENANT_ID="your-tenant-id"
```

---

## Troubleshooting

### "az: command not found"

- **Windows:** Restart your terminal after installation. If using WinGet, close and reopen PowerShell.
- **macOS:** Run `brew link azure-cli` or add to PATH: `export PATH="/opt/homebrew/bin:$PATH"`
- **Linux:** Run `source ~/.bashrc` or restart your terminal.

### "AADSTS50076: Multi-factor authentication required"

```bash
az login --tenant YOUR_TENANT_ID
```

### "The subscription is not registered to use namespace"

```bash
# Register a resource provider
az provider register --namespace Microsoft.CognitiveServices
az provider register --namespace Microsoft.Storage

# Check registration status
az provider show --namespace Microsoft.CognitiveServices --query "registrationState"
```

### "AuthorizationFailed"

You do not have permission. Contact your subscription administrator, or check that you are using the correct subscription:

```bash
az account list --output table
az account set --subscription "Correct Subscription Name"
```

### Update Azure CLI

```bash
# Windows (WinGet)
winget upgrade -e --id Microsoft.AzureCLI

# macOS (Homebrew)
brew upgrade azure-cli

# Linux (apt)
sudo apt-get update && sudo apt-get upgrade azure-cli

# Or use the built-in upgrade command
az upgrade
```

---

## Quick Reference Card

| Task | Command |
|------|---------|
| Login | `az login` |
| Show account | `az account show` |
| List subscriptions | `az account list -o table` |
| Set subscription | `az account set -s "Name"` |
| Create resource group | `az group create -n myRG -l eastus` |
| List resource groups | `az group list -o table` |
| Delete resource group | `az group delete -n myRG --yes` |
| Create VM | `az vm create -g myRG -n myVM --image Ubuntu2204` |
| Start VM | `az vm start -g myRG -n myVM` |
| Stop VM | `az vm deallocate -g myRG -n myVM` |
| Create storage | `az storage account create -n mysa -g myRG -l eastus --sku Standard_LRS` |
| Create AI service | `az cognitiveservices account create -n myAI -g myRG --kind CognitiveServices --sku S0 -l eastus` |
| Get AI keys | `az cognitiveservices account keys list -n myAI -g myRG` |
| Upgrade CLI | `az upgrade` |
| Help | `az <command> --help` |

---

## References

- [Azure CLI Documentation](https://learn.microsoft.com/en-us/cli/azure/)
- [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Azure CLI Command Reference](https://learn.microsoft.com/en-us/cli/azure/reference-index)
- [JMESPath Query Tutorial](https://learn.microsoft.com/en-us/cli/azure/query-azure-cli)
- [Azure Cloud Shell](https://shell.azure.com)

