# C4 Model - Level 1: System Context

| Version | Author      | Status | Last Updated |
| ------- | ----------- | ------ | ------------ |
| 1.0     | Ashok Karre | Draft  | June 2026    |

---

# Document Information

| Item     | Description                     |
| -------- | ------------------------------- |
| Project  | AI Career Intelligence Platform |
| Document | C4 Level 1 - System Context     |
| Version  | 1.0                             |
| Owner    | Solution Architecture           |

---

# Purpose

This document defines the **System Context** for the AI Career Intelligence Platform using the C4 Model.

The Context Diagram identifies the system, its users, and the external systems it interacts with. It provides a high-level view of the platform without exposing implementation details.

---

# Scope

This document covers:

* Primary users
* External systems
* Third-party integrations
* High-level communication
* System boundaries

---

# System Overview

The AI Career Intelligence Platform is an AI-powered SaaS application that assists users in discovering international job opportunities, optimizing resumes, preparing for interviews, researching companies, and tracking job applications.

The platform serves as the central system while integrating with external AI services, authentication providers, email services, and job information sources.

---

# Primary Actors

## Job Seeker

Primary user of the platform.

Responsibilities:

* Create an account
* Upload resumes
* Search jobs
* Tailor resumes
* Track applications
* Receive AI recommendations

---

## Recruiter (Future)

Responsibilities:

* Search candidates
* View candidate profiles
* Contact candidates
* Manage hiring pipeline

---

## Administrator

Responsibilities:

* Manage users
* Monitor platform health
* Review logs
* Configure system settings

---

# External Systems

## OpenAI Platform

Purpose:

* Language model inference
* Embedding generation
* Structured outputs
* Tool calling

Communication:

* HTTPS REST APIs

---

## Email Service

Purpose:

* Email verification
* Password reset
* Notifications

Examples:

* SendGrid
* Mailgun
* Amazon SES

---

## Object Storage

Purpose:

* Resume storage
* Generated documents
* Attachments

Development:

* Local Storage
* MinIO

Production:

* AWS S3 compatible storage

---

## Job Sources

Purpose:

* Job listings
* Company opportunities

Examples (future):

* LinkedIn
* Indeed
* Company Career Pages
* Greenhouse
* Lever

---

# System Boundary

```text
+--------------------------------------------------------------+
|            AI Career Intelligence Platform                   |
|--------------------------------------------------------------|
|                                                              |
|  - User Management                                           |
|  - Resume Intelligence                                       |
|  - Job Discovery                                             |
|  - Job Matching                                              |
|  - Company Intelligence                                      |
|  - Dashboard                                                 |
|  - Application Tracker                                       |
|  - AI Agents                                                 |
|                                                              |
+--------------------------------------------------------------+

          ▲                     ▲
          │                     │
          │                     │
    Job Seeker             Administrator

          │
          ▼

---------------------------------------------------------------
External Systems

OpenAI

Email Service

Object Storage

Job Sources
```

---

# External Communication

| Actor/System   | Interaction                        |
| -------------- | ---------------------------------- |
| Job Seeker     | Uses web application               |
| Administrator  | Manages platform                   |
| OpenAI         | AI inference and embeddings        |
| Email Service  | Verification and notifications     |
| Object Storage | Resume and document storage        |
| Job Sources    | Job retrieval (future integration) |

---

# Key Business Flows

## Resume Analysis

Job Seeker

↓

Upload Resume

↓

AI Career Intelligence Platform

↓

OpenAI

↓

Analysis Returned

↓

Dashboard Updated

---

## Job Search

Job Seeker

↓

Search Jobs

↓

Platform

↓

Internal Search Engine

↓

Results Displayed

---

## Resume Tailoring

Job Seeker

↓

Select Job

↓

Platform

↓

Resume Agent

↓

OpenAI

↓

Tailored Resume

---

# Assumptions

* Users access the platform through modern web browsers.
* AI capabilities are provided through external LLM APIs.
* Resume files are securely stored.
* Future integrations can be added without changing the core architecture.

---

# Future Integrations

The architecture supports future integration with:

* LinkedIn APIs
* ATS platforms
* Learning platforms
* Calendar providers
* Video interview platforms
* Payment gateways
* Identity providers (SSO)

---

# Related Documents

* Architecture Principles
* Technology Stack
* High Level Architecture
* Low Level Architecture

---

# Next Document

The next C4 document (Level 2) will describe the **Container Architecture**, identifying the deployable applications and services that make up the platform.

---

# Approval

| Role               | Name        | Status  |
| ------------------ | ----------- | ------- |
| Product Owner      | Ashok Karre | Pending |
| Solution Architect | Ashok Karre | Pending |
| Technical Lead     | TBD         | Pending |
| Engineering Lead   | TBD         | Pending |
