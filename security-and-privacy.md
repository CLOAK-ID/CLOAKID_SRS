---

## title: CLOAKID Security and Privacy

# CLOAKID : Security and Privacy

## 1. Introduction

CLOAKID is a project focused on securely sharing Personally Identifiable Information (PII) and Sensitive Personally Identifiable Information (SPII). Since the project handles sensitive user information, security and privacy must be considered throughout its design, development, and testing.

This document describes the security objectives, threat model, proposed development approach, identified risks, and relevant controls for CLOAKID. The approved Software Requirements Specification (SRS) is the primary source for project requirements.

## 2. Security Objectives

The main security and privacy objectives are:

- **Confidentiality:** Prevent unauthorized individuals from accessing shared information.
- **Integrity:** Protect information and security records from unauthorized modification.
- **Availability:** Ensure that authorized users can access the service when it is available.
- **Access control:** Restrict access to authorized and appropriately verified users.
- **Data minimization:** Limit the retention and exposure of sensitive information.
- **Privacy protection:** Reduce the risk of unintended disclosure, copying, or redistribution.
- **Accountability:** Maintain appropriate records of relevant actions.

These objectives guide security decisions and should be validated against the approved SRS.

## 3. Development Approach: Spiral Model

CLOAKID proposes the Spiral Model as its software development approach because security and privacy risks are central to the project.

Unlike an approach that postpones risk assessment until the end, the Spiral Model supports repeated cycles of planning, risk analysis, engineering, and evaluation. Each iteration should examine potential security threats and address the highest-priority risks before proceeding.

### 3.1 Spiral Model Activities

Each development iteration should include the following activities:

1. **Planning:** Define the iteration's objectives, requirements, deliverables, and constraints.
2. **Risk analysis:** Identify threats to sensitive information, assess their likelihood and impact, and select mitigation measures.
3. **Engineering:** Design, implement, or improve the relevant functionality and security controls.
4. **Evaluation:** Test the changes, review remaining risks, and determine whether the iteration's objectives have been met.
5. **Next iteration:** Reassess the system and repeat the process as new risks or requirements emerge.

### 3.2 Security Across Iterations

Security must be considered during requirements analysis, architecture design, implementation, testing, and maintenance.

For example, if a review identifies a risk that a sharing link could be reused by an unauthorized person, the team should assess the risk, design suitable access restrictions, implement the agreed controls, and test whether the restrictions work as intended.

The same process applies to data storage, authentication, redaction, retention, logging, and administrative access.

The goal is to reduce risk at every stage and prevent known security weaknesses from progressing unnoticed into later stages. Risk reduction does not guarantee that all threats can be eliminated.

## 4. Threat Model

The threat model identifies potential attacks against CLOAKID, the assets that require protection, the system's trust boundaries, and the controls that may reduce the identified risks.

The accompanying diagram is:

**File:** `threat-model.png`



The diagram's threat identifiers (T1–T11), SRS control identifiers (S1–S11), and proposed control identifiers (P1–P8) are used to distinguish threats from mitigations.

### 4.1 Assets Requiring Protection

The principal assets represented in the threat model include:

- User credentials and account information.
- Shared PII and SPII.
- Temporary stored data.
- Sharing links, tokens, and user sessions.
- Redacted information and controlled-reveal functionality.
- Activity logs and audit records.
- Administrative functions and access privileges.

### 4.2 Trust Boundaries

The diagram separates the CLOAKID system from untrusted internet traffic, user devices, and external notification services.

Security decisions should account for the fact that user devices may be compromised, receivers may misuse information they can view, and external services may have different security responsibilities.

HTTPS protects data in transit between supported endpoints when correctly configured. It does not prevent screenshots, malicious insiders, compromised endpoints, or unauthorized access caused by application vulnerabilities.

## 5. Identified Threats and Mitigations

The following threats are represented in the diagram. Controls must be checked against the SRS and validated during implementation.

### T1 — Account Takeover

**Threat:** An attacker gains access using stolen, guessed, or otherwise compromised credentials.

**Relevant SRS controls:** Email verification, multifactor authentication, and password hashing, where confirmed by the SRS.

**Proposed mitigations:** Login rate limiting, account lockout or equivalent throttling, and short-lived one-time passwords where appropriate.

**Verification:** Test authentication restrictions, credential handling, and recovery flows.

### T2 — Disclosure to an Unintended Recipient

**Threat:** Shared information reaches someone other than the intended recipient.

**Relevant SRS controls:** Verified-user sharing, sender confirmation of the receiver's profile, and resharing restrictions where specified.

**Proposed mitigation:** Bind access to the intended recipient's authenticated account rather than relying on possession of a link alone.

**Verification:** Test recipient authorization and attempts to access a share using another account.

### T3 — Interception in Transit

**Threat:** Network traffic is read or modified while being transmitted.

**Relevant SRS control:** HTTPS using TLS, as represented in the diagram.

**Proposed mitigations:** Enforce HTTPS, configure TLS securely, and use HTTP Strict Transport Security (HSTS) where appropriate.

**Verification:** Confirm that sensitive traffic is not transmitted over unencrypted HTTP.

### T4 — Theft of Stored Data

**Threat:** An attacker obtains unauthorized access to a database or storage system.

**Relevant SRS controls:** Encryption before storage and temporary storage with automatic deletion after the specified two-hour period, as represented in the diagram.

**Proposed mitigation:** Separate encryption keys from the encrypted data and restrict key access.

**Verification:** Review encryption, key-handling practices, storage permissions, and retention behavior.

### T5 — Copying or Leakage by the Receiver

