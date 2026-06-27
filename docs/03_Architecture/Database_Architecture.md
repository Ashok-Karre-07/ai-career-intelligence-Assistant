# Database Architecture

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Database Architecture |
| Version | 1.0 |
| Owner | Database Architecture Team |

---

# Purpose

This document defines the enterprise database architecture for the AI Career Intelligence Platform.

The platform uses PostgreSQL as the primary relational database and pgvector for semantic search.

The architecture is designed to support:

- Business transactions
- AI workflows
- Vector search
- Agent execution
- Audit logging
- Analytics
- Future scalability

---

# Database Goals

The database architecture shall:

- Support OLTP workloads
- Support AI retrieval
- Maintain ACID compliance
- Ensure data consistency
- Enable efficient search
- Scale horizontally in the future
- Support backup and disaster recovery

---

# Technology Stack

| Technology | Purpose |
|------------|---------|
| PostgreSQL | Primary relational database |
| pgvector | Vector similarity search |
| SQLAlchemy | ORM |
| Alembic | Schema migrations |
| Redis | Cache & session storage |

---

# High-Level Database Architecture

```text
                  FastAPI

                     │

                     ▼

              SQLAlchemy ORM

                     │

                     ▼

            PostgreSQL Database

                     │

      ┌──────────────┼───────────────┐

      ▼              ▼               ▼

Business Data   AI Metadata    Vector Data

                     │

                     ▼

                  pgvector
```

---

# Database Domains

The database is organized into the following logical domains.

---

## Identity Domain

Tables

- users
- user_profiles
- roles
- permissions
- user_sessions

Responsibilities

- Authentication
- Authorization
- User preferences

---

## Resume Domain

Tables

- resumes
- resume_versions
- resume_analysis
- resume_keywords

Responsibilities

- Resume storage
- Resume versions
- ATS analysis
- Resume history

---

## Job Domain

Tables

- jobs
- saved_jobs
- job_matches
- job_search_history

Responsibilities

- Job discovery
- Job matching
- Saved jobs
- Search history

---

## Company Domain

Tables

- companies
- company_profiles
- hiring_trends

Responsibilities

- Company information
- Hiring trends
- Technology stack

---

## Application Domain

Tables

- applications
- interviews
- offers
- application_notes

Responsibilities

- Application tracking
- Interview scheduling
- Offer management

---

## AI Domain

Tables

- ai_requests
- ai_responses
- agent_executions
- prompt_versions
- evaluation_results

Responsibilities

- AI request history
- Agent execution tracking
- Prompt versioning
- AI evaluation

---

## RAG Domain

Tables

- documents
- document_chunks
- embeddings
- vector_metadata

Responsibilities

- Knowledge storage
- Chunk management
- Embedding storage
- Retrieval metadata

---

## Audit Domain

Tables

- audit_logs
- user_activity
- security_events

Responsibilities

- Compliance
- Audit history
- Security monitoring

---

# Entity Relationships

```text
User

│

├── Resume

│      │

│      ├── ResumeVersion

│      └── ResumeAnalysis

│

├── SavedJob

│

├── Application

│      │

│      ├── Interview

│      └── Offer

│

└── AIRequest
```

---

# Vector Storage

Technology

- pgvector

Stores

- Embeddings
- Chunk vectors
- Similarity indexes

Each embedding references:

- document_id
- chunk_id
- embedding_model
- embedding_version

---

# Indexing Strategy

Indexes will be created for:

Business Tables

- User email
- Resume ID
- Company ID
- Job ID
- Application Status

Vector Tables

- HNSW Index
- IVFFlat (future)

---

# Transactions

The platform shall use transactions for:

- User registration
- Resume upload
- Job application creation
- AI request logging

---

# Migration Strategy

Technology

- Alembic

Rules

- Version-controlled migrations
- Rollback support
- Forward-only production migrations
- Automated migration testing

---

# Backup Strategy

Daily

- Full backup

Hourly

- WAL archive

Future

- Point-in-Time Recovery (PITR)

---

# Security

- Encrypted connections
- Least privilege access
- Row-level security (future)
- Secrets managed through environment variables

---

# Performance

Targets

| Metric | Target |
|--------|---------|
| Query Response | <100 ms |
| Vector Search | <500 ms |
| Insert | <200 ms |
| Update | <200 ms |

---

# Scalability

Future enhancements

- Read replicas
- Partitioning
- Connection pooling
- Sharding (if required)

---

# Monitoring

Monitor

- Slow queries
- Index usage
- Lock contention
- Storage growth
- Connection pool
- Vector search latency

---

# Data Retention

| Data | Retention |
|------|-----------|
| Audit Logs | 1 Year |
| AI Requests | 90 Days |
| User Sessions | 30 Days |
| Resume Files | Until User Deletes |
| Applications | Permanent |

---

# Dependencies

Depends on

- AI Architecture
- RAG Architecture
- Agent Architecture
- Technology Stack

Used by

- ER Diagram
- Data Dictionary
- SQLAlchemy Models
- Alembic Migrations
- Repository Layer

---

# Future Enhancements

- Multi-tenant schema
- Analytics warehouse
- Data lake integration
- Event sourcing
- CDC pipelines

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief Database Architect | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Technical Lead | TBD | Pending |