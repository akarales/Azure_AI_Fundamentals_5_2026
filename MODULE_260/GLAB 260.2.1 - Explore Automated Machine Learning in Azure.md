# **Guided LAB 260.2.1: Explore Automated Machine Learning in Azure**

Version 3.0, May 2026
Created by Alexandros Karales

---

# **Introduction**

In this lab, you will explore **Azure Machine Learning** by training and deploying an automated regression model using historical bicycle rental data. This exercise builds essential skills in model creation, evaluation, and deployment using no-code tools.

# **Objectives**

* Provision an Azure Machine Learning workspace.
* Execute an automated machine learning job using regression.
* Analyze the best-performing model and its metrics.
* Deploy the model as a real-time endpoint.
* Test the deployed model with sample input and interpret results.

# **Instructions**

You are working as a machine learning engineer tasked with building a predictive model to forecast bicycle rentals. You will use Azure Machine Learning Studio to automate model training, identify the best model, and deploy it for real-time testing.

- **Microsoft Learn Lab URL:** [https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/02-module-02.html](https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/02-module-02.html)

You will:

* Create a Machine Learning workspace and open Azure ML Studio.
* Configure and run an Automated ML job using the bike rental dataset.
* Review the best model's performance metrics.
* Deploy the model and test it using sample input.

Follow the steps in the link above to complete the tasks below:

## Part 1: Explore Automated Machine Learning

Step 1: Launch Azure Machine Learning Studio

1. Create an Azure Machine Learning workspace via the Azure portal.
2. Launch Azure Machine Learning Studio to access the workspace.

| *\[Paste image here\]* |
| :---- |

Step 2: Configure an Automated ML Job

1. In ML Studio, configure a new Automated ML job.
2. Use the bike rental dataset.
3. Select **Regression** as the task type.

Step 3: Review the Best Model

1. After the job completes, review the best model and its evaluation metrics (e.g., RMSE, MAE).
2. Explore the residuals and predicted vs. true values charts.

| *\[Paste image here\]* |
| :---- |

Step 4: Deploy the Model

1. Deploy the best model to a real-time endpoint.
2. Note the endpoint URL and key for testing.

Step 5: Test the Deployed Model

1. Use the test pane or REST API to send a sample input and observe the prediction output.

| *\[Paste image here\]* |
| :---- |

## Part 2: Reflection

1. *What metric did you find most useful for evaluating the regression model?*

| *\[Type answer here\]* |
| :---- |

2. *How does Automated ML simplify the model development process?*

| *\[Type answer here\]* |
| :---- |

3. *What are the benefits of deploying a model to a real-time endpoint?*

| *\[Type answer here\]* |
| :---- |

4. *What challenges did you encounter during the lab, and how did you resolve them?*

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
      `Example: John_Doe_GLAB260.2.1_ExploreAutoML`

* Upload your document to **Canvas** using the **Start** button.
