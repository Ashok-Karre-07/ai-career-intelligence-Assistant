# Table Definitions

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Table Definitions |
| Version | 1.0 |
| Owner | Database Architecture Team |

---

# Purpose

This document defines the physical database schema for the AI Career Intelligence Platform.

Each table includes:

- Purpose
- Primary Key
- Foreign Keys
- Constraints
- Relationships
- Storage considerations
- Future scalability notes

---

# Database Standards

## Primary Key

Every table uses:

```text
UUID
```

Column Name

```text
id
```

---

## Audit Columns

Every business table contains:

```text
id

created_at

updated_at

created_by

updated_by
```

Optional

```text
deleted_at
```

---

# Identity Domain

---

## users

Purpose

Stores user authentication information.

Primary Key

```text
id
```

Columns

| Column | Type | Constraints |
|---------|------|-------------|
| id | UUID | PK |
| email | VARCHAR(255) | UNIQUE |
| password_hash | TEXT | NOT NULL |
| first_name | VARCHAR(100) | NOT NULL |
| last_name | VARCHAR(100) | NOT NULL |
| is_active | BOOLEAN | DEFAULT TRUE |
| is_verified | BOOLEAN | DEFAULT FALSE |
| last_login_at | TIMESTAMP | NULL |
| created_at | TIMESTAMP | NOT NULL |
| updated_at | TIMESTAMP | NOT NULL |

Relationships

- 1 User → 1 Profile
- 1 User → Many Sessions
- 1 User → Many Resumes
- 1 User → Many Applications

---

## user_profiles

Purpose

Stores profile information.

Primary Key

```text
id
```

Foreign Keys

```text
user_id → users.id
```

Relationships

- One-to-One with users

---

## user_sessions

Purpose

Stores login sessions.

Columns

- refresh_token
- expires_at
- device_name
- ip_address

Relationship

Many Sessions → One User

---

## user_preferences

Purpose

Stores personalized preferences.

Examples

- Preferred Country
- Preferred Job Title
- Preferred Salary
- Notification Settings

---

# Resume Domain

---

## resumes

Purpose

Stores uploaded resumes.

Relationships

Many Resumes → One User

Important Columns

- file_name
- storage_path
- file_size
- file_type
- current_version
- processing_status

---

## resume_versions

Purpose

Stores resume history.

Relationship

Many Versions → One Resume

Columns

- version_number
- change_summary
- storage_path

---

## resume_analysis

Purpose

Stores AI analysis.

Columns

- ats_score
- summary
- missing_skills
- recommendations
- confidence_score
- analyzed_at

Relationship

One Analysis → One Resume

---

## resume_skills

Purpose

Stores extracted skills.

Columns

- skill_name
- category
- confidence_score

Relationship

Many Skills → One Resume

---

# Job Domain

---

## companies

Purpose

Stores company master data.

Columns

- company_name
- industry
- headquarters
- website
- company_size
- visa_sponsorship

Relationship

One Company → Many Jobs

---

## jobs

Purpose

Stores job postings.

Foreign Keys

```text
company_id → companies.id
```

Columns

- title
- location
- employment_type
- description
- salary_min
- salary_max
- currency
- experience_required

Relationship

One Job → Many Applications

---

## applications

Purpose

Stores job applications.

Relationships

Many Applications → One User

Many Applications → One Job

Columns

- application_status
- applied_at
- interview_date
- notes

---

## saved_jobs

Purpose

Stores bookmarked jobs.

Composite Unique Constraint

```text
user_id

job_id
```

---

## job_match_results

Purpose

Stores AI-generated matching results.

Columns

- match_score
- missing_skills
- strengths
- weaknesses
- recommendation

Relationship

One Resume

One Job

---

# AI Domain

---

## ai_prompts

Purpose

Stores prompt versions.

Columns

- prompt_name
- version
- prompt_text
- status

---

## ai_agent_runs

Purpose

Stores every AI execution.

Columns

- agent_name
- model_name
- prompt_version
- execution_time_ms
- tokens_input
- tokens_output
- estimated_cost
- execution_status

---

## ai_evaluations

Purpose

Stores evaluation metrics.

Columns

- accuracy
- relevance
- hallucination_rate
- latency
- evaluation_result

---

## tool_executions

Purpose

Stores tool execution history.

Columns

- tool_name
- execution_time
- execution_status
- error_message

---

# Knowledge Domain

---

## knowledge_documents

Purpose

Stores source documents.

Columns

- title
- document_type
- owner_id
- language
- source

---

## document_chunks

Purpose

Stores document chunks.

Foreign Key

```text
document_id
```

Columns

- chunk_index
- chunk_text
- token_count
- metadata

---

## embeddings

Purpose

Stores vector embeddings.

Technology

pgvector

Columns

- chunk_id
- embedding_vector
- embedding_model
- embedding_version

One Chunk

↓

One Embedding

---

# Notification Domain

---

## notifications

Purpose

Stores notifications.

Columns

- notification_type
- title
- message
- is_read
- sent_at

---

# Audit Domain

---

## audit_logs

Purpose

Stores security and activity logs.

Columns

- user_id
- entity_name
- entity_id
- action
- event_type
- ip_address
- user_agent

---

# Future Tables

Reserved for future implementation.

## interview_sessions

Stores interview coaching sessions.

---

## interview_feedback

Stores AI interview feedback.

---

## learning_paths

Stores personalized learning plans.

---

## certifications

Stores recommended certifications.

---

## salary_insights

Stores salary benchmarking data.

---

## recruiter_accounts

Supports recruiter portal.

---

## subscriptions

Stores subscription plans.

---

## payments

Stores payment history.

---

## feature_flags

Controls feature rollout.

---

# Referential Integrity

Every foreign key enforces:

- ON UPDATE CASCADE
- ON DELETE RESTRICT (default)

Exceptions

- Session cleanup
- Temporary AI records

---

# Constraints

Supported Constraints

- Primary Keys
- Foreign Keys
- Unique Constraints
- Check Constraints
- NOT NULL
- Default Values

---

# Storage Considerations

Large Objects

Stored in Object Storage

Examples

- Resume PDFs
- DOCX Files
- Reports

Database stores

- Metadata
- References

Never large binary files.

---

# Table Growth Estimates

| Table | Growth |
|--------|--------|
| users | Medium |
| resumes | High |
| resume_versions | High |
| applications | High |
| ai_agent_runs | Very High |
| document_chunks | Very High |
| embeddings | Extremely High |
| audit_logs | Extremely High |

---

# Archival Strategy

Archive periodically:

- Audit Logs
- AI Agent Runs
- Tool Executions
- Expired Sessions

---

# Future Enhancements

- Multi-tenancy
- Table Partitioning
- Read Replicas
- Dedicated Analytics Database
- Event Store
- Data Warehouse Integration

---

# Dependencies

Depends on

- Database Strategy
- ER Diagram
- Data Dictionary

Used by

- SQLAlchemy Models
- Alembic Migrations
- Backend Services
- API Layer

---

# Related Documents

- 01_Database_Strategy.md
- 02_ER_Diagram.md
- 03_Data_Dictionary.md
- 05_Indexing_Strategy.md
- 06_Partitioning_Strategy.md

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief Data Architect | Ashok Karre | Pending |
| Database Administrator | TBD | Pending |
| Technical Lead | TBD | Pending |