# Sequence Diagrams

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | Sequence Diagrams               |
| Version  | 1.0                             |
| Owner    | Solution Architecture Team      |

---

# Purpose

This document describes the runtime behavior of the AI Career Intelligence Platform using sequence diagrams.

These diagrams illustrate how users, frontend components, backend services, AI agents, databases, and external services interact to fulfill business requests.

The diagrams serve as implementation references for backend, frontend, AI, QA, and DevOps teams.

---

# Sequence Diagram Standards

Participants

* User
* Browser
* Frontend (Next.js)
* FastAPI Backend
* Business Service
* AI Orchestrator
* AI Agent
* RAG Engine
* PostgreSQL
* Redis
* OpenAI
* Object Storage

---

# SD-01 User Registration

```text
User
 │
 ▼
Frontend
 │
 ▼
POST /auth/register
 │
 ▼
Auth Service
 │
 ▼
Validate Input
 │
 ▼
Hash Password
 │
 ▼
PostgreSQL
 │
 ▼
Create User
 │
 ▼
Email Service
 │
 ▼
Verification Email
 │
 ▼
Success Response
```

---

# SD-02 User Login

```text
User
 │
 ▼
Frontend
 │
 ▼
POST /auth/login
 │
 ▼
Auth Service
 │
 ▼
Validate Credentials
 │
 ▼
PostgreSQL
 │
 ▼
Generate JWT
 │
 ▼
Return Access Token
 │
 ▼
Frontend Stores Token
```

---

# SD-03 Resume Upload

```text
User
 │
 ▼
Frontend
 │
 ▼
Upload Resume
 │
 ▼
Backend API
 │
 ▼
Validate File
 │
 ▼
Object Storage
 │
 ▼
Save File
 │
 ▼
Resume Service
 │
 ▼
Create Resume Record
 │
 ▼
PostgreSQL
 │
 ▼
Success Response
```

---

# SD-04 Resume AI Analysis

```text
User
 │
 ▼
Frontend
 │
 ▼
Analyze Resume
 │
 ▼
Backend
 │
 ▼
AI Orchestrator
 │
 ▼
Resume Agent
 │
 ▼
RAG Engine
 │
 ▼
Retrieve Context
 │
 ▼
OpenAI Responses API
 │
 ▼
Structured Analysis
 │
 ▼
Store Analysis
 │
 ▼
Dashboard
```

---

# SD-05 Job Search

```text
User
 │
 ▼
Frontend
 │
 ▼
Search Jobs
 │
 ▼
Job Service
 │
 ▼
PostgreSQL
 │
 ▼
Return Matching Jobs
 │
 ▼
Frontend
```

---

# SD-06 Resume Tailoring

```text
User
 │
 ▼
Frontend
 │
 ▼
Select Resume + Job
 │
 ▼
AI Orchestrator
 │
 ▼
Resume Agent
 │
 ▼
Job Agent
 │
 ▼
RAG Engine
 │
 ▼
OpenAI
 │
 ▼
Tailored Resume
 │
 ▼
Store Version
 │
 ▼
Return Updated Resume
```

---

# SD-07 Company Intelligence

```text
User
 │
 ▼
Frontend
 │
 ▼
Search Company
 │
 ▼
Company Service
 │
 ▼
Company Agent
 │
 ▼
RAG Engine
 │
 ▼
OpenAI
 │
 ▼
Company Insights
 │
 ▼
Frontend
```

---

# SD-08 Job Match Analysis

```text
User
 │
 ▼
Frontend
 │
 ▼
Match Resume
 │
 ▼
Matching Service
 │
 ▼
Resume Agent
 │
 ▼
Job Agent
 │
 ▼
AI Scoring
 │
 ▼
Match Score
 │
 ▼
Recommendations
```

---

# SD-09 Application Tracking

```text
User
 │
 ▼
Frontend
 │
 ▼
Create Application
 │
 ▼
Application Service
 │
 ▼
PostgreSQL
 │
 ▼
Application Tracker Agent
 │
 ▼
Schedule Reminder
 │
 ▼
Redis Queue
 │
 ▼
Notification Service
```

---

# SD-10 Multi-Agent Workflow

```text
User Request
 │
 ▼
AI Orchestrator
 │
 ├─────────────► Resume Agent
 │
 ├─────────────► Job Agent
 │
 ├─────────────► Company Agent
 │
 ├─────────────► Career Agent
 │
 ▼
Aggregate Results
 │
 ▼
Return Final Response
```

---

# SD-11 RAG Retrieval Flow

```text
AI Agent
 │
 ▼
Retriever
 │
 ▼
Metadata Filter
 │
 ▼
Semantic Search
 │
 ▼
Keyword Search
 │
 ▼
Merge Results
 │
 ▼
Context Builder
 │
 ▼
OpenAI Responses API
 │
 ▼
Final Answer
```

---

# SD-12 Background Resume Processing

```text
Resume Upload
 │
 ▼
Redis Queue
 │
 ▼
Celery Worker
 │
 ▼
Resume Parser
 │
 ▼
Embedding Generator
 │
 ▼
Vector Store
 │
 ▼
Update Resume Status
```

---

# Error Handling Pattern

For all runtime flows:

1. Validate Request
2. Authenticate User
3. Authorize Access
4. Execute Business Logic
5. Handle Exceptions
6. Log Events
7. Return Standardized Response

---

# Design Principles

Every sequence follows:

* Authentication before business logic
* Validation before persistence
* Structured error handling
* AI orchestration through LangGraph
* Database access via repositories
* Standard API responses

---

# Future Sequence Diagrams

Additional runtime flows will include:

* Interview Coach Session
* Visa Recommendation
* Career Roadmap Generation
* Password Reset
* Notification Delivery
* Recruiter Portal
* Admin Workflows
* Subscription Management

---

# Dependencies

Depends on

* C4 Component Diagram
* AI Architecture
* Agent Architecture
* API Architecture

Used by

* Backend Development
* Frontend Development
* QA Automation
* Technical Documentation

---

# Related Documents

* AI Architecture
* RAG Architecture
* Agent Architecture
* API Architecture

---

# Approval

| Role                     | Name        | Status  |
| ------------------------ | ----------- | ------- |
| Product Owner            | Ashok Karre | Pending |
| Chief Solution Architect | Ashok Karre | Pending |
| Technical Lead           | TBD         | Pending |
| Engineering Lead         | TBD         | Pending |
