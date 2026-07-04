# AI Career Intelligence Platform - AI Development Guide

> Read this document completely before implementing any feature.
> This document is the single source of truth for the project.

---

# Project Overview

Project Name:
AI Career Intelligence Platform

Goal:

Build a production-ready AI-powered Career Intelligence Platform that helps users:

- Upload resumes
- AI Resume Analysis
- ATS Score
- Resume Recommendations
- Job Matching
- Company Intelligence
- Career Roadmaps
- Interview Preparation

This is NOT a demo project.

Every implementation must be production-ready.

---

# Development Methodology

We follow Agile Scrum.

Development is done story-by-story from Jira.

Every implementation must satisfy the acceptance criteria of the current Jira story.

Never implement future stories unless explicitly requested.

---

# Technology Stack (LOCKED)

## Frontend

- Next.js 15
- React 19
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- Zustand
- React Hook Form
- Zod

## Backend

- Python 3.13+
- FastAPI
- SQLAlchemy 2.x
- Alembic
- Pydantic v2
- Redis
- Celery

## AI

- LangGraph
- LangChain
- OpenAI Responses API
- OpenAI text-embedding-3-large

## Database

- PostgreSQL 17
- pgvector

## Storage

Development

- MinIO

Production

- Amazon S3

## Infrastructure

- Docker
- Docker Compose
- GitHub Actions
- Nginx

Do NOT introduce new technologies unless explicitly instructed.

---

# Project Architecture

Follow Clean Architecture.

API

↓

Service

↓

Repository

↓

Database

Business logic belongs ONLY inside Services.

Repositories ONLY communicate with the database.

API routes should be thin.

Never bypass the service layer.

---

# Backend Folder Structure

backend/app/

api/
core/
db/
models/
schemas/
repositories/
services/
agents/
prompts/
rag/
embeddings/
vectorstore/
middleware/
utils/
exceptions/
main.py

Never create additional folders without approval.

---

# Frontend Structure

frontend/src/

app/
components/
layouts/
hooks/
services/
store/
context/
types/
utils/

Keep components reusable.

Separate business logic from UI.

---

# Coding Standards

Always:

- Use Type Hints
- Follow PEP8
- Use async where appropriate
- Write readable code
- Prefer composition over inheritance
- Keep functions small
- Use dependency injection
- Write meaningful variable names

Never:

- Write placeholder code
- Leave TODO comments
- Hardcode secrets
- Ignore errors
- Duplicate business logic

---

# API Standards

All APIs must:

- Follow REST conventions
- Use JSON
- Return proper HTTP status codes
- Validate input using Pydantic
- Return consistent response models
- Handle exceptions gracefully

---

# Database Standards

Use SQLAlchemy ORM.

Never use raw SQL unless approved.

Every model should have:

- UUID primary key
- created_at
- updated_at

Use Alembic for every schema change.

Never modify the database manually.

---

# AI Standards

Use:

- LangGraph for agent orchestration
- LangChain for utilities
- OpenAI Responses API for LLM
- OpenAI Embeddings for RAG

AI agents must be modular and reusable.

Never hardcode prompts inside business logic.

Store prompts separately.

---

# Security Standards

Always:

- Hash passwords using bcrypt
- Use JWT authentication
- Validate every request
- Sanitize user input
- Protect sensitive endpoints
- Store secrets in environment variables

Never expose secrets or API keys.

---

# Logging

Log:

- Application startup
- Errors
- AI requests
- Background jobs
- Authentication events

Never log passwords, tokens, or sensitive user data.

---

# Testing

Every feature should include:

- Unit Tests
- API Tests

Before completing a story:

- Ensure tests pass.
- Ensure the application runs without errors.

---

# Git Workflow

Branch naming:

feature/<story-name>

Example:

feature/auth-registration

Commit format:

feat(auth): implement registration API

fix(resume): fix upload validation

docs(api): update authentication docs

One Jira Story = One Git Commit (or a small logical set of commits)

---

# Development Workflow

For every Jira Story:

1. Understand the story.
2. Review acceptance criteria.
3. Identify impacted files.
4. Implement backend.
5. Implement frontend (if applicable).
6. Write tests.
7. Run tests.
8. Review code quality.
9. Commit changes.
10. Move to the next story.

Never implement multiple unrelated stories together.

---

# Performance Goals

Standard APIs

< 200 ms

AI APIs

< 5 seconds

Avoid unnecessary database queries.

Optimize expensive operations.

---

# Code Review Checklist

Before considering a story complete:

- Code compiles.
- Tests pass.
- No linting issues.
- No duplicated logic.
- Proper error handling.
- Logging added where appropriate.
- Documentation updated if needed.
- Matches existing architecture.

---

# AI Coding Assistant Rules

As an AI coding assistant:

- Read the current Jira story carefully.
- Implement ONLY the requested story.
- Respect the project architecture.
- Reuse existing code whenever possible.
- Do not introduce unnecessary libraries.
- Ask for clarification if requirements are ambiguous.
- Prefer maintainability over clever solutions.
- Generate production-quality code.

If multiple implementation options exist, choose the simplest solution that satisfies the requirements.

---

# Project Goal

The objective is to build a maintainable, scalable, enterprise-quality AI Career Intelligence Platform.

Every code change should move the project closer to that goal while maintaining high engineering standards.