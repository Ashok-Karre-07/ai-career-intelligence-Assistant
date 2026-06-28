# Data Dictionary

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Enterprise Data Dictionary |
| Version | 1.0 |
| Owner | Data Architecture Team |

---

# Purpose

This document defines the enterprise data dictionary for the AI Career Intelligence Platform.

The data dictionary provides a standardized definition of every business entity, database column, data type, validation rule, and relationship used throughout the platform.

It serves as the authoritative reference for database implementation, API development, AI services, reporting, and analytics.

---

# Data Standards

## Naming Convention

Tables

- Plural
- Snake Case

Example

```text
users

resume_versions

job_applications
```

Columns

- Snake Case

Examples

```text
first_name

created_at

resume_id

company_name
```

Primary Key

```text
id
```

Foreign Keys

```text
user_id

resume_id

company_id
```

Boolean Fields

Start with:

```text
is_

has_

can_
```

Examples

```text
is_active

is_verified

has_resume
```

Date Fields

End with:

```text
_at
```

Examples

```text
created_at

updated_at

deleted_at
```

---

# Standard Audit Columns

Every business table contains:

| Column | Type | Description |
|----------|------|-------------|
| id | UUID | Primary Key |
| created_at | TIMESTAMP | Record creation |
| updated_at | TIMESTAMP | Last update |
| created_by | UUID | User creating record |
| updated_by | UUID | User updating record |

Soft-delete enabled tables additionally contain:

| Column | Type |
|----------|------|
| deleted_at | TIMESTAMP NULL |

---

# USERS

Purpose

Stores authentication and account information.

| Column | Type | Required | Description |
|---------|------|----------|-------------|
| id | UUID | Yes | Primary Key |
| email | VARCHAR(255) | Yes | Unique email |
| password_hash | TEXT | Yes | BCrypt hash |
| first_name | VARCHAR(100) | Yes | First name |
| last_name | VARCHAR(100) | Yes | Last name |
| is_active | BOOLEAN | Yes | Account active |
| is_verified | BOOLEAN | Yes | Email verified |
| last_login_at | TIMESTAMP | No | Last successful login |
| created_at | TIMESTAMP | Yes | Creation timestamp |
| updated_at | TIMESTAMP | Yes | Update timestamp |

Constraints

- email UNIQUE
- email NOT NULL

---

# USER_PROFILE

Purpose

Stores user profile details.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| user_id | UUID | FK → users |
| phone_number | VARCHAR(25) | Contact number |
| country | VARCHAR(100) | Country |
| city | VARCHAR(100) | City |
| linkedin_url | TEXT | LinkedIn profile |
| github_url | TEXT | GitHub profile |
| portfolio_url | TEXT | Portfolio website |
| years_of_experience | DECIMAL(4,1) | Professional experience |
| current_role | VARCHAR(200) | Current designation |

Relationship

- One Profile → One User

---

# RESUMES

Purpose

Stores uploaded resumes.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| user_id | UUID | FK → users |
| file_name | VARCHAR(255) | Original filename |
| storage_path | TEXT | Object storage location |
| file_type | VARCHAR(20) | PDF/DOCX |
| file_size | BIGINT | File size in bytes |
| current_version | INTEGER | Latest version |
| status | VARCHAR(50) | Processing status |

Relationship

- Many Resumes → One User

---

# RESUME_VERSIONS

Purpose

Maintains resume history.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| resume_id | UUID | FK → resumes |
| version_number | INTEGER | Version |
| storage_path | TEXT | Resume file |
| change_summary | TEXT | User changes |

---

# RESUME_ANALYSIS

Purpose

Stores AI analysis.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| resume_id | UUID | FK → resumes |
| ats_score | DECIMAL(5,2) | ATS score |
| summary | TEXT | Resume summary |
| missing_skills | JSONB | Skills |
| recommendations | JSONB | AI recommendations |
| confidence_score | DECIMAL(5,2) | AI confidence |

---

# RESUME_SKILLS

Purpose

Stores extracted skills.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| resume_id | UUID | FK → resumes |
| skill_name | VARCHAR(150) | Skill |
| category | VARCHAR(100) | Technical / Soft |
| confidence | DECIMAL(5,2) | Extraction confidence |

---

# COMPANIES

Purpose

Stores company master data.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| company_name | VARCHAR(255) | Company |
| industry | VARCHAR(150) | Industry |
| headquarters | VARCHAR(150) | Headquarters |
| website | TEXT | Official website |
| company_size | VARCHAR(100) | Size |
| visa_sponsorship | BOOLEAN | Sponsorship available |

---

# JOBS

Purpose

