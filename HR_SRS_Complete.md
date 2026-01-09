# Software Requirements Specification (SRS)
# HR Onboarding Agent System

**Document Version Control**

| Version | Date       | Author   | Change Description                                      |
|---------|------------|----------|--------------------------------------------------------|
| 1.0     | 2026-01-09 | Md Sahil | Initial SRS document derived from HLD v2.1 |

---

## Document Approval

| Role                    | Name      | Signature | Date       |
|-------------------------|-----------|-----------|------------|
| Project Sponsor         |           |           |            |
| Project Manager         | Md Sahil  |           | 2026-01-09 |
| Technical Lead          |           |           |            |
| Quality Assurance Lead  |           |           |            |
| Business Analyst        |           |           |            |

---

## Executive Summary

This Software Requirements Specification (SRS) document provides a comprehensive description of the **HR Onboarding Agent System** for Sampurna Financial Services Pvt. Ltd. (SFSPL). The system digitalizes and automates the complete recruitment and onboarding lifecycle, processing approximately **1500 interviews per month**.

### Current Challenge

SFSPL's recruitment process is manual, relying on WhatsApp messaging, Excel spreadsheets, and email communications, resulting in:
- Data loss and duplication
- Delayed and unstructured communication  
- Limited visibility on candidate progress
- No tracking of interview lifecycle
- Inability to perform meaningful analysis

### Solution Overview  

A comprehensive digital platform with:
- **Multi-stage digital forms** (Form-1 through Form-4)
- **QR code-based check-in** with dual candidate paths
- **Automated notifications** via WhatsApp and Email
- **Background verification tracking**
- **Complete audit trails** for compliance
- **Real-time analytics** and reporting
- **Multilingual support** (English, Hindi, Bengali)

### Key Outcomes

