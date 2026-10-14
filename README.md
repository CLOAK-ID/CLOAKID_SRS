# CLOAKID
🔐 CLOAKID — A secure, verified, and controlled PII/SPII data-sharing platform with encryption, redaction, access controls, watermarking, activity tracking, and sender-controlled data access.

🔐 CLOAKID

Secure & Controlled PII/SPII Data Sharing Platform

CLOAKID is a secure web-based data-sharing platform designed for sharing Personally Identifiable Information (PII) and Sensitive Personally Identifiable Information (SPII) between verified users.

Unlike traditional file-sharing systems, CLOAKID focuses on giving the sender continuous control over shared data, even after it has been sent. Senders can define who can access their data, how long it remains accessible, how many times it can be viewed, whether it can be reshared, and when access should be revoked.

The system is designed around security, privacy, controlled disclosure, traceability, and temporary data storage.

---

🎯 Project Purpose

CLOAKID aims to provide a safer way to share sensitive information without relying on unrestricted public links or permanent file storage.

The platform is intended for information such as:

- Government/identity documents
- ID numbers
- Contact information
- Sensitive documents
- Medical records
- Criminal records
- Domicile information
- Other PII and SPII

The system ensures that sensitive information is shared only with verified users and remains accessible according to rules defined by the sender.

---

✨ Key Features

1. 👤 Verified User Sharing

CLOAKID uses a verification-based sharing model.

Both sender and receiver must have verified accounts before sensitive information can be exchanged.

Includes

- User registration
- Email verification
- Authentication
- Multi-factor authentication
- Verified receiver checking
- Prevention of sharing with unverified users

When a sender enters a receiver's email address, CLOAKID verifies whether that user exists and has a verified account before allowing the sharing process to continue.

---

2. 📤 Controlled Data Sharing

The sender can initiate a secure sharing session and choose how information will be provided.

Sharing modes

- Image Mode
- Form/Template Mode

The sender can upload or capture an image or create information using a predefined/custom form.

---

3. 🕵️ Sensitive Data Redaction

Before sharing information, the sender can hide sensitive portions of the data.

Supported redaction concepts include:

- Blur
- Pixelation
- Hiding selected areas
- Selective disclosure

This allows the sender to expose only the information required by the receiver.

---

4. 🔍 Progressive Disclosure

One of CLOAKID's main features is Progressive Disclosure.

Instead of exposing an entire document immediately, the receiver initially sees only the permitted information.

If additional information is required, the receiver can request access to more content.

The sender then decides whether the additional information should be revealed.

Example

A user needs to verify an identity document but does not need to see the complete document.

CLOAKID can initially hide certain fields.

The receiver can request access to a hidden section, while the sender retains the ability to approve or reject the request.

---

5. 👑 Sender Control After Sharing

CLOAKID is designed around the principle that sharing data should not mean losing control over it.

After sending information, the sender can:

- View active sharing sessions
- Modify permissions
- Change expiry time
- Change view limits
- Modify sharing permissions
- Revoke access
- Re-grant access
- Monitor receiver activity
- Respond to access requests
- Delete a sharing session

---

6. ⏱️ Time-Based Access Control

The sender can define how long the receiver can access shared information.

Once the permitted access period expires, the system restricts access.

The SRS specifies a deletion window after expiration during which access can potentially be restored or modified before permanent deletion.

---

7. 👁️ View Limits

The sender can control how many times the receiver can view shared information.

For every access:

- The system tracks the view
- The remaining view count is updated
- The sender receives an activity notification
- Access is blocked when the permitted limit is reached

---

8. 🚫 Revoke Access

The sender can immediately stop access to previously shared information.

When access is revoked:

1. The sender selects Revoke Access
2. The active permission is invalidated
3. The receiver can no longer access the shared data

This provides the sender with control even after the data has already been shared.

---

9. 🔄 Re-Grant Access

Previously revoked access can be restored by the sender.

The sender can reactivate permissions and potentially increase:

- Access duration
- Number of permitted views

---

10. 🔗 Controlled Resharing

By default, resharing is disabled.

If the sender allows resharing, it can be restricted according to the sharing rules defined by the system.

