# NetSage AI – Network Troubleshooting & Quality Engineering Platform

## 1. Project Overview

NetSage AI is an AI-assisted network troubleshooting and Quality Engineering platform designed to diagnose Cisco/Packet Tracer network problems using network evidence.

The platform accepts:

- Network problem/symptom
- Network topology
- Cisco show-command outputs
- Relevant configuration information

It combines:

1. AI-based diagnosis
2. Deterministic Python rule checking
3. Ground-truth test cases
4. Automated validation
5. Human review
6. Regression testing
7. API and UI testing
8. CI/CD quality gates

The goal is not only to build an AI troubleshooter, but also to test and evaluate whether the AI produces reliable and evidence-based answers.

---

## 2. Problem Statement

Network troubleshooting often requires engineers to analyze symptoms, topology, configurations, and device outputs before identifying the actual root cause.

AI can assist with this process, but an incorrect AI diagnosis can lead to incorrect network changes.

NetSage AI addresses this problem by combining AI diagnosis with deterministic validation, automated testing, human oversight, and regression testing.

The platform treats the AI system itself as a system under test.

---

## 3. Objectives

The main objectives are:

- Diagnose common Cisco network problems using AI.
- Analyze topology and network evidence.
- Identify probable root causes.
- Provide confidence levels and supporting evidence.
- Suggest the next troubleshooting command.
- Suggest corrective actions.
- Validate AI responses against known ground-truth cases.
- Detect incorrect or hallucinated diagnoses.
- Allow human reviewers to accept, edit, or reject AI answers.
- Maintain a regression suite for AI and application changes.
- Automate API, UI, unit, integration, and regression testing.
- Generate quality reports.
- Integrate testing into CI/CD pipelines.

---

## 4. Core Workflow

```text
User Problem
     ↓
Network Topology
     ↓
Show Commands / Configuration
     ↓
┌───────────────────────────┐
│      NetSage AI Engine    │
├───────────────────────────┤
│                           │
│  AI Diagnosis             │
│  Deterministic Rules      │
│                           │
└─────────────┬─────────────┘
              ↓
       Diagnosis Result
              ↓
       Validation Engine
              ↓
     Expected vs AI Result
              ↓
        PASS / FAIL
              ↓
        Human Review
       ┌──────┼──────┐
       ↓      ↓      ↓
    ACCEPT   EDIT   REJECT
              ↓
       Defect Analysis
              ↓
       Improvement/Fix
              ↓
       Regression Suite
              ↓
       Quality Report

5. Troubleshooting Areas

The initial test dataset will contain at least 30 troubleshooting cases covering:

VLAN
Default Gateway
DHCP
DNS
Routing
ACL
NAT
Wireless
IP addressing
Subnet masks
Interface status
Missing routes

The dataset will later be expanded to 100+ cases.

6. AI Diagnosis Output

For every troubleshooting case, NetSage AI will attempt to provide:

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

The AI response must be evidence-based and should not claim certainty when sufficient evidence is unavailable.

7. Quality Engineering Approach

NetSage AI follows a Quality Engineering approach where testing is integrated throughout the development lifecycle.

Testing Layers
Unit Testing
     ↓
Rule Engine Testing
     ↓
AI Evaluation
     ↓
API Testing
     ↓
Integration Testing
     ↓
UI Testing
     ↓
Regression Testing
     ↓
CI/CD Quality Gate
AI Quality Metrics

The platform will measure:

Root-cause accuracy
Evidence adherence
Human agreement
False diagnosis rate
Confidence calibration
Regression accuracy
Pass/fail rate
8. Human-in-the-Loop

AI-generated diagnoses are not automatically accepted as fixes.

A human reviewer can:

Accept the diagnosis
Edit the diagnosis
Reject the diagnosis

Human corrections are recorded for responsible AI evaluation and future improvement.

9. Technology Stack
Programming Languages
Java
Python
TypeScript
SQL
AI / Evaluation
LLM/API
Pydantic
Pandas
PyTest
Backend
FastAPI
Pydantic
SQLAlchemy
PostgreSQL
Alembic
Frontend
React
TypeScript
Tailwind CSS
Axios
React Query
Recharts
Test Automation
Selenium WebDriver
Playwright
TestNG
PyTest
REST Assured
Postman
Page Object Model
DevOps / CI-CD
Git
GitHub
GitHub Actions
Docker
Docker Compose
Maven
Reporting
Allure
Project Management
Jira
Networking
Cisco Packet Tracer
VLAN
DHCP
DNS
Routing
ACL
NAT
10. Project Architecture

The platform will contain the following major components:

Frontend
   ↓
Backend API
   ↓
Diagnosis Service
   ├── AI Engine
   └── Rule Engine
          ↓
     Validation Engine
          ↓
      PostgreSQL
          ↓
   Evaluation & Reports

The detailed architecture will be documented in:

docs/architecture.md

11. QA Automation Strategy

The project will include automated tests for:

Backend/API
Positive API tests
Negative API tests
Schema validation
Error handling
Integration tests
AI
Ground-truth evaluation
Evidence validation
Structured-output validation
Hallucination checks
Regression evaluation
Confidence evaluation
UI
Login/workflow tests where applicable
Diagnosis submission
Result display
Human review workflow
Dashboard validation
Regression

Whenever the prompt, model configuration, rules, backend, or frontend changes, the regression suite will be executed.

12. CI/CD Pipeline

The target pipeline is:

Git Push
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
Deploy

Example quality gates:

AI accuracy ≥ 90%
Rule tests = 100% pass
API tests = 100% pass
Critical UI tests = 100% pass
No unresolved P1 defects
