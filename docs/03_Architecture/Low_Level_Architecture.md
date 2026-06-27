# Low Level Architecture (LLA)

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | Low Level Architecture          |
| Version  | 1.0                             |
| Owner    | Solution Architecture           |

---

# Purpose

This document defines the internal implementation architecture of the AI Career Intelligence Platform. It describes the package structure, module interactions, service responsibilities, design patterns, and data flow within the application.

This document serves as the implementation blueprint for developers.

---

# Backend Package Structure

```text
backend/
└── app/
    ├── api/
    ├── core/
    ├── db/
    ├── models/
    ├── schemas/
    ├── repositories/
    ├── services/
    ├── agents/
    ├── rag/
    ├── prompts/
    ├── embeddings/
    ├── vectorstore/
    ├── middleware/
    ├── exceptions/
    ├── utils/
    └── main.py
```

---

# Layered Architecture

```text
Client
   │
   ▼
API Layer
   │
   ▼
Service Layer
   │
   ▼
Repository Layer
   │
   ▼
Database
```

Business logic must exist only in the **Service Layer**.

---

# API Layer

### Responsibilities

* HTTP Request Handling
* Input Validation
* Authentication
* Authorization
* Response Formatting
* Exception Handling

### Modules

```text
api/

auth/

users/

resumes/

jobs/

companies/

dashboard/

applications/

ai/

health/
```

---

# Service Layer

The Service Layer contains all business logic.

### Modules

```text
services/

auth/

resume/

jobs/

company/

dashboard/

application/

ai/
```

Responsibilities:

* Business rules
* Workflow orchestration
* Transaction management
* AI service invocation
* Repository coordination

---

# Repository Layer

Repositories encapsulate database access.

Responsibilities:

* CRUD operations
* Query optimization
* Database abstraction

Example:

```text
UserRepository

ResumeRepository

JobRepository

CompanyRepository

ApplicationRepository
```

---

# Domain Models

Primary entities include:

* User
* Resume
* ResumeVersion
* Job
* Company
* Application
* Skill
* Country
* Notification

Each model corresponds to a database table and uses SQLAlchemy ORM.

---

# AI Module Structure

```text
agents/

resume_agent/

job_search_agent/

company_agent/

career_agent/

interview_agent/

visa_agent/

notification_agent/
```

Each agent contains:

* Prompt templates
* Tool definitions
* Workflow logic
* Output parsers

---

# RAG Module

```text
rag/

loader.py

chunker.py

embedder.py

retriever.py

reranker.py

context_builder.py
```

Responsibilities:

* Load documents
* Chunk content
* Generate embeddings
* Retrieve relevant context
* Build prompts for LLMs

---

# Prompt Management

```text
prompts/

resume/

job/

company/

interview/

career/
```

Prompt files should be version-controlled and reusable.

---

# Vector Store

Responsibilities:

* Store embeddings
* Similarity search
* Metadata filtering

Technology:

* PostgreSQL
* pgvector

---

# Middleware

Responsibilities:

* JWT validation
* Logging
* Request tracing
* Rate limiting
* CORS

---

# Exception Handling

Centralized exception management for:

* Validation errors
* Authentication failures
* Authorization failures
* AI service errors
* Database errors
* External API failures

---

# Utility Layer

Shared utilities include:

* Date helpers
* File utilities
* Configuration
* Constants
* Encryption
* Validators

---

# Frontend Structure

```text
frontend/

src/

app/

pages/

components/

layouts/

hooks/

services/

store/

context/

styles/

types/

utils/

constants/
```

---

# Frontend Component Hierarchy

```text
App

↓

Layout

↓

Page

↓

Feature Components

↓

Shared Components

↓

API Services
```

---

# Communication Flow

```text
Frontend

↓

FastAPI API

↓

Business Service

↓

AI Orchestrator

↓

AI Agent

↓

Retriever

↓

Database

↓

LLM

↓

Response
```

---

# Design Patterns

The following design patterns are used:

* Layered Architecture
* Repository Pattern
* Service Pattern
* Dependency Injection
* Factory Pattern
* Strategy Pattern
* Adapter Pattern
* Builder Pattern
* Agent Pattern

---

# Coding Standards

* SOLID Principles
* Clean Architecture
* DRY
* KISS
* PEP 8
* Type Hints
* REST Naming Standards

---

# Module Dependencies

```text
API

↓

Services

↓

Repositories

↓

Database
```

AI modules communicate with Services through defined interfaces.

Repositories must never call AI modules directly.

---

# Future Extensions

The architecture supports future additions such as:

* Recruiter Portal
* University Portal
* Mobile API
* GraphQL API
* Event Bus
* Microservices
* AI Marketplace

without significant redesign.

---

# Dependencies

Depends on:

* Architecture Principles
* Technology Stack
* High Level Architecture

Used by:

* Database Architecture
* API Architecture
* AI Architecture
* Development Team
* Testing Team

---

# Approval

| Role               | Name        | Status  |
| ------------------ | ----------- | ------- |
| Product Owner      | Ashok Karre | Pending |
| Solution Architect | Ashok Karre | Pending |
| Technical Lead     | TBD         | Pending |
| Engineering Lead   | TBD         | Pending |
