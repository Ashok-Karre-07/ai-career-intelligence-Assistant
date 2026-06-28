# RAG Architecture

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | RAG Architecture |
| Version | 1.0 |
| Owner | AI Engineering Team |

---

# Purpose

This document defines the implementation architecture for the Retrieval-Augmented Generation (RAG) platform used by the AI Career Intelligence Platform.

The RAG system enables AI agents to retrieve relevant knowledge before generating responses, significantly improving factual accuracy, explainability, and consistency.

Unlike the system-level architecture document, this specification focuses on the implementation of the RAG pipeline.

---

# Objectives

The RAG platform shall:

- Minimize hallucinations
- Improve answer accuracy
- Support multiple knowledge bases
- Enable semantic retrieval
- Support metadata filtering
- Scale independently
- Support future hybrid search

---

# RAG Design Principles

The platform follows:

- Retrieval Before Generation
- Knowledge Separation
- Context First
- Metadata Driven
- Secure Retrieval
- Observable Retrieval
- Versioned Embeddings

---

# High-Level RAG Pipeline

```text
Knowledge Sources
        │
        ▼
Document Ingestion
        │
        ▼
Document Parsing
        │
        ▼
Cleaning & Normalization
        │
        ▼
Chunk Generation
        │
        ▼
Embedding Generation
        │
        ▼
Vector Storage (pgvector)
        │
        ▼
Retriever
        │
        ▼
Metadata Filter
        │
        ▼
Semantic Ranking
        │
        ▼
Context Builder
        │
        ▼
OpenAI Responses API
        │
        ▼
Structured AI Response
```

---

# Knowledge Sources

The platform maintains multiple knowledge domains.

## Resume Knowledge

Contains

- Resume Templates
- ATS Guidelines
- Resume Examples
- Skill Taxonomy

---

## Job Knowledge

Contains

- Job Descriptions
- Role Requirements
- Hiring Trends

---

## Company Knowledge

Contains

- Company Profiles
- Tech Stacks
- Culture
- Interview Experiences
- Visa Sponsorship Information

---

## Career Knowledge

Contains

- Learning Paths
- Certifications
- Salary Insights
- Career Roadmaps

---

## Interview Knowledge

Contains

- Technical Questions
- Behavioral Questions
- Coding Problems

---

# Document Ingestion Pipeline

Supported Formats

- PDF
- DOCX
- Markdown
- HTML
- CSV
- JSON
- TXT

Pipeline

```
Upload

↓

Validation

↓

Virus Scan (Future)

↓

OCR (if needed)

↓

Text Extraction

↓

Normalization

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

# Document Cleaning

The ingestion pipeline removes:

- Extra whitespace
- HTML tags
- Unsupported characters
- Duplicate sections
- Empty paragraphs

Normalizes

- Unicode
- Dates
- Headings
- Bullet lists

---

# Metadata Schema

Every chunk stores metadata.

```json
{
  "document_id": "...",
  "chunk_id": "...",
  "document_type": "resume",
  "source": "user_upload",
  "owner_id": "...",
  "language": "en",
  "embedding_model": "text-embedding-3-large",
  "embedding_version": "v1"
}
```

---

# Chunking Strategy

Primary Strategy

- Semantic chunking

Fallback

- Fixed-size chunking

Chunk Size

800–1000 tokens

Overlap

150–200 tokens

Chunk Types

- Heading
- Paragraph
- Table
- Bullet List
- Code (Future)

---

# Embedding Strategy

Technology

- OpenAI text-embedding-3-large

Responsibilities

- Generate embeddings
- Version embeddings
- Rebuild embeddings after model upgrades

---

# Vector Storage

Technology

- PostgreSQL
- pgvector

Stores

- Embedding Vector
- Metadata
- Chunk Relationships
- Source Reference

---

# Retrieval Pipeline

Steps

1. User Query
2. Query Embedding
3. Metadata Filtering
4. Vector Similarity Search
5. Top-K Retrieval
6. Context Deduplication
7. Reranking
8. Context Assembly
9. Prompt Construction

---

# Retrieval Strategies

Supported

## Semantic Search

Vector similarity.

---

## Metadata Filtering

Examples

- Country
- Company
- Skill
- Document Type
- User Ownership

---

## Hybrid Search (Future)

Combine:

- Semantic Search
- Keyword Search

---

# Context Builder

Responsibilities

- Remove duplicate chunks
- Preserve logical order
- Merge related sections
- Respect token limits
- Prioritize authoritative documents

Maximum Context

16,000 tokens (configurable)

---

# RAG Integration

The following agents use the RAG platform:

- Resume Agent
- Job Agent
- Company Agent
- Career Agent
- Interview Agent
- Visa Agent

Agents never access the vector store directly.

All retrieval requests go through the Retrieval Service.

---

# Caching

Cache

- Query embeddings
- Frequently used retrievals
- Metadata lookups

Technology

- Redis

---

# Security

The RAG platform enforces:

- User ownership validation
- Metadata filtering
- Prompt injection detection
- Sensitive document isolation
- Access control

---

# Evaluation Metrics

| Metric | Target |
|---------|--------|
| Retrieval Precision | >90% |
| Retrieval Recall | >90% |
| Context Relevance | >95% |
| Hallucination Rate | <2% |
| Retrieval Latency | <500 ms |

---

# Monitoring

Track

- Retrieval latency
- Top-K distribution
- Embedding generation time
- Cache hit ratio
- Context size
- Token usage
- Retrieval failures

---

# Failure Recovery

If retrieval fails:

1. Retry retrieval
2. Retry with relaxed metadata filters
3. Retry semantic search only
4. Return graceful fallback
5. Log incident

---

# Future Enhancements

- Graph RAG
- Knowledge Graph
- Multi-vector Retrieval
- Query Rewriting
- Cross-Encoder Reranking
- Adaptive Chunking
- Citation Generation
- Incremental Embedding Updates

---

# Dependencies

Depends on:

- AI Strategy
- Agent Architecture
- Prompt Library

Used by:

- Resume Agent
- Job Agent
- Company Agent
- Career Agent
- AI Evaluation

---

# Related Documents

- 01_AI_Strategy.md
- 02_Agent_Architecture.md
- 03_Prompt_Library.md
- 05_AI_Evaluation.md
- 06_Guardrails.md

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief AI Architect | Ashok Karre | Pending |
| AI Engineering Lead | TBD | Pending |
| Technical Lead | TBD | Pending |