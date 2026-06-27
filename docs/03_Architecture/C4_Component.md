# C4 Model – Level 3: Component Diagram

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | C4 Level 3 – Component Diagram  |
| Version  | 1.0                             |
| Owner    | Solution Architecture           |

---

# Purpose

This document defines the major software components within the AI Career Intelligence Platform.

Unlike the Container Diagram, this document focuses on the internal components of the FastAPI backend and how they collaborate to deliver business functionality.

This document serves as the implementation blueprint for backend development.

---

# Component Architecture Overview

```text
                              FastAPI Backend

┌────────────────────────────────────────────────────────────────────┐
│                         API Controllers                            │
└────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌────────────────────────────────────────────────────────────────────┐
│                        Business Services                           │
└────────────────────────────────────────────────────────────────────┘
                              │
          ┌─────────────┬──────────────┬──────────────┐
          ▼             ▼              ▼              ▼
 Authentication   Resume Service   Job Service   Company Service
          │             │              │              │
          ▼             ▼              ▼              ▼
      AI Orchestrator   Dashboard Service   Application Service
                              │
                              ▼
                    Repository Layer
                              │
                              ▼
                 PostgreSQL + pgvector
```

---

# Backend Components

## 1. Authentication Component

### Responsibilities

* User Registration
* Login
* Logout
* JWT Token Generation
* Refresh Tokens
* Password Reset
* Email Verification

### APIs

```
POST /auth/register
POST /auth/login
POST /auth/logout
POST /auth/refresh
POST /auth/forgot-password
```

---

## 2. User Profile Component

### Responsibilities

* User Profile Management
* Skills
* Education
* Experience
* Preferences

### APIs

```
GET /users/profile
PUT /users/profile
```

---

## 3. Resume Component

### Responsibilities

* Upload Resume
* Download Resume
* Resume Parsing
* Resume Versioning
* Resume Preview

### APIs

```
POST /resumes/upload
GET /resumes
GET /resumes/{id}
DELETE /resumes/{id}
```

---

## 4. Resume Intelligence Component

### Responsibilities

* Resume Analysis
* ATS Scoring
* Resume Tailoring
* Keyword Extraction
* Resume Suggestions

Depends on:

* Resume Agent
* RAG Engine
* OpenAI

---

## 5. Job Search Component

### Responsibilities

* Job Search
* Job Filtering
* Saved Jobs
* Job Details
* Search History

### APIs

```
GET /jobs
GET /jobs/search
POST /jobs/save
```

---

## 6. Job Matching Component

### Responsibilities

* Resume Matching
* Skill Matching
* Match Score
* Missing Skills
* Recommendations

Depends on:

* Resume Agent
* Job Agent

---

## 7. Company Intelligence Component

### Responsibilities

* Company Search
* Company Profile
* Hiring Trends
* Technology Stack
* Visa Sponsorship Insights

---

## 8. Application Tracker Component

### Responsibilities

* Track Applications
* Update Status
* Notes
* Interview Tracking
* Offer Tracking

---

## 9. Dashboard Component

### Responsibilities

* User Metrics
* Resume Statistics
* Application Statistics
* AI Recommendations
* Recent Activity

---

## 10. AI Orchestrator Component

### Technology

* LangGraph

### Responsibilities

* Route AI Requests
* Manage Agent Workflows
* Tool Calling
* Context Management
* Retry Logic

---

# AI Components

## Resume Agent

Responsibilities

* Resume Parsing
* ATS Score
* Resume Tailoring

---

## Job Search Agent

Responsibilities

* Job Ranking
* Semantic Search
* Recommendation

---

## Company Intelligence Agent

Responsibilities

* Company Analysis
* Hiring Trends
* Company Summaries

---

## Career Coach Agent

Responsibilities

* Skill Gap Analysis
* Career Advice
* Learning Roadmap

---

## Interview Coach Agent (Future)

Responsibilities

* Mock Interviews
* Question Generation
* Feedback

---

## Visa Intelligence Agent (Future)

Responsibilities

* Visa Rules
* Sponsorship Guidance
* Immigration Information

---

# Shared Components

## RAG Engine

Responsibilities

* Document Retrieval
* Context Building
* Metadata Filtering
* Semantic Search

---

## Prompt Manager

Responsibilities

* Prompt Templates
* Prompt Versioning
* Dynamic Prompt Assembly

---

## Embedding Service

Responsibilities

* Generate Embeddings
* Update Vector Store
* Similarity Search

---

## Notification Service

Responsibilities

* Email Notifications
* In-App Notifications
* Reminders

---

## Audit Logging

Responsibilities

* User Activity Logs
* AI Request Logs
* Security Events

---

# Repository Components

Repositories encapsulate all persistence logic.

```
UserRepository

ResumeRepository

JobRepository

CompanyRepository

ApplicationRepository

EmbeddingRepository

AuditRepository
```

---

# Component Communication

```
Frontend

↓

API Controller

↓

Business Service

↓

AI Orchestrator

↓

AI Agent

↓

RAG Engine

↓

Repository

↓

Database
```

---

# Component Dependencies

| Component       | Depends On                        |
| --------------- | --------------------------------- |
| Resume Service  | Resume Repository, Resume Agent   |
| Job Service     | Job Repository, Job Agent         |
| Company Service | Company Repository, Company Agent |
| Dashboard       | Multiple Services                 |
| AI Orchestrator | All AI Agents                     |
| RAG Engine      | pgvector, Embedding Service       |

---

# Design Principles

All components follow:

* Single Responsibility Principle
* Dependency Injection
* Loose Coupling
* High Cohesion
* Interface Segregation
* Open/Closed Principle

---

# Future Components

The architecture supports adding:

* Recruiter Portal
* University Portal
* Billing Service
* Subscription Service
* Analytics Service
* Recommendation Engine
* Workflow Engine
* Admin Console

without redesigning existing components.

---

# Dependencies

Depends on:

* C4 Context
* C4 Container
* High Level Architecture
* Low Level Architecture

Used by:

* AI Architecture
* API Architecture
* Database Architecture
* Development Team

---

# Related Documents

* 08_AI_Architecture.md
* 09_RAG_Architecture.md
* 10_Agent_Architecture.md

---

# Approval

| Role               | Name        | Status  |
| ------------------ | ----------- | ------- |
| Product Owner      | Ashok Karre | Pending |
| Solution Architect | Ashok Karre | Pending |
| Technical Lead     | TBD         | Pending |
| Engineering Lead   | TBD         | Pending |
