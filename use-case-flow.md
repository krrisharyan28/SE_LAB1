# Use-Case Flow Specification

## Core Use Case: Generate Cryptographically Verifiable Audit Export

**Primary Actor:** Compliance Officer  
**Supporting Actor:** Security Auditor  
**Goal:** Generate an immutable export of selected audit records that can be independently verified for integrity.

### Preconditions

1. The user is authenticated.
2. The user has permission to generate audit exports.
3. Audit records have already been ingested, PII-masked, persisted, and assigned SHA-256 integrity hashes.
4. The requested audit records are available in the historical audit store.

### Postconditions

**Success:**
- The selected audit records are included in an export.
- Each exported record is associated with its integrity hash.
- Verification metadata is included with the export.
- The resulting export is stored as an immutable audit artifact.
- The user receives the export reference.

**Failure:**
- No incomplete or unverified export is marked as a successful immutable export.
- The failure is recorded for operational/audit purposes.

### Main Success Scenario

1. The Compliance Officer signs in to the compliance platform.
2. The system authenticates the user and verifies the user's authorization to generate exports.
3. The user opens the historical audit search interface.
4. The user specifies filters such as date range, application, event type, severity, or actor.
5. The system validates the filters and retrieves matching audit records.
6. The system displays the matching records and their integrity-verification status.
7. The user selects the records to include and requests an audit export.
8. The system retrieves the selected protected audit records and their stored SHA-256 hashes.
9. The system verifies the integrity of the records before export.
10. The system creates the export together with the required verification metadata.
11. The system seals the export as an immutable audit artifact.
12. The system returns an export identifier/reference to the user.
13. The user can use the verification information to confirm that the exported audit evidence has not been altered.

### Alternate Flow: Integrity Verification Failure

**At Step 9:**

9A. The system detects that an audit record's calculated SHA-256 value does not match its stored integrity hash.  
9B. The system stops the export operation and does not mark the export as immutable/successful.  
9C. The system records the verification failure with the affected record identifier.  
9D. The system informs the user that the export could not be generated because an integrity check failed.  
9E. The user can investigate the affected record or retry after the underlying issue has been resolved.