**Threat:** A recipient captures or redistributes displayed information through screenshots, photographs, or other means.

**Relevant SRS controls:** Download restrictions, temporary access, mandatory watermarking, activity logging, sender notification, and time or view limits where specified.

**Proposed mitigation:** Use a receiver-identifying watermark where consistent with the approved requirements.

**Verification:** Test the relevant access restrictions and confirm that required logging and notifications work.

**Limitation:** Watermarks and download restrictions can discourage misuse, but they cannot reliably prevent photographs or all forms of screen capture.

### T6 — Bypassing Limits or Redaction

**Threat:** A user obtains additional views or accesses information that should remain concealed until authorization.

**Relevant SRS controls:** System-enforced limits, sender approval for revealing information, and revocation functionality where specified.

**Proposed mitigation:** Apply redaction on the server so concealed information is not sent to the client before authorization.

**Verification:** Test authorization checks, redaction behavior, view limits, and revocation.

### T7 — Alteration or Loss of Activity Logs

**Threat:** Security records are modified, deleted, or unavailable when an incident must be investigated.

**Relevant SRS control:** Activity logging for specified actions.

**Proposed mitigation:** Use tamper-evident logs and define suitable retention and access restrictions.

**Verification:** Confirm that required events are recorded and that unauthorized users cannot modify or delete the records.

### T8 — Misuse of Administrative Privileges

**Threat:** An administrator accesses user information or performs unauthorized administrative actions.

**SRS status:** The diagram identifies this area as a gap because no specific control is confirmed in the SRS.

**Proposed mitigations:** Apply least privilege, log administrative actions, and restrict administrative access to shared content unless explicitly authorized.

**Verification:** Review administrative permissions and test access boundaries.

### T9 — Malicious File Upload

**Threat:** A harmful or oversized file is uploaded, potentially affecting the service or its users.

**SRS status:** The diagram identifies this area as a gap because no specific control is confirmed in the SRS.

**Proposed mitigations:** Validate permitted file types and sizes, apply appropriate malware scanning, and store uploads securely if file uploads are within the approved project scope.

**Verification:** Test input validation and upload restrictions where applicable.

### T10 — Guessing or Replaying a Sharing Link

**Threat:** A sharing link is guessed, reused, or abused through a compromised session.

**Relevant SRS controls:** Secure sharing links and sessions and access restrictions for verified users, where specified.

**Proposed mitigations:** Use unpredictable link tokens, secure cookie settings, and appropriate Cross-Site Request Forgery (CSRF) protections.

**Verification:** Test token unpredictability, session handling, recipient authorization, and relevant CSRF defenses.

### T11 — Data Retained Beyond Its Deadline

**Threat:** Sensitive data remains accessible after its intended retention period.

**Relevant SRS control:** Automatic deletion after the specified retention period, represented as two hours after expiry in the diagram.

**Proposed mitigation:** Verify deletion, retry failed deletion operations, and ensure that copies and backups follow the approved retention policy.

**Verification:** Test expiration and deletion behavior, including relevant failure scenarios.

## 6. Control Classification

The threat model uses three control categories.

### 6.1 Controls Specified in the SRS

These are represented in green in the diagram. They indicate requirements attributed to the SRS, not proof that the controls have been implemented or tested.

### 6.2 Proposed Future Controls

These are represented in yellow. They are security recommendations that require review, approval, and implementation before they can be treated as system capabilities.

### 6.3 Unspecified Controls and Gaps

These are represented in grey. They identify areas where the diagram does not confirm a specific control in the SRS.

The team should assess these gaps during risk analysis and determine whether additional requirements or mitigations are necessary.

**Implementation status:** No controls are claimed as implemented solely on the basis of this document or the diagram. Implementation evidence and test results must be reviewed separately.

## 7. Security Testing and Validation

Security testing should be performed throughout the development lifecycle rather than being postponed until final submission.

Depending on the approved project scope, testing may include:

- Authentication and authorization tests.
- Attempts to access shares using unauthorized accounts.
- Tests of session and sharing-token behavior.
- Transport security checks.
- Storage encryption and access-control reviews.
- Redaction, revocation, and view-limit tests.
- Retention and deletion tests.
- Input validation and file-upload tests, if applicable.
- Logging, auditing, and administrative-permission tests.

Test results should be documented. Identified weaknesses should be prioritized, addressed where feasible, and retested.

## 8. Security and Privacy Review Process

The team should review security and privacy considerations at every Spiral Model iteration.

For each iteration:

1. Identify new or changed assets, threats, and trust boundaries.
2. Assess the likelihood and impact of relevant risks.
3. Select and document mitigation measures.
4. Implement approved controls within the project scope.
5. Test the controls and record the results.
6. Reassess remaining risks and plan the next iteration.

High-impact risks involving unauthorized disclosure of PII or SPII should receive particular attention.

## 9. Limitations and Assumptions

- The approved SRS remains the authoritative source for requirements.
- The threat model includes both SRS-derived controls and proposed future controls.
- Proposed mitigations must not be presented as implemented features.
- The diagram's assumptions should be reviewed against the actual system design.
- Security measures reduce risk but do not guarantee complete prevention of attacks.
- Any retention period, notification behavior, or access restriction must be confirmed against the approved requirements.

## 10. Conclusion

CLOAKID must treat data security and privacy as priorities throughout its lifecycle. The Spiral Model provides a structured way to identify threats, evaluate risks, apply mitigations, and reassess the system at every iteration.

The threat model supports this process by making key assets, threats, controls, and gaps visible to the development team. It should be updated as the SRS, architecture, implementation, and security test results evolve.
