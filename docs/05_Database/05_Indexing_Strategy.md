# Indexing Strategy

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Database Indexing Strategy |
| Version | 1.0 |
| Owner | Database Architecture Team |

---

# Purpose

This document defines the indexing strategy for the AI Career Intelligence Platform.

The objective is to optimize query performance, reduce response times, improve AI retrieval efficiency, and support future scalability.

The indexing strategy covers relational data, JSONB fields, full-text search, and vector similarity search.

---

# Objectives

The indexing strategy shall:

- Reduce query latency
- Improve lookup performance
- Optimize JOIN operations
- Accelerate filtering and sorting
- Enable fast semantic search
- Support high write throughput
- Scale efficiently with data growth

---

# Indexing Principles

The platform follows these principles:

- Index frequently queried columns
- Avoid unnecessary indexes
- Prefer composite indexes for common filters
- Optimize read-heavy workloads
- Balance read and write performance
- Regularly monitor index usage

---

# PostgreSQL Index Types

| Index Type | Purpose | Use Cases |
|------------|---------|-----------|
| B-Tree | Default index | Equality, range queries |
| Hash | Exact equality | Rarely used |
| GIN | JSONB, arrays, full-text | Skills, metadata |
| GiST | Geospatial, specialized search | Future extensions |
| BRIN | Large sequential tables | Audit logs |
| HNSW (pgvector) | Approximate nearest neighbor | Embedding search |
| IVFFlat (pgvector) | Approximate vector search | Large vector datasets |

---

# Primary Key Indexes

Every table automatically includes a primary key index.

Example

```sql
PRIMARY KEY (id)
```

---

# Unique Indexes

Examples

```sql
users.email

companies.website

ai_prompts(prompt_name, version)

saved_jobs(user_id, job_id)
```

Purpose

- Prevent duplicates
- Improve lookup speed

---

# Foreign Key Indexes

Every foreign key column should have an index.

Examples

```text
resume.user_id

jobs.company_id

applications.user_id

applications.job_id

resume_analysis.resume_id

document_chunks.document_id

embeddings.chunk_id
```

Benefits

- Faster JOINs
- Better cascading performance

---

# Composite Indexes

Composite indexes optimize multi-column queries.

Recommended Indexes

### Jobs

```sql
(company_id, location)
```

Used for

- Company job listings
- Location filters

---

### Applications

```sql
(user_id, status)
```

Used for

- User application history
- Dashboard statistics

---

### Resume Versions

```sql
(resume_id, version_number)
```

Used for

- Resume history retrieval

---

### AI Agent Runs

```sql
(user_id, created_at DESC)
```

Used for

- User AI activity timeline

---

### Notifications

```sql
(user_id, is_read)
```

Used for

- Unread notification queries

---

# Partial Indexes

Used when only a subset of records is queried frequently.

Examples

Unread Notifications

```sql
WHERE is_read = FALSE
```

Active Users

```sql
WHERE is_active = TRUE
```

Active Jobs

```sql
WHERE status = 'ACTIVE'
```

Benefits

- Smaller indexes
- Faster lookups
- Reduced storage

---

# JSONB Indexes

Technology

GIN

Tables

- resume_analysis
- jobs
- document_chunks

Indexed Fields

- missing_skills
- recommendations
- metadata
- required_skills

Example

```sql
CREATE INDEX idx_resume_analysis_missing_skills
ON resume_analysis
USING GIN (missing_skills);
```

---

# Full-Text Search

Supported Tables

- jobs
- companies
- knowledge_documents

Indexed Columns

- title
- description
- company_name
- content

Technology

GIN + tsvector

---

# Vector Search Indexes

Technology

pgvector

Primary Algorithm

HNSW

Embedding Table

```text
embeddings
```

Indexed Column

```text
embedding_vector
```

Example

```sql
CREATE INDEX idx_embeddings_hnsw
ON embeddings
USING hnsw (embedding_vector vector_cosine_ops);
```

Future Option

IVFFlat for very large datasets.

---

# Sorting Optimization

Frequently sorted columns:

- created_at
- updated_at
- applied_at
- salary_max
- ats_score
- match_score

Indexes should support ORDER BY operations.

---

# Pagination Optimization

Use indexed columns for pagination.

Preferred

```sql
ORDER BY created_at DESC
```

Avoid

OFFSET pagination for very large datasets.

Future

Keyset Pagination

---

# Covering Indexes

Use INCLUDE columns when beneficial.

Example

```sql
CREATE INDEX idx_jobs_location
ON jobs(location)
INCLUDE(title, company_id);
```

Benefits

- Reduce table lookups
- Faster read performance

---

# Index Maintenance

Monitor

- Index usage
- Fragmentation
- Bloat
- Slow queries

Maintenance Tasks

- REINDEX
- VACUUM
- ANALYZE

---

# Index Naming Convention

Format

```text
idx_<table>_<column>

idx_jobs_location

idx_users_email

idx_embeddings_hnsw
```

Unique Index

```text
uq_<table>_<column>
```

Examples

```text
uq_users_email

uq_saved_jobs_user_job
```

---

# Query Optimization Guidelines

Prefer

- Indexed WHERE clauses
- Indexed JOIN columns
- Prepared statements
- LIMIT clauses
- Keyset pagination

Avoid

- SELECT *
- Leading wildcard searches
- Functions on indexed columns
- Unnecessary DISTINCT
- Large OFFSET values

---

# Monitoring Metrics

Track

- Slow queries
- Index hit ratio
- Sequential scans
- Index scans
- Dead tuples
- Query execution time

Target

Index Hit Ratio

>95%

---

# Growth Strategy

Current

- B-Tree
- GIN
- HNSW

Future

- Partition-aware indexes
- Read replicas
- Materialized views
- Dedicated search cluster

---

# Future Enhancements

- Automatic index recommendations
- Query plan analysis
- Adaptive indexing
- Bloom indexes
- Hypothetical indexes
- AI-assisted query optimization

---

# Dependencies

Depends on

- Database Strategy
- Table Definitions
- Vector Database Design

Used by

- PostgreSQL
- SQLAlchemy
- Performance Testing
- DevOps

---

# Related Documents

- 01_Database_Strategy.md
- 04_Table_Definitions.md
- 06_Partitioning_Strategy.md
- 07_Vector_Database_Design.md

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief Data Architect | Ashok Karre | Pending |
| Database Administrator | TBD | Pending |
| Performance Engineer | TBD | Pending |