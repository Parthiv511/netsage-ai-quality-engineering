# NetSage AI – Software Requirements Specification

## 1. Document Purpose

This document defines the functional and non-functional requirements for the NetSage AI Network Troubleshooting and Quality Engineering Platform.

NetSage AI combines:

- AI-assisted network diagnosis
- Deterministic network validation
- Ground-truth test cases
- Automated testing
- Human review
- AI quality evaluation
- Regression testing
- CI/CD quality gates

The objective is to build a reliable, testable, and maintainable AI-assisted troubleshooting platform.

---

# 2. Project Scope

NetSage AI accepts network troubleshooting information from a user and generates an evidence-based diagnosis.

The input may contain:

- Network problem or symptom
- Complete network topology
- Device information
- Cisco `show` command outputs
- Relevant configuration information

The system analyzes the information using:

1. AI Diagnosis Engine
2. Deterministic Rule Engine
3. Validation Engine
4. Ground-Truth Evaluation
5. Human Review

The platform also tests the AI system and the application using Quality Engineering practices.

---

# 3. System Objectives

The system shall:

- Accept network troubleshooting problems.
- Accept network topology information.
- Accept Cisco show-command outputs and configuration evidence.
- Identify probable network root causes.
- Identify the relevant OSI layer.
- Provide supporting evidence.
- Suggest the next troubleshooting command.
- Suggest corrective actions.
- Provide a confidence value.
- Perform deterministic network checks.
- Compare AI results with ground-truth results.
- Detect incorrect AI diagnoses.
- Support human review.
- Record human corrections.
- Maintain an AI regression test suite.
- Provide automated API and UI testing.
- Generate quality metrics and reports.
- Integrate automated testing into CI/CD.

---

# 4. Users

## 4.1 Network Troubleshooter

A user who provides network symptoms, topology, and network evidence to obtain a troubleshooting diagnosis.

## 4.2 Human Reviewer

A user who reviews the AI-generated diagnosis and decides whether it should be:

- Accepted
- Edited
- Rejected

## 4.3 QA Engineer

A user who creates test cases, executes automated tests, evaluates AI responses, analyzes failures, and maintains regression suites.

## 4.4 Administrator

A user responsible for managing system configuration, test data, and application-level administration where applicable.

---

# 5. Functional Requirements

## FR-01 – Submit Network Problem

The system shall allow the user to provide a network problem or symptom.

Example:

> PC can communicate with the gateway but cannot reach the server.

---

## FR-02 – Submit Network Topology

The system shall allow the user to provide the network topology involved in the problem.

Example:

```text
PC → Access Switch → Router → Server
```

The topology may contain:

- PCs
- Switches
- Routers
- Servers
- Wireless devices
- VLANs
- Network connections

---

## FR-03 – Submit Network Evidence

The system shall allow the user to provide network evidence such as:

- `show ip route`
- `show vlan`
- `show interfaces`
- `show interfaces trunk`
- `show access-lists`
- `show ip interface`
- DHCP information
- NAT information
- Relevant configuration output

---

## FR-04 – Generate AI Diagnosis

The system shall analyze the submitted problem, topology, and evidence using an AI diagnosis engine.

The AI diagnosis shall attempt to identify:

- Root cause
- Confidence
- Supporting evidence
- OSI layer
- Next troubleshooting command
- Suggested fix

---

## FR-05 – Return Structured AI Response

The AI diagnosis shall follow a predefined structured response format.

Example:

```json
{
  "root_cause": "Missing route",
  "confidence": 0.91,
  "evidence": [
    "Destination network is missing from the routing table"
  ],
  "osi_layer": "Layer 3",
  "next_command": "show ip route",
  "fix_steps": [
    "Add the missing route",
    "Verify connectivity"
  ]
}
```

The system shall validate the AI response before passing it to downstream components.

---

## FR-06 – Deterministic Network Validation

The system shall provide deterministic Python-based validation rules.

The initial rule engine shall detect:

- Duplicate IP addresses
- Incorrect subnet masks
- Default gateway mismatch
- Interface down
- Missing VLAN
- Missing route

The deterministic rule engine shall produce repeatable results for the same input.

---

## FR-07 – Maintain Ground-Truth Dataset

The project shall maintain a ground-truth network troubleshooting dataset.

The initial dataset shall contain at least 30 troubleshooting cases.

Each case shall contain:

- Case ID
- Symptom
- Topology
- Network evidence
- Expected root cause
- Expected OSI layer
- Concept tag
- Expected next command
- Expected fix
- Severity

The dataset shall be designed for future expansion to 100+ cases.

---

## FR-08 – Evaluate AI Diagnosis

The system shall compare AI-generated diagnoses with ground-truth results.

