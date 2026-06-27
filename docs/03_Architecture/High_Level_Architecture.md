# High Level Architecture (HLA)

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | High Level Architecture         |
| Version  | 1.0                             |
| Owner    | Solution Architecture           |

---

# Purpose

This document defines the High-Level Architecture (HLA) of the AI Career Intelligence Platform.

It describes the major system components, their responsibilities, communication flow, external integrations, and architectural layers. This document serves as the primary blueprint for engineering teams implementing the platform.

---

# Architecture Vision

The AI Career Intelligence Platform is designed as a modular, cloud-native, AI-first SaaS application.

The architecture emphasizes:

* AI-First Design
* Modular Components
* API-First Communication
* Cloud-Native Deployment
* Secure by Design
* Scalability
* Maintainability
* Extensibility

---

# High-Level System Architecture

```text
+---------------------------------------------------------------+
|                        Client Layer                            |
|---------------------------------------------------------------|
| Next.js | React | TypeScript | Material UI                    |
+------------------------------+--------------------------------+
                               |
                               v
+---------------------------------------------------------------+
|                         API Layer                             |
|---------------------------------------------------------------|
| FastAPI REST APIs | JWT Authentication | OpenAPI              |
+------------------------------+--------------------------------+
                               |
                               v
+---------------------------------------------------------------+
|                     Business Services                         |
|---------------------------------------------------------------|
| User | Resume | Jobs | Company | Dashboard | Applications     |
+------------------------------+--------------------------------+
                               |
                               v
+---------------------------------------------------------------+
|                    AI Orchestration Layer                     |
|---------------------------------------------------------------|
| LangGraph | Agent Router | Tool Calling | Workflows           |
+------------------------------+--------------------------------+
                               |
                               v
+---------------------------------------------------------------+
|                      AI Agent Layer                           |
|---------------------------------------------------------------|
| Resume | Job | Company | Career | Interview | Visa Agents     |
+------------------------------+--------------------------------+
                               |
                               v
+---------------------------------------------------------------+
|                     Retrieval (RAG) Layer                     |
|---------------------------------------------------------------|
| Retriever | Embeddings | Context Builder | Vector Search      |
+------------------------------+--------------------------------+
                               |
                               v
+---------------------------------------------------------------+
|                         Data Layer                            |
|---------------------------------------------------------------|
| PostgreSQL | pgvector | Redis | Object Storage                |
+---------------------------------------------------------------+
```

---

# Architectural Layers

## 1. Presentation Layer

### Responsibilities

* User Interface
* Authentication Screens
* Dashboard
* Resume Management
* Job Search
* Company Search
* Application Tracking

### Technology

* Next.js
* React
* TypeScript
* Material UI

---

## 2. API Layer

### Responsibilities

* REST API Endpoints
* Request Validation
* Authentication
* Authorization
* Error Handling

### Technology

* FastAPI
* JWT
* Pydantic

---

## 3. Business Services Layer

### Responsibilities

* User Management
* Resume Management
* Job Management
* Company Services
* Dashboard
* Application Tracking

Business logic resides exclusively in this layer.

---

## 4. AI Orchestration Layer

This is the heart of the platform.

Responsibilities:

* Route AI requests
*
