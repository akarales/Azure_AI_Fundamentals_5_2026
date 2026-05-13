# Lesson 263.1 - Document Intelligence and Knowledge Mining by Alexandros Karales

## Document Intelligence and Knowledge Mining

## Table of Contents

- What is Document Intelligence?
- Azure AI Document Intelligence
- Prebuilt Models
- Custom Models
- What is Knowledge Mining?
- Azure AI Search
- Indexing and Querying
- AI Enrichment
- Knowledge Check
- Summary

## Learning Objectives

By the end of this lesson, learners will be able to:

- Define document intelligence and describe its role in AI.
- Identify the capabilities of Azure AI Document Intelligence.
- Explain the difference between prebuilt and custom document models.
- Describe knowledge mining and Azure AI Search.
- Explain AI enrichment pipelines and their applications.

---

## Section 1: What is Document Intelligence?

Document Intelligence is the AI capability that extracts structured information from unstructured documents such as invoices, receipts, forms, and contracts. It combines OCR, NLP, and machine learning to understand document layouts and extract key data points.

### Azure AI Document Intelligence

Azure AI Document Intelligence (formerly Form Recognizer) provides:

- **Prebuilt Models:** Ready-to-use models for common document types (invoices, receipts, ID documents, tax forms).
- **Custom Models:** Train your own models on domain-specific documents.
- **Layout Analysis:** Extract text, tables, and structure from documents.
- **Key-Value Pair Extraction:** Identify and extract labeled data from forms.

**Reference:** [Microsoft Learn - AI Information Extraction](https://learn.microsoft.com/en-us/training/paths/ai-extract-information/)

### Prebuilt Models

Azure AI Document Intelligence includes prebuilt models for:
- Invoices
- Receipts
- Business cards
- ID documents (passports, driver's licenses)
- W-2 tax forms
- Health insurance cards

### Custom Models

When prebuilt models do not cover your document type, you can train custom models:
1. Collect sample documents (minimum 5).
2. Label the fields you want to extract.
3. Train the model.
4. Test and evaluate the model.
5. Deploy for production use.

---

## Section 2: What is Knowledge Mining?

Knowledge Mining is the process of extracting insights, relationships, and patterns from large volumes of unstructured data (documents, images, audio, video). It uses AI to enrich raw data and make it searchable.

### Azure AI Search

Azure AI Search (formerly Azure Cognitive Search) is a fully managed search service that enables knowledge mining:

- **Indexing:** Ingest and index data from various sources (Azure Blob Storage, SQL databases, Cosmos DB).
- **AI Enrichment:** Apply AI skills (OCR, entity recognition, key phrase extraction, image analysis) during indexing to extract additional metadata.
- **Querying:** Full-text search, faceted navigation, filtering, and scoring.
- **Semantic Search:** AI-powered search ranking for more relevant results.

**Reference:** [Microsoft Learn - AI Information Extraction](https://learn.microsoft.com/en-us/training/modules/ai-information-extraction/)

### AI Enrichment

AI enrichment pipelines apply cognitive skills to data during the indexing process:
- Extract text from images (OCR)
- Detect language
- Extract key phrases
- Recognize entities
- Generate image descriptions
- Detect sentiment

---

## Knowledge Check

1. What is document intelligence, and what types of documents can it process?
2. What is the difference between prebuilt and custom models in Azure AI Document Intelligence?
3. What is knowledge mining, and how does Azure AI Search support it?
4. What are AI enrichment skills, and how are they applied?

---

## Summary

This lesson covered document intelligence and knowledge mining as key AI capabilities. We explored Azure AI Document Intelligence for extracting structured data from documents, including prebuilt and custom models. We also examined Azure AI Search for knowledge mining, including indexing, AI enrichment, and semantic search.

---

## Related Labs and Activities

### Guided Labs (GLABs)
- [GLAB 263.1.1 - Exploring Document Intelligence with Azure AI](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Exercises/06a-content-understanding.html)
- [GLAB 263.2.1 - Explore Azure AI Search](https://microsoftlearning.github.io/AI-900-AIFundamentals/instructions/05-create-cognitive-search-solution.html)

### Proof of Completion (POCs)
- **POC 263.1.1 - Introduction to AI-powered information extraction - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Introduction to AI-powered Information Extraction](https://learn.microsoft.com/en-us/training/modules/introduction-information-extraction/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 263.1.1 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636445)
- **POC 263.2.1 - AI-powered Information Extraction in Azure - Badge**
  - **Step 1:** Complete the Microsoft Learn module: [Get Started with AI-powered Information Extraction in Azure](https://learn.microsoft.com/en-us/training/modules/get-started-information-extraction/)
  - **Step 2:** Take a screenshot of your earned badge from your Microsoft Learn profile.
  - **Step 3:** Upload your badge screenshot here: [Submit POC 263.2.1 on Canvas](https://perscholas.instructure.com/courses/3268/assignments/636446)

### Microsoft Learn Module Links
- [Introduction to AI-powered Information Extraction](https://learn.microsoft.com/en-us/training/modules/introduction-information-extraction/)
- [Get Started with AI-powered Information Extraction in Azure](https://learn.microsoft.com/en-us/training/modules/get-started-information-extraction/)

### Canvas Links
- [Exit Feedback](https://perscholas.instructure.com/courses/3268/assignments/636487)

---

## Questions?
