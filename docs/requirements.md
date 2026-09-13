# NetSage AI – Software Requirements

## 1. Document Purpose

This document defines the functional and non-functional requirements for the NetSage AI Network Troubleshooting and Quality Engineering Platform.

NetSage AI combines AI-assisted network diagnosis, deterministic network validation, automated testing, human review, AI evaluation, regression testing, and CI/CD quality gates.

The system is designed to demonstrate that an AI-based troubleshooting system can be developed and evaluated using Quality Engineering principles.

---

# 2. Project Scope

NetSage AI will accept network troubleshooting information from a user and generate an evidence-based diagnosis.

The input may contain:

- Problem description / symptom
- Network topology
- Device information
- Cisco `show` command outputs
- Relevant configuration information

The system will analyze this information using:

1. AI diagnosis
2. Deterministic rule checking
3. Ground-truth validation
4. Human review

The platform will also provide automated testing and quality evaluation of the AI system and the application itself.

---

# 3. System Objectives

The system shall:

- Diagnose common network problems.
- Identify probable root causes.
- Identify the relevant OSI layer.
- Provide supporting evidence.
- Suggest the next troubleshooting command.
- Suggest corrective actions.
- Assign a confidence score.
- Validate AI responses against known expected results.
- Detect incorrect AI diagnoses.
- Support human review.
- Record human corrections.
- Maintain an AI regression test suite.
- Provide application-level API and UI testing.
- Generate quality metrics and reports.
- Integrate automated testing into CI/CD.

---

# 4. Users

## 4.1 Network Troubleshooter

A user who provides network symptoms, topology, and device evidence to obtain a troubleshooting diagnosis.

## 4.2 Human Reviewer

A user who reviews the AI-generated diagnosis and decides whether it is:

- Accepted
- Edited
- Rejected

## 4.3 QA Engineer

A user who creates test cases, executes automated tests, analyzes failures, and evaluates AI reliability.

## 4.4 Administrator

A user who manages the application, test data, configurations, and system-level functionality where applicable.

---

# 5. Functional Requirements

## FR-01 – Accept Troubleshooting Problem

The system shall allow a user to provide a network problem or symptom.

Example:

> PC can communicate with the gateway but cannot reach the server.

---

## FR-02 – Accept Network Topology

The system shall allow the user to provide the relevant network topology.

Example:

```text
PC → Access Switch → Router → Server