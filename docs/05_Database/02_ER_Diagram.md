# Entity Relationship (ER) Diagram

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Entity Relationship Diagram |
| Version | 1.0 |
| Owner | Data Architecture Team |

---

# Purpose

This document defines the logical Entity Relationship (ER) model for the AI Career Intelligence Platform.

The data model is designed using relational database principles while supporting AI workloads, vector search, auditability, and future enterprise scalability.

---

# Design Principles

The ER model follows these principles:

- Normalize transactional data (3NF)
- Maintain referential integrity
- Separate business domains
- Support auditability
- Enable AI metadata storage
- Minimize data duplication
- Optimize for scalability

---

# Business Domains

The database is divided into the following domains:

| Domain | Description |
|---------|-------------|
| Identity | Users, Roles, Sessions |
| Resume | Resume management and analysis |
| Jobs | Jobs and applications |
| Companies | Company information |
| AI | Agents, prompts, evaluations |
| Knowledge | RAG documents and embeddings |
| Notifications | Alerts and emails |
| Audit | Logs and activity tracking |

---

# High-Level ER Diagram

```text
                                    +----------------+
                                    |     USERS      |
                                    +----------------+
                                            |
               +----------------------------+-----------------------------+
               |                            |                             |
               ▼                            ▼                             ▼
       +---------------+          +----------------+           +------------------+
       | USER_PROFILE  |          | USER_SESSION   |           | USER_PREFERENCES |
       +---------------+          +----------------+           +------------------+

                                            |
                                            ▼

                                    +----------------+
                                    |    RESUMES     |
                                    +----------------+
                                            |
                      +---------------------+----------------------+
                      |                     |                      |
                      ▼                     ▼                      ▼
           +------------------+   +-------------------+   +------------------+
           | RESUME_VERSION   |   | RESUME_ANALYSIS   |   | RESUME_SKILLS    |
           +------------------+   +-------------------+   +------------------+

                                            |
                                            ▼

                                  +----------------------+
                                  | JOB_MATCH_RESULTS    |
                                  +----------------------+

                                            |
                                            ▼

                                    +----------------+
                                    |      JOBS      |
                                    +----------------+
                                            |
                      +---------------------+----------------------+
                      |                     |                      |
                      ▼                     ▼                      ▼
            +------------------+   +----------------+   +------------------+
            | APPLICATIONS     |   | SAVED_JOBS     |   | JOB_BOOKMARKS    |
            +------------------+   +----------------+   +------------------+

                                            |
                                            ▼

                                   +------------------+
                                   |   COMPANIES      |
                                   +------------------+
                                            |
                      +---------------------+----------------------+
                      |                     |                      |
                      ▼                     ▼                      ▼
           +------------------+   +------------------+   +------------------+
           | COMPANY_TECH     |   | COMPANY_REVIEWS  |   | HIRING_TRENDS    |
           +------------------+   +------------------+   +------------------+

                                            |
                                            ▼

                                   +------------------+
                                   | KNOWLEDGE_DOCS   |
                                   +------------------+
                                            |
                                            ▼
                                   +------------------+
                                   | DOCUMENT_CHUNKS  |
                                   +------------------+
                                            |
                                            ▼
                                   +------------------+
                                   |   EMBEDDINGS     |
                                   +------------------+

                                            |
                                            ▼

                                  +-------------------+
                                  |   AI_AGENT_RUNS   |
                                  +-------------------+
                                            |
                      +---------------------+----------------------+
                      |                     |                      |
                      ▼                     ▼                      ▼
              +---------------+    +----------------+    +----------------+
              | AI_PROMPTS    |    | AI_EVALUATION  |    | TOOL_EXECUTION |
              +---------------+    +----------------+    +----------------+

                                            |
                                            ▼

                                   +------------------+
                                   | NOTIFICATIONS    |
                                   +------------------+

                                            |
                                            ▼

                                   +------------------+
                                   | AUDIT_LOGS       |
                                   +------------------+
```

---

# Core Entities

## Identity Domain

### USERS

Stores authentication and account information.

Relationships

- One User → One Profile
- One User → Many Sessions
- One User → Many Resumes
- One User → Many Applications
- One User → Many Notifications

---

### USER_PROFILE

Stores personal profile information.

Relationship

- One-to-One with USERS

---

### USER_SESSION

Stores active login sessions.

Relationship

