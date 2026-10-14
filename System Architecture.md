---
title: CLOAKID System Architecture
---

# CLOAKID — System Architecture

## 1. Introduction

CLOAKID is a software project designed to support the secure sharing of Personally Identifiable Information (PII) and Sensitive Personally Identifiable Information (SPII).

This document describes the proposed system architecture, including the presentation layer, business logic layer, data layer, and external notification service.

The architecture is based on the CLOAKID Software Requirements Specification (SRS). Where the diagram includes an interpretation that is not explicitly established by the SRS, that distinction is identified.

## 2. Architectural Overview

CLOAKID is represented using a three-layer architecture:

1. **Presentation layer:** Provides interfaces through which senders, receivers, and, if included in scope, administrators interact with the system.
2. **Business logic layer:** Handles authentication, sharing, access control, security operations, notifications, activity tracking, and automatic deletion.
3. **Data layer:** Stores user information, temporary shared data, access rules, activity logs, and notification records.

An external email or notification service supports the delivery of notifications outside the application's internal components.

### System Architecture Diagram

The following diagram illustrates the proposed component structure and relationships.

**File:** `system-architecture.png`

![CLOAKID System Architecture](system-architecture.png)

The diagram represents the proposed design. It should not be interpreted as proof that these components have already been implemented.

## 3. Presentation Layer

The presentation layer provides the user-facing interfaces through a web browser.

### 3.1 Sender Interface

The sender interface supports the actions available to a person sharing information. Depending on the approved requirements, these actions may include initiating a share, configuring access restrictions, and managing the shared information.

### 3.2 Receiver Interface

The receiver interface allows the intended recipient to interact with information shared through CLOAKID, subject to authentication and the applicable access rules.

### 3.3 Administrator Interface

The diagram includes an optional administrator interface. Its inclusion and capabilities must be confirmed against the approved SRS.

Administrative access should be restricted according to defined permissions. The architecture diagram alone does not establish which administrative actions are authorized.

### 3.4 Communication with the Application

The diagram shows browser communication with the application over HTTPS using TLS.

HTTPS helps protect data in transit when configured correctly. It does not, by itself, guarantee the security of the application, user devices, stored data, or access-control logic.

## 4. Business Logic Layer

The business logic layer contains the proposed modules responsible for application behavior and security-related operations.

### 4.1 Authentication Module

The authentication module manages user authentication and the events associated with it.

Its responsibilities should be aligned with the approved authentication requirements. Successful authentication must not automatically grant access to every shared item; authorization checks are also required.

### 4.2 Sharing Module

The sharing module coordinates the process of sharing information.

The diagram associates this module with redaction, watermarking, and secure-link creation. It also shows the module defining rules for the Access Control Module.

The implementation must ensure that sharing operations follow the approved requirements and that sensitive information is not disclosed to unauthorized recipients.

### 4.3 Access Control Module

The access control module evaluates whether a user is permitted to perform an action or view shared information.

The diagram shows it interacting with the Sharing Module and Security Module. Access restrictions should be enforced by the application rather than relying solely on the presentation layer.

### 4.4 Security Module

The Security Module represents the encryption and decryption responsibilities shown in the diagram.

The proposed flow indicates that a copy of shared information is encrypted before storage and decrypted when an authorized recipient views it.

The exact encryption algorithms, key-management design, and handling of decrypted information must be established through detailed security design. They should not be inferred from the diagram alone.

### 4.5 Notification Module

The notification module coordinates notifications associated with sharing, viewing, and access requests, as represented in the architecture.

The notification behavior, supported delivery channels, and events that trigger notifications must follow the SRS.

### 4.6 Activity Tracking Module

The Activity Tracking Module records relevant application events.

The diagram shows authentication, sharing, and access-control activities generating events for this module, which stores activity logs in the data layer.

The design should define which events are recorded, who can access the records, and how long they are retained.

### 4.7 Automatic Deletion Job

The architecture includes an automatic deletion job that removes expired shared data.

