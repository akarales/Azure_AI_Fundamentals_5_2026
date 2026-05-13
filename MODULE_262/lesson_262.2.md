# Lesson 262.2 - Question Answering and Conversational Language by Alexandros Karales

## Question Answering and Conversational AI

## Table of Contents

- Question Answering in Azure
- Building a Knowledge Base
- Conversational Language Understanding (CLU)
- Intent and Entity Recognition
- Building Conversational AI with Azure
- Knowledge Check
- Summary

## Learning Objectives

By the end of this lesson, learners will be able to:

- Describe Azure AI Language question answering capabilities.
- Explain how knowledge bases are built and used for question answering.
- Define Conversational Language Understanding (CLU) and its components.
- Distinguish between intents and entities in conversational AI.

---

## Section 1: Question Answering in Azure

Question answering is an NLP capability that allows you to create a knowledge base from existing content (FAQs, documents, web pages) and provide automated answers to user questions.

### Building a Knowledge Base

1. **Source Content:** Import FAQs, documents, or URLs.
2. **Question-Answer Pairs:** The service extracts or you manually define Q&A pairs.
3. **Training:** The model learns to match user questions to the best answers.
4. **Testing:** Test the knowledge base with sample questions.
5. **Deployment:** Deploy as a web service and integrate with chatbots.

---

## Section 2: Conversational Language Understanding (CLU)

CLU (formerly LUIS) enables you to build custom language understanding models for conversational applications.

### Intent and Entity Recognition

- **Intent:** The purpose or goal behind a user's input (e.g., "BookFlight", "GetWeather").
- **Entity:** A specific piece of information within the input (e.g., "New York", "tomorrow").

### Building a CLU Model

1. Define intents that represent user goals.
2. Define entities that represent key data points.
3. Provide example utterances for each intent.
4. Train and evaluate the model.
5. Deploy and integrate with applications.

---

## Section 3: Building Conversational AI with Azure

Azure provides several tools for building conversational AI:

- **Azure AI Language (CLU):** Custom intent and entity recognition.
- **Azure AI Language (Question Answering):** FAQ-based chatbots.
- **Azure Bot Service:** Framework for building and deploying bots.
- **Power Virtual Agents:** Low-code bot building platform.

**Reference:** [Microsoft Learn - Build a Language Understanding Model](https://learn.microsoft.com/en-us/training/modules/build-language-understanding-model/)

---

## Knowledge Check

1. What is question answering, and how is a knowledge base created?
2. What is the difference between an intent and an entity in CLU?
3. How does CLU differ from general text analytics?
4. What Azure services can be used to build a chatbot?

---

## Summary

This lesson covered question answering and conversational language understanding in Azure. We explored how to build knowledge bases for automated Q&A, how CLU enables custom intent and entity recognition, and the Azure services available for building conversational AI applications.

---

## Related Labs and Activities

### Guided Labs (GLABs)
- [GLAB 262.2.1 - Explore Azure AI Language - Question Answering](https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/04d-create-a-bot.html)
- [GLAB 262.2.2 - Conversational AI with Azure Language Services](https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/04c-conversational-language-understanding.html)

### Proof of Completion (POCs)
- **POC 262.2.1 - Natural Language Processing in Azure - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Build a Language Understanding Model](https://learn.microsoft.com/en-us/training/modules/build-language-understanding-model/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 262.2.1 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636443)

### Microsoft Learn Module Links
- [Build a Language Understanding Model](https://learn.microsoft.com/en-us/training/modules/build-language-understanding-model/)

### Canvas Links
- [Exit Feedback](https://perscholas.instructure.com/courses/3268/assignments/636486)

---

## Questions?
