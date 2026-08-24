# Centralized Audit Trail Compliance Engine

PES University — CSE Lab 1: Requirements Engineering & UML Use-Case Modelling

## Problem Statement

The system is a compliance logging platform that ingests enterprise application event logs, masks sensitive PII in accordance with GDPR, and generates cryptographically verifiable immutable audit exports.

**Target stakeholders/actors:** Compliance Officer, Security Auditor.

## Deliverables

- `requirements.md` — exactly 5 Functional Requirements (FR-001 to FR-005) and 2 Non-Functional Requirements (NFR-001 to NFR-002).
- `use-case-diagram.puml` — UML Use-Case Diagram source with all actors and required `include` and `extend` relationships.
- `use-case-flow.md` — one-page-style flow specification for the core export use case, including preconditions, postconditions, main success scenario, and one alternate flow.

## UML Diagram

The PlantUML source can be rendered using any PlantUML-compatible renderer.

The diagram models:
- Compliance Officer
- Security Auditor
- Ingest Audit Logs
- Validate Audit Log
- Mask PII
- Persist Audit Record
- Calculate SHA-256 Integrity Hash
- Search/Filter Audit Records
- Generate Audit Export
- Verify Record Integrity
- Seal Immutable Export
- Verify Export Integrity

Required relationships:
- `Ingest Audit Logs` includes `Validate Audit Log`.
- `Persist Audit Record` includes `Mask PII`.
- `Persist Audit Record` includes `Calculate SHA-256 Integrity Hash`.
- `Generate Audit Export` includes `Search/Filter Audit Records`, `Verify Record Integrity`, and `Seal Immutable Export`.
- `Verify Export Integrity` extends `Generate Audit Export`.

## Suggested GitHub Structure

```text
centralized-audit-trail-compliance-engine/
├── README.md
├── requirements.md
├── use-case-diagram.puml
└── use-case-flow.md
```

## Source Basis

Prepared from the supplied Lab 1 Problem Statement #50: Centralized Audit Trail Compliance Engine.
