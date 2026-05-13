# Lesson 260.2 - Fundamentals of Machine Learning by Alexandros Karales

## Fundamentals of Machine Learning

## Table of Contents

- What is Machine Learning?
- Types of Machine Learning
- Supervised Learning
  - Regression
  - Classification
- Unsupervised Learning
  - Clustering
- Deep Learning and Neural Networks
- The Transformer Architecture
- Azure Machine Learning
- Knowledge Check
- Summary

## Learning Objectives

By the end of this lesson, learners will be able to:

- Define machine learning and differentiate it from traditional programming.
- Identify and describe the main types of machine learning: supervised, unsupervised, and deep learning.
- Explain regression, classification, and clustering scenarios.
- Describe features of deep learning techniques and the Transformer architecture.
- Describe Azure Machine Learning capabilities.

---

## Section 1: What is Machine Learning?

Machine Learning (ML) is a subset of AI that enables systems to learn from data and improve over time without being explicitly programmed. Instead of writing rules to solve a problem, you provide the machine with data and let it discover patterns.

### How Machine Learning Works

1. **Data Collection:** Gather relevant data for the problem.
2. **Feature Engineering:** Identify the most relevant attributes (features) and labels.
3. **Model Training:** Use algorithms to learn patterns from the data.
4. **Model Evaluation:** Test the model's accuracy and performance.
5. **Deployment:** Deploy the model to make predictions on new data.

---

## Section 2: Types of Machine Learning

### Supervised Learning

In supervised learning, the model is trained on labeled data, meaning each training example has a known output (label).

#### Regression

Regression models predict a continuous numeric value. Examples:
- Predicting house prices based on features like size, location, and age.
- Forecasting daily sales revenue based on historical data.

#### Classification

Classification models predict a categorical label. Examples:
- Determining whether an email is spam or not spam.
- Identifying whether a patient has a disease based on symptoms.

### Unsupervised Learning

In unsupervised learning, the model works with unlabeled data and must find patterns on its own.

#### Clustering

Clustering groups similar data points together. Examples:
- Customer segmentation for marketing.
- Grouping similar news articles.

---

## Section 3: Deep Learning and Neural Networks

Deep learning uses artificial neural networks with many layers (hence "deep") to learn complex patterns from data.

- **Neural Networks:** Inspired by the human brain, consisting of interconnected nodes (neurons) organized in layers.
- **Convolutional Neural Networks (CNNs):** Specialized for image processing and computer vision tasks.
- **Recurrent Neural Networks (RNNs):** Designed for sequential data like time series and text.

### The Transformer Architecture

Transformers are a type of neural network architecture that has revolutionized NLP and generative AI. Key features:

- **Self-Attention Mechanism:** Allows the model to weigh the importance of different parts of the input.
- **Parallelization:** Unlike RNNs, transformers can process all tokens simultaneously.
- **Foundation for LLMs:** Models like GPT-4 and BERT are built on transformer architecture.

---

## Section 4: Azure Machine Learning

Azure Machine Learning is a cloud-based platform for building, training, and deploying ML models.

### Key Capabilities

- **Automated Machine Learning (AutoML):** Automatically selects the best algorithm and hyperparameters.
- **Designer:** A drag-and-drop interface for building ML pipelines.
- **Notebooks:** Integrated Jupyter notebooks for code-first ML development.
- **Model Registry:** Track, version, and manage models.
- **Endpoints:** Deploy models as web services for real-time or batch inference.

**Reference:** [Microsoft Learn - Introduction to Machine Learning Concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)

---

## Knowledge Check

1. What is the difference between supervised and unsupervised learning?
2. Explain the difference between regression and classification.
3. What is a neural network, and how does deep learning differ from traditional ML?
4. What is the Transformer architecture, and why is it important?
5. What capabilities does Azure Machine Learning provide?

---

## Summary

In this lesson, we explored the fundamentals of machine learning, including how it differs from traditional programming by allowing systems to learn from data. We covered the main types of ML, including supervised learning (regression and classification), unsupervised learning (clustering), and deep learning with neural networks. We also introduced the Transformer architecture, which underpins modern large language models. Finally, we explored Azure Machine Learning's capabilities for building, training, and deploying models in the cloud.

---

## Related Labs and Activities

### Guided Labs (GLABs)
- [GLAB 260.2.1 - Explore Automated Machine Learning in Azure](https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/02-module-02.html)

### Proof of Completion (POCs)
- **POC 260.2.1 - Introduction to Machine Learning - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Introduction to Machine Learning Concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 260.2.1 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636439)
- **POC 260.2.2 - Machine Learning In Azure - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Introduction to Machine Learning Concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 260.2.2 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636440)

### Microsoft Learn Module Links
- [Introduction to Machine Learning Concepts](https://learn.microsoft.com/en-us/training/modules/fundamentals-machine-learning/)

### Canvas Links
- [Exit Feedback](https://perscholas.instructure.com/courses/3268/assignments/636484)

---

## Questions?
