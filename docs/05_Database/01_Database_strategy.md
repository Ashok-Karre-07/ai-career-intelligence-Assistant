# Database Strategy

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Database Strategy |
| Version | 1.0 |
| Owner | Data Architecture Team |

---

# Purpose

This document defines the database strategy for the AI Career Intelligence Platform.

The database architecture is designed to support transactional workloads, AI-powered features, semantic search, analytics, and future enterprise scalability.

The platform uses a relational-first approach while extending PostgreSQL with vector search capabilities through pgvector.

---

# Objectives

The database platform shall:

- Ensure data integrity
- Support AI workloads
- Enable semantic search
- Scale horizontally where required
- Maintain ACID compliance
- Provide strong security
- Support auditing
- Enable disaster recovery

---

# Database Design Principles

The database follows these principles:

- Relational First
- Normalize Core Business Data
- Denormalize Only When Necessary
- ACID Transactions
- Security by Design
- Version Everything
- Audit Critical Changes
- Optimize for Read and Write Performance

---

# Database Technology Stack

| Layer | Technology |
|--------|------------|
| Primary Database | PostgreSQL 17+ |
| Vector Storage | pgvector |
| ORM | SQLAlchemy 2.x |
| Migration Tool | Alembic |
| Cache | Redis |
| Object Storage | MinIO (Development), Amazon S3 Compatible Storage (Production) |

---

# Why PostgreSQL?

PostgreSQL was selected because it provides:

- ACID compliance
- High reliability
- Excellent indexing capabilities
- JSONB support
- Full-text search
- Mature ecosystem
- pgvector integration
- Strong community support

---

# Why pgvector?

The platform requires semantic search for:

- Resume similarity
- Job matching
- Company knowledge retrieval
- Career recommendations
- RAG document retrieval

Using pgvector allows us to:

- Keep transactional and vector data together
- Reduce operational complexity
- Simplify backups
- Use SQL alongside vector search

---

# Database Categories

The platform stores several categories of data.

## User Data

Examples

- Users
- Profiles
- Preferences
- Authentication

---

## Resume Data

Examples

- Resumes
- Resume Versions
- Resume Analysis
- ATS Scores

---

## Job Data

Examples

- Jobs
- Applications
- Saved Jobs
- Recommendations

---

## Company Data

Examples

- Company Profiles
- Technology Stack
- Hiring Trends
- Industry Information

---

## AI Data

Examples

- Prompt Versions
- Agent Executions
- AI Responses
- Evaluation Results

---

## Vector Data

Examples

- Embeddings
- Metadata
- Chunk Relationships

---

## Audit Data

Examples

- User Activity
- Login History
- Security Events
- Audit Logs

---

# High-Level Database Architecture

```text
                 FastAPI Backend
                        │
                        ▼
                SQLAlchemy ORM
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                ▼
 PostgreSQL       pgvector         Redis Cache
        │
        ▼
 Object Storage References
```

---

# Data Domains

The database is organized into logical domains.

| Domain | Purpose |
|--------|---------|
| Identity | Users, Roles, Sessions |
| Resume | Resume Management |
| Jobs | Job Search and Applications |
| Companies | Company Intelligence |
| AI | Agents, Prompts, Evaluations |
| Knowledge | RAG Documents and Embeddings |
| Notifications | Emails and Alerts |
| Audit | Security and Activity Logs |

---

# Transaction Strategy

Use transactions for:

- User registration
- Resume upload
- Resume analysis
- Job applications
- Subscription changes
- Profile updates

All business-critical operations must be atomic.

---

# Data Integrity

The database enforces:

- Primary Keys
- Foreign Keys
- Unique Constraints
- Check Constraints
- NOT NULL Constraints
- Cascading Rules (where appropriate)

---

# Security Strategy

Security controls include:

- Row ownership validation
- Encrypted connections (TLS)
- Role-based access
- Principle of least privilege
- Audit logging
- Secure backups

---

# Backup Strategy

Development

- Daily local backups

Production

- Daily full backups
- Hourly incremental backups
- Point-in-Time Recovery (PITR)

Retention

- Daily: 30 days
- Weekly: 12 weeks
- Monthly: 12 months

---

# Disaster Recovery

Recovery Objectives

| Metric | Target |
|---------|--------|
| Recovery Point Objective (RPO) | < 15 minutes |
| Recovery Time Objective (RTO) | < 1 hour |

---

# Scalability Strategy

Current

- Single PostgreSQL instance
- pgvector
- Redis cache

Future

- Read replicas
- Connection pooling
- Table partitioning
- Multi-region replication
- Dedicated vector database (if required)

---

# Performance Strategy

Optimization techniques:

- Proper indexing
- Query optimization
- Pagination
- Prepared statements
- Connection pooling
- Caching
- Background processing

---

# Data Lifecycle

```text
Create
   │
   ▼
Validate
   │
   ▼
Store
   │
   ▼
Read
   │
   ▼
Update
   │
   ▼
Archive
   │
   ▼
Delete
```

---

# Compliance

The database design supports:

- GDPR-ready principles
- Data minimization
- Auditability
- Secure deletion
- Retention policies

---

# Future Enhancements

- Multi-region databases