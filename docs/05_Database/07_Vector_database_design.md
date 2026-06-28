# Vector Database Design

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Vector Database Design |
| Version | 1.0 |
| Owner | AI Data Engineering Team |

---

# Purpose

This document defines the vector database architecture used by the AI Career Intelligence Platform.

The platform uses PostgreSQL with the pgvector extension to store vector embeddings alongside relational data. This provides a unified architecture for transactional data, AI knowledge retrieval, and semantic search.

The design supports Retrieval-Augmented Generation (RAG), AI agents, semantic similarity search, and future migration to dedicated vector databases if required.

---

# Objectives

The vector database shall:

- Support semantic search
- Store high-dimensional embeddings
- Enable Retrieval-Augmented Generation (RAG)
- Support metadata filtering
- Optimize retrieval latency
- Scale with growing knowledge bases
- Support embedding versioning
- Enable future migration to dedicated vector databases

---

# Architecture Overview

```text
                 Source Documents
                        │
                        ▼
              Document Processing
                        │
                        ▼
                 Chunk Generation
                        │
                        ▼
             Embedding Generation
                        │
                        ▼
          PostgreSQL + pgvector Storage
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                ▼
 Metadata Filter   Similarity Search   Hybrid Search
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

# Why PostgreSQL + pgvector?

Advantages

- Single database for transactional and AI data
- ACID compliance
- Simplified backups
- Native SQL support
- Mature PostgreSQL ecosystem
- Excellent integration with SQLAlchemy
- Cost-effective for MVP and enterprise growth

Future migration to specialized vector databases remains possible without changing the application architecture.

---

# Knowledge Domains

The vector database stores embeddings for multiple domains.

## Resume Knowledge

Examples

- Resume templates
- ATS guidelines
- Resume best practices

---

## Job Knowledge

Examples

- Job descriptions
- Skills
- Responsibilities
- Hiring trends

---

## Company Knowledge

Examples

- Company profiles
- Technology stacks
- Interview experiences
- Culture summaries

---

## Career Knowledge

Examples

- Learning paths
- Certifications
- Career roadmaps
- Salary insights

---

## Interview Knowledge

Examples

- Technical questions
- Behavioral questions
- Coding patterns

---

# Embedding Pipeline

```text
Document Upload
        │
        ▼
Validation
        │
        ▼
Text Extraction
        │
        ▼
Cleaning
        │
        ▼
Chunk Generation
        │
        ▼
Embedding Creation
        │
        ▼
Metadata Creation
        │
        ▼
Vector Storage
```

---

# Chunking Strategy

Primary Strategy

Semantic chunking.

Fallback Strategy

Fixed-size chunking.

Recommended Settings

| Parameter | Value |
|-----------|-------|
| Chunk Size | 800–1000 tokens |
| Chunk Overlap | 150–200 tokens |
| Chunk Order | Preserve original document sequence |

Chunk Types

- Heading
- Paragraph
- Table
- Bullet List
- FAQ
- Code (Future)

---

# Embedding Model

Initial Model

```text
text-embedding-3-large
```

Future Models

- text-embedding-3-small
- Open-source embedding models
- Domain-specific embedding models

Every embedding stores its originating model and version.

---

# Embedding Metadata

Each vector includes metadata for filtering and governance.

Example

```json
{
  "document_id": "uuid",
  "chunk_id": "uuid",
  "document_type": "resume",
  "owner_id": "uuid",
  "language": "en",
  "embedding_model": "text-embedding-3-large",
  "embedding_version": "v1",
  "created_at": "2026-06-30T10:15:00Z"
}
```

---

# Physical Schema

## knowledge_documents

Stores document metadata.

---

## document_chunks

Stores processed text chunks.

Important Fields

- chunk_index
- chunk_text
- token_count
- metadata

---

## embeddings

Stores vector embeddings.

Columns

| Column | Type |
|---------|------|
| id | UUID |
| chunk_id | UUID |
| embedding_vector | VECTOR |
| embedding_model | VARCHAR |
| embedding_version | VARCHAR |
| created_at | TIMESTAMP |

---

# Retrieval Workflow

```text
User Query
      │
      ▼
