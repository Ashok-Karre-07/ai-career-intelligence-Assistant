# API Architecture

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Enterprise API Architecture |
| Version | 1.0 |
| Owner | API Architecture Team |

---

# Purpose

This document defines the Enterprise API Architecture for the AI Career Intelligence Platform.

The API layer serves as the single entry point into the platform and provides secure, scalable, and well-governed communication between the frontend, AI services, and backend business logic.

The APIs are designed according to REST principles and OpenAPI specifications while remaining extensible for future GraphQL or gRPC integrations.

---

# API Design Goals

The API platform shall:

- Follow RESTful principles
- Be API-first
- Support versioning
- Provide consistent responses
- Be self-documenting
- Be secure
- Be observable
- Be backward compatible

---

# High Level API Architecture

```
                 Next.js Frontend

                        │

                        ▼

                HTTPS REST APIs

                        │

                        ▼

              FastAPI API Gateway

                        │

──────────────────────────────────────────

 Authentication Middleware

 Logging Middleware

 Rate Limiter

 Request Validation

 Exception Handler

──────────────────────────────────────────

                        │

                        ▼

               Business Services

                        │

                        ▼

              AI + Database Layer
```

---

# API Standards

Protocol

- HTTPS only

Format

- JSON

Character Encoding

- UTF-8

Documentation

- OpenAPI 3.1
- Swagger UI
- ReDoc

---

# API Versioning

Current Version

```
/api/v1/
```

Future

```
/api/v2/

/api/v3/
```

Versioning Rules

- Never break existing APIs
- Introduce new versions only for breaking changes
- Deprecate old versions with notice

---

# Endpoint Naming Standards

Use plural nouns.

Correct

```
GET /users

GET /jobs

GET /companies

POST /applications
```

Avoid

```
GET /getJobs

POST /createResume

GET /jobDetails
```

---

# HTTP Methods

GET

Retrieve resources.

POST

Create resources.

PUT

Replace resources.

PATCH

Partial update.

DELETE

Delete resources.

---

# API Modules

Authentication

```
/api/v1/auth
```

User

```
/api/v1/users
```

Resume

```
/api/v1/resumes
```

Jobs

```
/api/v1/jobs
```

Companies

```
/api/v1/companies
```

Applications

```
/api/v1/applications
```

Dashboard

```
/api/v1/dashboard
```

AI

```
/api/v1/ai
```

Health

```
/api/v1/health
```

Admin (Future)

```
/api/v1/admin
```

---

# Standard Response Format

Success

```json
{
  "success": true,
  "message": "Resume uploaded successfully.",
  "data": {},
  "timestamp": "2026-06-27T10:00:00Z"
}
```

Failure

```json
{
  "success": false,
  "error": {
    "code": "RESUME_UPLOAD_FAILED",
    "message": "Invalid file format."
  },
  "timestamp": "2026-06-27T10:00:00Z"
}
```

---

# HTTP Status Codes

| Code | Meaning |
|------|----------|
| 200 | Success |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

---

# Authentication

Technology

- JWT

Headers

```
Authorization: Bearer <token>
```

Token Types

- Access Token
- Refresh Token

---

# Authorization

Role Based Access Control (RBAC)

Roles

- User
- Recruiter (Future)
- Admin

Policies

- Least privilege
- Resource ownership validation

---

# Request Validation

Validation

- Pydantic Models
- Type validation
- Required fields
- Length validation
- File validation

---

# Pagination

Query Parameters

```
?page=1

&page_size=20
```

Response

```json
{
  "items": [],
  "page": 1,
  "page_size": 20,
  "total": 100,
  "total_pages": 5
}
```

---

# Filtering

Example

```
GET /jobs?

country=Germany

technology=Python

experience=3
```

---

# Sorting

Example

```
GET /jobs?sort=created_at

GET /jobs?sort=-salary
```

---

# Searching

Example

```
GET /jobs?search=data+engineer
```

---

# File Upload

Supported

- PDF
- DOCX

Maximum Size

20 MB

Content-Type Validation

Required

---

# Rate Limiting

Default

100 requests/minute/user

AI Endpoints

20 requests/minute/user

Authentication

10 requests/minute/IP

---

# API Security

- HTTPS
- JWT
- CORS
- Input validation
- Output sanitization
- SQL Injection prevention
- XSS prevention

---

# API Documentation

Generated automatically using

- FastAPI
- OpenAPI
- Swagger UI

Every endpoint shall contain

- Summary
- Description
- Parameters
- Request Model
- Response Model
- Status Codes
- Examples

---

# API Logging

Log

- Request ID
- User ID
- Endpoint
- Duration
- Status Code
- Error Details

---

# API Monitoring

Track

- Response Time
- Error Rate
- Throughput
- Latency
- Success Rate
- AI Token Usage

---

# Future Enhancements

- GraphQL Gateway
- gRPC Internal Services
- WebSockets
- Server Sent Events
- API Gateway
- Service Mesh

---

# Dependencies

Depends on

- Technology Stack
- High Level Architecture
- Security Architecture

Used by

- Frontend Team
- Backend Team
- Mobile Applications
- AI Platform
- Third-party Integrations

---

# Related Documents

- Database Architecture
- Security Architecture
- Deployment Architecture

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief API Architect | Ashok Karre | Pending |
| Solution Architect | TBD | Pending |
| Technical Lead | TBD | Pending |