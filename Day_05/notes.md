# Retrieval-Augmented Generation (RAG)

## Overview

Retrieval-Augmented Generation (RAG) is a technique that enhances Large Language Models (LLMs) by allowing them to retrieve relevant information from external knowledge sources before generating a response.

Instead of relying only on the knowledge learned during training, RAG gives the AI access to real-time, private, or domain-specific data.

> **Think of RAG as giving an AI an "open-book exam" instead of a closed-book exam.**

---

# Where RAG Fits in AI

```
Artificial Intelligence (AI)
│
├── Machine Learning (ML)
│
├── Deep Learning (DL)
│
├── Natural Language Processing (NLP)
│
├── Large Language Models (LLMs)
│
├── Generative AI
│
└── Retrieval-Augmented Generation (RAG)
```

RAG is **not a separate AI model**.

It is an **architecture** used alongside LLMs to improve their responses.

---

# Why Do We Need RAG?

LLMs have several limitations:

- Knowledge cut-off date
- Cannot access private company data
- May generate incorrect information (hallucinations)
- Expensive to retrain every time new data is added

RAG solves these problems by retrieving relevant information before generating an answer.

---

# Benefits of RAG

- Access to real-time information
- Reduces hallucinations
- Uses private company documents securely
- More cost-effective than retraining or fine-tuning
- Produces more accurate and grounded responses

---

# How RAG Works

The RAG workflow consists of two main pipelines:

1. **Ingestion Pipeline**
2. **Retrieval Pipeline**

---

# 1. Ingestion Pipeline

Before users can ask questions, the documents must be prepared.

### Step 1 - Collect Data

Example sources:

- PDFs
- Word documents
- CSV files
- Company documentation
- Websites
- Databases

↓

### Step 2 - Chunking

Large documents are split into smaller pieces called **chunks**.

Example

```
100-page PDF

↓

500 smaller chunks
```

Chunking improves search accuracy.

---

### Step 3 - Create Embeddings

Each chunk is converted into a **vector embedding**.

An embedding is a numerical representation of the meaning of text.

Instead of storing words, the AI stores their semantic meaning.

---

### Step 4 - Store in Vector Database

The embeddings are stored inside a **Vector Database**.

Popular Vector Databases:

- ChromaDB
- Pinecone
- Weaviate
- Milvus
- Qdrant

---

# 2. Retrieval Pipeline

When a user asks a question:

### Step 1

User enters a query.

↓

### Step 2

The query is converted into an embedding.

↓

### Step 3

Semantic Search finds the most relevant document chunks.

↓

### Step 4

The retrieved chunks are added to the prompt.

↓

### Step 5

The LLM generates a response using both:

- User prompt
- Retrieved context

---

# Complete RAG Pipeline

```
Documents
     │
     ▼
Chunking
     │
     ▼
Embeddings
     │
     ▼
Vector Database
     │
────────────────────────────
     │
User Question
     │
     ▼
Embedding
     │
     ▼
Semantic Search
     │
     ▼
Relevant Context
     │
     ▼
LLM
     │
     ▼
Final Response
```

---

# What are Embeddings?

Embeddings convert text into numbers while preserving meaning.

Example

```
Dog
Cat
Puppy
```

These words will have vectors that are close together because they are semantically related.

This allows AI to search by **meaning**, not just exact words.

---

# What is a Vector Database?

A Vector Database stores embeddings instead of plain text.

Instead of asking:

> "Does this document contain the exact word?"

it asks:

> "Which documents are most similar in meaning?"

Examples

- Pinecone
- ChromaDB
- Weaviate
- Milvus
- Qdrant

---

# Keyword Search vs Vector Search

## Keyword Search

Searches for exact words.

Example

Search:

```
Car
```

Finds:

```
Car
```

Does **not** find:

- Automobile
- Vehicle

---

## Vector (Semantic) Search

Searches by meaning.

Search:

```
Car
```

Can also find:

- Automobile
- Vehicle
- Sedan
- SUV

This is why RAG uses vector search.

---

# Chunking Strategies

Different chunking methods affect retrieval quality.

### Fixed Chunking

Documents are split into equal-sized pieces.

Example

```
500 words

500 words

500 words
```

---

### Semantic Chunking

Splits documents based on meaning rather than size.

This usually produces better retrieval quality.

---

### Hierarchical Chunking

Documents are split into sections and subsections while preserving structure.

Useful for:

- Books
- Documentation
- Legal documents

---

# Popular RAG Architectures

## 1. Standard RAG

```
Retrieve
      │
Generate
```

The simplest RAG implementation.

---

## 2. Hybrid RAG

Combines:

- Keyword Search
- Vector Search

This improves retrieval accuracy.

---

## 3. RAG with Memory

Remembers previous conversations.

Useful for chatbots.

---

## 4. Graph RAG

Uses **Knowledge Graphs** to understand relationships between entities.

Example

```
John
 │
Works At
 │
Google
```

This allows the AI to answer more complex relationship-based questions.

---

## 5. Agentic RAG

Combines RAG with AI Agents.

The AI can:

- Search multiple sources
- Use tools
- Break complex tasks into smaller ones
- Plan
- Re-plan if necessary

---

# RAG vs Fine-Tuning

| RAG | Fine-Tuning |
|------|-------------|
| Uses external knowledge | Updates the model itself |
| Data stays outside the model | Data becomes part of the model |
| Easy to update | Requires retraining |
| Lower cost | More expensive |
| Best for frequently changing information | Best for changing model behavior or style |

---

# Real-World Applications

## Customer Support

- Order status
- Booking information
- Product documentation

---

## Healthcare

- Medical reports
- Lab results
- Patient FAQs

---

## Finance

- Banking documents
- Investment reports
- Internal policies

---

## Legal

- Contracts
- Compliance documents
- Legal research

---

## Research

- Scientific papers
- Academic journals
- Company documentation

---

# Key Takeaways

- RAG stands for **Retrieval-Augmented Generation**.
- It improves LLM responses using external knowledge.
- It reduces hallucinations by grounding answers in retrieved data.
- The two major stages are:
  - Ingestion Pipeline
  - Retrieval Pipeline
- Documents are converted into embeddings and stored inside vector databases.
- Semantic search retrieves information based on meaning instead of exact words.
- RAG is more cost-effective than retraining an LLM for frequently changing knowledge.
- Different RAG architectures exist for different use cases, including Standard, Hybrid, Memory, Graph, and Agentic RAG.

---

# New Concepts Learned

- Retrieval-Augmented Generation (RAG)
- Ingestion Pipeline
- Retrieval Pipeline
- Embeddings
- Vector Embeddings
- Vector Database
- Semantic Search
- Chunking
- Fixed Chunking
- Semantic Chunking
- Hierarchical Chunking
- Standard RAG
- Hybrid RAG
- RAG with Memory
- Graph RAG
- Agentic RAG
- Knowledge Graph
- Fine-Tuning vs RAG
- Pinecone
- ChromaDB
- Weaviate
- Milvus
- Qdrant