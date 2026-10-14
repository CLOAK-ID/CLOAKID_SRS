# CLOAKID Requirements and Use Cases

## 1. Overview

CLOAKID is designed to enable users to share sensitive personal information (PII) and sensitive personal information (SPII) securely. The system provides mechanisms for controlled sharing, redaction, access restrictions, notifications, activity tracking, and automatic deletion of expired shared data.

This document describes the system actors, functional requirements, and principal use cases represented in the CLOAKID Use Case Diagram. It is based on the CLOAKID Software Requirements Specification (SRS).

## 2. System Actors

The system includes the following actors.

| Actor | Description |
|---|---|
| Sender | The primary actor who prepares and shares sensitive information, configures access controls, and manages shared data. |
| Receiver | The secondary actor who receives shared information and accesses it according to the sender's permissions. |
| User | A general role representing common account-related activities, including registration, email verification, and login. |
| Admin (Optional) | An administrative role that may support system activity monitoring and user management, subject to the final system scope. |

The Sender and Receiver are specialized user roles. Depending on the sharing workflow, a user may act as a sender in one interaction and a receiver in another.

## 3. Functional Requirements

The following requirements are derived from the use-case diagram and should be checked against the approved SRS before being treated as the final requirements baseline.

### 3.1 Account Management

- **FR-01: Account Registration** — The system shall allow users to register an account.
- **FR-02: Email Verification** — The system shall support email verification for user accounts.
- **FR-03: User Login** — The system shall allow registered users to log in.

### 3.2 Data Sharing and Preparation

- **FR-04: Initiate Sharing** — The system shall allow a sender to initiate a sharing process by entering the receiver's email address.
- **FR-05: Select Sharing Mode** — The system shall allow the sender to select an appropriate sharing mode, such as an image or form template.
- **FR-06: Upload or Create Data** — The system shall allow the sender to upload or create the information to be shared.
- **FR-07: Redact Information** — The system shall support redaction operations such as blurring, pixelation, or hiding selected information.
- **FR-08: Preview Shared Data** — The system shall allow the sender to preview the data before sharing it.
- **FR-09: Configure Access Controls** — The system shall allow the sender to configure applicable sharing restrictions, including expiry, view limits, resharing permissions, and watermarking.
- **FR-10: Send Shared Data** — The system shall allow the sender to initiate the sharing process after preparing the information and configuring the applicable controls.

### 3.3 Shared Data Management

- **FR-11: Manage Shared Data** — The system shall support applicable management operations, including modifying, revoking, re-granting access to, and deleting shared data.
- **FR-12: Respond to Access Requests** — The system shall allow the sender to respond to access requests from receivers.
- **FR-13: Track Sharing Activity** — The system shall provide the sender with access to relevant activity information and access logs.

### 3.4 Receiver Operations

- **FR-14: Receive Notifications** — The system shall notify receivers about relevant sharing events.
- **FR-15: View Shared Data** — The system shall allow an authorized receiver to view shared information.
- **FR-16: Request Additional Access** — The system shall allow a receiver to request additional access when required.
- **FR-17: Mark Areas for Reveal** — The system shall allow a receiver to mark an area of shared information for possible reveal, where supported by the sharing mode.
- **FR-18: Request Access to a Marked Area** — The system shall allow a receiver to request permission to access a marked area.
- **FR-19: View Updated Data** — The system shall allow the receiver to view updated information when the sender changes the shared data or grants the requested access.

### 3.5 Internal System Operations

- **FR-20: Verify Receiver Identity** — The system shall support verification of the intended receiver's identity before granting access, as specified by the SRS.
- **FR-21: Prepare a Secure Copy** — The system shall create a secure copy of shared information and apply the specified encryption and watermarking controls.
- **FR-22: Generate a Sharing Session** — The system shall generate the necessary sharing session or secure-link information and initiate relevant notifications.
- **FR-23: Decrypt at Viewing Time** — The system shall perform the required decryption operation when authorized access to shared information is granted.
- **FR-24: Enforce Access Restrictions** — The system shall enforce configured view limits and expiry restrictions.
- **FR-25: Automatically Delete Expired Data** — The system shall support automatic deletion of expired shared information. The diagram represents a two-hour delay after expiry; this timing must be verified against the approved SRS.
- **FR-26: Record Activity and Audit Logs** — The system shall record relevant events to support activity tracking and auditing.

### 3.6 Optional Administrative Operations

- **FR-27: Administrative Login** — The system shall support a separate administrative login process if an admin interface is included.
- **FR-28: Monitor System Activity** — The system shall support administrative monitoring of relevant system activity.
- **FR-29: Manage Users** — The system shall support authorized administrative user-management operations if included in the final scope.

## 4. Principal Use Cases

### 4.1 Register and Log In

**Primary actor:** User

**Description:** A user registers an account, verifies their email address, and logs in to access the system.

**Main flow:**
1. The user opens the application.
2. The user registers an account or enters existing login credentials.
3. The system performs the applicable validation and authentication checks.
4. Where required, the system verifies the user's email address.
5. The system grants access after successful authentication.

**Expected outcome:** The user can access the system using a valid account.

### 4.2 Share Sensitive Information

**Primary actor:** Sender

**Supporting components:** Receiver identity verification, security processing, access control, notifications, and activity tracking.

**Description:** The sender prepares sensitive information and shares it with an intended receiver under configured restrictions.

**Main flow:**
1. The sender initiates a sharing process and enters the receiver's email address.
2. The sender selects a sharing mode.
3. The sender uploads or creates the information.
4. The sender applies redaction where necessary and previews the result.
5. The sender configures access controls.
6. The system performs the required receiver-verification and security operations.
7. The system creates the secure sharing session or link.
8. The system initiates relevant notifications and records applicable activity.

