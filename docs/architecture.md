# NetSage AI – System Architecture

## 1. Architecture Overview

NetSage AI is designed as an AI-assisted network troubleshooting and Quality Engineering platform.

The architecture separates:

- User interface
- Backend API
- AI diagnosis
- Deterministic validation
- Evaluation
- Human review
- Database
- Automated testing
- CI/CD

The system treats the AI diagnosis component as a system under test.

---

# 2. High-Level Architecture

```text
                         ┌───────────────────┐
                         │       USER        │
                         │ Network           │
                         │ Troubleshooter    │
                         └─────────┬─────────┘
                                   │
                                   ↓
                         ┌───────────────────┐
                         │  React Dashboard  │
                         │   TypeScript UI   │
                         └─────────┬─────────┘
                                   │
                                   ↓
                         ┌───────────────────┐
                         │    REST API       │
                         │     FastAPI       │
                         └─────────┬─────────┘
                                   │
                     ┌─────────────┴─────────────┐
                     │                           │
                     ↓                           ↓
          ┌───────────────────┐       ┌───────────────────┐
          │  AI Diagnosis     │       │ Deterministic     │
          │     Engine        │       │   Rule Engine     │
          └─────────┬─────────┘       └─────────┬─────────┘
                    │                           │
                    └─────────────┬─────────────┘
                                  ↓
                       ┌─────────────────────┐
                       │  Validation Engine  │
                       └──────────┬──────────┘
                                  │
                                  ↓
                       ┌─────────────────────┐
                       │ Evaluation Engine   │
                       └──────────┬──────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    ↓                           ↓
          ┌──────────────────┐        ┌──────────────────┐
          │ Ground-Truth     │        │    AI Result     │
          │ Expected Result  │        │                  │
          └────────┬─────────┘        └────────┬─────────┘
                   │                           │
                   └─────────────┬─────────────┘
                                 ↓
                          ┌──────────────┐
                          │ PASS / FAIL  │
                          └──────┬───────┘
                                 │
                                 ↓
                       ┌────────────────────┐
                       │   Human Review     │
                       ├────────────────────┤
                       │ ACCEPT / EDIT /    │
                       │ REJECT             │
                       └─────────┬──────────┘
                                 │
                                 ↓
                       ┌────────────────────┐
                       │    PostgreSQL      │
                       └────────────────────┘
```

---

# 3. Major Components

## 3.1 React Frontend

The frontend provides the user interface for:

- Submitting troubleshooting problems
- Providing topology
- Providing network evidence
- Viewing AI diagnoses
- Reviewing AI results
- Accepting, editing, or rejecting results
- Viewing quality metrics
- Viewing regression results

### Technology

- React
- TypeScript
- Tailwind CSS
- Axios
- React Query
- Recharts

---

# 4. Backend API

The backend acts as the central application service.

### Responsibilities

- Receive user requests.
- Validate input.
- Communicate with the AI service.
- Execute deterministic rules.
- Invoke evaluation logic.
- Store results.
- Return structured responses.
- Support human review.

### Technology

- Python
- FastAPI
- Pydantic
- SQLAlchemy
- PostgreSQL
- Alembic

---

# 5. Diagnosis Service

The diagnosis service coordinates AI and deterministic troubleshooting.

```text
Troubleshooting Input
        │
        ↓
Diagnosis Service
        │
   ┌────┴────┐
   ↓         ↓
  AI       Rules
   │         │
   └────┬────┘
        ↓
   Validation
        ↓
    Diagnosis
```

The diagnosis service shall not automatically modify network devices.

---

# 6. AI Diagnosis Engine

The AI engine receives:

- Problem/symptom
- Network topology
- Show-command output
- Configuration evidence

It produces:

- Root cause
- Confidence
- Evidence
- OSI layer
- Next command
- Suggested fix

Example:

```json
{
  "root_cause": "Missing route",
  "confidence": 0.91,
  "evidence": [
    "Destination network is not present in routing table"
  ],
  "osi_layer": "Layer 3",
  "next_command": "show ip route",
  "fix_steps": [
    "Add the missing route",
    "Verify connectivity"
  ]
}
```

---

# 7. Deterministic Rule Engine

The rule engine provides deterministic checks for known network problems.

Initial rules:

```text
Duplicate IP
Incorrect Subnet Mask
Gateway Mismatch
Interface Down
Missing VLAN
Missing Route
```

The rule engine is independent of the AI model.

