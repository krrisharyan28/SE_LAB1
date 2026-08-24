# Requirements Table

## Project: Centralized Audit Trail Compliance Engine

### Functional Requirements

| ID | Type | Description | Priority | Acceptance Criteria | Rationale |
|---|---|---|---|---|---|
| FR-001 | Functional | The system shall ingest structured JSON audit logs from configured enterprise applications and validate the required event fields before processing. | High | **Pass:** A valid JSON audit event is accepted and queued for processing. **Fail:** Malformed JSON or a missing mandatory event field is rejected and recorded as an ingestion error. | Reliable ingestion is the foundation for complete and trustworthy audit records. |
| FR-002 | Functional | The system shall identify and mask sensitive PII, including Social Security Numbers and credit card numbers, before an audit record is persisted. | High | **Pass:** Persisted records contain masked PII and no cleartext SSN or credit card number. **Fail:** Any cleartext protected value is persisted. | Prevents sensitive personal and financial data from being exposed in audit storage and supports GDPR-oriented data protection. |
| FR-003 | Functional | The system shall persist each successfully processed audit record together with a SHA-256 integrity hash calculated from the protected audit content. | High | **Pass:** Every persisted audit record has a SHA-256 hash and the same record produces a reproducible verification result. **Fail:** A record is stored without an integrity hash or with an invalid hash. | Provides evidence that stored audit records have not been altered after processing. |
| FR-004 | Functional | The system shall allow authorized Compliance Officers and Security Auditors to search and filter historical audit records using multiple criteria such as date range, event type, application, severity, and actor. | High | **Pass:** An authorized user can apply multiple filters and receives matching records. **Fail:** An unauthorized user can retrieve audit records or a valid query ignores an applied filter. | Makes large audit histories usable for investigations, compliance checks, and security reviews. |
| FR-005 | Functional | The system shall generate cryptographically verifiable immutable audit exports containing the selected audit records and their integrity hashes. | High | **Pass:** An export is generated with verification metadata and cannot be silently modified without detection. **Fail:** Exported records can be changed without causing integrity verification to fail. | Enables auditors to produce trustworthy evidence for compliance reviews and investigations. |

### Non-Functional Requirements

| ID | Type | Description | Priority | Acceptance Criteria | Rationale |
|---|---|---|---|---|---|
| NFR-001 | Performance & Scalability | Audit-log query endpoints shall support complex filtering across up to 10 million historical records with a target response time of under 1 second under the defined benchmark workload. | High | **Pass:** Benchmark tests meet the <1 second target for the specified representative query workload at 10 million records. **Fail:** The target is not met under the same benchmark conditions. | The problem statement explicitly requires sub-second complex queries at large historical-record scale. |
| NFR-002 | Security & Privacy | The system shall enforce role-based access control for Compliance Officers and Security Auditors, protect sensitive data in storage and exports, and prevent unauthorized access to audit records and PII. | High | **Pass:** Security tests show only permitted roles can access relevant functions, protected PII is masked, and unauthorized requests are denied. **Fail:** A protected value is exposed or an unauthorized role accesses restricted audit data/functions. | Audit evidence and PII are security-sensitive; access control and privacy protection are essential to compliance. |