**Expected outcome:** The information is prepared for controlled sharing with the intended receiver.

### 4.3 View Shared Information

**Primary actor:** Receiver

**Supporting components:** Access control, decryption, expiry enforcement, and activity tracking.

**Description:** The receiver accesses shared information according to the sender's configured permissions.

**Main flow:**
1. The receiver receives a sharing notification.
2. The receiver opens the relevant sharing link or session.
3. The system verifies the receiver's identity and checks the applicable access rules.
4. The system checks whether the information is still available and whether access limits have been reached.
5. The system performs the required decryption operation.
6. The receiver views the authorized information.
7. The system records the relevant access event.

**Expected outcome:** The receiver can view shared information only when the applicable access conditions are satisfied.

### 4.4 Request Additional Access

**Primary actor:** Receiver

**Supporting actor:** Sender

**Description:** The receiver requests additional access to shared information or to a specific marked area.

**Main flow:**
1. The receiver attempts to access information that requires additional permission.
2. The receiver submits an access request or marks an area for reveal and requests access to it.
3. The system notifies the sender of the request.
4. The sender reviews the request.
5. The sender approves, rejects, or otherwise responds according to the supported workflow.
6. If access is granted, the receiver can access the permitted information under the updated rules.

**Expected outcome:** The request is processed, and access is updated only when authorized.

### 4.5 Manage Shared Information

**Primary actor:** Sender

**Description:** The sender manages information that has already been shared.

**Main flow:**
1. The sender opens the relevant shared-data record.
2. The sender selects an available management operation.
3. The system validates the sender's authority to perform the operation.
4. The system applies the permitted modification, revocation, re-granting, or deletion operation.
5. The system records relevant activity.

**Expected outcome:** The shared information and its access permissions reflect the authorized changes.

### 4.6 Automatically Delete Expired Information

**Primary actor:** System

**Description:** The system removes shared information when its permitted retention period has ended.

**Main flow:**
1. The system identifies shared information whose expiry condition has been met.
2. The scheduled deletion process determines when deletion should occur.
3. The system deletes the applicable expired data.
4. The system records relevant deletion activity where required.

**Expected outcome:** Expired shared information is removed according to the approved retention policy.

**Note:** The two-hour delay shown in the diagram is a design detail that must be confirmed against the SRS and implementation.

## 5. Use Case Relationships

The diagram represents the following relationships.

| Relationship | Meaning in the Diagram |
|---|---|
| Sender and Receiver to User | Sender and Receiver represent specialized user roles. |
| Initiate Sharing includes Verify Receiver Identity | Sharing initiation includes the intended receiver-verification step. |
| Send Data includes Prepare Secure Copy | The sharing process includes the required security preparation. |
| Send Data includes Generate Session and Notifications | The sharing process includes session generation and notification activities. |
| Redaction extends Upload/Create Data | Redaction is an optional or conditional extension of data preparation. |
| Request Additional Access extends View Shared Data | An additional-access request can occur during the viewing workflow. |
| Mark Area for Reveal extends View Shared Data | Marking an area is an optional viewing-related interaction. |
| Request Access to Marked Area includes Mark Area | The request applies to an area identified by the receiver. |
| View Shared Data includes Decryption | Authorized viewing requires the applicable decryption operation. |
| View Shared Data includes Access Enforcement | The system checks applicable access restrictions during viewing. |
| View Shared Data includes Activity Auditing | Relevant viewing activity is recorded. |
| Access Request notifies Sender | The sender is notified when a receiver submits a relevant request. |
| Access Enforcement followed by Auto-delete | The diagram illustrates expiry enforcement followed by the deletion process. This is a process relationship, not a standard UML include/extend relationship. |

Mermaid flowcharts do not provide native UML use-case notation. The diagram therefore uses flowchart shapes and labelled arrows to communicate actors, use cases, and their relationships.

## 6. Security and Privacy Considerations

The use cases incorporate security and privacy objectives that must be considered during implementation and testing.

- **Identity verification:** Ensure that shared information is accessed by the intended recipient.
- **Authorization:** Enforce the sender's configured access rules before providing access.
- **Confidentiality:** Protect sensitive information during transmission, storage, and authorized viewing.
- **Redaction:** Support hiding or obscuring information that should not be disclosed.
- **Controlled sharing:** Apply expiry, view limits, resharing restrictions, and watermarking where configured.
- **Auditability:** Record relevant sharing, access, permission-change, and deletion events.
- **Data retention:** Remove expired information according to the approved retention requirements.
- **Administrative restrictions:** If administrative functionality is included, restrict it to authorized administrators.

These are intended requirements and design considerations; they do not by themselves demonstrate that the controls have been implemented or tested.

## 7. Scope and Validation Notes

1. The administrative functions are marked optional and should be confirmed against the approved SRS.
2. The diagram represents automatic deletion two hours after expiry. This timing should be validated before being treated as a definitive requirement.
3. The exact receiver-verification method, cryptographic mechanisms, and secure-session implementation must be defined in the appropriate technical documentation.
4. The precise conditions for modifying shared data, re-granting access, and viewing updated data should be specified in detailed use-case descriptions.
5. The diagram describes logical interactions; it does not establish that every feature has been implemented.
6. The functional requirements in this document should be reviewed against the approved SRS to resolve any differences before implementation or final submission.

## 8. Conclusion

The CLOAKID use cases describe how users register and authenticate, prepare and share sensitive information, configure access controls, view shared data, request additional permissions, and manage shared information. Internal system operations support security processing, access enforcement, notifications, activity tracking, and data deletion.

Together, these requirements provide a structured basis for implementation planning, system testing, and validation of CLOAKID's intended security and privacy behavior.