This provides a deterministic validation layer against which AI results can be compared.

---

# 8. Validation Engine

The validation engine checks:

1. AI response structure.
2. Required fields.
3. Valid confidence value.
4. Evidence presence.
5. Ground-truth comparison.
6. Rule-engine results.

Example:

```text
AI Response
     ↓
Schema Validation
     ↓
Evidence Validation
     ↓
Ground-Truth Comparison
     ↓
PASS / PARTIAL / FAIL
```

---

# 9. Ground-Truth Dataset

The ground-truth dataset contains known network troubleshooting cases.

Initial target:

```text
30+ cases
```

Future target:

```text
100+ cases
```

Each case contains:

```text
Case ID
Symptom
Topology
Network Evidence
Expected Root Cause
Expected OSI Layer
Concept Tag
Expected Next Command
Expected Fix
Severity
```

The dataset becomes the foundation of AI evaluation and regression testing.

---

# 10. Evaluation Engine

The evaluation engine compares the AI output with the expected ground-truth result.

Example:

```text
Expected:
Missing Route

AI:
Missing Route

Result:
PASS
```

Another example:

```text
Expected:
Missing Route

AI:
Incorrect VLAN

Result:
FAIL
```

The evaluator calculates:

- Root-cause accuracy
- Evidence adherence
- Human agreement
- False diagnosis rate
- Confidence calibration
- Regression accuracy

---

# 11. Human Review Layer

Human review is mandatory before accepting a troubleshooting recommendation.

The reviewer can:

```text
┌──────────┐
│  ACCEPT  │
└──────────┘

┌──────────┐
│   EDIT   │
└──────────┘

┌──────────┐
│  REJECT  │
└──────────┘
```

Human corrections are recorded for responsible AI evaluation.

---

# 12. Database

PostgreSQL stores:

- Troubleshooting cases
- Ground-truth results
- AI diagnoses
- Validation results
- Human reviews
- Defects
- Test execution results
- Regression results
- Evaluation metrics

Target technology:

```text
PostgreSQL
SQLAlchemy
Alembic
```

---

# 13. Quality Engineering Architecture

Testing is integrated into the architecture.

```text
                NetSage AI
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
   Application              AI System
      Testing                 Testing
        │                       │
   ┌────┼────┐             ┌────┼────┐
   ↓    ↓    ↓             ↓    ↓    ↓
 Unit API  UI           Accuracy Evidence
   │    │    │             │    │
   └────┴────┘             └────┴────┘
        │                       │
        └──────────┬────────────┘
                   ↓
             Regression
                   ↓
              CI/CD Gate
```

---

# 14. Test Automation Architecture

## Python Testing

Used for:

- Rule engine testing
- Evaluation testing
- AI evaluation
- Backend unit testing

Technology:

```text
PyTest
Pandas
```

## Java Testing

Used for:

- API automation
- UI automation

Technology:

```text
Java
TestNG
REST Assured
Selenium WebDriver
Maven
```

## UI Automation

The primary UI automation framework will be:

```text
Selenium WebDriver
+
TestNG
+
Page Object Model
```

Playwright may be used for selected scenarios where it provides additional value.

---

# 15. API Architecture

Primary endpoint:

```text
POST /api/v1/diagnose
```

Example request:

```json
{
  "case_id": "NET-017",
  "symptom": "PC cannot reach server",
  "topology": "PC → Switch → Router → Server",
  "show_output": "show ip route ..."
}
```

Example response:

```json
{
  "root_cause": "Missing route",
  "confidence": 0.91,
  "osi_layer": "Layer 3",
  "evidence": [
    "Destination network is missing from routing table"
  ],
  "next_command": "show ip route",
  "fix_steps": [
    "Add the missing route",
    "Verify connectivity"
  ]
}
```

---

# 16. Application Data Flow

```text
User
 ↓
Problem + Topology + Evidence
 ↓
Frontend
 ↓
FastAPI
 ↓
Diagnosis Service
 ↓
┌───────────────┬────────────────┐
│               │                │
AI Engine    Rule Engine         │
│               │                │
└───────────────┴────────────────┘
                ↓
        Validation Engine
                ↓
        Evaluation Engine
                ↓
         PASS / FAIL
                ↓
          Human Review
                ↓
          PostgreSQL
                ↓
        Dashboard / Reports
```

---

# 17. AI Regression Architecture

AI prompts and model configurations are treated as testable artifacts.

