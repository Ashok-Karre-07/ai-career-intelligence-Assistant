# User Stories

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | User Stories |
| Version | 1.0 |
| Status | Draft |

---

# Purpose

This document defines the user stories for Version 1.0 of the AI Career Intelligence Platform.

Each user story follows the standard Agile format:

> As a <User>, I want <Capability>, so that <Business Value>.

These stories will later become Jira Epics, Features, Stories, and Sprint Backlog items.

---

# Epic 1 - Authentication

## US-001 User Registration

**As a** new user

**I want** to register an account

**So that** I can access the platform.

### Acceptance Criteria

- Registration form available
- Email validation
- Password validation
- User account created successfully

Priority: High

---

## US-002 User Login

**As a** registered user

**I want** to login securely

**So that** I can access my dashboard.

### Acceptance Criteria

- Valid credentials authenticate user
- Invalid credentials show error
- JWT token generated

Priority: High

---

## US-003 Forgot Password

**As a** user

**I want** to reset my password

**So that** I can regain access to my account.

Priority: High

---

# Epic 2 - User Profile

## US-011 Complete Profile

**As a** user

**I want** to maintain my professional profile

**So that** AI recommendations become personalized.

Acceptance Criteria

- Update skills
- Update education
- Update experience
- Save profile

Priority: High

---

# Epic 3 - Resume Management

## US-021 Upload Resume

**As a** user

**I want** to upload my resume

**So that** the platform can analyze my experience.

Acceptance Criteria

- PDF supported
- DOCX supported
- File validation
- Upload confirmation

Priority: High

---

## US-022 Resume Preview

**As a** user

**I want** to preview my uploaded resume

**So that** I can verify the uploaded document.

Priority: Medium

---

## US-023 Resume Version Management

**As a** user

**I want** to manage multiple resume versions

**So that** I can tailor resumes for different roles.

Priority: Medium

---

# Epic 4 - AI Resume Intelligence

## US-041 Resume Analysis

**As a** user

**I want** AI to analyze my resume

**So that** I understand my strengths and weaknesses.

Priority: High

---

## US-042 ATS Score

**As a** user

**I want** to see my ATS score

**So that** I know how ATS-friendly my resume is.

Priority: High

---

## US-043 Resume Tailoring

**As a** user

**I want** AI to tailor my resume for a selected job

**So that** I improve my interview chances.

Priority: High

---

# Epic 5 - AI Job Search

## US-061 Search Jobs

**As a** user

**I want** to search international jobs

**So that** I can find relevant opportunities.

Priority: High

---

## US-062 Filter Jobs

**As a** user

**I want** to filter jobs

**So that** I only see relevant opportunities.

Acceptance Criteria

- Country
- Technology
- Visa Sponsorship
- Experience

Priority: High

---

## US-063 Save Jobs

**As a** user

**I want** to bookmark interesting jobs

**So that** I can review them later.

Priority: Medium

---

# Epic 6 - AI Job Matching

## US-081 Resume Matching

**As a** user

**I want** AI to compare my resume with a job description

**So that** I understand my suitability.

Priority: High

---

## US-082 Skill Gap Analysis

**As a** user

**I want** AI to identify missing skills

**So that** I know what to improve.

Priority: High

---

# Epic 7 - Company Intelligence

## US-101 Company Search

**As a** user

**I want** to research companies

**So that** I can make informed career decisions.

Priority: Medium

---

## US-102 Company Insights

**As a** user

**I want** company information

**So that** I understand culture, hiring trends, and visa sponsorship.

Priority: Medium

---

# Epic 8 - Application Tracker

## US-121 Track Applications

**As a** user

**I want** to track all job applications

**So that** I stay organized.

Priority: High

---

## US-122 Update Application Status

**As a** user

**I want** to update application progress

**So that** I know where I stand.

Supported Statuses

- Applied
- Interview
- Offer
- Rejected
- Accepted

Priority: High

---

# Epic 9 - Dashboard

## US-141 Dashboard Overview

**As a** user

**I want** a dashboard

**So that** I can quickly understand my career progress.

Priority: High

---

## US-142 AI Recommendations

**As a** user

**I want** personalized recommendations

**So that** I can improve my job search.

Priority: High

---

# Story Priorities

| Priority | Meaning |
|----------|---------|
| High | Mandatory for MVP |
| Medium | Important but can follow |
| Low | Future enhancement |

---

# Story Mapping

| Epic | Story Count |
|------|-------------|
| Authentication | 3 |
| User Profile | 1 |
| Resume Management | 3 |
| Resume Intelligence | 3 |
| Job Search | 3 |
| Job Matching | 2 |
| Company Intelligence | 2 |
| Application Tracker | 2 |
| Dashboard | 2 |

---

# Definition of Ready (DoR)

A story is Ready when:

- Business requirement exists
- Acceptance criteria are defined
- Dependencies identified
- Story estimated
- Product Owner approves

---

# Definition of Done (DoD)

A story is Done when:

- Development completed
- Code reviewed
- Unit tests passed
- Integration tests passed
- Documentation updated
- Product Owner accepts

---

# Traceability

Each story maps to:

- Business Requirement
- Functional Requirement
- Jira Epic
- API Endpoint
- Database Entity
- UI Screen
- Test Case

Example

| Story | Requirement | API | Database |
|--------|-------------|-----|----------|
| US-021 | FR-021 | POST /resume/upload | Resumes |
| US-061 | FR-061 | GET /jobs | Jobs |
| US-081 | FR-081 | POST /jobs/match | JobMatches |

---

# Dependencies

Depends on:

- BRD.md
- PRD.md
- Functional_Requirements.md
- Non_Functional_Requirements.md

Future Documents

- Architecture
- Database Design
- API Design
- Jira Backlog
- Sprint Planning
- Test Cases

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Scrum Master | TBD | Pending |
| Technical Lead | TBD | Pending |