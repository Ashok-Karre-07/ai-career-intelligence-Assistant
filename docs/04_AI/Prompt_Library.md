# Prompt Library

| Version | Author | Status | Last Updated |
|----------|---------|--------|--------------|
| 1.0 | Ashok Karre | Draft | June 2026 |

---

# Document Information

| Item | Description |
|------|-------------|
| Project | AI Career Intelligence Platform |
| Document | Prompt Library |
| Version | 1.0 |
| Owner | AI Engineering Team |

---

# Purpose

This document defines the Prompt Engineering standards for the AI Career Intelligence Platform.

The platform uses structured, version-controlled prompts to ensure consistency, accuracy, maintainability, and high-quality AI responses across all agents.

Rather than embedding prompts directly into application code, prompts are managed as reusable assets with versioning, testing, and lifecycle management.

---

# Objectives

The Prompt Library shall:

- Standardize prompt design
- Enable prompt reuse
- Support prompt versioning
- Improve AI consistency
- Reduce hallucinations
- Simplify maintenance
- Support structured outputs

---

# Prompt Engineering Principles

Every prompt should be:

- Clear
- Specific
- Deterministic
- Context-aware
- Secure
- Testable
- Version-controlled
- Modular

---

# Prompt Lifecycle

```
Design

↓

Review

↓

Testing

↓

Versioning

↓

Deployment

↓

Monitoring

↓

Evaluation

↓

Improvement
```

---

# Prompt Categories

The platform maintains prompts for:

- System Prompts
- Agent Prompts
- Tool Prompts
- RAG Prompts
- Validation Prompts
- Reflection Prompts (Future)

---

# Prompt Structure

Every prompt contains:

1. Role Definition
2. Objective
3. Context
4. Constraints
5. Instructions
6. Output Format
7. Examples (Optional)

---

# Standard Prompt Template

```text
Role

You are an expert AI assistant.

Objective

Complete the requested task accurately.

Context

{{context}}

Instructions

{{instructions}}

Constraints

{{constraints}}

Output Format

{{output_schema}}
```

---

# Prompt Variables

Dynamic placeholders include:

| Variable | Description |
|-----------|-------------|
| {{user_name}} | User's name |
| {{resume}} | Parsed resume |
| {{job_description}} | Selected job |
| {{company}} | Company information |
| {{conversation_history}} | Previous conversation |
| {{rag_context}} | Retrieved knowledge |
| {{current_date}} | Current system date |

---

# Resume Agent Prompt

Purpose

Analyze a resume and provide actionable recommendations.

System Prompt

```text
You are an expert Resume Review Assistant.

Analyze the resume for clarity, ATS compatibility, technical skills, achievements, formatting, and completeness.

Return recommendations as structured JSON.
```

Expected Output

```json
{
  "ats_score": 91,
  "summary": "...",
  "missing_skills": [],
  "recommendations": []
}
```

---

# Resume Tailoring Prompt

Purpose

Tailor a resume for a specific job.

Inputs

- Resume
- Job Description

System Prompt

```text
Rewrite the resume to maximize alignment with the provided job description while preserving factual accuracy.

Do not fabricate experience or skills.

Highlight transferable skills where appropriate.

Return structured JSON containing the tailored content and improvement summary.
```

---

# Job Intelligence Prompt

Purpose

Recommend the most relevant jobs.

System Prompt

```text
Analyze the user's skills, experience, preferred location, and career goals.

Rank the jobs by relevance.

Explain why each recommendation was selected.
```

---

# Company Intelligence Prompt

Purpose

Generate company insights.

System Prompt

```text
Summarize the company's business, technology stack, hiring trends, interview process, and career opportunities.

Return factual information only.
```

---

# Career Coach Prompt

Purpose

Provide career guidance.

System Prompt

```text
Identify skill gaps.

Recommend certifications.

Suggest learning resources.

Generate a realistic six-month learning roadmap.
```

---

# Interview Coach Prompt (Future)

Purpose

Prepare users for interviews.

Capabilities

- Technical Questions
- Behavioral Questions
- Coding Exercises
- Feedback

---

# RAG Prompt Template

Purpose

Ground AI responses using retrieved documents.

Template

```text
Use ONLY the supplied context to answer the user's question.

If the answer cannot be found in the context, clearly state that the available information is insufficient.

Context:

{{rag_context}}

Question:

{{user_query}}
```

---

# Tool Calling Prompt

Purpose

Guide the model when tool execution is required.

Template

```text
If external information is required, select the most appropriate tool.

Do not guess.

Return structured tool arguments.
```

---

# Prompt Versioning

Naming Convention

```
resume_analysis_v1

resume_analysis_v2

job_search_v1
```

Version Metadata

- Prompt ID
- Version
- Author
- Created Date
- Status
- Notes

---

# Prompt Storage

Prompts are stored outside the application code.

Recommended Structure

```
backend/

app/

prompts/

resume/

job/

company/

career/

shared/
```

Example

```
backend/app/prompts/resume/resume_analysis_v1.md

backend/app/prompts/job/job_search_v1.md
```

---

# Prompt Testing

Each prompt is tested for:

- Accuracy
- Consistency
- Hallucination Rate
- Response Time
- JSON Validity
- Token Usage

---

# Prompt Evaluation Metrics

| Metric | Target |
|---------|--------|
| JSON Validity | 100% |
| Hallucination Rate | <2% |
| Prompt Success Rate | >99% |
| Average Latency | <5 sec |
| User Satisfaction | >90% |

---

# Prompt Security

Prompts shall:

- Reject prompt injection attempts
- Protect sensitive information
- Avoid unsafe instructions
- Validate tool usage
- Mask confidential data

---

# Prompt Optimization

Optimization techniques include:

- Reduce prompt length
- Remove ambiguity
- Reuse instructions
- Improve output schemas
- Minimize token usage
- Add examples only when beneficial

---

# Prompt Governance

Every prompt change requires:

- Technical review
- AI evaluation
- Regression testing
- Version increment
- Documentation update

---

# Future Enhancements

- Prompt Registry
- Prompt A/B Testing
- Dynamic Prompt Assembly
- Automatic Prompt Evaluation
- Prompt Performance Dashboard
- Prompt Cost Analytics

---

# Dependencies

Depends on:

- AI Strategy
- Agent Architecture
- RAG Architecture

Used by:

- AI Agents
- Tool Registry
- Evaluation Framework
- Backend Implementation

---

# Related Documents

- 01_AI_Strategy.md
- 02_Agent_Architecture.md
- 04_RAG_Architecture.md
- 05_AI_Evaluation.md
- 06_Guardrails.md

---
s
# Approval

| Role | Name | Status |
|------|------|--------|
| Product Owner | Ashok Karre | Pending |
| Chief AI Architect | Ashok Karre | Pending |
| Prompt Engineering Lead | TBD | Pending |
| Technical Lead | TBD | Pending |