Each evaluated result shall be classified as:

- Correct
- Partially Correct
- Incorrect

The evaluation shall consider:

- Root cause
- Evidence
- OSI layer
- Next command
- Suggested fix

---

## FR-09 – Calculate AI Quality Metrics

The system shall calculate AI quality metrics including:

- Root-cause accuracy
- Evidence adherence
- Human agreement
- False diagnosis rate
- Confidence calibration
- Regression accuracy
- Overall pass/fail rate

---

## FR-10 – Human Review

The system shall require human review before an AI-generated troubleshooting result is treated as an accepted recommendation.

The reviewer shall be able to:

- Accept the diagnosis
- Edit the diagnosis
- Reject the diagnosis

---

## FR-11 – Record Human Corrections

The system shall record human corrections to AI-generated diagnoses.

The project shall document at least five human-corrected AI responses for responsible AI evaluation.

---

## FR-12 – Defect Management

Incorrect AI diagnoses and application failures shall be treated as defects when appropriate.

A defect record should contain:

- Defect ID
- Case ID
- Description
- Expected result
- Actual result
- Severity
- Priority
- Root cause
- Status
- Resolution

---

## FR-13 – Regression Testing

The system shall maintain a regression suite containing previously validated cases.

Regression testing shall be performed after significant changes to:

- AI prompts
- AI model or model configuration
- Rule engine
- Backend
- API
- Frontend
- Evaluation logic

---

## FR-14 – Detect AI Regression

The system shall compare current AI evaluation results with an established baseline.

Example:

```text
Baseline Accuracy = 92%

New Accuracy = 84%

Result = REGRESSION DETECTED
```

The system shall identify cases that changed from PASS to FAIL.

---

## FR-15 – REST API

The backend shall expose REST APIs for major application operations.

The primary diagnosis endpoint shall be:

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

---

## FR-16 – API Validation

The API shall validate:

- Required fields
- Data types
- Request structure
- Invalid input
- Unknown case IDs
- AI response structure
- Error conditions

---

## FR-17 – Quality Dashboard

The system shall provide a dashboard displaying troubleshooting and quality information.

The dashboard should display:

- Total test cases
- AI accuracy
- AI/human agreement
- Passed cases
- Failed cases
- Critical defects
- Issue types
- Severity distribution
- Regression results

---

## FR-18 – Human Review Interface

The application shall provide a human review interface.

The reviewer shall be able to:

1. View the original problem.
2. View topology.
3. View network evidence.
4. View AI diagnosis.
5. Compare expected and AI results where applicable.
6. Accept, edit, or reject the diagnosis.
7. Record review comments.

---

## FR-19 – Automated Testing

The project shall include automated testing for:

### Unit Testing

- Rule engine
- Validation logic
- Evaluation logic

### API Testing

- Positive tests
- Negative tests
- Schema validation
- Error handling

### UI Testing

- Diagnosis workflow
- Result display
- Human review workflow
- Dashboard validation

### AI Testing

- Ground-truth evaluation
- Structured response validation
- Evidence validation
- Regression evaluation

---

## FR-20 – Test Reporting

The system shall generate test execution and quality reports.

Reports should include:

- Total tests
- Passed tests
- Failed tests
- Skipped tests
- AI evaluation metrics
- Regression results
- Defect information

Allure may be used for automated test reporting.

---

# 6. Network Troubleshooting Coverage

The initial troubleshooting dataset shall cover:

| Area | Example Problems |
|---|---|
| VLAN | Missing VLAN, incorrect VLAN assignment |
| Gateway | Incorrect default gateway |
| DHCP | Incorrect or missing IP assignment |
| DNS | DNS resolution failure |
| Routing | Missing or incorrect route |
| ACL | Traffic blocked by ACL |
| NAT | Incorrect NAT configuration |
| Wireless | Wireless connectivity or isolation problems |
| IP Addressing | Duplicate or incorrect IP |
| Subnetting | Incorrect subnet mask |
| Interfaces | Interface administratively down |

The initial dataset shall contain at least 30 cases across these areas.

---

# 7. AI Requirements

## AI-01 – Evidence-Based Diagnosis

The AI shall use the supplied network evidence when generating a diagnosis.

The AI should not rely only on the symptom description when sufficient evidence is available.

## AI-02 – Confidence

The AI shall provide a confidence value or confidence category.

Example:

```text
High
Medium
Low
```

or:

```text
0.91
```

## AI-03 – Uncertainty Handling

When available evidence is insufficient, the AI should indicate uncertainty and recommend an appropriate next troubleshooting command.

## AI-04 – Human-Controlled Fix

The system shall not automatically apply network configuration changes based only on an AI recommendation.

