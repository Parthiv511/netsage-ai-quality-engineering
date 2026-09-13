# NetSage AI – User Stories

## 1. Purpose

This document defines the Agile user stories for the NetSage AI Network Troubleshooting and Quality Engineering Platform.

The user stories are derived from the software requirements and will later be connected to acceptance criteria and automated test cases.

---

# 2. User Story Format

Each story follows:

```text
As a <user>,
I want <capability>,
so that <business/user value>.
```

---

# US-01 – Submit Network Problem

**As a** Network Troubleshooter,

**I want** to provide a network problem or symptom,

**so that** NetSage AI can analyze the problem.

### Priority
High

### Related Requirements
FR-01

---

# US-02 – Provide Network Topology

**As a** Network Troubleshooter,

**I want** to provide the complete network topology involved in the problem,

**so that** the system can understand the relationships between network devices.

### Priority
High

### Related Requirements
FR-02

---

# US-03 – Provide Network Evidence

**As a** Network Troubleshooter,

**I want** to provide Cisco show-command outputs and relevant configuration information,

**so that** the diagnosis can be based on actual network evidence.

### Priority
High

### Related Requirements
FR-03

---

# US-04 – Generate AI Diagnosis

**As a** Network Troubleshooter,

**I want** NetSage AI to analyze the problem, topology, and evidence,

**so that** I can receive a probable root-cause diagnosis.

### Priority
High

### Related Requirements
FR-04, AI-01

---

# US-05 – Receive Structured Diagnosis

**As a** Network Troubleshooter,

**I want** the AI diagnosis to contain root cause, confidence, evidence, OSI layer, next command, and suggested fix,

**so that** I can understand and verify the troubleshooting recommendation.

### Priority
High

### Related Requirements
FR-05, AI-02, AI-05

---

# US-06 – Perform Deterministic Network Checks

**As a** QA Engineer,

**I want** deterministic rules to check common network configuration problems,

**so that** known network faults can be validated without depending only on AI.

### Priority
High

### Related Requirements
FR-06

---

# US-07 – Maintain Ground-Truth Cases

**As a** QA Engineer,

**I want** to maintain a dataset containing known network troubleshooting cases and expected results,

**so that** AI diagnoses can be objectively evaluated.

### Priority
High

### Related Requirements
FR-07

---

# US-08 – Evaluate AI Diagnosis

**As a** QA Engineer,

**I want** to compare AI diagnoses with ground-truth results,

**so that** I can determine whether the AI diagnosis is correct.

### Priority
High

### Related Requirements
FR-08

---

# US-09 – Measure AI Quality

**As a** QA Engineer,

**I want** to calculate AI quality metrics,

**so that** I can measure the reliability of the AI system.

### Priority
High

### Related Requirements
FR-09

---

# US-10 – Review AI Diagnosis

**As a** Human Reviewer,

**I want** to review the AI-generated diagnosis before accepting it,

**so that** incorrect recommendations are not blindly accepted.

### Priority
Critical

### Related Requirements
FR-10, AI-04

---

# US-11 – Correct AI Diagnosis

**As a** Human Reviewer,

**I want** to edit or reject an AI diagnosis when it is incorrect,

**so that** the final troubleshooting result is controlled by a human.

### Priority
Critical

### Related Requirements
FR-10, FR-11

---

# US-12 – Record AI Corrections

**As a** QA Engineer,

**I want** human corrections to AI responses to be recorded,

**so that** AI reliability and responsible AI behavior can be evaluated.

### Priority
High

### Related Requirements
FR-11

---

# US-13 – Track Defects

**As a** QA Engineer,

**I want** incorrect AI results and application failures to be recorded as defects,

**so that** failures can be analyzed and resolved systematically.

### Priority
High

### Related Requirements
FR-12

---

# US-14 – Run Regression Tests

**As a** QA Engineer,

**I want** previously validated cases to be automatically re-tested after system changes,

**so that** existing functionality is not accidentally broken.

### Priority
Critical

### Related Requirements
FR-13

---

# US-15 – Detect AI Regression

**As a** QA Engineer,

**I want** current AI evaluation results to be compared with a baseline,

**so that** degradation in AI quality can be detected.

### Priority
Critical

### Related Requirements
FR-14

---

# US-16 – Submit Diagnosis Through API

**As a** QA Engineer,

**I want** a REST API for submitting diagnosis requests,

**so that** the backend can be tested independently and integrated with other components.

### Priority
High

### Related Requirements
FR-15, FR-16

---

# US-17 – View Quality Dashboard

**As a** QA Engineer,

**I want** a dashboard showing AI accuracy, failures, defects, severity, and regression results,

**so that** I can monitor overall system quality.

### Priority
Medium

### Related Requirements
FR-17

---

# US-18 – Review Diagnosis Through UI

**As a** Human Reviewer,

**I want** to view the problem, topology, evidence, AI diagnosis, and review controls in one interface,

**so that** I can efficiently review troubleshooting recommendations.

### Priority
High

### Related Requirements
FR-18

---

# US-19 – Execute Automated Tests

**As a** QA Engineer,

**I want** automated unit, API, UI, integration, and AI evaluation tests,

**so that** defects can be detected consistently and early.

### Priority
Critical

### Related Requirements
FR-19

---

# US-20 – Generate Quality Reports

**As a** QA Engineer,

**I want** test execution and AI evaluation reports,

**so that** I can measure and communicate system quality.

### Priority
Medium

### Related Requirements
FR-20

---

# US-21 – Execute Tests Through CI/CD

**As a** QA Engineer,

**I want** automated tests to run in the CI/CD pipeline,

**so that** code changes are automatically validated before deployment.

### Priority
Critical

### Related Requirements
CI/CD Requirements

---

# 3. User Story Traceability

| User Story | Requirement |
|---|---|
| US-01 | FR-01 |
| US-02 | FR-02 |
| US-03 | FR-03 |
| US-04 | FR-04 |
| US-05 | FR-05 |
| US-06 | FR-06 |
| US-07 | FR-07 |
| US-08 | FR-08 |
| US-09 | FR-09 |
| US-10 | FR-10 |
| US-11 | FR-10, FR-11 |
| US-12 | FR-11 |
| US-13 | FR-12 |
| US-14 | FR-13 |
| US-15 | FR-14 |
| US-16 | FR-15, FR-16 |
| US-17 | FR-17 |
| US-18 | FR-18 |
| US-19 | FR-19 |
| US-20 | FR-20 |
| US-21 | CI/CD Requirements |

---

# 4. Definition of Done

A user story will be considered complete when:

- Requirements are implemented.
- Acceptance criteria are satisfied.
- Appropriate test cases are created.
- Automated tests are implemented where applicable.
- Tests pass.
- Defects are resolved or formally accepted.
- Regression testing is completed.
- Documentation is updated.