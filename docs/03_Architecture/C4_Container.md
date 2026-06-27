# C4 Model - Level 2: Container Diagram

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | C4 Level 2 - Container Diagram  |
| Version  | 1.0                             |
| Owner    | Solution Architecture           |

---

# Purpose

This document describes the major deployable containers that make up the AI Career Intelligence Platform.

Each container has a clearly defined responsibility and communicates with other containers through well-defined interfaces.

This architecture promotes modularity, scalability, and maintainability.

---

# Objectives

The container architecture should:

* Separate concerns
* Support horizontal scaling
* Enable independent deployments (future)
* Minimize coupling
* Maximize reusability
* Support cloud-native deployment

---

# Container Overview

```text
                        +--------------------------------------+
                        |          User Web Browser            |
                        +------------------+-------------------+
                                           |
                                           |
                                           ▼
+--------------------------------------------------------------------------+
|                     Frontend Container                                   |
|--------------------------------------------------------------------------|
| Next.js + React + TypeScript + Material UI                              |
+----------------------------------+---------------------------------------+
                                   |
                                   | HTTPS REST APIs
                                   ▼
+--------------------------------------------------------------------------+
|                     Backend API Container                                |
|--------------------------------------------------------------------------|
| FastAPI + SQLAlchemy + JWT + Business Services                           |
+----------------------------------+---------------------------------------+
                                   |
            +----------------------+-------------------------+
            |                      |                         |
            ▼                      ▼                         ▼
+------------------+     +------------------+     +----------------------+
| AI Orchestrator  |     | PostgreSQL DB   |     | Redis Cache          |
| LangGraph        |     | + pgvector      |     | Sessions / Tasks      |
+--------+---------+     +--------+--------+     +----------+-----------+
         |                        |                          |
         |                        |                          |
         ▼                        ▼                          ▼
+--------------------------------------------------------------------------+
|                      Object Storage                                      |
|--------------------------------------------------------------------------|
| Local Storage / MinIO / AWS S3                                           |
+--------------------------------------------------------------------------+
         |
         ▼
+--------------------------------------------------------------------------+
|                  External AI & Integration Services                      |
|--------------------------------------------------------------------------|
| OpenAI Responses API | OpenAI Embeddings | Email Service | Future APIs   |
+--------------------------------------------------------------------------+
```

---

# Container Descriptions

## 1. Frontend Container

### Technology

* Next.js
* React
* TypeScript
* Material UI

### Responsibilities

* User Interface
* Authentication Screens
* Dashboard
* Resume Management
* Job Search
* Company Search
* Application Tracker
* AI Chat Interface (Future)

### Communication

* REST API over HTTPS

---

## 2. Backend API Container

### Technology

* FastAPI
* Python
* SQLAlchemy
* Alembic
* JWT Authentication

### Responsibilities

* API Gateway
* Authentication
* Authorization
* Business Logic
* Validation
* Error Handling
* AI Request Routing

---

## 3. AI Orchestrator Container

### Technology

* LangGraph
* OpenAI SDK

### Responsibilities

* Agent orchestration
* Workflow execution
* Tool calling
* Context management
* Prompt routing
* Agent collaboration

---

## 4. PostgreSQL Container

### Technology

* PostgreSQL
* pgvector

### Responsibilities

* Relational data storage
* Vector embeddings
* Metadata storage
* Transaction management

Primary Data:

* Users
* Resumes
* Jobs
* Companies
* Applications
* Embeddings

---

## 5. Redis Container

### Responsibilities

* Session storage
* Caching
* Background task broker
* Rate limiting
* Temporary AI context

---

## 6. Object Storage Container

### Technology

* Local Storage (Development)
* MinIO (Development/Testing)
* AWS S3 (Future)

### Stores

* Resume files
* Generated resumes
* Attachments
* Reports

---

## 7. External AI Services

### OpenAI

Responsibilities

* Language model inference
* Embedding generation
* Tool execution
* Structured outputs

---

## 8. Email Service

Responsibilities

* Email verification
* Password reset
* Notifications
* Application reminders

---

# Container Communication

| Source          | Target          | Protocol              |
| --------------- | --------------- | --------------------- |
| Browser         | Frontend        | HTTPS                 |
| Frontend        | Backend API     | REST/HTTPS            |
| Backend         | AI Orchestrator | Internal Python Calls |
| Backend         | PostgreSQL      | SQL                   |
| Backend         | Redis           | TCP                   |
| Backend         | Object Storage  | S3 API / File System  |
| AI Orchestrator | OpenAI          | HTTPS                 |
| Backend         | Email Service   | HTTPS                 |

---

# Deployment Boundaries

| Container       | Deployable Independently |
| --------------- | ------------------------ |
| Frontend        | Yes                      |
| Backend         | Yes                      |
| AI Orchestrator | Future                   |
| PostgreSQL      | Yes                      |
| Redis           | Yes                      |
| Object Storage  | Yes                      |

---

# Security Considerations

* HTTPS for all external communication
* JWT authentication
* RBAC authorization
* Secrets stored in environment variables
* Database access restricted to backend
* AI services accessed only through backend

---

# Scalability Strategy

## Frontend

Horizontal scaling using multiple instances.

## Backend

Stateless APIs allow horizontal scaling.

## PostgreSQL

Read replicas (future).

## Redis

Cluster mode (future).

## AI Orchestrator

Independent scaling based on AI workload.

---

# High Availability

Future production deployment supports:

* Multiple frontend replicas
* Multiple backend replicas
* Database backup and recovery
* Redis persistence
* Load balancing
* Health checks

---

# Dependencies

Depends on:

* High Level Architecture
* Low Level Architecture
* Technology Stack

Used by:

* Deployment Architecture
* Infrastructure Design
* Kubernetes Design
* Docker Compose
* CI/CD Pipelines

---

# Related Documents

* 05_C4_Context.md
* 07_C4_Component.md
* 11_Deployment_Architecture.md

---

# Approval

| Role               | Name        | Status  |
| ------------------ | ----------- | ------- |
| Product Owner      | Ashok Karre | Pending |
| Solution Architect | Ashok Karre | Pending |
| Technical Lead     | TBD         | Pending |
| DevOps Lead        | TBD         | Pending |