Resharing activity is also recorded so that the sender can maintain visibility over where the information has been shared.

---

11. 💧 Watermarking

Shared information receives a watermark for security and traceability.

The watermark can be:

- Customized by the sender
- Generated using the purpose of sharing
- Applied with the default phrase defined by the system

The SRS specifies the default watermark concept as:

«"NOT VALID FOR OTHER PURPOSES"»

Watermarks are intended to discourage misuse and provide visible context about the purpose of shared information.

---

12. 📋 Activity Monitoring & Audit Logs

CLOAKID records activities associated with shared data.

The sender can monitor:

- Who accessed the information
- When it was accessed
- Number of views
- Access requests
- Resharing activity, where permitted
- Other relevant sharing events

These activities are stored as audit information to provide traceability and accountability.

---

13. 🔔 Notifications

The system provides notifications for important sharing events.

Examples include:

- New data shared with a receiver
- Receiver viewed the data
- Receiver requested additional access
- Receiver requested hidden information
- Data was reshared where permitted
- Access requests were approved or rejected

Notifications are intended to keep the sender aware of activity involving their shared information.

---

14. 🔐 Encryption & Secure Transmission

CLOAKID is designed to encrypt sensitive information before temporary storage and transmission.

The SRS specifies:

- Encryption of sensitive data
- Secure HTTPS/TLS communication
- Temporary encrypted storage
- Decryption when authorized data is viewed

Data is intended to remain encrypted until a valid access request is processed.

---

15. 🗑️ Temporary Data Storage & Automatic Deletion

CLOAKID is not intended to be a permanent file-storage platform.

Shared information remains available only for the defined sharing/deletion period.

After the deletion deadline:

- The shared session is removed
- Stored data is permanently deleted
- The original/shared temporary copy is removed according to the system's deletion process

The SRS specifies a two-hour post-expiration deletion window.

---

👥 User Roles

Sender

The sender is the primary controller of shared information.

The sender can:

- Register and verify an account
- Select a receiver
- Upload/create information
- Redact sensitive information
- Preview the receiver's view
- Apply watermarks
- Configure access controls
- Share information
- Monitor activity
- Modify permissions
- Revoke access
- Re-grant access
- Respond to access requests
- Delete sharing sessions

---

Receiver

The receiver accesses information under the permissions defined by the sender.

The receiver can:

- Log in
- Receive sharing notifications
- View permitted information
- Check remaining access/view limits
- Request additional access
- Request visibility of hidden areas
- View updated information after approval

The receiver does not receive unrestricted download or permanent-storage functionality according to the current SRS.

---

Administrator

The administrator supervises the operation of the platform.

Responsibilities include:

- Monitoring system activity
- Managing users where required
- Maintaining system integrity
- Receiving user feedback
- Supporting system improvements

---

🔄 How CLOAKID Works

A typical sharing workflow is:

Register
   ↓
Email Verification / MFA
   ↓
Login
   ↓
Select Receiver
   ↓
Verify Receiver
   ↓
Choose Image / Form
   ↓
Upload or Create Data
   ↓
Redact Sensitive Information
   ↓
Preview Receiver's View
   ↓
Apply Watermark
   ↓
Configure Access Controls
   ├── Expiry Time
   ├── View Limit
   └── Reshare Permission
   ↓
Encrypt Data
   ↓
Create Secure Sharing Session
   ↓
Notify Receiver
   ↓
Receiver Views Data
   ↓
Activity Logged
   ↓
Sender Can Modify / Revoke / Re-Grant Access
   ↓
Expiration
   ↓
Temporary Deletion Window
   ↓
Permanent Data Deletion

---

🛡️ Security Model

CLOAKID's security model is based on multiple layers:

Verified Identity
       ↓
Authentication / MFA
       ↓
Receiver Verification
       ↓
Encryption
       ↓
Temporary Secure Storage
       ↓
Access Control
       ↓
Time & View Restrictions
       ↓
Watermarking
       ↓
Activity Logging
       ↓
Sender-Controlled Revocation
       ↓
Automatic Deletion

The system boundary defined in the SRS includes encryption/decryption, secure session/token generation, temporary storage, watermarking, access-control enforcement, activity logging, and notification handling.

