# Lesson 264.1 - Introduction to Generative AI by Alexandros Karales

## Introduction to Generative AI

## Table of Contents

- What is Generative AI?
- How Generative AI Works
- Large Language Models (LLMs)
- Foundation Models
- Generative AI Applications
- Responsible Generative AI
- Azure OpenAI Service
- Azure AI Foundry
- Content Safety
- Knowledge Check
- Summary

## Learning Objectives

By the end of this lesson, learners will be able to:

- Define generative AI and explain how it differs from traditional AI.
- Describe the role of large language models (LLMs) and foundation models.
- Identify common generative AI applications.
- Explain the responsible AI considerations specific to generative AI.
- Describe Azure OpenAI Service and Azure AI Foundry capabilities.

---

## Section 1: What is Generative AI?

Generative AI is a category of artificial intelligence that can create new content, including text, images, code, audio, and video. Unlike traditional AI models that classify or predict based on existing data, generative AI produces original outputs based on learned patterns.

### How Generative AI Works

Generative AI models are trained on vast datasets to learn patterns, relationships, and structures in data. When given a prompt (input), the model generates a response by predicting the most likely continuation based on its training.

Key concepts:
- **Training Data:** The large corpus of text, images, or other data used to train the model.
- **Prompts:** User inputs that guide the model's output.
- **Tokens:** The basic units of text that the model processes (words, subwords, or characters).
- **Temperature:** A parameter that controls the randomness/creativity of the output.

### Large Language Models (LLMs)

LLMs are a type of generative AI model trained specifically on text data. They can:
- Generate human-like text
- Answer questions
- Summarize documents
- Translate languages
- Write and explain code

Examples: GPT-4, GPT-4o, Claude, Llama, Gemini.

### Foundation Models

Foundation models are large, pre-trained models that can be fine-tuned for specific tasks. They serve as a "foundation" for building specialized AI applications.

---

## Section 2: Generative AI Applications

- **Content Creation:** Writing articles, marketing copy, social media posts.
- **Code Generation:** Writing, debugging, and explaining code (e.g., GitHub Copilot).
- **Image Generation:** Creating images from text descriptions (e.g., DALL-E).
- **Chatbots and Assistants:** Conversational AI for customer support, education, and more.
- **Data Analysis:** Summarizing data, generating reports, and answering questions about datasets.

---

## Section 3: Responsible Generative AI

Generative AI introduces unique challenges for responsible AI:

- **Hallucinations:** Models may generate plausible-sounding but incorrect information.
- **Bias:** Training data biases can be reflected in model outputs.
- **Misinformation:** Generated content could be used to create misleading information.
- **Copyright:** Questions about ownership of AI-generated content.
- **Content Safety:** Need to filter harmful, offensive, or inappropriate content.

### Mitigation Strategies

- Use content filters and safety systems.
- Provide clear disclaimers that content is AI-generated.
- Implement human review processes.
- Use grounding techniques (RAG) to reduce hallucinations.

---

## Section 4: Azure OpenAI Service

Azure OpenAI Service provides access to OpenAI's powerful language models (GPT-4, GPT-4o, DALL-E, Whisper) through Azure's secure, enterprise-grade infrastructure.

### Key Features

- **Chat Completions:** Generate conversational responses.
- **Text Completions:** Generate text based on prompts.
- **Image Generation:** Create images from text descriptions.
- **Code Generation:** Write and explain code.
- **Content Filtering:** Built-in safety systems to filter harmful content.
- **Enterprise Security:** Azure Active Directory, RBAC, private endpoints.

**Reference:** [Microsoft Learn - Introduction to Generative AI and Agents](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)

### Azure AI Foundry

Azure AI Foundry (formerly Azure AI Studio) is a unified platform for building, evaluating, and deploying generative AI applications:

- **Prompt Flow:** Build and test prompt-based workflows.
- **Model Catalog:** Access and deploy models from Azure OpenAI, Meta, Mistral, and more.
- **Evaluation:** Tools for evaluating model quality and safety.
- **Deployment:** Deploy models as managed endpoints.

**Reference:** [Microsoft Learn - Explore Azure AI Foundry](https://learn.microsoft.com/en-us/training/modules/explore-azure-ai-foundry-portal/)

### Content Safety

Azure AI Content Safety provides tools to detect and filter harmful content in text and images:

- **Text Moderation:** Detect hate speech, violence, sexual content, and self-harm.
- **Image Moderation:** Detect inappropriate images.
- **Prompt Shields:** Protect against prompt injection attacks.

**Reference:** [Microsoft Learn - Implement Content Safety with Azure AI Services](https://learn.microsoft.com/en-us/training/modules/moderate-content-detect-harm-azure-ai-content-safety/)

---

## Knowledge Check

1. What is generative AI, and how does it differ from traditional AI?
2. What are large language models, and what can they do?
3. What are the main responsible AI concerns with generative AI?
4. What capabilities does Azure OpenAI Service provide?
5. What is Azure AI Foundry, and how does it support generative AI development?

---

## Summary

This lesson introduced generative AI as a transformative AI capability that can create new content including text, images, code, and more. We explored how LLMs work, common generative AI applications, and the unique responsible AI challenges they present. We also covered Azure OpenAI Service, Azure AI Foundry, and Azure AI Content Safety as key tools for building and deploying generative AI solutions.

---

## Related Labs and Activities

### Guided Labs (GLABs)
- [GLAB 264.1.1 - Explore Azure AI Foundry](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Exercises/02a-generative-ai.html)
- [GLAB 264.1.2 - Azure AI Content Safety](https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/06-explore-content-safety.html)
- [GLAB 264.2.1 - Implement Content Safety with Azure AI Services](https://microsoftlearning.github.io/mslearn-ai-services/Instructions/Exercises/05-implement-content-safety.html)

### Proof of Completion (POCs)
- **POC 264.1.1 - Introduction to generative AI concepts - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Fundamentals of Generative AI](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 264.1.1 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636447)
- **POC 264.2.1 - Get Started with Generative AI in Azure - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Get Started with Generative AI and Agents](https://learn.microsoft.com/en-us/training/modules/get-started-with-generative-ai-and-agents/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 264.2.1 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636448)

### Microsoft Learn Module Links
- [Fundamentals of Generative AI](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)
- [Get Started with Generative AI and Agents](https://learn.microsoft.com/en-us/training/modules/get-started-with-generative-ai-and-agents/)
- [Implement Content Safety with Azure AI Services](https://learn.microsoft.com/en-us/training/modules/moderate-content-detect-harm-azure-ai-content-safety/)

### Canvas Links
- [Exit Feedback](https://perscholas.instructure.com/courses/3268/assignments/636488)

---

## Questions?