- ✅ 100% digital capture of candidate information
- ✅ 90% reduction in manual data entry
- ✅ 50% reduction in time-to-hire
- ✅ Real-time visibility for all stakeholders
- ✅ Complete compliance with data retention requirements
- ✅ Scalable architecture supporting 1500+ monthly interviews

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Overall Description](#2-overall-description)
3. [System Features](#3-system-features)
4. [External Interface Requirements](#4-external-interface-requirements)
5. [Non-Functional Requirements](#5-non-functional-requirements)
6. [Other Requirements](#6-other-requirements)
7. [Appendices](#7-appendices)

---

## 1. Introduction

### 1.1 Purpose

This SRS document specifies all functional and non-functional requirements for the HR Onboarding Agent System. It serves as:
- Primary reference for development team
- Basis for project planning and estimation
- Foundation for testing and validation
- Contractual agreement between stakeholders

**Target Audience:** Development team, QA engineers, project managers, business analysts, HR personnel, system administrators, executive management.

### 1.2 Scope

#### Problem Statement

SFSPL's current employee onboarding process is highly manual and unstructured:
- Candidates submit CVs via WhatsApp with no tracking
- HR conducts preliminary assessments through unstructured calls
- Interview information recorded in disparate Excel sheets
- No centralized candidate database
- Only mandatory details entered into HRMS post-hire
- Significant data loss throughout recruitment lifecycle
- Inability to analyze recruitment trends

#### Solution Scope

**In Scope:**
- Candidate registration and profile management (Forms 1-4)
- Interview scheduling with QR-based check-in
- Dual candidate path handling (screened vs. walk-in)
- Interview evaluation and selection workflow
- Background verification tracking
- Offer letter generation and delivery
- Onboarding checklist management
- Multi-channel notifications (Email, WhatsApp)
- Real-time analytics and reporting
- Multilingual support (English, Hindi, Bengali)
- Complete audit trail

**Out of Scope (Phase 1):**
- Automated background verification (manual HR process)
- Direct HRMS integration (manual data export)
- AI-powered candidate matching
- Video interview platform
- Payroll integration

###  1.3 Definitions and Acronyms

| Term | Definition |
|------|------------|
| **API** | Application Programming Interface |
| **BG Verification** | Background Verification |
| **CV** | Curriculum Vitae (Resume) |
| **Form-1** | Basic candidate registration form |
| **Form-2** | Qualifications, skills, and documents form |
| **Form-3** | Interview evaluation form (completed by panel) |
| **Form-4** | Final onboarding details (bank, emergency contacts) |
| **HRMS** | Human Resource Management System (Octane) |
| **JWT** | JSON Web Token for authentication |
| **KYC** | Know Your Customer verification documents |
| **n8n** | Workflow automation tool |
| **QR** | Quick Response code for check-in |
| **RBAC** | Role-Based Access Control |
| **Screened Candidate** | Candidate who submitted Form-1 before interview |
| **SFSPL** | Sampurna Financial Services Pvt. Ltd. |
| **Walk-in Candidate** | Candidate appearing for first time at interview |

### 1.4 References

- HR Onboarding Agent HLD v2.1 (December 2025)
- IEEE Std 830-1998 (Software Requirements Specifications)
- SFSPL HR Policy Manual
- PostgreSQL 15 Documentation
- FastAPI Documentation  
- Streamlit Documentation

---

## 2. Overall Description

### 2.1 Product Perspective

The HR Onboarding Agent is a new, self-contained system designed specifically for SFSPL's recruitment needs. It operates independently while interfacing with:
- **WhatsApp Business API** (via n8n)
- **Email Services** (SMTP)
- **Supabase** (PostgreSQL database and blob storage)
- **Octane HRMS** (one-way data export)

### 2.2 Product Functions

**Major Functions:**

1. **Candidate Registration** - Multi-stage form capture (Forms 1-4)
2. **Interview Management** - Scheduling, QR check-in, dual-path routing
3. **Evaluation & Selection** - Panel assessments, HR decisions
4. **Background Verification** - Status tracking and workflow
5. **Offer Management** - Generation, delivery, acceptance tracking
6. **Onboarding** - Induction management, Form-4 completion
7. **Communications** - Automated WhatsApp/Email notifications
8. **Analytics** - Real-time dashboards and reports
9. **Security** - JWT authentication, RBAC, audit logging

### 2.3 User Classes

| User Class | Characteristics | Key Tasks |
|------------|----------------|-----------|
| **Candidate** | Job applicants; low-medium tech proficiency; episodic use | Submit forms, scan QR, check status, accept offer |
| **HR Personnel** | Daily users; medium-high tech proficiency | Schedule interviews, review applications, make selections, generate reports |
| **Interview Panel** | Weekly-monthly users; medium tech proficiency | Access candidate profiles, complete evaluations |
| **HR Manager** | Daily users; medium tech proficiency; approval authority | Review metrics, approve decisions, audit activities |
| **System Admin** | As-needed; high tech proficiency | Deploy updates, manage infrastructure, troubleshoot issues |

### 2.4 Operating Environment

**Server:**
- Azure VM (Ubuntu 24.04 LTS)
- 4-8 CPU cores, 16GB RAM
- Docker containerized deployment

**Client:**
- Modern web browsers (Chrome 110+, Firefox 115+, Edge 110+, Safari 16+)
- Mobile devices (iOS 14+, Android 10+)
- Minimum 2 Mbps internet connection

**Dependencies:**
- Supabase (PostgreSQL database, blob storage)
- n8n workflow automation
- WhatsApp Business API
- SMTP email service

### 2.5 Constraints

**Technical:**
- Must use Python 3.11+, FastAPI, Streamlit
- Database must be PostgreSQL on Supabase
- Seven-service architecture (2 APIs, 5 frontends)
- Services must auto-start via systemd on VM boot

**Business:**
- Must handle 1500+ interviews per month
- Azure infrastructure budget constraints
- Phase 1 delivery within 3 months

**Regulatory:**
- Comply with Indian IT Act 2000
- Data must reside in India-based servers
- Complete audit trail required

---

## 3. System Features

### 3.1 Candidate Registration (Form-1)

**Description:** Initial candidate registration with basic personal details.

**Functional Requirements:**

**FR-REG-001:** System shall allow candidates to self-register via Form-1
- **Input:** Name, father's name, DOB, gender, mobile, email, address, language
- **Processing:** Validate data, check mobile uniqueness, generate candidate ID
- **Output:** Candidate record created, confirmation sent
- **Priority:** CRITICAL

**FR-REG-002:** System shall enforce mobile number uniqueness
- **Validation:** No duplicate mobile numbers allowed
- **Error Handling:** Display existing application link if duplicate
- **Priority:** CRITICAL

**FR-REG-003:** System shall validate all Form-1 inputs
- **Client-side:** Real-time validation
- **Server-side:** Mandatory validation on submit
- **Rules:** Format, length, required fields, character sets
- **Priority:** CRITICAL

**FR-REG-004:** System shall send Form-1 link via WhatsApp
- **Trigger:** CV submission via WhatsApp  
- **Delivery:** Automated via n8n workflow
- **Content:** Personalized message with unique link
- **Priority:** HIGH

**FR-REG-005:** System shall provide multilingual Form-1
- **Languages:** English, Hindi, Bengali
- **Detection:** User preference or browser settings
- **Switching:** Language selector on form
- **Priority:** HIGH

### 3.2 Interview Scheduling

**Description:** HR schedules interviews and generates QR codes.

**FR-SCH-001:** System shall allow HR to schedule interviews
- **Input:** Candidate ID, date, time, venue, panel members
- **Validation:** Candidate eligibility, future date
- **Output:** Interview record created, status updated
- **Priority:** CRITICAL

**FR-SCH-002:** System shall generate unique QR codes
- **Generation:** Unique code per interview
- **Encoding:** Interview metadata (candidate ID, date, venue)
- **Format:** PNG image, 300x300 pixels
- **Expiration:** 24 hours after interview
- **Priority:** CRITICAL

**FR-SCH-003:** System shall send interview notifications with QR
- **Channels:** WhatsApp (primary), Email (backup)
- **Content:** Date, time, venue, QR image, instructions
- **Timing:** Immediately after scheduling
- **Priority:** CRITICAL

**FR-SCH-004:** System shall send interview reminders
- **Timing:** 24 hours before interview
- **Channels:** WhatsApp and Email
- **Priority:** MEDIUM

**FR-SCH-005:** System shall support interview rescheduling
- **Limit:** Maximum 2 reschedules per candidate
- **Process:** Invalidate old QR, generate new, notify candidate
- **Priority:** HIGH

### 3.3 QR Check-in

**Description:** Venue check-in using QR code with candidate path detection.

**FR-QR-001:** System shall enable QR scanning at venue
- **Device:** Tablet/mobile camera
- **Validation:** QR authenticity, usage status, timing window
- **Metadata:** Timestamp, device info, IP, location
- **Priority:** CRITICAL

**FR-QR-002:** System shall validate QR codes
- **Checks:** Not expired, not used, correct interview time (±2 hours)
- **Error Handling:** Clear messages for invalid scans
- **Priority:** CRITICAL

**FR-QR-003:** System shall detect candidate type
- **Logic:** Query for existing Form-1 record
- **Types:** Screened (Form-1 exists) or Walk-in (new)
- **Priority:** CRITICAL

**FR-QR-004:** System shall route walk-in candidates
- **Provide:** Form-1 + Form-2 links sequentially
- **Behavior:** Form-2 disabled until Form-1 complete
- **Priority:** HIGH

**FR-QR-005:** System shall route screened candidates  
- **Provide:** Form-2 link only
- **Display:** Form-1 summary (read-only)
- **Priority:** HIGH

**FR-QR-006:** System shall log check-in events
- **Captured:** Timestamp, device, browser, IP, location
- **Storage:** Audit log table
- **Retention:** 2 years minimum
- **Priority:** HIGH

### 3.4 Interview Evaluation (Form-3)

**Description:** Panel members evaluate candidates with structured ratings.

**FR-EVAL-001:** System shall authenticate panel members
- **Access:** Only assigned candidates visible
- **Authorization:** Panel role required
- **Priority:** CRITICAL

**FR-EVAL-002:** System shall display candidate profiles to panel
- **Content:** Form-1, Form-2, documents
- **Format:** Clean, readable interface
- **Priority:** HIGH

**FR-EVAL-003:** System shall provide evaluation form (Form-3)
- **Categories:** Communication, technical knowledge, experience, problem-solving, cultural fit
- **Scale:** 1-5 rating per category
- **Comments:** Text areas for remarks
- **Priority:** CRITICAL

**FR-EVAL-004:** System shall capture ratings
- **Validation:** All categories mandatory
- **Calculation:** Weighted average score
- **Priority:** CRITICAL

**FR-EVAL-005:** System shall capture panel remarks
- **Fields:** Strengths, areas of improvement, hiring recommendation, detailed comments
- **Limits:** Character limits per field
- **Priority:** HIGH

**FR-EVAL-006:** System shall finalize evaluations
- **Action:** Submit locks form (no edits)
- **Status Update:** Candidate to 'interview_completed'
- **Notification:** HR notified
- **Priority:** CRITICAL

**FR-EVAL-007:** System shall aggregate multi-panel evaluations
- **Calculation:** Average ratings across panel members
- **Output:** Consolidated score and report
- **Priority:** MEDIUM

### 3.5 Selection and Background Verification

**Description:** HR makes selection decisions and tracks background verification.

**FR-SEL-001:** System shall provide selection interface
- **Display:** Evaluation summary, ratings, recommendations
- **Actions:** Select, Reject, Hold
- **Justification:** Remarks field for decisions
- **Priority:** CRITICAL

**FR-SEL-002:** System shall send rejection notifications
- **Trigger:** Rejection decision
- **Content:** Polite message, encouragement for future
- **Channels:** Email and WhatsApp
- **Priority:** HIGH

**FR-SEL-003:** System shall initiate background verification
- **Trigger:** Selection decision
- **Status:** 'bg_verification_pending'
- **Timeline:** Expected completion in 7 days
- **Priority:** CRITICAL

**FR-SEL-004:** System shall track BG verification status
- **Statuses:** In Progress, Completed-Cleared, Completed-Issues, Failed
- **Updates:** HR manual updates
- **Documentation:** Upload verification documents
- **Priority:** HIGH

**FR-SEL-005:** System shall handle BG cleared workflow
- **Action:** Trigger offer generation
- **Status:** Update to 'bg_cleared'
- **Notification:** HR notified
- **Priority:** CRITICAL

**FR-SEL-006:** System shall handle BG failed workflow
- **Action:** Send rejection, close application
- **Status:** Update to 'bg_failed'
- **Archival:** Archive candidate record
- **Priority:** CRITICAL

### 3.6 Offer Management

**Description:** Generate, deliver, and track offer letters.

**FR-OFFER-001:** System shall manage offer templates
- **Storage:** Database-stored templates
- **Placeholders:** Dynamic data insertion points
- **Versioning:** Template version control
- **Priority:** HIGH

**FR-OFFER-002:** System shall populate offer data
- **Sources:** Candidate details, position, salary, start date
- **Validation:** All required data present
- **Priority:** CRITICAL

**FR-OFFER-003:** System shall generate offer PDFs
- **Format:** Professional PDF with branding
- **Storage:** Supabase blob storage
- **Security:** Secure download links
- **Priority:** CRITICAL

**FR-OFFER-004:** System shall deliver offers via email
- **Content:** Congratulations, PDF attachment/link
- **Tracking:** Delivery status logged
- **Priority:** CRITICAL

**FR-OFFER-005:** System shall enable offer acceptance
- **Interface:** Online acceptance page
- **Capture:** Digital signature (optional), timestamp
- **Workflow:** Trigger onboarding
- **Priority:** CRITICAL

**FR-OFFER-006:** System shall handle offer rejection
- **Update:** Status to 'offer_rejected'
- **Notification:** HR notified with reason
- **Priority:** HIGH

**FR-OFFER-007:** System shall expire offers
- **Validity:** 7 days (configurable)
- **Reminder:** 2 days and 1 day before expiry
- **Auto-expiry:** Scheduled job marks expired
- **Priority:** MEDIUM

### 3.7 Onboarding (Form-4)

**Description:** Induction management and final onboarding details.

**FR-ONBRD-001:** System shall communicate induction date
- **Content:** Date, time, venue, required documents
- **QR Generation:** Induction day QR code
- **Channels:** Email and WhatsApp
- **Priority:** HIGH

**FR-ONBRD-002:** System shall enable induction QR check-in
- **Validation:** Similar to interview QR
- **Trigger:** Form-4 delivery
- **Priority:** HIGH

**FR-ONBRD-003:** System shall provide Form-4
- **Fields:** Bank account, emergency contacts, preferences, acknowledgments
- **Validation:** Bank details format, IFSC code
- **Priority:** CRITICAL

**FR-ONBRD-004:** System shall verify bank details
- **Format Validation:** Account number, IFSC code
- **Name Matching:** Account holder name vs. candidate name
- **Priority:** MEDIUM

**FR-ONBRD-005:** System shall finalize onboarding
- **Trigger:** Form-4 submission
- **Actions:** Status to 'onboarded', generate employee ID, HRMS export
- **Notification:** Confirmation to candidate and HR
- **Priority:** CRITICAL

**FR-ONBRD-006:** System shall track onboarding checklist
- **Items:** Configurable checklist (documents verified, access created, equipment issued, etc.)
- **Progress:** Completion percentage
- **Reminders:** For pending items
- **Priority:** MEDIUM

### 3.8 Data Export to HRMS

**Description:** Prepare and export data to Octane HRMS.

**FR-EXPORT-001:** System shall prepare HRMS export data
- **Sources:** All candidate forms and evaluations
- **Mapping:** Internal fields to HRMS fields
- **Validation:** Data completeness check
- **Priority:** HIGH

**FR-EXPORT-002:** System shall generate CSV/Excel exports
- **Format:** HRMS-compatible structure
- **Naming:** Timestamped file names
- **Storage:** Secure download location
- **Priority:** HIGH

**FR-EXPORT-003:** System shall export documents in bulk
- **Organization:** Folder structure by candidate
- **Format:** ZIP archive with manifest
- **Priority:** MEDIUM

**FR-EXPORT-004:** System shall maintain export history
- **Logging:** Export timestamp, user, candidates included
- **Audit:** Queryable export history
- **Priority:** MEDIUM

### 3.9 Analytics and Reporting

**Description:** Real-time dashboards and recruitment metrics.

**FR-REPT-001:** System shall provide recruitment funnel dashboard
- **Stages:** Application → Interview → Selection → Onboarding
- **Metrics:** Counts, conversion rates, time per stage
- **Visualization:** Interactive funnel chart
- **Priority:** HIGH

**FR-REPT-002:** System shall analyze interview quality
- **Metrics:** Average scores, score distribution, panel consistency
- **Priority:** MEDIUM

**FR-REPT-003:** System shall calculate time-to-hire
- **Measurement:** CV submission to offer acceptance
- **Sub-stages:** Application to interview, interview to selection, etc.
- **Statistics:** Average, median, min, max
- **Priority:** HIGH

**FR-REPT-004:** System shall analyze source effectiveness
- **Grouping:** By candidate source (WhatsApp, walk-in, referral, etc.)
- **Metrics:** Application count, selection rate, quality score
- **Priority:** MEDIUM

**FR-REPT-005:** System shall support custom reports
- **Configurability:** User-selectable metrics and filters
- **Formats:** Tabular, charts, pivot tables
- **Saving:** Save report configurations
- **Priority:** LOW

**FR-REPT-006:** System shall export reports
- **Formats:** PDF, Excel, CSV
- **Priority:** MEDIUM

### 3.10 Security and Access Control

**Description:** Authentication, authorization, and audit logging.

**FR-SEC-001:** System shall authenticate users via JWT
- **Method:** Username/email and password
- **Token:** JWT with 8-hour expiration
- **Lockout:** 5 failed attempts = 15-minute lockout
- **Priority:** CRITICAL

**FR-SEC-002:** System shall enforce role-based access
- **Roles:** Candidate, HR Personnel, Interview Panel, HR Manager, System Admin, Audit Officer
- **Permissions:** Role-specific access to features
- **Enforcement:** On every API request
- **Priority:** CRITICAL

**FR-SEC-003:** System shall manage sessions securely
- **Storage:** Redis cache
- **Timeout:** 30 minutes inactivity
- **Logout:** Manual and automatic
- **Priority:** HIGH

**FR-SEC-004:** System shall encrypt sensitive data
- **At Rest:** AES-256 for Aadhaar, PAN, bank details
- **In Transit:** TLS 1.3 for all communications
- **Priority:** CRITICAL

**FR-SEC-005:** System shall maintain audit logs
- **Events:** Login, data access, modifications, config changes
- **Content:** Who, what, when, where, result
- **Storage:** Append-only, separate from application data
- **Retention:** 2 years minimum
- **Priority:** HIGH

**FR-SEC-006:** System shall enforce password policy
- **Requirements:** Min 8 chars, uppercase, lowercase, digit, special char
- **History:** No reuse of last 5 passwords
- **Priority:** MEDIUM

---

## 4. External Interface Requirements

### 4.1 User Interfaces

**UI-001: General Requirements**
- Responsive design (mobile, tablet, desktop)
- Browser compatibility (Chrome 110+, Firefox 115+, Edge 110+, Safari 16+)
- Accessibility (WCAG 2.1 Level A)
- Loading indicators for operations > 1 second
- User-friendly error messages

**UI-002: Candidate Portal**
- Single/two-column form layouts
- Progress indicators
- Language selector (English/Hindi/Bengali)
- Document upload with drag-drop
- Status tracking timeline
- QR scanner interface

**UI-003: HR Dashboard**
- Navigation sidebar with modules
- Candidate list with filters and search
- Candidate profile tabs (Overview, Forms, Documents, Timeline, Audit)
- Interview scheduling calendar
- Analytics dashboards with KPI cards and charts

**UI-004: Interview Panel Portal**
- Candidate summary panel
- Evaluation form with rating sliders
- Document viewer with zoom
- Draft saving functionality

### 4.2 Hardware Interfaces

**HW-001: QR Scanning Devices**
- Mobile/tablet cameras (5MP minimum)
- iOS 14+ or Android 10+
- Browser camera API support

**HW-002: Production Server**
- Azure VM or equivalent VPS
- 4-8 CPU cores, 16GB RAM, 100GB SSD
- 100 Mbps bandwidth
- Ubuntu 24.04 LTS

### 4.3 Software Interfaces

**SW-001: Supabase PostgreSQL**
- Protocol: PostgreSQL wire protocol
- Connection: SSL/TLS required
- Pooling: Connection pooling (max 100 connections)

**SW-002: Supabase Blob Storage**
- API: RESTful over HTTPS
- Authentication: JWT bearer token
- Buckets: Resumes, documents, certificates, offers, photos

**SW-003: Email Service (SMTP)**
- Protocol: SMTP over TLS (port 587)
- Content: Multipart (text and HTML)
- Attachments: Up to 5MB

**SW-004: WhatsApp Business API (via n8n)**
- Integration: REST API via n8n webhooks
- Messages: Text, templates, media (QR images)
- Templates: Pre-approved by Meta

**SW-005: n8n Workflow Automation**
- Interface: HTTP POST to webhooks
- Payload: JSON format
- Events: Form submissions, interview scheduling, selection decisions, etc.

### 4.4 Communications Interfaces

**COMM-001: HTTPS Protocol**
- Version: TLS 1.3 (minimum TLS 1.2)
- Port: 443
- Certificate: Valid SSL/TLS certificate

**COMM-002: REST API**
- Data Format: JSON (UTF-8)
- HTTP Methods: GET, POST, PUT, PATCH, DELETE
- Status Codes: Standard HTTP codes
- Rate Limiting: 100 requests/min (authenticated), 20/min (public)

**COMM-003: WebSocket (Optional)**
- Protocol: WSS over port 443
- Use: Real-time dashboard updates
- Authentication: JWT token

---

## 5. Non-Functional Requirements

### 5.1 Performance

**PERF-001: Response Times**
- Page load: < 3 seconds
- Simple API calls: < 200ms
- Complex queries: < 500ms
- Form submissions: < 1 second
- Report generation: < 5 seconds

**PERF-002: Throughput**
- Concurrent users: 100 without degradation
- Requests per minute: 500 sustained
- Interview volume: 1500+ per month
- Peak load: 1000 requests/min for 5-minute bursts

**PERF-003: Resource Utilization**
- CPU usage: < 70% under normal load
- Memory usage: < 80% of available RAM
- Database connections: Pool of 10-50
- Storage growth: ~5GB/month (documents)

### 5.2 Security

**SEC-001: Authentication & Authorization**
- Strong password policy enforced
- Account lockout after 5 failed attempts
- JWT-based authentication (8-hour expiration)
- Role-based access control (RBAC)
- Principle of least privilege

**SEC-002: Data Protection**
- Sensitive data encrypted at rest (AES-256)
- All data encrypted in transit (TLS 1.3)
- PII masked in UI and logs
- Secure file storage with signed URLs

**SEC-003: Application Security**
- Input validation (client and server)
- SQL injection prevention (parameterized queries)
- XSS prevention (output escaping, CSP)
- CSRF protection (tokens)
- API rate limiting

**SEC-004: Infrastructure Security**
- Server hardening (SSH keys only, firewall)
- Network segmentation
- Encrypted backups
- Security monitoring and alerting
- Audit logging (all security events)

**SEC-005: Privacy & Compliance**
- Candidate data privacy protection
- Data retention policies enforced
- Complete audit trail (2-year retention)
- Compliance with Indian IT Act 2000

### 5.3 Reliability

**REL-001: System Uptime**
- 99.5% uptime during business hours (9 AM - 6 PM IST, Mon-Fri)
- Allowed downtime: 54 minutes/month
- Scheduled maintenance excluded

**REL-002: Failure Handling**
- MTBF: 720 hours (30 days)
- MTTR: < 2 hours for critical issues
- Graceful error handling (no data loss)
- Transaction rollback on errors

**REL-003: Data Integrity**
- 100% data integrity maintained
- ACID-compliant transactions
- Foreign key constraints
- Regular consistency checks

### 5.4 Maintainability

**MAINT-001: Code Quality**
- PEP 8 standards for Python
- Code comments for complex logic
- Mandatory code reviews

**MAINT-002: Documentation**
- SRS, API docs (Swagger), database schema
- Deployment guide, user manuals
- Updated with each major release

**MAINT-003: Modularity**
- Clear separation of concerns
- Loosely coupled modules
- Well-defined interfaces

**MAINT-004: Configuration**
- Externalized configuration (env variables)
- No hard-coded values
- Configuration validation on startup

### 5.5 Usability

**USAB-001: Ease of Use**
- Intuitive interfaces for all user types
- 90% of candidates complete Form-1 without assistance
- New HR users productive after 1-hour training
- User satisfaction score: 4/5 minimum

**USAB-002: Learnability**
- Candidates complete Form-1 in < 10 minutes
- Panel completes Form-3 in < 15 minutes

**USAB-003: User Assistance**
- Context-sensitive help (tooltips, help icons)
- FAQ section accessible
- Contact HR option on all candidate pages

**USAB-004: Accessibility**
- WCAG 2.1 Level A compliance
- Keyboard navigation support
- Screen reader compatibility
- Sufficient color contrast

**USAB-005: Error Prevention**
- Real-time input validation
- Confirmation dialogs for destructive actions
- Default values for common fields
- Undo functionality where feasible

### 5.6 Portability

**PORT-001: Platform Independence**
- Accessible from any modern OS (Windows, macOS, Linux, iOS, Android)

**PORT-002: Browser Independence**
- Works on all major browsers (see UI-001)

**PORT-003: Containerization**
- Docker containers for all services
- Docker Compose orchestration

**PORT-004: Cloud Agnostic**
- Deployable on Azure, AWS, Google Cloud with minimal changes

### 5.7 Testability

**TEST-001: Automated Testing**
- Unit tests: 70% code coverage minimum
- Integration tests for critical workflows
- End-to-end tests for key user journeys

**TEST-002: Test Environment**
- Separate staging environment mirroring production
- Test database with sample data

**TEST-003: Logging**
- DEBUG, INFO, WARNING, ERROR, CRITICAL levels
- Production: INFO level and above

---

## 6. Other Requirements

### 6.1 Business Rules

**BR-001:** Only candidates with status 'form1_submitted' or 'eligible' can be scheduled for interviews (HR Manager can override)

**BR-002:** Each QR code can be used only once for check-in

**BR-003:** Candidates can check in within ±2 hours of scheduled interview time

**BR-004:** Minimum 3 documents required for Form-2 submission (Aadhaar, PAN, Photo)

**BR-005:** All selected candidates must undergo background verification before offer generation

**BR-006:** Offer letters valid for 7 days (HR Manager can extend)

**BR-007:** Maximum 2 interview reschedules per candidate

**BR-008:** Only HR Personnel and HR Managers can make selection decisions

**BR-009:** Rejected candidate data retained for 1 year before archival

**BR-010:** All panel members must submit evaluations before HR selection decision (HR Manager can override)

### 6.2 Data Requirements

**Data Volume Estimates:**

| Data Type | 1 Year | 3 Years |
|-----------|--------|---------|
| Candidate Records | 18,000 | 54,000 |
| Interview Records | 18,000 | 54,000 |
| Document Files | ~50GB | ~150GB |
| Database Size | ~2GB | ~6GB |

**Backup Strategy:**
- Full backup: Weekly (Sundays 2:00 AM IST)
- Incremental: Daily (2:00 AM IST)
- Retention: 30 days (daily), 12 weeks (weekly), 12 months (monthly)
- RTO: 4 hours, RPO: 24 hours

### 6.3 Internationalization

**I18N-001: Language Support**
- English, Hindi, Bengali for candidate interfaces
- English only for HR and admin interfaces
- Resource bundle approach (JSON key-value pairs)

**I18N-002: Date/Time Formats**
- Date: DD/MM/YYYY
- Time: 12-hour with AM/PM
- Timezone: IST

**I18N-003: Currency/Number Formats**
- Currency: ₹1,00,000 (Indian numbering)
- Numbers: Comma at thousand, lakh, crore positions

### 6.4 Legal and Compliance

**LEGAL-001: Data Protection**
- Comply with Indian IT Act 2000
- Explicit consent before data collection
- Data used only for stated purposes
- Candidate rights: access, correction, deletion

**LEGAL-002: Employment Law**
- No discrimination (religion, caste, gender, etc.)
- Equal opportunity for all
- Age restriction: 18+ years
- Documented hiring decisions

**LEGAL-003: Document Retention**
- Successful candidates: Employment + 7 years
- Rejected candidates: 1 year minimum
- Audit logs: 2 years minimum

**LEGAL-004: Accessibility**
- Strive for WCAG 2.1 Level A compliance

---

## 7. Appendices

### 7.1 Analysis Models

Detailed data flow diagrams, state machines, and ER diagrams are provided in the High-Level Design (HLD) document version 2.1, incorporated by reference.

**Key State Machines:**

**Candidate Status Flow:**
```
registered → eligible → interview_scheduled → checked_in → 
interview_completed → selected → bg_verification_pending → 
bg_cleared → offer_sent → offer_accepted → onboarding → onboarded
```

**Alternative paths:** rejected, on_hold, bg_failed, offer_rejected, offer_expired

### 7.2 Open Issues and Future Enhancements

| ID | Description | Priority | Target |
|----|-------------|----------|--------|
| ISS-001 | Automated BG verification integration | Medium | Phase 2 |
| ISS-002 | Direct HRMS API integration | Low | Phase 2 |
| ISS-003 | Two-factor authentication (2FA) | Medium | Phase 2 |
| ISS-004 | Video interview integration | Low | Phase 3 |
| ISS-005 | Native mobile apps (iOS/Android) | Low | Phase 3 |
| ISS-006 | AI/ML predictive hiring analytics | Low | Phase 3 |

### 7.3 Known Limitations (Phase 1)

- Manual background verification (no automation)
- No direct HRMS sync (manual CSV export)
- Single server deployment (no HA)
- English-only HR interfaces
- No candidate self-service portal beyond forms

### 7.4 Glossary

Complete glossary of terms provided in Section 1.3.

---

## Approval Sign-off

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Project Sponsor** | | | |
| **Project Manager** | Md Sahil | | 2026-01-09 |
| **Technical Lead** | | | |
| **HR Department Head** | | | |
| **QA Lead** | | | |

---

**Document Status:** DRAFT - Pending Stakeholder Approval

**Document Owner:** Md Sahil, Project Manager

**Contact:** [To be filled]

---

## Important Notes

1. This SRS is derived from HLD v2.1 and expands requirements with implementation details.

2. All requirements are subject to change through formal change control process.

3. This document serves as contractual agreement between stakeholders and development team.

4. Traceability matrix linking requirements to test cases maintained separately.

5. For clarifications, contact the document owner.

---

**END OF SOFTWARE REQUIREMENTS SPECIFICATION**

---

*Generated: January 09, 2026*  
*Version: 1.0*  
*Format: Markdown*
