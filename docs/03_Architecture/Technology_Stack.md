# Technology Stack

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | Technology Stack                |
| Version  | 1.0                             |
| Owner    | Solution Architecture           |

---

# Purpose

This document defines the approved technology stack for the AI Career Intelligence Platform.

The selected technologies have been evaluated based on:

* Enterprise adoption
* Scalability
* Performance
* Community support
* AI ecosystem compatibility
* Open-source availability
* Long-term maintainability

All development must adhere to this technology stack unless an Architecture Decision Record (ADR) approves an exception.

---

# Architecture Overview

```
Frontend
      │
      ▼
FastAPI REST APIs
      │
      ▼
Business Services
      │
      ▼
AI Orchestrator (LangGraph)
      │
      ▼
LLMs + RAG + Tools
      │
      ▼
PostgreSQL + pgvector + Redis
```

---

# Frontend Stack

| Technology        | Purpose                 | Why Selected                                                |
| ----------------- | ----------------------- | ----------------------------------------------------------- |
| Next.js           | Frontend Framework      | Enterprise-ready React framework with excellent performance |
| React             | UI Library              | Industry standard for web applications                      |
| TypeScript        | Programming Language    | Strong typing, maintainability, scalability                 |
| Material UI (MUI) | UI Components           | Professional enterprise component library                   |
| TanStack Query    | Server State Management | API caching and synchronization                             |
| React Hook Form   | Forms                   | Efficient form handling and validation                      |
| Zod               | Validation              | Type-safe schema validation                                 |
| Axios             | API Client              | Reliable HTTP communication                                 |

---

# Backend Stack

| Technology   | Purpose              | Why Selected                                         |
| ------------ | -------------------- | ---------------------------------------------------- |
| Python 3.13+ | Programming Language | Best ecosystem for AI development                    |
| FastAPI      | REST API Framework   | High performance, async support, OpenAPI integration |
| Uvicorn      | ASGI Server          | Lightweight, production-ready server                 |
| Pydantic     | Validation           | Data validation and serialization                    |
| SQLAlchemy   | ORM                  | Enterprise-grade ORM                                 |
| Alembic      | Database Migrations  | Version-controlled schema management                 |

---

# AI Stack

| Technology           | Purpose             | Why Selected                                  |
| -------------------- | ------------------- | --------------------------------------------- |
| LangGraph            | Agent Orchestration | Multi-agent workflows and state management    |
| OpenAI SDK           | LLM Integration     | Unified interface for OpenAI models           |
| OpenAI Responses API | AI Reasoning        | Tool calling, structured outputs, streaming   |
| OpenAI Embeddings    | Embeddings          | High-quality semantic embeddings              |
| Ollama               | Local LLM Support   | Local model execution for development/testing |

---

# Retrieval-Augmented Generation (RAG)

| Technology        | Purpose                  |
| ----------------- | ------------------------ |
| PostgreSQL        | Metadata storage         |
| pgvector          | Vector similarity search |
| OpenAI Embeddings | Embedding generation     |
| LangGraph         | Retrieval orchestration  |

Knowledge bases include:

* Resume Knowledge Base
* Job Knowledge Base
* Company Knowledge Base
* Visa Knowledge Base
* Interview Knowledge Base
* Career Knowledge Base

---

# Database Stack

| Technology | Purpose                                |
| ---------- | -------------------------------------- |
| PostgreSQL | Primary relational database            |
| pgvector   | Vector database extension              |
| Redis      | Cache, sessions, background job broker |

---

# Authentication & Security

| Technology  | Purpose              |
| ----------- | -------------------- |
| JWT         | Authentication       |
| OAuth2      | Authentication flow  |
| Passlib     | Password hashing     |
| python-jose | JWT token management |
| HTTPS       | Secure communication |

---

# Background Processing

| Technology | Purpose                   |
| ---------- | ------------------------- |
| Celery     | Background task execution |
| Redis      | Task queue broker         |

Example background jobs:

* Resume parsing
* AI analysis
* Email notifications
* Batch imports
* Scheduled tasks

---

# Storage

| Technology    | Purpose                      |
| ------------- | ---------------------------- |
| Local Storage | Development environment      |
| MinIO         | S3-compatible object storage |
| AWS S3        | Future production storage    |

---

# Testing

| Technology            | Purpose                              |
| --------------------- | ------------------------------------ |
| Pytest                | Backend unit and integration testing |
| React Testing Library | Frontend component testing           |
| Playwright            | End-to-end browser testing           |

---

# API Documentation

| Technology | Purpose                       |
| ---------- | ----------------------------- |
| OpenAPI    | API specification             |
| Swagger UI | Interactive API documentation |

---

# Logging & Monitoring

| Technology | Purpose                        |
| ---------- | ------------------------------ |
| Loguru     | Structured application logging |
| Prometheus | Metrics collection             |
| Grafana    | Dashboards and visualization   |

---

# Containerization

| Technology     | Purpose                         |
| -------------- | ------------------------------- |
| Docker         | Application containerization    |
| Docker Compose | Local multi-service development |

---

# CI/CD

| Technology     | Purpose                                     |
| -------------- | ------------------------------------------- |
| GitHub Actions | Build, test, lint, and deployment pipelines |

Pipelines include:

* Backend CI
* Frontend CI
* Test Execution
* Docker Build
* Release Automation

---

# Deployment

| Technology       | Purpose                      |
| ---------------- | ---------------------------- |
| Nginx            | Reverse proxy                |
| Docker           | Container runtime            |
| Railway / Render | MVP cloud hosting            |
| Kubernetes       | Future enterprise deployment |

---

# Documentation

| Technology | Purpose               |
| ---------- | --------------------- |
| Markdown   | Project documentation |
| Confluence | Knowledge management  |
| Draw.io    | Architecture diagrams |

---

# Development Standards

* RESTful API design
* OpenAPI specification
* Conventional Commits
* Git Flow branching strategy
* Clean Architecture
* SOLID principles
* Twelve-Factor App methodology

---

# Approved Technology Stack Summary

| Layer              | Technology                                    |
| ------------------ | --------------------------------------------- |
| Frontend           | Next.js + React + TypeScript + MUI            |
| Backend            | FastAPI + Python                              |
| Database           | PostgreSQL + pgvector + Redis                 |
| AI                 | LangGraph + OpenAI SDK + OpenAI Responses API |
| Authentication     | JWT + OAuth2                                  |
| Background Jobs    | Celery + Redis                                |
| Containerization   | Docker                                        |
| CI/CD              | GitHub Actions                                |
| Documentation      | Markdown + Confluence                         |
| Project Management | Jira                                          |

---

# Future Technology Considerations

Potential future additions include:

* Kubernetes
* Elasticsearch
* Apache Kafka
* Temporal
* MLflow
* LangSmith
* OpenTelemetry
* Multi-region deployment

These technologies are intentionally excluded from the MVP to reduce complexity while keeping the architecture extensible.

---

# Dependencies

Depends on:

* Architecture_Principles.md
* BRD.md
* PRD.md
* Functional_Requirements.md
* Non_Functional_Requirements.md

Used by:

* High Level Architecture
* Low Level Architecture
* AI Architecture
* Deployment Architecture
* Infrastructure Design

---

# Approval

| Role               | Name        | Status  |
| ------------------ | ----------- | ------- |
| Product Owner      | Ashok Karre | Pending |
| Solution Architect | Ashok Karre | Pending |
| Technical Lead     | TBD         | Pending |
| DevOps Lead        | TBD         | Pending |