Query Embedding
      │
      ▼
Metadata Filtering
      │
      ▼
Vector Similarity Search
      │
      ▼
Top-K Retrieval
      │
      ▼
Deduplication
      │
      ▼
Context Builder
      │
      ▼
LLM
```

---

# Similarity Search

Supported Distance Metrics

- Cosine Similarity (Primary)
- Euclidean Distance
- Inner Product

Default

Cosine Similarity

---

# HNSW Index

Technology

pgvector HNSW

Advantages

- High recall
- Low latency
- Excellent scalability

Example

```sql
CREATE INDEX idx_embeddings_hnsw
ON embeddings
USING hnsw (embedding_vector vector_cosine_ops);
```

---

# Hybrid Search

Current

Semantic Search

Future

Semantic Search +

- PostgreSQL Full-Text Search
- BM25 Ranking
- Keyword Search

---

# Metadata Filtering

Supported Filters

- document_type
- owner_id
- company
- country
- language
- skill
- created_at

Metadata filtering is always applied before similarity ranking when possible.

---

# Context Assembly

Responsibilities

- Remove duplicate chunks
- Preserve logical ordering
- Merge related content
- Respect token budget
- Prioritize authoritative sources

Maximum Context Size

Configurable.

---

# Embedding Versioning

Every embedding stores:

- Embedding model
- Version
- Creation date

When the embedding model changes:

1. Generate new embeddings
2. Keep previous version until migration completes
3. Switch retrieval to the latest version
4. Archive obsolete embeddings

---

# Update Strategy

When a document changes:

1. Detect modified sections
2. Regenerate affected chunks
3. Recompute embeddings
4. Update metadata
5. Refresh indexes

---

# Performance Targets

| Metric | Target |
|---------|--------|
| Embedding Generation | < 1 sec/document |
| Retrieval Latency | < 500 ms |
| Context Assembly | < 200 ms |
| Top-K Search | < 300 ms |
| Cache Hit Ratio | > 90% |

---

# Security

The vector database enforces:

- Row ownership validation
- Metadata-based access control
- Encrypted connections
- Audit logging
- Sensitive document isolation

---

# Monitoring

Track

- Embedding generation time
- Retrieval latency
- Top-K distribution
- Index usage
- Cache hit ratio
- Failed retrievals
- Embedding storage growth

---

# Backup and Recovery

Backup

- Daily full backup
- Incremental backups
- Point-in-Time Recovery

Recovery includes:

- Relational data
- Vector data
- Metadata
- Index definitions

---

# Future Evolution

The architecture supports migration to:

- Qdrant
- Pinecone
- Weaviate
- Milvus

Migration strategy

- Introduce a Vector Repository abstraction
- Keep application APIs unchanged
- Synchronize embeddings during migration
- Cut over after validation

---

# Best Practices

- Keep chunk sizes consistent
- Avoid duplicate embeddings
- Rebuild embeddings after model upgrades
- Monitor retrieval quality
- Cache frequently used query embeddings
- Validate metadata before indexing

---

# Dependencies

Depends on

- Database Strategy
- RAG Architecture
- AI Strategy

Used by

- Resume Agent
- Job Agent
- Company Agent
- Career Agent
- AI Evaluation

---

# Related Documents

- 01_Database_Strategy.md
- 04_AI/04_RAG_Architecture.md
- 04_AI/05_AI_Evaluation.md
- 05_Indexing_Strategy.md
- 06_Partitioning_Strategy.md

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief Data Architect | Ashok Karre | Pending |
| AI Engineering Lead | TBD | Pending |
| Database Administrator | TBD | Pending |