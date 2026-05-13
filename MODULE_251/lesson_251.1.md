# Lesson 251.1 - Introduction to Cloud Computing by Alexandros Karales

## Introduction to Cloud Computing

## Table of Contents

- Fundamentals of Cloud Computing
- Introduction to Cloud Computing
- Key Characteristics of Cloud Computing
- Shared Responsibility Model
- Benefits of Cloud Computing
- Cloud Deployment Models
- Cloud Computing Deployment Models
- Overview of Private Cloud
- Overview of Public Cloud
- Overview of Hybrid Cloud
- Overview of Community Cloud
- Overview of CapEx and OpEx
- CapEx vs. OpEx
- Azure Fundamentals
- Introduction to Azure
- What Does Azure Offer
- Core Architectural Components in Azure
- Azure Compute and Networking Services
- Azure Storage Services
- Azure Identity, Access, and Security Services
- Azure Management and Governance Services

## Learning Objectives

By the end of this lesson, learners will be able to:

- Define the concept of cloud computing and illustrate its core characteristics.
- Describe the shared responsibility model and differentiate roles between cloud providers and customers.
- Compare various cloud deployment models, including public, private, and hybrid approaches.
- Identify and analyze the key benefits of adopting cloud computing.
- Explain the consumption-based pricing model used in cloud services.

---

## Section 1: Fundamentals of Cloud Computing

### Introduction to Cloud Computing

Describe cloud computing as a way to deliver services like servers, storage, databases, networking, software, analytics, and intelligence through the internet (called "the cloud"). This helps businesses achieve faster innovation, flexible use of resources, and lower costs.

Explain how the term "cloud" is used as a metaphor for a large, flexible computing system that hides the complex setup of hardware and software behind the scenes.

Interpret the meaning of "five nines" availability (99.999%), which means the system is highly reliable, allowing for only about five minutes of downtime in a whole year. This level of availability is usually required for critical systems where even small failures can cause big problems.

