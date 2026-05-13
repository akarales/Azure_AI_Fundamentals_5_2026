# Azure CLI Complete Reference Guide

Version 1.0, May 2026
Created by Alexandros Karales

**Current Azure CLI Version:** 2.86.0
**Official Documentation:** [Microsoft Learn - Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)

---

## Table of Contents

1. [Installation (All Platforms)](#1-installation)
2. [Authentication and Account Management](#2-authentication-and-account-management)
3. [Resource Groups](#3-resource-groups)
4. [Resource Locks (GLAB 251.2.2)](#4-resource-locks)
5. [Cost Management (GLAB 251.2.1, 251.2.3)](#5-cost-management)
6. [Storage Accounts and Blobs (GLAB 251.1.3)](#6-storage-accounts-and-blobs)
7. [Virtual Machines](#7-virtual-machines)
8. [Networking (GLAB 251.1.2)](#8-networking)
9. [Azure AI Services (Multi-Service)](#9-azure-ai-services-multi-service)
10. [Azure Machine Learning (GLAB 260.2.1)](#10-azure-machine-learning)
11. [Azure AI Vision / Computer Vision (GLAB 261.2.3)](#11-azure-ai-vision--computer-vision)
12. [Azure AI Face (GLAB 261.2.1)](#12-azure-ai-face)
13. [Azure AI Language / Text Analytics (GLAB 262.1.1, 262.2.1, 262.2.2)](#13-azure-ai-language--text-analytics)
14. [Azure AI Speech (GLAB 262.3.1)](#14-azure-ai-speech)
15. [Azure AI Translator (GLAB 262.3.2)](#15-azure-ai-translator)
16. [Azure AI Document Intelligence (GLAB 263.1.1)](#16-azure-ai-document-intelligence)
17. [Azure AI Search (GLAB 263.2.1)](#17-azure-ai-search)
18. [Azure OpenAI Service (GLAB 264.1.1)](#18-azure-openai-service)
19. [Azure AI Content Safety (GLAB 264.1.2, 264.2.1)](#19-azure-ai-content-safety)
20. [Azure AI Foundry](#20-azure-ai-foundry)
21. [App Service and Web Apps](#21-app-service-and-web-apps)
22. [Azure Key Vault](#22-azure-key-vault)
23. [Azure Monitor and Logging](#23-azure-monitor-and-logging)
24. [Role-Based Access Control (RBAC)](#24-role-based-access-control-rbac)
25. [Tags and Organization](#25-tags-and-organization)
26. [ARM Templates and Bicep](#26-arm-templates-and-bicep)
27. [Output Formatting and JMESPath Queries](#27-output-formatting-and-jmespath-queries)
28. [Tips, Tricks, and Shortcuts](#28-tips-tricks-and-shortcuts)
29. [Troubleshooting](#29-troubleshooting)
30. [Quick Reference Card](#30-quick-reference-card)

---

## 1. Installation

### Windows

```powershell
# Option 1: WinGet (Recommended)
winget install -e --id Microsoft.AzureCLI

# Option 2: MSI Installer
# Download from: https://aka.ms/installazurecliwindows

# Option 3: PowerShell (Silent Install)
$ProgressPreference = 'SilentlyContinue'
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi
Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'
Remove-Item .\AzureCLI.msi
```

### macOS

```bash
# Homebrew (Recommended)
brew update && brew install azure-cli

# Update
brew upgrade azure-cli
```

### Linux (Ubuntu/Debian)

```bash
# One-liner
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

### Linux (RHEL/CentOS/Fedora)

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo dnf install -y https://packages.microsoft.com/config/rhel/9.0/packages-microsoft-prod.rpm
sudo dnf install -y azure-cli
```

### Azure Cloud Shell (No Install)

Go to [https://shell.azure.com](https://shell.azure.com) and sign in. The CLI is pre-installed.

### Verify and Update

```bash
az version
az upgrade
```

---

## 2. Authentication and Account Management

```bash
# Login (interactive browser)
az login

# Login to a specific tenant
az login --tenant YOUR_TENANT_ID

# Login with device code (useful for remote/SSH sessions)
az login --use-device-code

# Login with service principal (automation)
az login --service-principal -u APP_ID -p PASSWORD --tenant TENANT_ID

# Check current session
az account show
az account show --query "{Sub:name, ID:id, Tenant:tenantId}" --output table

# List all subscriptions
az account list --output table

# Set active subscription
az account set --subscription "Your Subscription Name"
az account set --subscription "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

# List available locations/regions
az account list-locations --output table

# Logout
az logout

# Clear all cached credentials
az account clear
```

### Configure Defaults

```bash
# Set defaults (saves typing --location and --resource-group every time)
az configure --defaults location=eastus group=myResourceGroup

# View current defaults
az configure --list-defaults

# Clear defaults
az configure --defaults location='' group=''
```

---

## 3. Resource Groups

Resource groups are containers that hold related Azure resources for an application.

```bash
# Create a resource group
az group create --name myResourceGroup --location eastus

# Create with tags
az group create --name myResourceGroup --location eastus \
    --tags Environment=Dev Project=AI-900 Owner=Student

# List all resource groups
az group list --output table

# Show details
az group show --name myResourceGroup

# List all resources in a group
az resource list --resource-group myResourceGroup --output table

# Check if a resource group exists
az group exists --name myResourceGroup

# Delete a resource group (and ALL resources inside)
az group delete --name myResourceGroup --yes --no-wait

# Export as ARM template
az group export --name myResourceGroup > template.json
```

---

## 4. Resource Locks

*Relevant to: GLAB 251.2.2 - Configure a Resource Lock*

Resource locks prevent accidental deletion or modification of critical resources.

```bash
# Create a delete lock on a resource group
az lock create --name NoDelete --resource-group myResourceGroup \
    --lock-type CanNotDelete --notes "Prevent accidental deletion"

# Create a read-only lock
az lock create --name ReadOnly --resource-group myResourceGroup \
    --lock-type ReadOnly --notes "Prevent modifications"

# Create a lock on a specific resource
az lock create --name ProtectStorage \
    --resource-group myResourceGroup \
    --resource-type Microsoft.Storage/storageAccounts \
    --resource-name mystorageaccount \
    --lock-type CanNotDelete

# List locks
az lock list --resource-group myResourceGroup --output table

# Show lock details
az lock show --name NoDelete --resource-group myResourceGroup

# Delete a lock
az lock delete --name NoDelete --resource-group myResourceGroup
```

### Lock Types

| Type | Allows Read | Allows Modify | Allows Delete |
|------|------------|--------------|--------------|
| **CanNotDelete** | Yes | Yes | No |
| **ReadOnly** | Yes | No | No |

---

## 5. Cost Management

*Relevant to: GLAB 251.2.1 - Pricing Calculator, GLAB 251.2.3 - TCO Calculator*

```bash
# Show current spending for subscription
az consumption usage list --top 10 --output table

# List budgets
az consumption budget list --output table

# Create a budget
az consumption budget create \
    --budget-name MonthlyBudget \
    --amount 50 \
    --time-grain Monthly \
    --start-date 2026-05-01 \
    --end-date 2026-12-31 \
    --category Cost

# Show cost for a resource group
az consumption usage list \
    --query "[?contains(instanceName, 'myResourceGroup')]" \
    --output table

# List usage for cognitive services
az cognitiveservices account list-usage \
    --name myAIService \
    --resource-group myResourceGroup \
    --output table

# Pricing Calculator (web tool, no CLI equivalent)
# https://azure.microsoft.com/en-us/pricing/calculator/

# TCO Calculator (web tool, no CLI equivalent)
# https://azure.microsoft.com/en-us/pricing/tco/calculator/
```

---

## 6. Storage Accounts and Blobs

*Relevant to: GLAB 251.1.3 - Create a Storage Blob*

```bash
# Create a storage account
az storage account create \
    --name mystorageaccount123 \
    --resource-group myResourceGroup \
    --location eastus \
    --sku Standard_LRS \
    --kind StorageV2

# List storage accounts
az storage account list --output table

# Show details
az storage account show --name mystorageaccount123 --resource-group myResourceGroup

# Get access keys
az storage account keys list \
    --account-name mystorageaccount123 \
    --resource-group myResourceGroup --output table

# Get connection string
az storage account show-connection-string \
    --name mystorageaccount123 \
    --resource-group myResourceGroup --output tsv
```

### Blob Storage

```bash
# Create a container
az storage container create \
    --name mycontainer \
    --account-name mystorageaccount123 \
    --public-access off

# List containers
az storage container list --account-name mystorageaccount123 --output table

# Upload a file
az storage blob upload \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --name uploaded-file.txt \
    --file ./local-file.txt

# Upload a directory
az storage blob upload-batch \
    --account-name mystorageaccount123 \
    --destination mycontainer \
    --source ./local-folder/

# List blobs
az storage blob list \
    --account-name mystorageaccount123 \
    --container-name mycontainer --output table

# Download a blob
az storage blob download \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --name uploaded-file.txt \
    --file ./downloaded-file.txt

# Generate a SAS token (Shared Access Signature)
az storage blob generate-sas \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --name uploaded-file.txt \
    --permissions r \
    --expiry 2026-12-31T23:59:59Z \
    --output tsv

# Delete a blob
az storage blob delete \
    --account-name mystorageaccount123 \
    --container-name mycontainer \
    --name uploaded-file.txt

# Delete a container
az storage container delete \
    --name mycontainer --account-name mystorageaccount123
```

### Storage SKUs

| SKU | Redundancy | Description |
|-----|-----------|-------------|
| `Standard_LRS` | Local | 3 copies in one datacenter |
| `Standard_ZRS` | Zone | 3 copies across zones |
| `Standard_GRS` | Geo | 6 copies across regions |
| `Standard_RAGRS` | Read-access Geo | GRS with read from secondary |
| `Premium_LRS` | Local (SSD) | High-performance SSD |

---

## 7. Virtual Machines

```bash
# Create a VM (Ubuntu)
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Ubuntu2204 \
    --size Standard_B1s \
    --admin-username azureuser \
    --generate-ssh-keys

# Create a Windows VM
az vm create \
    --resource-group myResourceGroup \
    --name myWinVM \
    --image Win2022Datacenter \
    --size Standard_B2s \
    --admin-username azureuser \
    --admin-password 'SecureP@ss123!'

# List VMs
az vm list --output table
az vm list --resource-group myResourceGroup --output table

# Show details with power state
az vm show --resource-group myResourceGroup --name myVM --show-details --output table

# Start / Stop / Restart / Delete
az vm start --resource-group myResourceGroup --name myVM
az vm deallocate --resource-group myResourceGroup --name myVM  # Stop + free resources
az vm stop --resource-group myResourceGroup --name myVM        # Stop (still billed)
az vm restart --resource-group myResourceGroup --name myVM
az vm delete --resource-group myResourceGroup --name myVM --yes

# Get public IP
az vm show --resource-group myResourceGroup --name myVM \
    --show-details --query publicIps --output tsv

# Open a port
az vm open-port --resource-group myResourceGroup --name myVM --port 80
az vm open-port --resource-group myResourceGroup --name myVM --port 443 --priority 900

# Resize a VM
az vm resize --resource-group myResourceGroup --name myVM --size Standard_B2s

# List available sizes
az vm list-sizes --location eastus --output table

# List available images
az vm image list --output table
az vm image list --publisher Canonical --offer ubuntu --all --output table
```

---

## 8. Networking

*Relevant to: GLAB 251.1.2 - Configure Network Access*

```bash
# Create a virtual network with a subnet
az network vnet create \
    --resource-group myResourceGroup \
    --name myVNet \
    --address-prefix 10.0.0.0/16 \
    --subnet-name default \
    --subnet-prefix 10.0.0.0/24

# List VNets
az network vnet list --output table

# Add a subnet
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --name backendSubnet \
    --address-prefix 10.0.1.0/24

# Create a Network Security Group
az network nsg create \
    --resource-group myResourceGroup \
    --name myNSG

# Add inbound rules
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --name AllowHTTP \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --destination-port-range 80 \
    --access allow

az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --name AllowHTTPS \
    --protocol tcp \
    --direction inbound \
    --priority 900 \
    --source-address-prefix '*' \
    --destination-port-range 443 \
    --access allow

az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --name DenyAllInbound \
    --protocol '*' \
    --direction inbound \
    --priority 4096 \
    --source-address-prefix '*' \
    --destination-port-range '*' \
    --access deny

# List NSG rules
az network nsg rule list --resource-group myResourceGroup --nsg-name myNSG --output table

# Associate NSG with a subnet
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --name default \
    --network-security-group myNSG

# Create a public IP
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --sku Standard \
    --allocation-method Static

# List public IPs
az network public-ip list --resource-group myResourceGroup --output table

# DNS zone management
az network dns zone create --resource-group myResourceGroup --name example.com
az network dns record-set a add-record \
    --resource-group myResourceGroup \
    --zone-name example.com \
    --record-set-name www \
    --ipv4-address 1.2.3.4
```

---

## 9. Azure AI Services (Multi-Service)

*Relevant to: GLAB 251.1.1 - Create an Azure Resource*

The multi-service resource gives access to multiple AI services with one key.

```bash
# Create a multi-service AI resource
az cognitiveservices account create \
    --name myAIServices \
    --resource-group myResourceGroup \
    --kind CognitiveServices \
    --sku S0 \
    --location eastus \
    --yes

# List all cognitive services accounts
az cognitiveservices account list --output table

# Show endpoint
az cognitiveservices account show \
    --name myAIServices \
    --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv

# Get keys
az cognitiveservices account keys list \
    --name myAIServices \
    --resource-group myResourceGroup

# Regenerate a key
az cognitiveservices account keys regenerate \
    --name myAIServices \
    --resource-group myResourceGroup \
    --key-name key1

# Check usage
az cognitiveservices account list-usage \
    --name myAIServices \
    --resource-group myResourceGroup --output table

# List available SKUs for a kind
az cognitiveservices account list-skus \
    --kind CognitiveServices \
    --location eastus --output table

# Delete
az cognitiveservices account delete \
    --name myAIServices \
    --resource-group myResourceGroup

# Purge (permanently delete a soft-deleted resource)
az cognitiveservices account purge \
    --name myAIServices \
    --resource-group myResourceGroup \
    --location eastus

# List soft-deleted resources
az cognitiveservices account list-deleted --output table
```

### AI Service Kind Values

| Kind | Service |
|------|---------|
| `CognitiveServices` | Multi-service (all-in-one) |
| `ComputerVision` | Computer Vision |
| `Face` | Face API |
| `TextAnalytics` | Language / Text Analytics |
| `SpeechServices` | Speech to Text, Text to Speech |
| `TextTranslation` | Translator |
| `FormRecognizer` | Document Intelligence |
| `OpenAI` | Azure OpenAI |
| `ContentSafety` | Content Safety |
| `AnomalyDetector` | Anomaly Detector |
| `CustomVision.Training` | Custom Vision (training) |
| `CustomVision.Prediction` | Custom Vision (prediction) |
| `ImmersiveReader` | Immersive Reader |
| `AIServices` | Azure AI Services (newer multi-service) |

### Free Tier (F0) Available For

```bash
# These services offer an F0 (free) SKU
az cognitiveservices account create --kind ComputerVision --sku F0 ...
az cognitiveservices account create --kind TextAnalytics --sku F0 ...
az cognitiveservices account create --kind Face --sku F0 ...
az cognitiveservices account create --kind SpeechServices --sku F0 ...
az cognitiveservices account create --kind TextTranslation --sku F0 ...
az cognitiveservices account create --kind FormRecognizer --sku F0 ...
az cognitiveservices account create --kind ContentSafety --sku F0 ...
```

---

## 10. Azure Machine Learning

*Relevant to: GLAB 260.2.1 - Explore Automated Machine Learning in Azure*

```bash
# Install the ML extension
az extension add --name ml

# Create an ML workspace
az ml workspace create \
    --name myMLWorkspace \
    --resource-group myResourceGroup \
    --location eastus

# List workspaces
az ml workspace list --output table

# Show workspace details
az ml workspace show \
    --name myMLWorkspace \
    --resource-group myResourceGroup

# Create a compute instance (for notebooks)
az ml compute create \
    --name myCompute \
    --type ComputeInstance \
    --size Standard_DS3_v2 \
    --resource-group myResourceGroup \
    --workspace-name myMLWorkspace

# Create a compute cluster (for training jobs)
az ml compute create \
    --name myCluster \
    --type AmlCompute \
    --size Standard_DS3_v2 \
    --min-instances 0 \
    --max-instances 4 \
    --resource-group myResourceGroup \
    --workspace-name myMLWorkspace

# List compute resources
az ml compute list --resource-group myResourceGroup --workspace-name myMLWorkspace --output table

# Start/Stop compute instance
az ml compute start --name myCompute --resource-group myResourceGroup --workspace-name myMLWorkspace
az ml compute stop --name myCompute --resource-group myResourceGroup --workspace-name myMLWorkspace

# Submit an AutoML job (YAML config required)
az ml job create \
    --file automl-job.yml \
    --resource-group myResourceGroup \
    --workspace-name myMLWorkspace

# List jobs
az ml job list --resource-group myResourceGroup --workspace-name myMLWorkspace --output table

# List registered models
az ml model list --resource-group myResourceGroup --workspace-name myMLWorkspace --output table

# Create an online endpoint
az ml online-endpoint create \
    --name myEndpoint \
    --resource-group myResourceGroup \
    --workspace-name myMLWorkspace

# Delete workspace
az ml workspace delete \
    --name myMLWorkspace \
    --resource-group myResourceGroup --yes
```

---

## 11. Azure AI Vision / Computer Vision

*Relevant to: GLAB 261.2.3 - Analyze Images with the Computer Vision Service*

```bash
# Create Computer Vision resource
az cognitiveservices account create \
    --name myComputerVision \
    --resource-group myResourceGroup \
    --kind ComputerVision \
    --sku F0 \
    --location eastus \
    --yes

# Get endpoint and key
CV_ENDPOINT=$(az cognitiveservices account show \
    --name myComputerVision --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv)

CV_KEY=$(az cognitiveservices account keys list \
    --name myComputerVision --resource-group myResourceGroup \
    --query "key1" --output tsv)

echo "Endpoint: $CV_ENDPOINT"
echo "Key: $CV_KEY"
```

### Test with curl (Analyze Image)

```bash
# Analyze an image from URL
curl -X POST "${CV_ENDPOINT}computervision/imageanalysis:analyze?api-version=2024-02-01&features=caption,tags,objects,people,read" \
    -H "Ocp-Apim-Subscription-Key: ${CV_KEY}" \
    -H "Content-Type: application/json" \
    -d '{"url": "https://upload.wikimedia.org/wikipedia/commons/thumb/4/47/PNG_transparency_demonstration_1.png/300px-PNG_transparency_demonstration_1.png"}'
```

### Test with Python

```python
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.core.credentials import AzureKeyCredential
import os

client = ImageAnalysisClient(
    endpoint=os.environ["CV_ENDPOINT"],
    credential=AzureKeyCredential(os.environ["CV_KEY"])
)

result = client.analyze_from_url(
    image_url="https://example.com/image.jpg",
    visual_features=["CAPTION", "TAGS", "OBJECTS", "READ"]
)

print(f"Caption: {result.caption.text} ({result.caption.confidence:.2f})")
for tag in result.tags.list:
    print(f"Tag: {tag.name} ({tag.confidence:.2f})")
```

### OCR (GLAB 261.2.2 - Optical Character Recognition)

```bash
# OCR via REST API
curl -X POST "${CV_ENDPOINT}computervision/imageanalysis:analyze?api-version=2024-02-01&features=read" \
    -H "Ocp-Apim-Subscription-Key: ${CV_KEY}" \
    -H "Content-Type: application/json" \
    -d '{"url": "https://example.com/document-image.jpg"}'
```

---

## 12. Azure AI Face

*Relevant to: GLAB 261.2.1 - Face Detection with Azure AI*

```bash
# Create Face resource
az cognitiveservices account create \
    --name myFaceAPI \
    --resource-group myResourceGroup \
    --kind Face \
    --sku F0 \
    --location eastus \
    --yes

# Get endpoint and key
FACE_ENDPOINT=$(az cognitiveservices account show \
    --name myFaceAPI --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv)

FACE_KEY=$(az cognitiveservices account keys list \
    --name myFaceAPI --resource-group myResourceGroup \
    --query "key1" --output tsv)
```

### Test with curl

```bash
curl -X POST "${FACE_ENDPOINT}face/v1.0/detect?returnFaceAttributes=age,gender,headPose,smile,facialHair,glasses,emotion" \
    -H "Ocp-Apim-Subscription-Key: ${FACE_KEY}" \
    -H "Content-Type: application/json" \
    -d '{"url": "https://example.com/face-photo.jpg"}'
```

### Test with Python

```python
from azure.ai.vision.face import FaceClient
from azure.core.credentials import AzureKeyCredential

client = FaceClient(
    endpoint=os.environ["FACE_ENDPOINT"],
    credential=AzureKeyCredential(os.environ["FACE_KEY"])
)

with open("photo.jpg", "rb") as image_file:
    faces = client.detect(
        image_content=image_file.read(),
        detection_model="detection_03",
        recognition_model="recognition_04",
        return_face_attributes=["headPose", "blur", "exposure", "noise"]
    )

for face in faces:
    print(f"Face ID: {face.face_id}")
    print(f"Age: {face.face_attributes.age}")
```

---

## 13. Azure AI Language / Text Analytics

*Relevant to: GLAB 262.1.1, GLAB 262.2.1, GLAB 262.2.2*

```bash
# Create Language resource
az cognitiveservices account create \
    --name myLanguageService \
    --resource-group myResourceGroup \
    --kind TextAnalytics \
    --sku F0 \
    --location eastus \
    --yes

# Get endpoint and key
LANG_ENDPOINT=$(az cognitiveservices account show \
    --name myLanguageService --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv)

LANG_KEY=$(az cognitiveservices account keys list \
    --name myLanguageService --resource-group myResourceGroup \
    --query "key1" --output tsv)
```

### Sentiment Analysis (GLAB 262.1.1)

```bash
curl -X POST "${LANG_ENDPOINT}language/:analyze-text?api-version=2024-11-15-preview" \
    -H "Ocp-Apim-Subscription-Key: ${LANG_KEY}" \
    -H "Content-Type: application/json" \
    -d '{
        "kind": "SentimentAnalysis",
        "analysisInput": {
            "documents": [
                {"id": "1", "language": "en", "text": "The food was delicious and the service was excellent."},
                {"id": "2", "language": "en", "text": "The room was dirty and the staff was rude."}
            ]
        }
    }'
```

### Key Phrase Extraction

```bash
curl -X POST "${LANG_ENDPOINT}language/:analyze-text?api-version=2024-11-15-preview" \
    -H "Ocp-Apim-Subscription-Key: ${LANG_KEY}" \
    -H "Content-Type: application/json" \
    -d '{
        "kind": "KeyPhraseExtraction",
        "analysisInput": {
            "documents": [
                {"id": "1", "language": "en", "text": "Azure AI services provide powerful tools for building intelligent applications."}
            ]
        }
    }'
```

### Named Entity Recognition

```bash
curl -X POST "${LANG_ENDPOINT}language/:analyze-text?api-version=2024-11-15-preview" \
    -H "Ocp-Apim-Subscription-Key: ${LANG_KEY}" \
    -H "Content-Type: application/json" \
    -d '{
        "kind": "EntityRecognition",
        "analysisInput": {
            "documents": [
                {"id": "1", "language": "en", "text": "Microsoft was founded by Bill Gates in Redmond, Washington in 1975."}
            ]
        }
    }'
```

### Language Detection

```bash
curl -X POST "${LANG_ENDPOINT}language/:analyze-text?api-version=2024-11-15-preview" \
    -H "Ocp-Apim-Subscription-Key: ${LANG_KEY}" \
    -H "Content-Type: application/json" \
    -d '{
        "kind": "LanguageDetection",
        "analysisInput": {
            "documents": [
                {"id": "1", "text": "Bonjour, comment allez-vous?"},
                {"id": "2", "text": "Hola, como estas?"}
            ]
        }
    }'
```

### Question Answering (GLAB 262.2.1)

```bash
# Create a QnA project (done via Language Studio or REST API)
curl -X POST "${LANG_ENDPOINT}language/query-knowledgebases/projects/myProject/:query?api-version=2021-10-01" \
    -H "Ocp-Apim-Subscription-Key: ${LANG_KEY}" \
    -H "Content-Type: application/json" \
    -d '{
        "question": "What is Azure AI?",
        "top": 3,
        "confidenceScoreThreshold": 0.2
    }'
```

### Python SDK

```python
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

client = TextAnalyticsClient(
    endpoint=os.environ["LANG_ENDPOINT"],
    credential=AzureKeyCredential(os.environ["LANG_KEY"])
)

# Sentiment analysis
documents = ["The product is amazing!", "Terrible experience."]
result = client.analyze_sentiment(documents)
for doc in result:
    print(f"Sentiment: {doc.sentiment} (pos: {doc.confidence_scores.positive:.2f})")

# Key phrases
result = client.extract_key_phrases(documents)
for doc in result:
    print(f"Key phrases: {doc.key_phrases}")

# Entity recognition
result = client.recognize_entities(["Microsoft was founded by Bill Gates."])
for doc in result:
    for entity in doc.entities:
        print(f"Entity: {entity.text} ({entity.category})")
```

---

## 14. Azure AI Speech

*Relevant to: GLAB 262.3.1 - Explore Azure AI Speech Capabilities*

```bash
# Create Speech resource
az cognitiveservices account create \
    --name mySpeechService \
    --resource-group myResourceGroup \
    --kind SpeechServices \
    --sku F0 \
    --location eastus \
    --yes

# Get key and region
SPEECH_KEY=$(az cognitiveservices account keys list \
    --name mySpeechService --resource-group myResourceGroup \
    --query "key1" --output tsv)

SPEECH_REGION="eastus"
```

### Speech to Text (curl)

```bash
# Convert audio to text
curl -X POST "https://${SPEECH_REGION}.stt.speech.microsoft.com/speech/recognition/conversation/cognitiveservices/v1?language=en-US" \
    -H "Ocp-Apim-Subscription-Key: ${SPEECH_KEY}" \
    -H "Content-Type: audio/wav" \
    --data-binary @audio-file.wav
```

### Text to Speech (curl)

```bash
# Get an access token first
TOKEN=$(curl -X POST "https://${SPEECH_REGION}.api.cognitive.microsoft.com/sts/v1.0/issueToken" \
    -H "Ocp-Apim-Subscription-Key: ${SPEECH_KEY}" \
    -H "Content-Length: 0" --output -)

# Convert text to speech
curl -X POST "https://${SPEECH_REGION}.tts.speech.microsoft.com/cognitiveservices/v1" \
    -H "Authorization: Bearer ${TOKEN}" \
    -H "Content-Type: application/ssml+xml" \
    -H "X-Microsoft-OutputFormat: audio-16khz-128kbitrate-mono-mp3" \
    -d '<speak version="1.0" xmlns="http://www.w3.org/2001/10/synthesis" xml:lang="en-US">
        <voice name="en-US-JennyNeural">Hello, welcome to Azure AI Speech services!</voice>
    </speak>' \
    --output output.mp3
```

### Python SDK

```python
import azure.cognitiveservices.speech as speechsdk

# Speech to Text
speech_config = speechsdk.SpeechConfig(
    subscription=os.environ["SPEECH_KEY"],
    region=os.environ["SPEECH_REGION"]
)
recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config)
result = recognizer.recognize_once()
print(f"Recognized: {result.text}")

# Text to Speech
speech_config.speech_synthesis_voice_name = "en-US-JennyNeural"
synthesizer = speechsdk.SpeechSynthesizer(speech_config=speech_config)
result = synthesizer.speak_text("Hello, welcome to Azure AI!")
```

---

## 15. Azure AI Translator

*Relevant to: GLAB 262.3.2 - Exploring Language Translation with Azure AI*

```bash
# Create Translator resource
az cognitiveservices account create \
    --name myTranslator \
    --resource-group myResourceGroup \
    --kind TextTranslation \
    --sku F0 \
    --location global \
    --yes

TRANSLATOR_KEY=$(az cognitiveservices account keys list \
    --name myTranslator --resource-group myResourceGroup \
    --query "key1" --output tsv)
```

### Translate Text (curl)

```bash
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=es&to=fr&to=de" \
    -H "Ocp-Apim-Subscription-Key: ${TRANSLATOR_KEY}" \
    -H "Ocp-Apim-Subscription-Region: eastus" \
    -H "Content-Type: application/json" \
    -d '[{"text": "Hello, how are you today?"}]'
```

### Detect Language

```bash
curl -X POST "https://api.cognitive.microsofttranslator.com/detect?api-version=3.0" \
    -H "Ocp-Apim-Subscription-Key: ${TRANSLATOR_KEY}" \
    -H "Content-Type: application/json" \
    -d '[{"text": "Bonjour le monde"}]'
```

### Get Supported Languages

```bash
curl "https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation"
```

### Python

```python
import requests, uuid

headers = {
    'Ocp-Apim-Subscription-Key': os.environ['TRANSLATOR_KEY'],
    'Ocp-Apim-Subscription-Region': 'eastus',
    'Content-Type': 'application/json',
    'X-ClientTraceId': str(uuid.uuid4())
}

body = [{'text': 'Hello, how are you?'}]
response = requests.post(
    'https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=es&to=fr',
    headers=headers, json=body
)
print(response.json())
```

---

## 16. Azure AI Document Intelligence

*Relevant to: GLAB 263.1.1 - Exploring Document Intelligence with Azure AI*

```bash
# Create Document Intelligence resource
az cognitiveservices account create \
    --name myDocIntelligence \
    --resource-group myResourceGroup \
    --kind FormRecognizer \
    --sku F0 \
    --location eastus \
    --yes

DOC_ENDPOINT=$(az cognitiveservices account show \
    --name myDocIntelligence --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv)

DOC_KEY=$(az cognitiveservices account keys list \
    --name myDocIntelligence --resource-group myResourceGroup \
    --query "key1" --output tsv)
```

### Analyze Document (Prebuilt Invoice Model)

```bash
# Start analysis
curl -X POST "${DOC_ENDPOINT}documentintelligence/documentModels/prebuilt-invoice:analyze?api-version=2024-11-30" \
    -H "Ocp-Apim-Subscription-Key: ${DOC_KEY}" \
    -H "Content-Type: application/json" \
    -d '{"urlSource": "https://raw.githubusercontent.com/Azure/azure-sdk-for-python/main/sdk/documentintelligence/azure-ai-documentintelligence/tests/sample_forms/forms/Invoice_1.pdf"}'
```

### Available Prebuilt Models

| Model | Use Case |
|-------|----------|
| `prebuilt-read` | Extract text from documents |
| `prebuilt-layout` | Extract text, tables, structure |
| `prebuilt-invoice` | Extract invoice fields |
| `prebuilt-receipt` | Extract receipt data |
| `prebuilt-idDocument` | Extract ID card/passport data |
| `prebuilt-businessCard` | Extract business card data |
| `prebuilt-tax.us.w2` | Extract W-2 tax form data |
| `prebuilt-healthInsuranceCard.us` | Extract insurance card data |

### Python SDK

```python
from azure.ai.documentintelligence import DocumentIntelligenceClient
from azure.core.credentials import AzureKeyCredential

client = DocumentIntelligenceClient(
    endpoint=os.environ["DOC_ENDPOINT"],
    credential=AzureKeyCredential(os.environ["DOC_KEY"])
)

poller = client.begin_analyze_document(
    "prebuilt-invoice",
    analyze_request={"url_source": "https://example.com/invoice.pdf"}
)
result = poller.result()

for doc in result.documents:
    print(f"Vendor: {doc.fields.get('VendorName', {}).get('content')}")
    print(f"Total: {doc.fields.get('InvoiceTotal', {}).get('content')}")
```

---

## 17. Azure AI Search

*Relevant to: GLAB 263.2.1 - Explore Azure AI Search*

```bash
# Create a search service
az search service create \
    --name mysearchservice123 \
    --resource-group myResourceGroup \
    --sku free \
    --location eastus

# List search services
az search service list --resource-group myResourceGroup --output table

# Get admin keys
az search admin-key show \
    --service-name mysearchservice123 \
    --resource-group myResourceGroup

# Get query keys
az search query-key list \
    --service-name mysearchservice123 \
    --resource-group myResourceGroup --output table

# Create a query key
az search query-key create \
    --name myQueryKey \
    --service-name mysearchservice123 \
    --resource-group myResourceGroup
```

### Index Operations (REST API)

```bash
SEARCH_ENDPOINT="https://mysearchservice123.search.windows.net"
SEARCH_KEY="your-admin-key"

# Create an index
curl -X PUT "${SEARCH_ENDPOINT}/indexes/my-index?api-version=2024-07-01" \
    -H "Content-Type: application/json" \
    -H "api-key: ${SEARCH_KEY}" \
    -d '{
        "name": "my-index",
        "fields": [
            {"name": "id", "type": "Edm.String", "key": true, "filterable": true},
            {"name": "title", "type": "Edm.String", "searchable": true},
            {"name": "content", "type": "Edm.String", "searchable": true},
            {"name": "category", "type": "Edm.String", "filterable": true, "facetable": true}
        ]
    }'

# Upload documents
curl -X POST "${SEARCH_ENDPOINT}/indexes/my-index/docs/index?api-version=2024-07-01" \
    -H "Content-Type: application/json" \
    -H "api-key: ${SEARCH_KEY}" \
    -d '{
        "value": [
            {"@search.action": "upload", "id": "1", "title": "AI Fundamentals", "content": "Introduction to AI concepts", "category": "AI"},
            {"@search.action": "upload", "id": "2", "title": "Machine Learning", "content": "Supervised and unsupervised learning", "category": "ML"}
        ]
    }'

# Search
curl "${SEARCH_ENDPOINT}/indexes/my-index/docs?api-version=2024-07-01&search=AI&\$top=5" \
    -H "api-key: ${SEARCH_KEY}"
```

### Search SKUs

| SKU | Indexes | Storage | Price |
|-----|---------|---------|-------|
| `free` | 3 | 50 MB | Free |
| `basic` | 15 | 2 GB | ~$75/mo |
| `standard` | 50 | 25 GB | ~$250/mo |

---

## 18. Azure OpenAI Service

*Relevant to: GLAB 264.1.1 - Explore Azure AI Foundry*

```bash
# Create Azure OpenAI resource
az cognitiveservices account create \
    --name myAzureOpenAI \
    --resource-group myResourceGroup \
    --kind OpenAI \
    --sku S0 \
    --location eastus \
    --yes

AOAI_ENDPOINT=$(az cognitiveservices account show \
    --name myAzureOpenAI --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv)

AOAI_KEY=$(az cognitiveservices account keys list \
    --name myAzureOpenAI --resource-group myResourceGroup \
    --query "key1" --output tsv)

# Deploy a model
az cognitiveservices account deployment create \
    --name myAzureOpenAI \
    --resource-group myResourceGroup \
    --deployment-name gpt-4o-mini \
    --model-name gpt-4o-mini \
    --model-version "2024-07-18" \
    --model-format OpenAI \
    --sku-capacity 10 \
    --sku-name Standard

# List deployments
az cognitiveservices account deployment list \
    --name myAzureOpenAI \
    --resource-group myResourceGroup --output table

# Delete a deployment
az cognitiveservices account deployment delete \
    --name myAzureOpenAI \
    --resource-group myResourceGroup \
    --deployment-name gpt-4o-mini
```

### Test with curl

```bash
curl -X POST "${AOAI_ENDPOINT}openai/deployments/gpt-4o-mini/chat/completions?api-version=2024-08-01-preview" \
    -H "Content-Type: application/json" \
    -H "api-key: ${AOAI_KEY}" \
    -d '{
        "messages": [
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": "What is Azure AI?"}
        ],
        "max_tokens": 200
    }'
```

### Python SDK

```python
from openai import AzureOpenAI

client = AzureOpenAI(
    api_key=os.environ["AOAI_KEY"],
    api_version="2024-08-01-preview",
    azure_endpoint=os.environ["AOAI_ENDPOINT"]
)

response = client.chat.completions.create(
    model="gpt-4o-mini",  # deployment name
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Explain Azure AI services."}
    ]
)
print(response.choices[0].message.content)
```

---

## 19. Azure AI Content Safety

*Relevant to: GLAB 264.1.2, GLAB 264.2.1*

```bash
# Create Content Safety resource
az cognitiveservices account create \
    --name myContentSafety \
    --resource-group myResourceGroup \
    --kind ContentSafety \
    --sku F0 \
    --location eastus \
    --yes

CS_ENDPOINT=$(az cognitiveservices account show \
    --name myContentSafety --resource-group myResourceGroup \
    --query "properties.endpoint" --output tsv)

CS_KEY=$(az cognitiveservices account keys list \
    --name myContentSafety --resource-group myResourceGroup \
    --query "key1" --output tsv)
```

### Analyze Text

```bash
curl -X POST "${CS_ENDPOINT}contentsafety/text:analyze?api-version=2024-09-01" \
    -H "Ocp-Apim-Subscription-Key: ${CS_KEY}" \
    -H "Content-Type: application/json" \
    -d '{
        "text": "Your text to analyze for safety",
        "categories": ["Hate", "SelfHarm", "Sexual", "Violence"],
        "outputType": "FourSeverityLevels"
    }'
```

### Severity Levels

| Level | Score | Description |
|-------|-------|-------------|
| Safe | 0 | No harmful content detected |
| Low | 2 | Mild content |
| Medium | 4 | Moderate content |
| High | 6 | Severe content |

### Python SDK

```python
from azure.ai.contentsafety import ContentSafetyClient
from azure.ai.contentsafety.models import AnalyzeTextOptions
from azure.core.credentials import AzureKeyCredential

client = ContentSafetyClient(
    endpoint=os.environ["CS_ENDPOINT"],
    credential=AzureKeyCredential(os.environ["CS_KEY"])
)

result = client.analyze_text(AnalyzeTextOptions(text="Text to check"))
for category in result.categories_analysis:
    print(f"{category.category}: severity {category.severity}")
```

---

## 20. Azure AI Foundry

Azure AI Foundry (formerly Azure AI Studio) is accessed via the web portal, but you can manage some components via CLI.

```bash
# Install the AI extension
az extension add --name ai

# Create an AI Hub
az ai hub create \
    --name myAIHub \
    --resource-group myResourceGroup \
    --location eastus

# Create an AI Project
az ai project create \
    --name myAIProject \
    --resource-group myResourceGroup \
    --hub-name myAIHub

# List projects
az ai project list --resource-group myResourceGroup --output table

# Portal access
# https://ai.azure.com
```

---

## 21. App Service and Web Apps

```bash
# Create an App Service Plan
az appservice plan create \
    --name myAppPlan \
    --resource-group myResourceGroup \
    --sku F1 \
    --is-linux

# Create a Python Web App
az webapp create \
    --resource-group myResourceGroup \
    --plan myAppPlan \
    --name myWebApp123 \
    --runtime "PYTHON:3.11"

# Deploy from local Git
az webapp deployment source config-local-git \
    --name myWebApp123 \
    --resource-group myResourceGroup

# Deploy from GitHub
az webapp deployment source config \
    --name myWebApp123 \
    --resource-group myResourceGroup \
    --repo-url https://github.com/user/repo \
    --branch main --manual-integration

# Set environment variables
az webapp config appsettings set \
    --name myWebApp123 \
    --resource-group myResourceGroup \
    --settings OPENAI_API_KEY=sk-xxx AI_ENDPOINT=https://xxx

# View logs
az webapp log tail --name myWebApp123 --resource-group myResourceGroup

# Restart / Stop / Start
az webapp restart --name myWebApp123 --resource-group myResourceGroup
az webapp stop --name myWebApp123 --resource-group myResourceGroup
az webapp start --name myWebApp123 --resource-group myResourceGroup

# List runtimes
az webapp list-runtimes --output table

# Delete
az webapp delete --name myWebApp123 --resource-group myResourceGroup
```

---

## 22. Azure Key Vault

Store API keys and secrets securely.

```bash
# Create a Key Vault
az keyvault create \
    --name myKeyVault123 \
    --resource-group myResourceGroup \
    --location eastus

# Store a secret
az keyvault secret set \
    --vault-name myKeyVault123 \
    --name OpenAIKey \
    --value "sk-your-api-key-here"

# Get a secret
az keyvault secret show \
    --vault-name myKeyVault123 \
    --name OpenAIKey \
    --query "value" --output tsv

# List secrets
az keyvault secret list --vault-name myKeyVault123 --output table

# Delete a secret
az keyvault secret delete --vault-name myKeyVault123 --name OpenAIKey

# Purge a deleted secret (permanent)
az keyvault secret purge --vault-name myKeyVault123 --name OpenAIKey

# Delete vault
az keyvault delete --name myKeyVault123 --resource-group myResourceGroup
```

---

## 23. Azure Monitor and Logging

```bash
# View activity log for a resource group
az monitor activity-log list \
    --resource-group myResourceGroup \
    --max-events 20 --output table

# Create an alert rule
az monitor metrics alert create \
    --name HighCPU \
    --resource-group myResourceGroup \
    --scopes /subscriptions/xxx/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM \
    --condition "avg Percentage CPU > 80" \
    --description "Alert when CPU exceeds 80%"

# List diagnostic settings
az monitor diagnostic-settings list \
    --resource /subscriptions/xxx/resourceGroups/myRG/providers/Microsoft.CognitiveServices/accounts/myAI

# Create a Log Analytics workspace
az monitor log-analytics workspace create \
    --resource-group myResourceGroup \
    --workspace-name myLogWorkspace \
    --location eastus
```

---

## 24. Role-Based Access Control (RBAC)

```bash
# List role assignments for a resource group
az role assignment list --resource-group myResourceGroup --output table

# Assign a role to a user
az role assignment create \
    --assignee user@example.com \
    --role "Contributor" \
    --resource-group myResourceGroup

# Assign Cognitive Services User role
az role assignment create \
    --assignee user@example.com \
    --role "Cognitive Services User" \
    --scope /subscriptions/xxx/resourceGroups/myRG/providers/Microsoft.CognitiveServices/accounts/myAI

# List available roles
az role definition list --output table
az role definition list --query "[?contains(roleName, 'Cognitive')]" --output table

# Remove a role assignment
az role assignment delete \
    --assignee user@example.com \
    --role "Contributor" \
    --resource-group myResourceGroup
```

### Common Roles for AI Labs

| Role | Description |
|------|-------------|
| `Owner` | Full access + manage permissions |
| `Contributor` | Full access, cannot manage permissions |
| `Reader` | Read-only access |
| `Cognitive Services User` | Read keys and make API calls |
| `Cognitive Services Contributor` | Create and manage AI resources |
| `Storage Blob Data Contributor` | Read/write blob data |

---

## 25. Tags and Organization

```bash
# Add tags to a resource group
az group update --name myResourceGroup \
    --tags Environment=Lab Course=AI-900 Module=251

# Add tags to a resource
az resource tag \
    --tags Purpose=Demo \
    --ids /subscriptions/xxx/resourceGroups/myRG/providers/Microsoft.Storage/storageAccounts/mysa

# List resources by tag
az resource list --tag Environment=Lab --output table

# Remove a tag
az group update --name myResourceGroup --tags ""
```

---

## 26. ARM Templates and Bicep

```bash
# Export a resource group as ARM template
az group export --name myResourceGroup > template.json

# Deploy an ARM template
az deployment group create \
    --resource-group myResourceGroup \
    --template-file template.json \
    --parameters @parameters.json

# Validate a template (dry run)
az deployment group validate \
    --resource-group myResourceGroup \
    --template-file template.json

# Deploy a Bicep file
az deployment group create \
    --resource-group myResourceGroup \
    --template-file main.bicep

# What-if (preview changes)
az deployment group what-if \
    --resource-group myResourceGroup \
    --template-file template.json
```

---

## 27. Output Formatting and JMESPath Queries

```bash
# Output formats
az account list --output table    # Human readable
az account list --output json     # JSON (default)
az account list --output tsv      # Tab-separated (for scripting)
az account list --output yaml     # YAML

# Query specific fields
az account show --query "{Name:name, ID:id}" --output table

# Filter arrays
az vm list --query "[?location=='eastus'].name" --output tsv

# Complex queries
az cognitiveservices account list \
    --query "[].{Name:name, Kind:kind, SKU:sku.name, Region:location}" \
    --output table

# Get the first item
az vm list --query "[0].name" --output tsv

# Sort results
az vm list --query "sort_by([].{Name:name, Size:hardwareProfile.vmSize}, &Name)" --output table

# Count items
az resource list --resource-group myResourceGroup --query "length(@)"
```

---

## 28. Tips, Tricks, and Shortcuts

### Interactive Mode

```bash
az interactive
# Auto-complete, inline docs, command history
```

### Parameter Shorthand

Most commands support shortened parameter names:

```bash
# Full form
az group create --name myRG --location eastus

# Short form
az group create -n myRG -l eastus
```

### Common Short Parameters

| Short | Full | Meaning |
|-------|------|---------|
| `-n` | `--name` | Resource name |
| `-g` | `--resource-group` | Resource group |
| `-l` | `--location` | Azure region |
| `-o` | `--output` | Output format |
| `-s` | `--subscription` | Subscription |

### Useful Aliases

```bash
az alias create --name rg --command "group"
az alias create --name ls-rg --command "group list -o table"
az alias create --name ls-vm --command "vm list -o table"
az alias create --name ls-ai --command "cognitiveservices account list -o table"
```

### Run Commands in Parallel (Bash)

```bash
# Delete multiple resource groups at once
for rg in lab1-rg lab2-rg lab3-rg; do
    az group delete --name $rg --yes --no-wait &
done
wait
echo "All resource groups deleted."
```

### Export Credentials to Environment Variables

```bash
# Useful for Python scripts
export AZURE_AI_ENDPOINT=$(az cognitiveservices account show -n myAI -g myRG --query "properties.endpoint" -o tsv)
export AZURE_AI_KEY=$(az cognitiveservices account keys list -n myAI -g myRG --query "key1" -o tsv)
```

---

## 29. Troubleshooting

### "az: command not found"

- **Windows:** Restart terminal. If WinGet install, close/reopen PowerShell.
- **macOS:** `brew link azure-cli` or add to PATH.
- **Linux:** `source ~/.bashrc` or restart terminal.

### "AADSTS50076: Multi-factor authentication required"

```bash
az login --tenant YOUR_TENANT_ID
```

### "The subscription is not registered to use namespace"

```bash
az provider register --namespace Microsoft.CognitiveServices
az provider register --namespace Microsoft.Storage
az provider register --namespace Microsoft.MachineLearningServices
az provider register --namespace Microsoft.Search

# Check registration
az provider show --namespace Microsoft.CognitiveServices --query "registrationState"
```

### "AuthorizationFailed"

Check subscription and permissions:

```bash
az account list -o table
az account set -s "Correct Subscription"
az role assignment list --assignee user@email.com -o table
```

### "Resource already exists"

```bash
# Check for soft-deleted resources
az cognitiveservices account list-deleted -o table

# Purge if needed
az cognitiveservices account purge -n myAI -g myRG -l eastus
```

### "QuotaExceeded"

```bash
# Check current usage
az cognitiveservices account list-usage -n myAI -g myRG -o table

# Try a different region or upgrade SKU
```

### Update Azure CLI

```bash
# Built-in upgrade
az upgrade

# Windows (WinGet)
winget upgrade -e --id Microsoft.AzureCLI

# macOS (Homebrew)
brew upgrade azure-cli

# Linux (apt)
sudo apt-get update && sudo apt-get upgrade azure-cli
```

---

## 30. Quick Reference Card

### Account

| Task | Command |
|------|---------|
| Login | `az login` |
| Show account | `az account show` |
| List subscriptions | `az account list -o table` |
| Set subscription | `az account set -s "Name"` |

### Resources

| Task | Command |
|------|---------|
| Create resource group | `az group create -n myRG -l eastus` |
| List resource groups | `az group list -o table` |
| Delete resource group | `az group delete -n myRG --yes` |
| List resources in group | `az resource list -g myRG -o table` |
| Add lock | `az lock create -n NoDelete -g myRG --lock-type CanNotDelete` |

### AI Services

| Task | Command |
|------|---------|
| Create multi-service | `az cognitiveservices account create -n myAI -g myRG --kind CognitiveServices --sku S0 -l eastus --yes` |
| Create Computer Vision | `az cognitiveservices account create -n myCV -g myRG --kind ComputerVision --sku F0 -l eastus --yes` |
| Create Language | `az cognitiveservices account create -n myLang -g myRG --kind TextAnalytics --sku F0 -l eastus --yes` |
| Create Speech | `az cognitiveservices account create -n mySpeech -g myRG --kind SpeechServices --sku F0 -l eastus --yes` |
| Create Translator | `az cognitiveservices account create -n myTrans -g myRG --kind TextTranslation --sku F0 -l global --yes` |
| Create Face | `az cognitiveservices account create -n myFace -g myRG --kind Face --sku F0 -l eastus --yes` |
| Create Doc Intelligence | `az cognitiveservices account create -n myDoc -g myRG --kind FormRecognizer --sku F0 -l eastus --yes` |
| Create OpenAI | `az cognitiveservices account create -n myOAI -g myRG --kind OpenAI --sku S0 -l eastus --yes` |
| Create Content Safety | `az cognitiveservices account create -n myCS -g myRG --kind ContentSafety --sku F0 -l eastus --yes` |
| Get endpoint | `az cognitiveservices account show -n myAI -g myRG --query "properties.endpoint" -o tsv` |
| Get keys | `az cognitiveservices account keys list -n myAI -g myRG` |
| List all AI services | `az cognitiveservices account list -o table` |

### Infrastructure

| Task | Command |
|------|---------|
| Create VM | `az vm create -g myRG -n myVM --image Ubuntu2204 --size Standard_B1s --generate-ssh-keys` |
| Create storage | `az storage account create -n mysa -g myRG -l eastus --sku Standard_LRS` |
| Create web app | `az webapp create -g myRG -p myPlan -n myApp --runtime "PYTHON:3.11"` |
| Create search | `az search service create -n mySearch -g myRG --sku free -l eastus` |
| Create ML workspace | `az ml workspace create -n myML -g myRG -l eastus` |
| Create Key Vault | `az keyvault create -n myKV -g myRG -l eastus` |

---

## Lab-to-CLI Mapping

| Lab | Azure Services Used | CLI Kind |
|-----|-------------------|----------|
| GLAB 251.1.1 - Create an Azure Resource | Resource Groups, Storage | `az group create`, `az storage account create` |
| GLAB 251.1.2 - Configure Network Access | NSG, VNet | `az network nsg create` |
| GLAB 251.1.3 - Create a Storage Blob | Blob Storage | `az storage blob upload` |
| GLAB 251.2.2 - Configure a Resource Lock | Resource Locks | `az lock create` |
| GLAB 260.2.1 - Automated Machine Learning | ML Workspace | `az ml workspace create` |
| GLAB 261.2.1 - Face Detection | Face API | `--kind Face` |
| GLAB 261.2.2 - OCR | Computer Vision | `--kind ComputerVision` |
| GLAB 261.2.3 - Analyze Images | Computer Vision | `--kind ComputerVision` |
| GLAB 262.1.1 - Text Analysis | Language / Text Analytics | `--kind TextAnalytics` |
| GLAB 262.2.1 - Question Answering | Language | `--kind TextAnalytics` |
| GLAB 262.2.2 - Conversational AI | Language | `--kind TextAnalytics` |
| GLAB 262.3.1 - Speech Capabilities | Speech Services | `--kind SpeechServices` |
| GLAB 262.3.2 - Language Translation | Translator | `--kind TextTranslation` |
| GLAB 263.1.1 - Document Intelligence | Document Intelligence | `--kind FormRecognizer` |
| GLAB 263.2.1 - Azure AI Search | Search Service | `az search service create` |
| GLAB 264.1.1 - Azure AI Foundry | Azure OpenAI | `--kind OpenAI` |
| GLAB 264.1.2 - Content Safety | Content Safety | `--kind ContentSafety` |
| GLAB 264.2.1 - Implement Content Safety | Content Safety | `--kind ContentSafety` |

---

## References

- [Azure CLI Documentation](https://learn.microsoft.com/en-us/cli/azure/)
- [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Azure CLI Command Reference](https://learn.microsoft.com/en-us/cli/azure/reference-index)
- [JMESPath Query Tutorial](https://learn.microsoft.com/en-us/cli/azure/query-azure-cli)
- [Azure Cloud Shell](https://shell.azure.com)
- [Azure AI Services Documentation](https://learn.microsoft.com/en-us/azure/ai-services/)
- [Azure OpenAI Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- [Azure TCO Calculator](https://azure.microsoft.com/en-us/pricing/tco/calculator/)

---

*Last Updated: May 2026*
