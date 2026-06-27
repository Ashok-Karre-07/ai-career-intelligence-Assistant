# Deployment Architecture

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Deployment Architecture |
| Version | 1.0 |
| Owner | DevOps Architecture Team |

---

# Purpose

This document defines the deployment architecture for the AI Career Intelligence Platform.

The deployment strategy is designed to support the complete software development lifecycle, from local development to enterprise production deployment. The architecture is cloud-native, containerized, scalable, secure, and automation-friendly.

---

# Deployment Objectives

The deployment platform shall:

- Support local development
- Support automated CI/CD deployments
- Minimize downtime
- Enable horizontal scaling
- Support zero-downtime deployments
- Provide disaster recovery
- Remain cloud agnostic
- Be Kubernetes-ready
- Support Infrastructure as Code

---

# Deployment Principles

The deployment architecture follows:

- Container First
- Cloud Native
- Immutable Infrastructure
- Infrastructure as Code
- Automated Deployments
- Zero Downtime
- Security by Default
- Environment Parity

---

# Deployment Environments

| Environment | Purpose |
|-------------|---------|
| Local | Developer workstation |
| Development | Shared development environment |
| QA | Functional and regression testing |
| UAT | Business validation |
| Production | Live customer environment |

---

# Environment Configuration

Configuration is managed through environment variables.

Examples

- DATABASE_URL
- REDIS_URL
- OPENAI_API_KEY
- JWT_SECRET_KEY
- SMTP_HOST
- STORAGE_PROVIDER
- STORAGE_BUCKET
- ENVIRONMENT

Each environment has its own configuration.

---

# High-Level Deployment Architecture

```text
                        Internet
                            │
                            ▼
                     HTTPS (443)
                            │
                            ▼
                    Reverse Proxy (Nginx)
                            │
            ┌───────────────┴───────────────┐
            ▼                               ▼
     Next.js Frontend                FastAPI Backend
                                             │
      ┌──────────────────────────────────────┼─────────────────────────────┐
      ▼                                      ▼                             ▼
 PostgreSQL + pgvector                  Redis Cache                 Object Storage
                                                                      (MinIO / S3)
                                             │
                                             ▼
                                   OpenAI Responses API
```

---

# Deployment Components

## Reverse Proxy

Technology

- Nginx

Responsibilities

- SSL termination
- HTTP to HTTPS redirection
- Compression
- Static asset delivery
- Security headers
- Reverse proxy
- Future load balancing

---

## Frontend

Technology

- Next.js
- React
- TypeScript

Deployment

- Docker Container

Responsibilities

- User Interface
- Authentication Screens
- Dashboard
- Resume Management
- Job Search
- Company Intelligence

---

## Backend

Technology

- FastAPI
- Python
- Uvicorn

Deployment

- Docker Container

Responsibilities

- REST APIs
- Authentication
- Authorization
- Business Logic
- AI Orchestration

---

## Database

Technology

- PostgreSQL
- pgvector

Responsibilities

- Business Data
- AI Metadata
- Vector Storage

Persistence

- Docker Volumes
- Managed Database (Production)

---

## Redis

Responsibilities

- Session Storage
- API Cache
- Background Queue
- Rate Limiting

---

## Object Storage

Development

- MinIO

Production

- AWS S3
- Azure Blob Storage
- Google Cloud Storage

Stores

- Resume Files
- Reports
- Attachments
- Generated Documents

---

## External AI Services

Current

- OpenAI Responses API
- OpenAI Embeddings API

Future

- Azure OpenAI
- Anthropic
- Google Gemini
- Local Ollama

---

# Container Architecture

```text
Docker Network

├── nginx

├── frontend

├── backend

├── postgres

├── redis

├── minio

└── celery-worker
```

Every service runs independently and communicates through the internal Docker network.

---

# Local Development

Technology

- Docker Compose

Services

- Frontend
- Backend
- PostgreSQL
- Redis
- MinIO
- Celery Worker

Command

```bash
docker compose up -d
```

Benefits

- Consistent environments
- Easy onboarding
- Minimal setup

---

# Production Deployment

Recommended Platform

- Kubernetes (Future)

Initial MVP

- Docker Compose
- Linux VM
- Ubuntu Server

Production Components

- Nginx
- Next.js
- FastAPI
- PostgreSQL
- Redis
- MinIO/S3
- Celery Worker

---

# Networking

Ports

| Service | Port |
|----------|------|
| HTTPS | 443 |
| HTTP | 80 |
| Frontend | 3000 |
| Backend | 8000 |
| PostgreSQL | 5432 |
| Redis | 6379 |
| MinIO | 9000 |

Only Nginx is exposed publicly.

All other services remain private.

---

# SSL

Technology

- Let's Encrypt (Development)
- Cloud-managed certificates (Production)

Requirements

- TLS 1.2+
- Automatic renewal
- HTTP to HTTPS redirect

---

# Storage

Persistent Volumes

- PostgreSQL Data
- Redis Persistence
- Uploaded Files
- AI Reports

Storage Policy

- Daily backups
- Encrypted storage
- Lifecycle management

---

# Background Workers

Technology

- Celery
- Redis

Responsibilities

- Resume Parsing
- Embedding Generation
- AI Analysis
- Email Notifications
- Scheduled Jobs

Workers scale independently from the backend.

---

# CI/CD Pipeline

Source Control

- GitHub

Pipeline Stages

```text
Developer Push

↓

GitHub Actions

↓

Code Quality

↓

Unit Tests

↓

Security Scan

↓

Build Docker Images

↓

Push Container Registry

↓

Deploy Environment

↓

Health Checks

↓

Deployment Complete
```

---

# Infrastructure as Code

Future

- Terraform
- Helm Charts
- Kubernetes