**Reference:** [Microsoft Learn - Describe Cloud Computing](https://learn.microsoft.com/en-us/training/modules/describe-cloud-computing/)

### Key Characteristics of Cloud Computing (1 of 2)

- **On-Demand Access:** Cloud services let users pay only for what they use, giving them flexibility and cost savings. Customers can quickly access resources on their own, without needing help from a salesperson or IT support.
- **Elasticity:** Cloud systems can automatically adjust resources, increasing or decreasing based on the workload. This means users always have the right amount of power to handle their tasks, helping to balance performance and cost.
- **Measured Service:** Cloud providers use usage-based billing, so users are charged only for what they use over time. In private clouds, IT teams can use chargebacks to track and assign costs to different departments based on how much they use.
- **Serverless Computing:** Serverless Computing allows developers to write and deploy code without managing servers. The cloud provider takes care of server setup, scaling, and maintenance, so teams can focus only on application logic.
- **Network-Based Access:** Cloud resources are accessible through the internet, allowing users to connect to services anytime and from anywhere. This supports remote collaboration and enables global scalability.
- **Shared Pool of Resources:** Cloud computing uses a multi-tenant model, where computing resources are pooled together and automatically allocated to different users. Unlike traditional IT environments with siloed infrastructure, this approach improves efficiency, scalability, and resource utilization.

### Key Characteristics of Cloud Computing (2 of 2)

### Shared Responsibility Model (1 of 2)

Analyze the shared responsibility model in cloud computing. Cloud providers are responsible for the security of the cloud, which includes the physical infrastructure, hosts, network, and data centers. Customers are responsible for security in the cloud, including data, user identities, applications, and access control.

**Reference:** [Microsoft Learn - Describe the Shared Responsibility Model](https://learn.microsoft.com/en-us/training/modules/describe-cloud-compute/4-describe-shared-responsibility-model)

### Shared Responsibility Model (2 of 2)

Evaluate how the distribution of security responsibilities changes based on the cloud service model being used: IaaS, PaaS, or SaaS.

- **IaaS:** The customer manages most responsibilities, including virtual machines, storage, and networking.
- **PaaS:** The customer manages fewer tasks, mainly focusing on application settings and data.
- **SaaS:** The cloud provider handles most responsibilities; the customer is responsible for data and user access.

### Benefits of Cloud Computing (1 of 3)

Cloud computing offers a range of powerful benefits that help individuals and organizations work smarter, faster, and more cost-effectively. Let's break down the key advantages:

- **Availability:** Cloud services maintain high availability, often referred to as "uptime." Cloud platforms are designed to stay online even during system failures or maintenance. For example, Azure provides data redundancy across global regions to ensure service continuity.
- **Accessibility:** Cloud services can be accessed anytime and from anywhere with an internet connection. This supports remote work, global collaboration, and real-time teamwork.
- **Scalability:** Cloud computing provides automatic scalability. Resources can scale up when demand increases (e.g., needing more storage or computing power) and scale down when demand drops (e.g., after completing a project), helping to control costs efficiently.

**Reference:** [Horizontal Vs. Vertical Scaling: Which Should You Choose?](https://www.cloudzero.com/blog/horizontal-vs-vertical-scaling)

---

## Section 2: Azure Fundamentals

### Introduction to Azure

Microsoft Azure is a comprehensive cloud computing platform that provides a wide range of services including compute, storage, networking, databases, analytics, AI, and more. Azure supports both IaaS and PaaS models, enabling organizations to build, deploy, and manage applications through Microsoft's global network of data centers.

**Reference:** [Microsoft Learn - Describe Core Architectural Components of Azure](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/)

### What Does Azure Offer

- Virtual Machines (IaaS)
- App Services (PaaS)
- Azure SQL Database
- Azure Blob Storage
- Azure Functions (Serverless)
- Azure Kubernetes Service (AKS)
- Azure AI Services (including Azure OpenAI)
- Azure DevOps

### Core Architectural Components in Azure

- **Regions and Availability Zones:** Azure operates data centers across 60+ regions worldwide. Availability Zones provide fault isolation within a region.
- **Resource Groups:** Logical containers for grouping related Azure resources.
- **Subscriptions:** Units of management, billing, and scale in Azure.
- **Management Groups:** Hierarchical containers for organizing subscriptions.

### Azure Compute and Networking Services

**Reference:** [Microsoft Learn - Describe Azure Compute and Networking Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-networking-services/)

### Azure Storage Services

**Reference:** [Microsoft Learn - Describe Azure Storage Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-storage-services/)

### Azure Identity, Access, and Security Services

Overview of Azure Active Directory (Microsoft Entra ID), Role-Based Access Control (RBAC), and Azure security tools.

### Azure Management and Governance Services

**Reference:** [Microsoft Learn - Describe Features and Tools for Azure Governance and Compliance](https://learn.microsoft.com/en-us/training/modules/describe-features-tools-azure-for-governance-compliance/)

---

## Knowledge Check

1. What is cloud computing, and how does it differ from traditional on-premises infrastructure?
2. Explain the shared responsibility model. How does it change across IaaS, PaaS, and SaaS?
3. What are the key benefits of cloud computing for organizations?
4. What is the difference between vertical and horizontal scaling?
5. Describe the role of Azure Resource Groups.

---

## Summary

This lesson introduced the fundamentals of cloud computing, including core characteristics such as on-demand access, elasticity, measured services, and serverless computing. We explored the shared responsibility model and how security duties shift between the cloud provider and customer depending on the service model (IaaS, PaaS, SaaS). We also covered the key benefits of cloud adoption and introduced Microsoft Azure's core architectural components and services.

---

## Related Labs and Activities

### Guided Labs (GLABs)
- [GLAB 251.1.1 - Create an Azure Resource](https://learn.microsoft.com/en-us/training/modules/intro-to-azure-virtual-machines/)
- [GLAB 251.1.2 - Configure Network Access](https://learn.microsoft.com/en-us/training/modules/configure-network-security-groups/)
- [GLAB 251.1.3 - Create a Storage Blob](https://learn.microsoft.com/en-us/training/modules/configure-blob-storage/)

### Microsoft Learn Module Links
- [Describe Core Architectural Components of Azure](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/)
- [Describe Azure Networking Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-networking-services/)
- [Describe Azure Storage Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-storage-services/)

### Canvas Links
- [Module 251 Page](https://perscholas.instructure.com/courses/3268/pages/module-251)
- [KBA](https://perscholas.instructure.com/courses/3268/assignments/636429)
- [Exit Feedback](https://perscholas.instructure.com/courses/3268/assignments/636431)

---

## Questions?
