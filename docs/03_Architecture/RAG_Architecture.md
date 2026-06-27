# Retrieval-Augmented Generation (RAG) Architecture

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Enterprise RAG Architecture |
| Version | 1.0 |
| Owner | AI Architecture Team |

---

# Purpose

This document defines the Retrieval-Augmented Generation (RAG) architecture used by the AI Career Intelligence Platform.

The objective is to build an enterprise-grade knowledge retrieval platform that delivers accurate, explainable, and context-aware responses for multiple AI agents.

Unlike a chatbot-specific RAG implementation, this architecture supports multiple knowledge domains, reusable retrieval pipelines, metadata-driven search, and future extensibility.

---

# Objectives

The RAG platform shall:

- Support multiple knowledge bases.
- Provide semantic and keyword retrieval.
- Deliver high-quality context to AI agents.
- Reduce hallucinations.
- Improve response relevance.
- Scale independently from business services.

---

# High-Level RAG Architecture

```text
                     Knowledge Sources
                            │
                            ▼
                  Document Ingestion Pipeline
                            │
                            ▼
                   Document Preprocessing
                            │
                            ▼
                     Chunking Strategy
                            │
                            ▼
                  Embedding Generation
                            │
                            ▼
             PostgreSQL + pgvector Storage
                            │
                            ▼
                  Retrieval Orchestrator
                            │
        ┌───────────────────┼────────────────────┐
        ▼                   ▼                    ▼
 Semantic Search      Keyword Search      Metadata Filter
        │                   │                    │
        └───────────────────┴────────────────────┘
                            │
                            ▼
                     Reranking Engine
                            │
                            ▼
                    Context Builder
                            │
                            ▼
                   Prompt Construction
                            │
                            ▼
                 OpenAI Responses API
                            │
                            ▼
                       AI Response
```

---

# Knowledge Domains

The platform maintains separate knowledge collections.

## Resume Knowledge Base

Contains:

- Resume templates
- ATS best practices
- Resume examples
- Skill taxonomy

---

## Job Knowledge Base

Contains:

- Job descriptions
- Role definitions
- Technology requirements
- Hiring trends

---

## Company Knowledge Base

Contains:

- Company profiles
- Tech stacks
- Hiring processes
- Visa sponsorship information

---

## Interview Knowledge Base

Contains:

- Technical questions
- Behavioral questions
- Coding patterns
- Evaluation rubrics

---

## Career Knowledge Base

Contains:

- Learning paths
- Certifications
- Salary insights
- Career roadmaps

---

## Visa Knowledge Base

Contains:

- Visa programs
- Immigration requirements
- Country-specific guidance

---

# Document Ingestion Pipeline

Supported document formats:

- PDF
- DOCX
- Markdown
- HTML
- JSON
- CSV
- Plain Text

Pipeline:

```text
Upload

↓

Validation

↓

OCR (if required)

↓

Cleaning

↓

Metadata Extraction

↓

Chunking

↓

Embedding

↓

Storage
```

---

# Metadata Model

Each chunk stores metadata.

Example

```json
{
  "document_id": "...",
  "document_type": "resume",
  "source": "user_upload",
  "title": "...",
  "created_at": "...",
  "chunk_id": "...",
  "chunk_index": 12,
  "language": "en",
  "embedding_version": "v1"
}
```

---

# Chunking Strategy

Supported strategies:

- Fixed-size chunking
- Semantic chunking
- Section-based chunking
- Heading-aware chunking

Default MVP:

- 800–1200 tokens
- 150–200 token overlap

---

# Embedding Strategy

Technology:

- OpenAI Embeddings

Responsibilities:

- Generate embeddings
- Version embeddings
- Rebuild embeddings when models change

---

# Vector Storage

Technology:

- PostgreSQL
- pgvector

Stores:

- Embeddings
- Metadata
- Chunk relationships

---

# Retrieval Strategies

The system supports:

## Semantic Search

Vector similarity search.

---

## Keyword Search

PostgreSQL Full-Text Search.

---

## Hybrid Search

Semantic + keyword scoring.

---

## Metadata Filtering

Examples:

- Country
- Technology
- Company
- Document type
- User ownership

---

# Reranking

Retrieved documents are reranked before prompt construction.

Future enhancements:

- Cross-encoder reranking
- Learned ranking models

---

# Context Builder

Responsibilities:

- Remove duplicates
- Preserve document order
- Merge related chunks
- Respect token budget
- Prioritize authoritative sources

---

# Prompt Construction

Each AI agent receives:

- User question
- Retrieved context
- Conversation context
- System prompt
- Tool definitions

The Context Builder assembles this prompt dynamically.

---

# Agent Integration

RAG is shared across:

- Resume Agent
- Job Search Agent
- Company Agent
- Career Agent
- Interview Agent
- Visa Agent

No agent accesses the vector store directly. All retrieval requests pass through the Retrieval Orchestrator.

---

# Performance Targets

| Metric | Target |
|---------|--------|
| Embedding Generation | < 2 seconds |
| Retrieval | < 500 ms |
| Context Building | < 500 ms |
| Total RAG Latency | < 2 seconds |

---

# Security

- Row-level security for user-owned documents.
- Encrypted storage.
- Access control through backend services.
- Metadata validation.
- Prompt injection mitigation.

---

# Monitoring

Track:

- Retrieval latency
- Top-K usage
- Cache hit rate
- Embedding generation time
- Token consumption
- Retrieval precision
- Retrieval recall

---

# Future Enhancements

- Multi-vector retrieval
- Graph RAG
- Knowledge Graph integration
- Adaptive chunking
- Query rewriting
- Multi-hop retrieval
- Citation generation
- Retrieval evaluation framework

---

# Dependencies

Depends on:

- AI Architecture
- Technology Stack
- C4 Component Diagram

Used by:

- Agent Architecture
- Resume Agent
- Job Agent
- Company Agent
- Backend Implementation

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief AI Architect | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Technical Lead | TBD | Pending |