Human review shall occur before accepting a proposed fix.

## AI-05 – Structured Output Validation

AI responses shall be validated against a predefined schema before downstream processing.

---

# 8. Quality Engineering Requirements

The project shall follow a Quality Engineering approach in which testing is integrated throughout development.

The quality lifecycle shall include:

```text
Requirements
     ↓
User Stories
     ↓
Acceptance Criteria
     ↓
Test Design
     ↓
Implementation
     ↓
Unit Testing
     ↓
Integration Testing
     ↓
AI Evaluation
     ↓
API Testing
     ↓
UI Testing
     ↓
Regression Testing
     ↓
CI/CD Quality Gate
```

---

# 9. Non-Functional Requirements

## NFR-01 – Reliability

Deterministic network validation rules shall produce consistent results for the same input.

## NFR-02 – Maintainability

The system shall be modular so that:

- New troubleshooting rules can be added.
- New test cases can be added.
- AI prompts can be modified independently.
- Evaluation logic can be extended.
- New APIs can be added.

## NFR-03 – Testability

Major system components shall be independently testable.

These include:

- Rule Engine
- AI Service
- Evaluation Engine
- API
- Database Layer
- Frontend

## NFR-04 – Observability

The system should maintain logs for:

- Diagnosis requests
- AI responses
- Rule results
- Validation results
- Human reviews
- Test execution
- Regression results
- Application errors

Sensitive information shall not be unnecessarily stored in logs.

## NFR-05 – Performance

The application should provide reasonable response times for normal troubleshooting requests.

Performance targets will be defined during implementation and measured through testing.

## NFR-06 – Security

The system shall:

- Validate user input.
- Protect API endpoints where authentication is implemented.
- Avoid unnecessary exposure of sensitive network information.
- Validate AI-generated output before processing it.
- Prevent automatic execution of AI-generated network commands.

## NFR-07 – Scalability

The architecture shall support expansion from:

```text
30 cases
   ↓
100 cases
   ↓
500+ cases
```

without major architectural changes.

---

# 10. Database Requirements

The database shall store information such as:

- Troubleshooting cases
- AI diagnoses
- Validation results
- Human reviews
- Defects
- Test execution results
- Regression results
- Evaluation metrics

PostgreSQL will be used as the target relational database.

---

# 11. Testing Requirements

The project shall implement multiple testing levels.

| Testing Type | Purpose |
|---|---|
| Unit Testing | Test individual components |
| Rule Testing | Validate deterministic network rules |
| AI Evaluation | Measure AI diagnosis quality |
| API Testing | Validate backend APIs |
| Integration Testing | Validate component interaction |
| UI Testing | Validate user workflows |
| Regression Testing | Detect previously fixed failures |
| Negative Testing | Validate invalid and error scenarios |
| UAT | Validate user-facing behavior |

---

# 12. CI/CD Requirements

The project shall integrate automated testing into a CI/CD pipeline.

Target pipeline:

```text
Developer Push
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
Test Report
      ↓
Quality Gate
```

Example quality gates:

```text
AI Accuracy >= 90%
Rule Tests = 100% Pass
API Tests = 100% Pass
Critical UI Tests = 100% Pass
No unresolved P1 defects
```

Exact thresholds may be adjusted after the first baseline is established.

---

# 13. Responsible AI Requirements

The platform shall support responsible use of AI by:

- Keeping humans in the decision loop.
- Recording AI outputs.
- Recording human corrections.
- Tracking incorrect AI diagnoses.
- Evaluating AI against ground truth.
- Running regression tests after AI changes.
- Preventing unsupported automatic network changes.

At least five human-corrected AI responses shall be documented.

---

# 14. Out of Scope

The initial version shall not automatically modify live network devices.

The system will focus on:

- Diagnosis
- Evidence analysis
- Suggested troubleshooting
- Validation
- Testing
- Human review
- Quality evaluation

Actual network configuration changes remain under human control.

---

# 15. Requirement Traceability

Each major requirement shall eventually map to:

```text
Requirement
     ↓
User Story
     ↓
Acceptance Criteria
     ↓
Test Case
     ↓
Automation
     ↓
Test Result
```

This traceability will be maintained as the project progresses.

---

# 16. Requirement Status

| Area | Status |
|---|---|
| Project Scope | Defined |
| Functional Requirements | Defined |
| AI Requirements | Defined |
| Network Requirements | Defined |
| QA Requirements | Defined |
| Non-Functional Requirements | Defined |
| Database Requirements | Defined |
| API Requirements | Defined |
| CI/CD Requirements | Defined |
| Responsible AI | Defined |
| Implementation | Not Started |
| Automated Tests | Not Started |
| Deployment | Not Started |