When an AI-related change occurs:

```text
Prompt / Model Change
        ↓
AI Evaluation
        ↓
Regression Suite
        ↓
Compare With Baseline
        ↓
┌───────────────┐
│ Quality Gate  │
└───────┬───────┘
        │
   ┌────┴────┐
   ↓         ↓
 PASS       FAIL
```

Example:

```text
Baseline AI Accuracy = 92%

New AI Accuracy = 84%

Quality Gate = FAILED
```

---

# 18. CI/CD Architecture

The target CI/CD pipeline is:

```text
Developer
    ↓
Git Push
    ↓
GitHub
    ↓
GitHub Actions
    ↓
Build
    ↓
Unit Tests
    ↓
Rule Tests
    ↓
API Tests
    ↓
AI Evaluation
    ↓
Regression Tests
    ↓
UI Tests
    ↓
Allure Report
    ↓
Quality Gate
    ↓
Deployment
```

---

# 19. CI/CD Quality Gates

Example quality gates:

```text
AI Accuracy >= 90%
Rule Tests = 100% Pass
API Tests = 100% Pass
Critical UI Tests = 100% Pass
No unresolved P1 defects
```

If a critical quality gate fails, the pipeline shall fail.

---

# 20. Docker Architecture

The target deployment architecture will use Docker Compose.

```text
Docker Compose
│
├── NetSage API
│
├── React Frontend
│
├── PostgreSQL
│
└── Test Runner
```

This provides a reproducible development and testing environment.

---

# 21. Security Considerations

The system shall:

- Validate user input.
- Validate AI output.
- Avoid executing AI-generated network commands automatically.
- Protect sensitive information.
- Avoid unnecessary sensitive information in logs.
- Apply API security controls where authentication is implemented.

---

# 22. Scalability

The system is designed to scale from:

```text
30 troubleshooting cases
        ↓
100+ cases
        ↓
500+ cases
```

The modular architecture allows:

- Additional network rules.
- Additional AI models.
- Additional test cases.
- Additional APIs.
- Additional dashboard metrics.
- Additional testing frameworks.

---

# 23. Responsible AI Architecture

The system follows a human-in-the-loop design.

```text
AI Diagnosis
     ↓
Validation
     ↓
Human Review
     ↓
┌────┼────┐
↓    ↓    ↓
Accept Edit Reject
     │
     ↓
Human Correction Log
     │
     ↓
AI Quality Evaluation
     │
     ↓
Regression Testing
```

The AI does not independently apply network configuration changes.

---

# 24. Architecture Principles

The system follows these principles:

### 1. Separation of Concerns

AI, deterministic rules, evaluation, backend, frontend, and testing remain modular.

### 2. Testability

Each major component should be independently testable.

### 3. Human Oversight

AI recommendations require human review.

### 4. Evidence-Based Diagnosis

AI responses should use supplied network evidence.

### 5. Deterministic Validation

Known network conditions should be validated using deterministic rules.

### 6. Regression Protection

Changes must be evaluated against previously validated cases.

### 7. Quality Gates

Critical quality failures should prevent progression through CI/CD.

---

# 25. Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React, TypeScript |
| UI Styling | Tailwind CSS |
| Backend | Python, FastAPI |
| Validation | Pydantic |
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| Migration | Alembic |
| AI | LLM/API |
| Data/Evaluation | Pandas |
| Python Testing | PyTest |
| Java Testing | TestNG |
| API Automation | REST Assured |
| UI Automation | Selenium WebDriver |
| UI Alternative | Playwright |
| Build | Maven |
| Version Control | Git, GitHub |
| CI/CD | GitHub Actions |
| Containers | Docker, Docker Compose |
| Reporting | Allure |
| Network Simulation | Cisco Packet Tracer |
| Project Management | Jira |

---

# 26. Architecture Evolution

The project will be implemented incrementally.

```text
Phase 1
Requirements + Architecture
        ↓
Phase 2
Ground-Truth Dataset
        ↓
Phase 3
Deterministic Rule Engine
        ↓
Phase 4
AI Diagnosis
        ↓
Phase 5
Evaluation + Validation
        ↓
Phase 6
Backend API + Database
        ↓
Phase 7
Frontend + Dashboard
        ↓
Phase 8
QA Automation
        ↓
Phase 9
Regression
        ↓
Phase 10
CI/CD + Docker
```

The architecture may be refined during implementation while maintaining the core Quality Engineering principles.