Stores available jobs.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| company_id | UUID | FK → companies |
| title | VARCHAR(255) | Job title |
| location | VARCHAR(255) | Job location |
| employment_type | VARCHAR(50) | Full-time |
| salary_min | DECIMAL(12,2) | Minimum salary |
| salary_max | DECIMAL(12,2) | Maximum salary |
| description | TEXT | Job description |
| required_skills | JSONB | Skills |

---

# APPLICATIONS

Purpose

Tracks applications.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| user_id | UUID | FK → users |
| job_id | UUID | FK → jobs |
| resume_id | UUID | FK → resumes |
| status | VARCHAR(50) | Applied / Interview / Offer / Rejected |
| applied_at | TIMESTAMP | Application date |
| notes | TEXT | User notes |

---

# KNOWLEDGE_DOCUMENTS

Purpose

Stores RAG source documents.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| title | VARCHAR(255) | Document title |
| document_type | VARCHAR(100) | Resume / Job / Company |
| source | VARCHAR(100) | Upload source |
| owner_id | UUID | Document owner |
| language | VARCHAR(20) | Language |

---

# DOCUMENT_CHUNKS

Purpose

Stores processed chunks.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| document_id | UUID | FK → knowledge_documents |
| chunk_index | INTEGER | Sequence |
| chunk_text | TEXT | Chunk content |
| token_count | INTEGER | Tokens |
| metadata | JSONB | Additional metadata |

---

# EMBEDDINGS

Purpose

Stores vector embeddings.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| chunk_id | UUID | FK → document_chunks |
| embedding_model | VARCHAR(100) | Embedding model |
| embedding_vector | VECTOR | pgvector column |
| embedding_version | VARCHAR(20) | Version |

---

# AI_PROMPTS

Purpose

Stores versioned prompts.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| prompt_name | VARCHAR(200) | Prompt name |
| version | VARCHAR(20) | Version |
| prompt_text | TEXT | Prompt content |
| status | VARCHAR(50) | Draft / Active / Deprecated |

---

# AI_AGENT_RUNS

Purpose

Stores every AI execution.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| user_id | UUID | FK → users |
| agent_name | VARCHAR(100) | Agent |
| model_name | VARCHAR(100) | AI model |
| prompt_version | VARCHAR(50) | Prompt version |
| tokens_used | INTEGER | Tokens |
| latency_ms | INTEGER | Response time |
| cost | DECIMAL(10,4) | Estimated cost |
| status | VARCHAR(50) | Success / Failed |

---

# NOTIFICATIONS

Purpose

Stores notifications.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| user_id | UUID | FK → users |
| notification_type | VARCHAR(100) | Email / In-App |
| title | VARCHAR(255) | Title |
| message | TEXT | Message |
| is_read | BOOLEAN | Read status |

---

# AUDIT_LOGS

Purpose

Stores audit information.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary Key |
| user_id | UUID | FK → users |
| event_type | VARCHAR(100) | Login / Upload / AI |
| entity_name | VARCHAR(100) | Table name |
| entity_id | UUID | Record ID |
| action | VARCHAR(100) | Create / Update / Delete |
| ip_address | VARCHAR(50) | Client IP |
| created_at | TIMESTAMP | Event time |

---

# Common Data Types

| Type | Usage |
|------|-------|
| UUID | Primary and Foreign Keys |
| VARCHAR | Short text |
| TEXT | Long text |
| BOOLEAN | Flags |
| INTEGER | Counts |
| BIGINT | File sizes |
| DECIMAL | Scores and salaries |
| TIMESTAMP | Date/time |
| JSONB | Flexible structured data |
| VECTOR | Embedding storage |

---

# Enumerations

## Application Status

- Applied
- Under Review
- Interview Scheduled
- Offer Received
- Rejected
- Withdrawn

---

## Resume Status

- Uploaded
- Processing
- Analyzed
- Failed

---

## Notification Type

- Email
- In-App
- System

---

## AI Agent Status

- Pending
- Running
- Completed
- Failed

---

# Data Quality Rules

- UUIDs generated by backend
- Email addresses validated
- Foreign keys enforced
- Soft delete for business entities
- UTC timestamps only
- JSON validated before persistence

---

# Dependencies

Depends on:

- Database Strategy
- ER Diagram

Used by:

- SQLAlchemy Models
- Alembic Migrations
- FastAPI Schemas
- Frontend Models
- API Documentation

---

# Related Documents

- 01_Database_Strategy.md
- 02_ER_Diagram.md
- 04_Table_Definitions.md
- 05_Indexing_Strategy.md

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief Data Architect | Ashok Karre | Pending |
| Database Administrator | TBD | Pending |
| Technical Lead | TBD | Pending |