# Functional Requirements Specification

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Functional Requirements Specification |
| Version | 1.0 |
| Status | Draft |

---

# Purpose

This document defines the functional requirements of the AI Career Intelligence Platform. It specifies the system capabilities, expected behavior, business functions, and user interactions required to deliver the Version 1.0 MVP.

Each functional requirement will later map directly to Jira Epics, Features, User Stories, APIs, Database entities, UI screens, and test cases.

---

# Functional Requirement Summary

| Module | Requirement ID Range |
|----------|----------------------|
| Authentication | FR-001 – FR-010 |
| User Profile | FR-011 – FR-020 |
| Resume Management | FR-021 – FR-040 |
| Resume Intelligence | FR-041 – FR-060 |
| Job Search | FR-061 – FR-080 |
| Job Matching | FR-081 – FR-100 |
| Company Intelligence | FR-101 – FR-120 |
| Application Tracker | FR-121 – FR-140 |
| Dashboard | FR-141 – FR-150 |

---

# Module 1 – Authentication

## FR-001

The system shall allow a new user to register using email and password.

Priority: High

---

## FR-002

The system shall verify the user's email before account activation.

Priority: High

---

## FR-003

The system shall allow registered users to log in securely.

Priority: High

---

## FR-004

The system shall support password reset using email verification.

Priority: High

---

## FR-005

The system shall allow users to log out securely.

Priority: Medium

---

# Module 2 – User Profile

## FR-011

The system shall allow users to create a personal profile.

---

## FR-012

Users shall update:

- Name
- Email
- Country
- Skills
- Experience
- Education
- Preferred Roles
- Preferred Countries

---

## FR-013

The system shall save profile changes immediately.

---

## FR-014

The system shall validate mandatory profile fields.

---

# Module 3 – Resume Management

## FR-021

Users shall upload PDF resumes.

---

## FR-022

Users shall upload DOCX resumes.

---

## FR-023

The system shall validate uploaded file formats.

---

## FR-024

The system shall store uploaded resumes securely.

---

## FR-025

Users shall preview uploaded resumes.

---

## FR-026

Users shall download resumes.

---

## FR-027

Users shall maintain multiple resume versions.

---

# Module 4 – AI Resume Intelligence

## FR-041

The system shall parse uploaded resumes.

---

## FR-042

The system shall extract:

- Skills
- Education
- Experience
- Projects
- Certifications

---

## FR-043

The system shall calculate an ATS compatibility score.

---

## FR-044

The system shall identify missing keywords.

---

## FR-045

The system shall provide AI-generated resume improvement suggestions.

---

## FR-046

The system shall tailor resumes to selected job descriptions.

---

# Module 5 – AI Job Search

## FR-061

Users shall search international jobs.

---

## FR-062

The system shall filter jobs by:

- Country
- Technology
- Experience
- Visa Sponsorship
- Employment Type

---

## FR-063

Users shall save jobs for later review.

---

## FR-064

Users shall view complete job descriptions.

---

# Module 6 – AI Job Matching

## FR-081

The system shall compare resumes against job descriptions.

---

## FR-082

The system shall calculate a match percentage.

---

## FR-083

The system shall identify missing skills.

---

## FR-084

The system shall recommend improvements.

---

# Module 7 – Company Intelligence

## FR-101

Users shall search companies.

---

## FR-102

The system shall display:

- Company Overview
- Industry
- Technology Stack
- Hiring Trends
- Visa Sponsorship Information

---

## FR-103

Users shall bookmark companies.

---

# Module 8 – Application Tracker

## FR-121

Users shall record submitted applications.

---

## FR-122

Users shall update application status.

Supported statuses:

- Applied
- Screening
- Interview
- Offer
- Rejected
- Accepted

---

## FR-123

Users shall attach notes to applications.

---

## FR-124

Users shall receive application reminders.

---

# Module 9 – Dashboard

## FR-141

Users shall view profile completion.

---

## FR-142

Users shall view application statistics.

---

## FR-143

Users shall view resume analytics.

---

## FR-144

Users shall view AI recommendations.

---

## FR-145

Users shall view recent activity.

---

# Functional Dependencies

Authentication

↓

User Profile

↓

Resume Upload

↓

Resume Parsing

↓

Resume Intelligence

↓

Job Search

↓

Job Matching

↓

Application Tracker

↓

Dashboard

---

# Acceptance Criteria

Each functional requirement shall satisfy the following:

- Function implemented
- UI available
- API available
- Database persistence
- Validation implemented
- Unit tests completed
- Integration tests passed

---

# Traceability Matrix

| Requirement | Epic | Story | API | Database |
|-------------|------|-------|-----|----------|
| FR-001 | Authentication | User Registration | POST /auth/register | Users |
| FR-021 | Resume Management | Upload Resume | POST /resume/upload | Resumes |
| FR-061 | Job Search | Search Jobs | GET /jobs | Jobs |
| FR-081 | Job Matching | Match Resume | POST /jobs/match | JobMatches |

---

# Dependencies

Depends on:

- BRD.md
- PRD.md
- Product Vision Documents

Used by:

- Architecture
- Database Design
- API Design
- UI Design
- Jira Backlog
- Sprint Planning
- Test Cases

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Technical Lead | TBD | Pending |
| QA Lead | TBD | Pending |