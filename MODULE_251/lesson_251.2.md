# Lesson 251.2 - Cloud Service Types and Azure Cost Management by Alexandros Karales

## Cloud Service Types

## Table of Contents

- Infrastructure as a Service (IaaS)
  - Overview of Infrastructure as a Service
  - Core Components of IaaS
  - Shared Responsibility in IaaS
  - Examples and Scenarios
- Platform as a Service (PaaS)
  - Overview of Platform as a Service
  - Shared Responsibility in PaaS
- Software as a Service (SaaS)
  - Overview of Software as a Service
  - Examples and Scenarios
- Comparing IaaS, PaaS, and SaaS
- Comparing Deployment Models
- Azure Cost Management
  - Cost Management in Azure
  - Overview of Azure Pricing Calculator
  - Azure Total Cost of Ownership Calculator

## Learning Objectives

By the end of this lesson, learners will be able to:

- Define the three main cloud service types: Infrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS).
- Identify common examples within each model:
  - **IaaS:** Virtual machines, storage, and networking (e.g., Azure Virtual Machines).
  - **PaaS:** Application hosting and development tools (e.g., Azure App Service).
  - **SaaS:** Ready-to-use applications (e.g., Microsoft 365, Outlook).
- Differentiate which responsibilities are managed by the cloud provider and which remain with the customer under each model.
- Determine which cloud service model is best suited for specific scenarios based on control, flexibility, and ease of use.

---

## Section 1: Infrastructure as a Service

### Overview of Infrastructure as a Service

IaaS provides the most control over cloud resources. The cloud provider manages the physical hardware, network connectivity, and physical security. The customer is responsible for everything else: operating system installation, configuration, patching, network configuration, database and storage configuration, etc.

### Core Components of IaaS

- Virtual Machines
- Virtual Networks
- Storage Accounts
- Load Balancers

### Shared Responsibility in IaaS

In IaaS, the customer manages the most responsibilities compared to PaaS and SaaS. The cloud provider ensures the physical infrastructure is maintained and operational.

### Examples and Scenarios

- Migrating existing on-premises workloads to the cloud
- Test and development environments
- Storage, backup, and recovery solutions

---

## Section 2: Platform as a Service

### Overview of Platform as a Service

PaaS provides a complete development and deployment environment in the cloud. The cloud provider manages the infrastructure (servers, storage, networking) as well as the middleware, development tools, and database management services.

### Shared Responsibility in PaaS

The customer manages fewer tasks than IaaS, mainly focusing on application settings, data, and user access.

---

## Section 3: Software as a Service

### Overview of Software as a Service

SaaS provides a fully functional application that runs and is managed by the cloud provider. Users simply use the application through a web browser or app.

### Examples and Scenarios

- Microsoft 365 (Word, Excel, Teams)
- Salesforce
- Gmail

---

## Section 4: Comparing IaaS, PaaS, and SaaS

| Feature | IaaS | PaaS | SaaS |
|---------|------|------|------|
| Control | Most | Moderate | Least |
| Management | Customer manages OS, apps | Customer manages apps, data | Provider manages everything |
| Use Case | Lift-and-shift migration | App development | End-user productivity |
| Example | Azure VMs | Azure App Service | Microsoft 365 |

---

## Section 5: Azure Cost Management

### Cost Management in Azure

Azure provides several tools to help estimate, monitor, and optimize cloud spending.

### Overview of Azure Pricing Calculator

The Azure Pricing Calculator helps you estimate the cost of Azure products and services before deployment.

**Reference:** [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

### Azure Total Cost of Ownership Calculator

The TCO Calculator helps compare the cost of running on-premises infrastructure vs. migrating to Azure over a defined time period.

**Reference:** [Microsoft Learn - Describe Cost Management in Azure](https://learn.microsoft.com/en-us/training/modules/describe-cost-management-azure/)

---

## Knowledge Check

1. What are the three main cloud service types?
2. How does the shared responsibility model differ across IaaS, PaaS, and SaaS?
3. When would you choose PaaS over IaaS?
4. What tools does Azure provide for cost estimation and management?

---

## Related Labs and Activities

### Guided Labs (GLABs)
- [GLAB 251.2.1 - Estimate Workload Costs by Using the Pricing Calculator](https://learn.microsoft.com/en-us/training/modules/analyze-costs-create-budgets-azure-cost-management/)
- [GLAB 251.2.2 - Configure a Resource Lock](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/)
- [GLAB 251.2.3 - Compare Workload Costs Using the TCO Calculator](https://learn.microsoft.com/en-us/training/modules/analyze-costs-create-budgets-azure-cost-management/)

### Microsoft Learn Module Links
- [Describe Cost Management in Azure](https://learn.microsoft.com/en-us/training/modules/describe-cost-management-azure/)
- [Describe Features and Tools for Governance and Compliance](https://learn.microsoft.com/en-us/training/modules/describe-features-tools-azure-for-governance-compliance/)

### Other Resources
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

### Canvas Links
- [Module 251 Page](https://perscholas.instructure.com/courses/3268/pages/module-251)
- [KBA](https://perscholas.instructure.com/courses/3268/assignments/636429)
- [Exit Feedback](https://perscholas.instructure.com/courses/3268/assignments/636431)

---

## Questions?