- Many Sessions → One User

---

### USER_PREFERENCES

Stores user-specific preferences.

Examples

- Preferred country
- Preferred job role
- Preferred salary range
- Notification settings

---

# Resume Domain

### RESUMES

Stores uploaded resumes.

Relationships

- Many Resumes → One User
- One Resume → Many Versions
- One Resume → One Analysis
- One Resume → Many Skills

---

### RESUME_VERSION

Tracks version history of resumes.

Relationship

- Many Versions → One Resume

---

### RESUME_ANALYSIS

Stores AI-generated resume insights.

Examples

- ATS Score
- Missing Skills
- Improvement Suggestions

---

### RESUME_SKILLS

Stores extracted skills.

Relationship

- Many Skills → One Resume

---

# Job Domain

### JOBS

Stores job postings.

Relationships

- One Job → Many Applications
- One Job → Many Match Results

---

### APPLICATIONS

Tracks user job applications.

Relationship

- Many Applications → One User
- Many Applications → One Job

---

### SAVED_JOBS

Stores jobs saved by users.

Relationship

- Many Saved Jobs → One User

---

### JOB_MATCH_RESULTS

Stores AI matching results.

Relationship

- One Resume
- One Job

Produces

- Match Score
- Skill Gap
- Recommendations

---

# Company Domain

### COMPANIES

Stores company information.

Relationships

- One Company → Many Jobs
- One Company → Many Reviews
- One Company → Many Hiring Trends

---

### COMPANY_TECH

Stores technology stack.

Relationship

- Many Technologies → One Company

---

### COMPANY_REVIEWS

Stores company insights.

---

### HIRING_TRENDS

Stores AI-generated hiring trends.

---

# Knowledge Domain

### KNOWLEDGE_DOCS

Stores RAG source documents.

Relationships

- One Document → Many Chunks

---

### DOCUMENT_CHUNKS

Stores processed document chunks.

Relationship

- Many Chunks → One Document

---

### EMBEDDINGS

Stores vector embeddings.

Relationship

- One Chunk → One Embedding

Technology

- pgvector

---

# AI Domain

### AI_PROMPTS

Stores versioned prompts.

Relationship

- One Prompt → Many Agent Runs

---

### AI_AGENT_RUNS

Stores every AI execution.

Contains

- Model
- Prompt Version
- Token Usage
- Latency
- Status

---

### AI_EVALUATION

Stores evaluation metrics.

Examples

- Accuracy
- Hallucination
- Latency
- Cost

---

### TOOL_EXECUTION

Stores tool invocation history.

---

# Notification Domain

### NOTIFICATIONS

Stores:

- Email notifications
- In-app notifications
- Reminder notifications

---

# Audit Domain

### AUDIT_LOGS

Stores:

- User activity
- Login history
- Security events
- AI actions
- Administrative actions

---

# Relationship Summary

| Parent | Child | Cardinality |
|----------|-------|-------------|
| User | Profile | 1 : 1 |
| User | Resume | 1 : N |
| Resume | Resume Version | 1 : N |
| Resume | Resume Analysis | 1 : 1 |
| Resume | Resume Skills | 1 : N |
| Resume | Job Match | 1 : N |
| Job | Application | 1 : N |
| Company | Job | 1 : N |
| Company | Hiring Trends | 1 : N |
| Knowledge Document | Chunk | 1 : N |
| Chunk | Embedding | 1 : 1 |
| Prompt | Agent Run | 1 : N |
| User | Notification | 1 : N |
| User | Audit Log | 1 : N |

---

# Naming Conventions

Tables

- Singular business concepts represented as plural table names.
- Snake_case naming convention.

Primary Keys

- id (UUID)

Foreign Keys

- <entity>_id

Indexes

- idx_<table>_<column>

Unique Constraints

- uq_<table>_<column>

---

# Future Extensions

The model is designed to support:

- Recruiter Portal
- Team Collaboration
- Subscription Billing
- Interview Scheduling
- AI Memory
- Multi-language Resumes
- Multi-tenancy
- Analytics Warehouse

---

# Dependencies

Depends on:

- Database Strategy
- Architecture Documents

Used by:

- SQLAlchemy Models
- Alembic Migrations
- API Design
- Backend Services
- AI Platform

---

# Related Documents

- 01_Database_Strategy.md
- 03_Data_Dictionary.md
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