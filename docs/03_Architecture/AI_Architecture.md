# AI Architecture

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | AI Architecture |
| Version | 1.0 |
| Owner | AI Architecture Team |

---

# Purpose

This document defines the Artificial Intelligence Architecture for the AI Career Intelligence Platform.

The platform is designed as an **Enterprise AI Agent System**, where multiple specialized AI agents collaborate through a central orchestration layer to deliver intelligent career guidance.

The architecture emphasizes:

- Multi-Agent Design
- Retrieval-Augmented Generation (RAG)
- Tool Calling
- Context Awareness
- Structured Outputs
- Agent Collaboration
- Enterprise Scalability

---

# AI Vision

The AI platform should function as an intelligent career assistant capable of:

- Understanding user profiles
- Analyzing resumes
- Discovering relevant jobs
- Matching resumes to jobs
- Researching companies
- Coaching interview preparation
- Planning career growth
- Providing personalized recommendations

---

# AI Architecture Overview

```
                        User

                          │

                          ▼

                 FastAPI Backend

                          │

                          ▼

               AI Orchestrator (LangGraph)

                          │

 ┌──────────────┬──────────────┬──────────────┬──────────────┐
 ▼              ▼              ▼              ▼              ▼

Resume      Job Search    Company      Interview      Career
 Agent         Agent        Agent          Agent         Agent

                          │

                          ▼

                  Shared Tool Layer

                          │

          ┌───────────────┬───────────────┬──────────────┐

          ▼               ▼               ▼

        RAG          Database        External APIs

                          │

                          ▼

                   OpenAI Responses API
```

---

# AI Design Principles

The AI platform follows these principles:

- AI First
- Agent Based
- Stateless Execution
- Tool Driven
- Context Aware
- Retrieval Enhanced
- Modular
- Explainable
- Observable

---

# AI Layers

## Layer 1 – User Interaction

Responsibilities

- Receive user requests
- Maintain conversation context
- Validate input

---

## Layer 2 – AI Orchestrator

Technology

- LangGraph

Responsibilities

- Route requests
- Select appropriate agents
- Coordinate workflows
- Execute tools
- Handle retries
- Aggregate responses

---

## Layer 3 – Specialized Agents

The platform consists of domain-specific agents.

---

### Resume Agent

Responsibilities

- Resume parsing
- Resume analysis
- ATS scoring
- Resume tailoring
- Resume rewriting
- Skill extraction

Inputs

- Resume
- Job Description

Outputs

- ATS Score
- Resume Suggestions
- Tailored Resume

---

### Job Search Agent

Responsibilities

- Search jobs
- Rank jobs
- Filter jobs
- Recommend jobs
- Detect duplicates

Inputs

- Skills
- Country
- Experience

Outputs

- Ranked Job List

---

### Company Intelligence Agent

Responsibilities

- Company overview
- Technology stack
- Hiring trends
- Visa sponsorship insights
- Company culture summary

---

### Career Coach Agent

Responsibilities

- Career planning
- Skill gap analysis
- Certification recommendations
- Learning roadmap

---

### Interview Coach Agent (Phase 2)

Responsibilities

- Technical interviews
- Behavioral interviews
- Mock interviews
- AI feedback

---

### Visa Intelligence Agent (Phase 2)

Responsibilities

- Visa rules
- Country requirements
- Sponsorship guidance

---

### Application Tracker Agent

Responsibilities

- Track application lifecycle
- Generate reminders
- Recommend follow-ups

---

# AI Orchestrator

Technology

- LangGraph

Responsibilities

- Request routing
- Workflow execution
- Agent collaboration
- Tool execution
- State management
- Error recovery

---

# Shared AI Services

## Prompt Manager

Responsibilities

- Prompt templates
- Prompt versioning
- Dynamic prompt generation
- Prompt testing

---

## Context Manager

Responsibilities

- Conversation context
- User profile context
- Resume context
- Job context

---

## Memory Manager (Future)

Responsibilities

- Long-term memory
- User preferences
- AI memory
- Session history

---

## Tool Registry

Central registry for AI tools.

Example tools:

- Resume Parser
- Job Search
- Company Lookup
- ATS Calculator
- Embedding Generator
- Resume Exporter
- Notification Sender

---

# AI Workflow

Example:

```
User uploads resume

↓

Resume Agent

↓

RAG Retrieval

↓

OpenAI

↓

Resume Analysis

↓

Dashboard
```

---

# AI Communication

```
User

↓

Frontend

↓

FastAPI

↓

LangGraph

↓

Agent

↓

Tool

↓

RAG

↓

OpenAI

↓

Response
```

---

# AI Guardrails

The AI system shall implement:

- Prompt validation
- Input sanitization
- Output validation
- Hallucination reduction
- Rate limiting
- Toxicity detection
- Secure tool execution

---

# Structured Outputs

All AI responses should use structured JSON.

Example

```json
{
  "summary": "...",
  "ats_score": 91,
  "missing_skills": [],
  "recommendations": []
}
```

---

# Error Handling

If an AI request fails:

- Retry once
- Fallback prompt
- Log error
- Notify monitoring
- Return graceful message

---

# AI Observability

Capture:

- Agent execution time
- Tool latency
- Token usage
- Model usage
- Prompt version
- Success rate
- Failure rate

---

# Future Enhancements

- Planner Agent
- Reflection Agent
- Multi-Agent Collaboration
- Human-in-the-Loop
- Autonomous Workflows
- Self-Improving Prompts

---

# Dependencies

Depends on:

- Architecture Principles
- Technology Stack
- C4 Component Diagram

Used by:

- RAG Architecture
- Agent Architecture
- API Design
- Backend Implementation

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief AI Architect | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Technical Lead | TBD | Pending |