---

📊 Core Security Controls

Security Control| CLOAKID
Verified users| ✅
Email verification| ✅
Multi-factor authentication| ✅
Receiver verification| ✅
Encryption| ✅
HTTPS/TLS| ✅
Redaction| ✅
Progressive disclosure| ✅
Expiry-based access| ✅
View limits| ✅
Sender-controlled revocation| ✅
Re-grant access| ✅
Resharing restrictions| ✅
Watermarking| ✅
Activity/audit logs| ✅
Notifications| ✅
Temporary storage| ✅
Automatic deletion| ✅
Permanent unrestricted storage| ❌
Anonymous sharing| ❌
Public file sharing| ❌
Unrestricted downloading| ❌

---

🧩 System Architecture Concept

At a high level, CLOAKID will consist of:

                 ┌─────────────────────┐
                 │       User          │
                 │ Sender / Receiver   │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │   CLOAKID Web App   │
                 └──────────┬──────────┘
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
       Authentication   Data Sharing   Access Control
             │              │              │
             ▼              ▼              ▼
       Verification     Encryption    Expiry / Views
                            │
                            ▼
                    Temporary Storage
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
        Watermarking     Audit Logs    Notifications
                            │
                            ▼
                    Automatic Deletion

The exact implementation architecture, technology stack, database design, and deployment configuration are not specified by the current SRS and will be determined during implementation.

---

📁 Project Scope

CLOAKID covers:

- Secure upload of sensitive information
- Verified-user data sharing
- Authentication
- Encryption
- Controlled access
- Redaction
- Progressive disclosure
- Expiry-based access
- View limitations
- Watermarking
- Activity tracking
- Access requests
- Sender-controlled revocation
- Temporary storage
- Automatic deletion

CLOAKID does not cover:

- Public file sharing
- Anonymous users
- General social-media functionality
- Casual file sharing
- Large-scale unrelated data storage
- Permanent unrestricted file storage

---

🚧 Project Status

«Status: SRS / Development Planning»

This repository currently contains the requirements and design documentation for CLOAKID.

The implementation will progressively convert the requirements defined in the SRS into a functional secure data-sharing platform.

---

🗺️ Planned Development

The implementation can be developed in stages:

Phase 1 — Authentication

- Registration
- Login
- Email verification
- MFA
- User management

Phase 2 — Secure Sharing

- Receiver verification
- Image/Form sharing
- Temporary sharing sessions
- Secure links

Phase 3 — Data Protection

- Encryption
- Redaction
- Watermarking
- Secure temporary storage

Phase 4 — Access Control

- Expiry times
- View limits
- Revoke access
- Re-grant access
- Resharing controls

Phase 5 — Progressive Disclosure

- Hidden areas
- Request-more workflow
- Sender approval/rejection
- Updated receiver view

Phase 6 — Monitoring

- Activity logs
- View tracking
- Reshare tracking
- Notifications
- Audit trail

Phase 7 — Lifecycle Management

- Expiration handling
- Temporary recovery/change window
- Automatic deletion
- Permanent removal

---

🎓 Academic Project

Project: CLOAKID
Course: ADSS
Institution: Quaid-e-Azam University, Islamabad

CLOAKID was designed as a software engineering project focused on secure information sharing, privacy, authentication, access control, and traceability.

---

👨‍💻 Team

- Muhammad Hassan
- Hasnain Shabbir
- Moazzam
- Hajra Kareem

---

📄 Documentation

The complete Software Requirements Specification is available in this repository:

"CLOAKID SRS" (./CLOAKID_SRS.pdf)

The SRS contains:

- System scope
- Requirements
- Distinguished features
- Sender use cases
- Receiver use cases
- System use cases
- Actors
- System boundaries
- Business rules
- Constraints
- Assumptions
- Use-case diagram

---

⚠️ Important Security Note

CLOAKID is designed as a security-focused academic project. Security claims made by the project should be validated through implementation testing, code review, penetration testing, and appropriate security assessment before the system is used for real sensitive information.

The current SRS defines the intended functionality and security requirements; it does not by itself guarantee that an implementation will be secure.

---

📜 License

License information will be added when the project licensing decision is finalized.
