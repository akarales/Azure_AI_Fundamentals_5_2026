# **Guided Lab 251.2.2: Configure a Resource Lock**

Version 3.0, May 2026
Created by Alexandros Karales

---

# **Introduction**

In this lab, you will learn how to apply and manage resource locks in Azure. Resource locks are used to protect critical resources from accidental changes or deletions. You will explore how different lock types behave and how they enforce governance and control in cloud environments.

# **Objectives**

* **Identify** the purpose and types of Azure resource locks.
* **Apply** and **adjust** a lock on an Azure storage account.
* **Evaluate** how locks prevent unauthorized modifications or deletions.

# **Instructions**

You are working as a cloud administrator responsible for preventing accidental deletion of key Azure resources. In this exercise, you will create a storage account, apply a resource lock, and test how it restricts actions. You will analyze both Read-only and Delete lock types.

- **Microsoft Learn Lab URL:** [https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/)

You will:

* Create a storage account.
* Apply a resource lock and attempt restricted operations.
* Modify the lock and observe the effect.
* Test delete protection and verify lock enforcement.

Follow the steps in the link above to complete the tasks below:

## Part 1: Configure and Test a Resource Lock

Step 1: Create a Storage Account

1. Use the Azure Portal to create a new storage account.
2. Use any globally unique name.

Step 2: Apply a Read-Only Lock

1. Add a lock named `readOnlyLock` with type **Read-only.**

Step 3: Attempt to Add a Container

1. Try to create a blob container in the locked account.
2. Observe and understand the error due to the read-only lock.

| *\[Paste image here\]* |
| :---- |

Step 4: Modify Lock and Create a Container

1. Change the lock type from **Read-only** to **Delete.**
2. Retry creating the container, it should succeed now.

Step 5: Attempt to Delete the Storage Account (Expect Failure)

1. Attempt to delete the storage account.
2. You should receive an error indicating the operation failed due to a lock.

| *\[Paste image here\]* |
| :---- |

## Part 2: Reflection

1. *What are the functional differences between Read-only and Delete locks?*

| *\[Type answer here\]* |
| :---- |

2. *How do resource locks enhance security and governance in Azure?*

| *\[Type answer here\]* |
| :---- |

3. *Why is it critical to check for locks before modifying or deleting resources?*

| *\[Type answer here\]* |
| :---- |

4. *In what scenarios would you apply a Delete lock instead of a Read-only lock?*

| *\[Type answer here\]* |
| :---- |

---

# **Submission Guidelines:**

* Download this document as a Microsoft Word (.docx) format.

  * Still confused? Refer to [The Lab Process guide](https://docs.google.com/document/d/1NPvgfPqudpqyYux_CNUTxeQ8HjgLXy7wXy59BjFf3lc/edit?usp=sharing).

* Add or paste your screenshots in the section provided below.

* Please upload your lab document with the screenshots.

  * **Prepare Your Document**

    * Paste your screenshot(s) into a Word document.
    * Name your file using this format:
      `Firstname_Lastname_LabName.docx`
      `Example: John_Doe_GLAB251.2.2_ConfigureResourceLock`

* Upload your document to **Canvas** using the **Start** button.
