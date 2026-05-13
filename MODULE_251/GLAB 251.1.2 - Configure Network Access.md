# **Guided Lab 251.1.2: Configure Network Access**

Version 3.0, May 2026
Created by Alexandros Karales

---

# **Introduction**

This lab enables learners to provision an **Azure virtual machine** (VM), configure network access rules using Network Security Groups (NSGs), and validate the VM's external accessibility using its public IP. Learners will perform the tasks using the Azure Portal interface and Microsoft Learn documentation.

# **Objectives**

* Deploy a virtual machine with network access settings.
* Design and apply inbound security rules using a Network Security Group (NSG).
* Verify external connectivity through a public IP address.
* Assess the impact of network security configurations on accessibility.

# **Instructions**

You are working as a cloud administrator tasked with deploying a Windows Server VM in Azure and configuring it to allow HTTP (port 80) access. You must create the VM, modify the network access configuration using an NSG, and test the configuration using the public IP address.

- **Microsoft Learn Lab URL:** [https://learn.microsoft.com/en-us/training/modules/configure-network-security-groups/](https://learn.microsoft.com/en-us/training/modules/configure-network-security-groups/)

You will:

* Create a Windows virtual machine in Azure
* Add an inbound security rule to allow HTTP traffic
* Use the public IP address to confirm network access

Follow the steps in the link above to complete the tasks below:

## Part 1: Configure Network Access

Step 1: Create a Virtual Machine with Network Access Settings

1. Use the Azure portal to deploy a virtual machine with default networking settings and HTTP/RDP access enabled.

| *\[Paste image here\]* |
| :---- |

Step 2: Configure Network Security Group (NSG)

1. Navigate to the VM's networking settings and modify or add an inbound security rule to allow HTTP traffic on port 80.

Step 3: Verify Network Access Using Public IP

1. Use the VM's public IP address to test browser access over HTTP. Confirm that access is successfully allowed.

| *\[Paste image here\]* |
| :---- |

## Part 2: Reflection

1. *What are the potential risks of misconfiguring NSG rules?*

| *\[Type answer here\]* |
| :---- |

2. *How does public IP access help in testing and troubleshooting?*

| *\[Type answer here\]* |
| :---- |

3. *Why is it important to limit open ports on a VM?*

| *\[Type answer here\]* |
| :---- |

4. *What did you learn about the relationship between VMs and NSGs in Azure?*

| *\[Type answer here\]* |
| :---- |

---

# **Submission Guidelines:**

* Download this document in Microsoft Word (.docx) format.

  * Still confused? Refer to [The Lab Process guide](https://docs.google.com/document/d/1NPvgfPqudpqyYux_CNUTxeQ8HjgLXy7wXy59BjFf3lc/edit?usp=sharing).

* Add or paste your screenshots in the section provided below.

* Please upload your lab document with the screenshots.

  * **Prepare Your Document**

    * Paste your screenshot(s) into a Word document.
    * Name your file using this format:
      `Firstname_Lastname_LabName.docx`
      `Example: John_Robin_GLAB251.1.2_ConfigureNetworkAccess`

* Upload your document to **Canvas** using the **Start** button.
