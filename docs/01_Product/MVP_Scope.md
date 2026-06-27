# Minimum Viable Product (MVP) Scope

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Purpose

This document defines the Minimum Viable Product (MVP) scope for the AI Career Intelligence Platform. It identifies the features that will be delivered in Version 1.0 and explicitly defines what is out of scope.

---

# MVP Vision

The MVP aims to help international job seekers efficiently discover jobs, optimize resumes, and manage their applications using Artificial Intelligence.

The objective is to validate the product idea with a complete end-to-end user journey while keeping development manageable.

---

# MVP Objectives

The MVP should allow users to:

- Register and manage their profile.
- Upload and manage resumes.
- Search international jobs.
- Match resumes against job descriptions.
- Tailor resumes using AI.
- Research companies.
- Track job applications.
- View career insights through a dashboard.

---

# In Scope (Version 1.0)

## Epic 1 – User Authentication

### Features

- User Registration
- Login
- Logout
- Forgot Password
- Email Verification
- JWT Authentication

---

## Epic 2 – User Profile

### Features

- Personal Information
- Skills
- Experience
- Education
- Preferred Countries
- Preferred Roles

---

## Epic 3 – Resume Management

### Features

- Resume Upload (PDF/DOCX)
- Resume Parsing
- Resume Version Management
- Resume Download
- Resume Preview

---

## Epic 4 – AI Resume Intelligence

### Features

- Resume Analysis
- ATS Score
- Missing Keywords
- Resume Suggestions
- AI Resume Tailoring

---

## Epic 5 – AI Job Search

### Features

- Job Search
- Country Filter
- Visa Sponsorship Filter
- Technology Filter
- Experience Filter
- Saved Jobs

---

## Epic 6 – AI Job Matching

### Features

- Resume vs Job Matching
- Match Percentage
- Missing Skills
- AI Recommendations
- Skill Gap Report

---

## Epic 7 – Company Intelligence

### Features

- Company Overview
- Technology Stack
- Hiring Trends
- Visa Sponsorship Information
- Company Insights

---

## Epic 8 – Application Tracker

### Features

- Applied Jobs
- Interview Status
- Offer Tracking
- Rejection Tracking
- Notes

---

## Epic 9 – Dashboard

### Features

- Job Search Summary
- Resume Statistics
- Applications Summary
- AI Recommendations
- Career Progress

---

# Out of Scope (Future Releases)

The following features will not be included in Version 1.0.

## Version 2

- AI Interview Coach
- Salary Prediction
- Recruiter CRM
- Learning Recommendations
- Career Roadmap
- AI Career Coach
- Skill Certification Tracking

---

## Version 3

- Enterprise Hiring Portal
- University Portal
- Candidate Marketplace
- Recruiter Marketplace
- Referral Management
- Multi-language Support
- Mobile Applications

---

# Functional Scope

The MVP will support:

- User Management
- Resume Management
- Job Discovery
- AI Resume Optimization
- AI Job Matching
- Company Research
- Application Tracking
- Dashboard

---

# Non-Functional Scope

The platform should satisfy the following requirements:

- Secure Authentication
- Responsive UI
- Cloud Deployment
- Modular Architecture
- API-first Design
- AI Response < 5 Seconds
- Resume Parsing < 30 Seconds
- High Availability
- Audit Logging

---

# Success Criteria

The MVP will be considered successful when:

- Users can complete profile creation.
- Resume parsing accuracy exceeds 90%.
- AI Resume Tailoring completes within 30 seconds.
- AI Job Match accuracy exceeds 80%.
- Dashboard updates in real time.
- Users can track applications end-to-end.

---

# Risks

Potential risks include:

- Limited job API availability.
- AI hallucinations.
- Resume parsing failures.
- Infrastructure costs.
- External API dependency.

---

# Assumptions

The MVP assumes:

- Users upload resumes in supported formats.
- AI models provide consistent recommendations.
- Job data sources remain accessible.
- Cloud services scale with demand.

---

# Dependencies

Depends on:

- Product_Vision.md
- Problem_Statement.md
- Business_Goals.md
- User_Personas.md

Future documents depending on this document:

- BRD.md
- PRD.md
- High_Level_Architecture.md
- Database Design
- API Design
- Jira Epics
- Sprint Planning

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Technical Lead | TBD | Pending |