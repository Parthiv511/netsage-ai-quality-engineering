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