The diagram represents deletion two hours after expiry. The retention period and its precise interpretation must match the approved SRS.

The SRS does not explicitly assign ownership of this function to a particular module, so its placement in the business logic layer is an architectural interpretation.

The implementation should also consider deletion failures and any other copies of data covered by the approved retention policy.

## 5. Data Layer

The data layer is represented by MongoDB and contains the following logical data categories.

### 5.1 User Data

Stores user-related information required by the application, potentially including account and authentication-related data as permitted by the SRS.

Sensitive information should be protected using appropriate access controls and storage safeguards.

### 5.2 Temporary Shared Data

Represents shared information that is stored temporarily and encrypted, as shown in the diagram.

The data lifecycle should follow the approved sharing, expiration, and deletion requirements.

### 5.3 Access Rules

Stores or represents the rules used to determine whether a user may access a shared item.

These rules must be enforced by the application's authorization logic.

### 5.4 Activity Logs

Stores records generated by the Activity Tracking Module.

Access to logs should be restricted, and their integrity and retention should be considered during security design.

### 5.5 Notifications

Represents notification records associated with the application's notification functionality.

The exact information stored and its retention period should be determined by the approved requirements and privacy considerations.

**Architecture note:** The diagram presents these as logical data categories. It does not establish whether each category will use a separate MongoDB database, collection, or document structure. Those implementation details require a separate data design.

## 6. External Notification Service

The diagram places the email or notification service outside the CLOAKID system boundary.

The Notification Module communicates with this external service to deliver notifications through supported channels.

The external service should receive only the information necessary to perform its function. Sensitive PII or SPII should not be included in notification content unless explicitly required and appropriately protected.

The team's design should document the service's responsibilities, data exchanged, and relevant privacy considerations.

## 7. Main Component Interactions

The proposed architecture represents the following interactions:

1. A sender or receiver interacts with CLOAKID through a browser interface.
2. The Authentication Module handles authentication-related operations.
3. The Sharing Module coordinates the sharing process and defines applicable access rules.
4. The Access Control Module evaluates access according to those rules.
5. The Security Module performs the encryption and decryption operations represented in the design.
6. Relevant application events are passed to the Activity Tracking Module.
7. The Notification Module coordinates notifications and communicates with the external service.
8. The automatic deletion job removes expired shared data according to the defined retention policy.

These interactions describe the intended architectural responsibilities, not a verified execution sequence for every use case.

## 8. Security Considerations

Security is a primary consideration because CLOAKID handles sensitive information.

The architecture should be reviewed for:

- Authentication and authorization weaknesses.
- Unauthorized access to shared information.
- Secure handling of encryption keys.
- Protection of sensitive data in transit and at rest.
- Correct enforcement of sharing rules, redaction, and revocation.
- Appropriate activity logging and restricted log access.
- Reliable expiration and deletion of temporary data.
- Privacy risks involving external notification services.
- Appropriate separation of user and administrative privileges.

These considerations should be reviewed throughout design, implementation, and testing. Their inclusion in this document does not confirm that the associated controls have been implemented.

## 9. Architectural Assumptions and Limitations

- The architecture is based on the available CLOAKID SRS and the accompanying diagram.
- Node.js, Express.js, and MongoDB are shown as the proposed technologies.
- The administrator interface is optional and requires confirmation against the project scope.
- The automatic deletion job's placement in the business logic layer is an interpretation rather than an explicitly assigned SRS responsibility.
- The diagram does not specify deployment topology, database schema, API contracts, encryption algorithms, or key-management mechanisms.
- Actual implementation and testing evidence is needed before any component can be described as operational.

## 10. Conclusion

The proposed CLOAKID architecture separates user interaction, application logic, and data storage into distinct layers. Its modules represent the major responsibilities involved in authentication, secure sharing, access control, encryption, notification, activity tracking, and data retention.

This separation provides a foundation for further design and implementation. The architecture should be refined against the approved SRS and reviewed for security, privacy, correctness, and feasibility before implementation decisions are finalized.