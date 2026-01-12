# HR Onboarding Agent temp
## Business Requirements Document (BRD)

**Document Version:** 1.0  
**Created Date:** January 05, 2026  
**Organization:** Sampurna Financial Services Pvt. Ltd. (SFSPL)  
**Last Updated:** January 05, 2026

---

## TABLE OF CONTENTS

1. [Executive Summary](#executive-summary)
2. [Business Problem & Objectives](#business-problem--objectives)
3. [Business Scope](#business-scope)
4. [Business Requirements](#business-requirements)
5. [Business Process Flow](#business-process-flow)
6. [Key Performance Indicators (KPIs)](#key-performance-indicators-kpis)
7. [Business Benefits](#business-benefits)
8. [Stakeholder Analysis](#stakeholder-analysis)
9. [Assumptions & Constraints](#assumptions--constraints)
10. [Approval & Sign-off](#approval--sign-off)

---

## 1. EXECUTIVE SUMMARY

The **HR Onboarding Agent Project** is a comprehensive digital transformation initiative for Sampurna Financial Services Pvt. Ltd. (SFSPL) aimed at automating and streamlining the complete employee recruitment and onboarding lifecycle.

### 1.1 Current State (AS-IS)

The existing recruitment process at SFSPL faces significant operational challenges:

- **Manual, paper-based recruitment process** with minimal digital tracking
- **Candidate information collected via WhatsApp, emails, and Excel sheets** leading to data fragmentation
- **No centralized candidate database** or tracking mechanism
- **Delayed communication** and limited visibility on application status for candidates
- **High data loss and duplication risks** due to manual data handling
- **Inefficient interview scheduling** and evaluation process
- **No structured onboarding workflow** leading to inconsistent new hire experiences
- **Limited analytics** and inability to measure recruitment effectiveness

### 1.2 Desired State (TO-BE)

The proposed HR Onboarding Agent will transform the recruitment landscape:

- **Fully digitized, end-to-end automation** of recruitment and onboarding
- **Centralized, secure digital platform** with PostgreSQL database as single source of truth
- **Real-time visibility** for all stakeholders (HR, Recruiters, Interviewers, Candidates)
- **AI-assisted screening** and automated workflow management
- **Multi-channel communication** (WhatsApp, Email, SMS) for timely updates
- **Multilingual support** (English, Hindi, Bengali) for wider accessibility
- **QR-based check-in** at interview venues for seamless candidate experience
- **Comprehensive analytics & reporting** for data-driven decision-making
- **Structured onboarding** with automated checklist and task management

### 1.3 Expected Business Outcomes

| Outcome | Target | Timeline |
|---------|--------|----------|
| **Reduction in Recruitment Time** | 60-70% (from 30 days → 10 days) | Year 1 |
| **Manual Data Entry Reduction** | 90% (from 50 hours → 5 hours per 100 applications) | Immediate |
| **Cost Per Hire Reduction** | 40% ($2000 → $1200 per hire) | Year 1 |
| **HR Time Savings** | 30-35 hours/month per 100 applications | Year 1 |
| **Improved Offer Acceptance Rate** | Increase by 15% (from 75% → 90%) | Year 1 |
| **Improved Joining Rate** | Increase by 10% (from 85% → 95%) | Year 1 |
| **Candidate Satisfaction (NPS)** | Improve NPS by 40 points | Year 1 |

### 1.4 Strategic Alignment

This project aligns with SFSPL's strategic objectives:

- **Digital Transformation:** Moving from manual to digital-first operations
- **Operational Excellence:** Streamlining processes to improve efficiency
- **Talent Acquisition:** Building competitive advantage in attracting top talent
- **Data-Driven Culture:** Leveraging analytics for informed decision-making
- **Scalability:** Supporting business growth without proportional HR headcount increase

---

## 2. BUSINESS PROBLEM & OBJECTIVES

### 2.1 PROBLEM STATEMENT

**Current Challenges and Their Business Impact:**

| Challenge | Business Impact | Quantified Loss |
|-----------|----------------|-----------------|
| **Manual CV submission via WhatsApp** | No audit trail, data loss, inefficient screening | 15-20 hours/week lost in data compilation |
| **Unstructured data storage (Excel, emails)** | Difficult to track candidate progress, duplicate work | 10-15% candidates lost in process |
| **No digital interview records** | Difficulty in analysis and decision-making | Poor hire quality, 20% early attrition |
| **Delayed communication with candidates** | Poor candidate experience, high drop-off | 25% candidate drop-off rate |
| **Manual document verification** | High error rates and time-consuming | 5-7 days per candidate for verification |
| **No candidate database** | Difficulty in rehiring or referral tracking | Lost opportunity for quality rehires |
| **Limited visibility on recruitment metrics** | Cannot analyze hiring trends or bottlenecks | Unable to identify process improvements |
| **Duplicate data entry in HRMS** | Redundancy and data inconsistency | 3-4 hours per successful hire |

**Root Cause Analysis:**

1. **Process Gaps:** No standardized recruitment workflow
2. **Technology Gaps:** Lack of integrated HR technology platform
3. **Data Management:** Fragmented data across multiple tools
4. **Communication:** Manual, delayed notification system
5. **Analytics:** No real-time visibility into recruitment metrics

### 2.2 BUSINESS OBJECTIVES

#### Primary Objectives

**1. Centralize Data Management**
- **Goal:** Establish single source of truth for all candidate and hiring information
- **Success Criteria:**
  - 100% of candidate data stored in centralized database
  - Eliminate Excel-based tracking by Q2
  - Zero data loss incidents
  - Secure storage with 99.9% uptime
- **Business Value:** Improved data quality, audit trail, and compliance

**2. Automate Recruitment Process**
- **Goal:** Reduce manual intervention and accelerate hiring
- **Success Criteria:**
  - 90% reduction in manual data entry
  - 60-70% decrease in recruitment cycle time
  - 100% consistent process across all departments
  - Automated notifications for all candidate touchpoints
- **Business Value:** Faster time-to-hire, reduced HR workload

**3. Improve Candidate Experience**
- **Goal:** Provide world-class candidate experience
- **Success Criteria:**
  - Candidate NPS score > 70
  - Application completion rate > 85%
  - < 10% candidate drop-off between stages
  - Real-time status updates (< 5 min lag)
- **Business Value:** Enhanced employer brand, better talent attraction

**4. Enable Data-Driven Decision Making**
- **Goal:** Provide actionable insights for recruitment optimization
- **Success Criteria:**
  - Real-time dashboards for all stakeholders
  - 20+ KPIs tracked automatically
  - Monthly recruitment analytics reports
  - Predictive insights on hiring trends
- **Business Value:** Optimized recruitment strategy, better ROI

**5. Ensure Compliance & Audit Trail**
- **Goal:** Maintain complete audit trail for legal and regulatory compliance
- **Success Criteria:**
  - 100% action logging with timestamp
  - Complete audit trail for 7 years
  - DPDP Act 2023 compliance
  - Zero compliance incidents
- **Business Value:** Legal protection, regulatory compliance

#### Secondary Objectives

- **Reduce Cost Per Hire:** Target 40% reduction through process efficiency
- **Improve Hiring Quality:** Structured evaluation leading to better hire quality
- **Enable Scalability:** Support 2-3x hiring volume without additional HR staff
- **Enhance Collaboration:** Better coordination between recruiters, interviewers, and managers
- **Standardize Process:** Consistent recruitment process across all departments and locations

---

## 3. BUSINESS SCOPE

### 3.1 IN-SCOPE FEATURES

#### Phase 1: Core Recruitment (MVP) - 3 Months

**Candidate Management:**
- Vacancy identification and posting
- Candidate self-registration via WhatsApp campaign
- Digital form submission (Form-1: Basic Details)
- Eligibility checking (30-day rule, qualification validation)
- Candidate status tracking and timeline

**Interview Management:**
- Interview scheduling and assignment
- **QR-based check-in** at interview venue
- **Dual candidate paths** (Screened vs Walk-in)
- Interview evaluation (Form-3)
- Panel management and coordination

**Decision & Offer:**
- Selection/Rejection decision workflow
- Background verification tracking
- Offer letter generation and delivery
- Offer acceptance tracking

**Communication & Reporting:**
- WhatsApp notifications via n8n
- Email notifications
- Basic HR dashboard
- Recruitment pipeline reports

#### Phase 2: Onboarding & Advanced Features - 2 Months

**Extended Data Collection:**
- Form-2 (Address, Qualifications, Skills) collection
- Form-4 (Onboarding Details) post-induction
- Document and KYC management
- Enhanced profile management

**Onboarding Workflow:**
- Offer letter generation and acceptance
- Onboarding checklist creation
- Task tracking and completion
- Induction QR check-in
- Pre-joining and post-joining workflows

**Advanced Features:**
- Advanced analytics and dashboards
- Multilingual interface (English, Hindi, Bengali)
- Candidate analytics and quality metrics
- Source effectiveness analysis

#### Phase 3: Optimization & Hardening - 1 Month

**Performance & Security:**
- Load testing and optimization
- Security penetration testing
- Performance tuning
- Infrastructure hardening

**Integration & Export:**
- Data export capability to Octane/HRMS
- Automated data synchronization
- Backup and disaster recovery testing

**Documentation & Training:**
- User manuals and guides
- Training materials and sessions
- Operational runbooks

### 3.2 OUT-OF-SCOPE ITEMS

**Current Release:**
- ❌ Full automation of background verification (remains manual with status tracking)
- ❌ Direct auto-sync with Octane system (manual data export initially)
- ❌ Automated salary offer calculations (HR-driven decisions)
- ❌ AI-based candidate ranking (structured evaluation only)
- ❌ Direct email sending from HR mailbox (managed via n8n automation)
- ❌ Automated rejection without HR review
- ❌ Video interview platform integration (Phase 2 consideration)
- ❌ Multi-company support (single-company setup)
- ❌ Applicant Tracking System (ATS) marketplace integrations
- ❌ Social media recruitment integration
- ❌ Candidate assessment tests (technical, psychometric)
- ❌ Payroll system integration (export only)

**Future Considerations (Phase 2+):**
- 🔮 AI-powered resume parsing and candidate matching
- 🔮 Video interview platform integration
- 🔮 Automated reference checking
- 🔮 Skills assessment integration
- 🔮 Candidate relationship management (CRM)
- 🔮 Career site/job portal creation
- 🔮 Social media recruitment campaigns
- 🔮 Employee referral program management

### 3.3 BUSINESS ASSUMPTIONS

| Category | Assumption | Risk if Invalid | Mitigation |
|----------|-----------|-----------------|------------|
| **Volume** | Active recruitment with 10-20+ positions monthly | Low system utilization, ROI impact | Phased rollout, start with high-volume departments |
| **Technology Adoption** | HR team and candidates willing to adopt digital tools | Resistance to change, low adoption | Change management, training, user feedback |
| **Data Availability** | Legacy candidate data can be migrated/archived | Data loss, incomplete history | Data audit, cleansing, migration plan |
| **Budget** | Sufficient budget allocated for development and deployment | Project delays, scope reduction | Budget approval upfront, contingency fund |
| **Change Management** | Organization will provide support for process reengineering | Process adherence issues | Executive sponsorship, training program |
| **Regulatory Compliance** | Data handling complies with Indian employment laws | Legal issues, penalties | Legal review, compliance framework |
| **Device Accessibility** | Candidates and HR have smartphones/computers and internet | Access barriers for candidates | SMS fallback, offline capability consideration |
| **Infrastructure** | Stable internet connectivity and cloud services | System downtime, poor UX | Multi-zone deployment, offline mode |
| **Data Quality** | Candidates provide accurate information | Data integrity issues | Validation rules, verification process |
| **Support** | IT support available for system maintenance | Operational issues | SLA with vendors, in-house capability |

### 3.4 CONSTRAINTS

**Technical Constraints:**
- Must use existing tech stack (Python, PostgreSQL, AWS)
- Integration with existing Supabase and n8n infrastructure
- Database size and query performance limitations
- API rate limits for WhatsApp and email services

**Business Constraints:**
- Budget cap for Phase 1 development
- 6-month timeline for complete implementation
- Limited HR team availability for UAT (2 weeks max)
- Dependency on third-party services (WhatsApp, email)

**Regulatory Constraints:**
- DPDP Act 2023 compliance requirements
- Data localization (India) requirements
- Employment law compliance for candidate data retention
- Privacy and consent management requirements

**Resource Constraints:**
- Development team size (1 lead + 2 developers)
- HR team bandwidth for testing and feedback
- Training window for HR staff (1 week)
- Limited budget for external integrations

---

## 4. BUSINESS REQUIREMENTS

### 4.1 FUNCTIONAL BUSINESS REQUIREMENTS

#### BR-1: Candidate Registration & Application Management
- **Requirement ID:** BR-1
- **Category:** Core
- **Priority:** HIGH
- **Business Need:** Enable candidates to easily apply for positions through a simple digital form
- **Current Gap:** Manual WhatsApp/email submissions, no standardized process
- **Proposed Solution:** 
  - Mobile number-based passwordless login
  - Multi-stage form submission (Form-1 → Form-2 → Form-4)
  - Real-time status tracking visible to candidate
  - Document upload capability for resume, certificates, etc.
  - 30-day cooldown rule between applications for same role
- **Business Value:** 
  - Reduce application friction by 70%
  - Increase application completion rate to 85%
  - Eliminate duplicate applications
- **Success Metrics:**
  - Application completion rate > 85%
  - Average application time < 10 minutes
  - Zero duplicate applications
- **Dependencies:** WhatsApp API integration, OTP service

---

#### BR-2: Interview Scheduling & Management
- **Requirement ID:** BR-2
- **Category:** Core
- **Priority:** HIGH
- **Business Need:** HR should efficiently schedule interviews and manage panel assignments
- **Current Gap:** Manual calendar management, coordination via email/calls
- **Proposed Solution:**
  - Calendar-based scheduling interface
  - Interviewer availability management
  - Location/department assignment
  - Automatic notification to candidates and interviewers
  - **QR code generation for venue check-in**
  - Interview panel composition management
- **Business Value:**
  - Reduce scheduling time from 2-3 days to < 4 hours
  - Eliminate scheduling conflicts
  - Professional candidate communication
- **Success Metrics:**
  - Time-to-schedule < 24 hours
  - Zero scheduling conflicts
  - 95%+ candidate attendance rate
- **Dependencies:** Calendar integration, notification system

---

#### BR-3: QR-Based Check-in System
- **Requirement ID:** BR-3
- **Category:** Innovation
- **Priority:** HIGH
- **Business Need:** Enable venue-based candidate check-in using QR codes for seamless experience
- **Current Gap:** Manual attendance, paper-based forms at venue
- **Proposed Solution:**
  - Unique QR code per interview session
  - Single-use, time-limited (15-30 min) QR codes
  - Mobile scanner app for check-in
  - Automatic form population based on candidate type (Screened vs Walk-in)
  - Timestamp logging for attendance tracking
- **Business Value:**
  - Eliminate paper forms at interview venue
  - Reduce no-shows by 15-20% through tracking
  - Professional, tech-forward impression
  - Capture accurate attendance data
- **Success Metrics:**
  - QR check-in adoption > 95%
  - Zero paper forms at venue
  - Accurate attendance tracking 100%
- **Dependencies:** QR generation library, mobile camera access

---

#### BR-4: Dual Candidate Path Support
- **Requirement ID:** BR-4
- **Category:** Process
- **Priority:** MEDIUM
- **Business Need:** System should handle both pre-screened candidates and walk-in applicants efficiently
- **Current Gap:** Inconsistent process for different candidate types
- **Proposed Solution:**
  - **Screened Path:** Candidates pre-fill Form-1, receive Form-2 link after QR check-in
  - **Walk-in Path:** Candidates fill both Form-1 and Form-2 on interview day after QR check-in
  - Dynamic form presentation based on candidate type
  - Clear workflow differentiation in system
- **Business Value:**
  - Support diverse hiring channels
  - Maintain data quality regardless of source
  - Reduce interview day paperwork
- **Success Metrics:**
  - 100% of both types supported seamlessly
  - Same data quality for both paths
  - Zero confusion at venue
- **Dependencies:** QR check-in system, form routing logic

---

#### BR-5: Interview Evaluation & Decision Management
- **Requirement ID:** BR-5
- **Category:** Core
- **Priority:** HIGH
- **Business Need:** Structured capture of interview evaluation and hiring decision
- **Current Gap:** Unstructured feedback, delayed decisions, no historical record
- **Proposed Solution:**
  - Form-3: Standardized evaluation form with scoring rubric
  - Multiple dimensions: Technical, Communication, Problem-solving, Culture-fit
  - HR manager approval workflow
  - Selection/Rejection decision with reason tracking
  - Automated feedback to candidate
- **Business Value:**
  - Standardized evaluation process
  - Better hiring decisions through structured data
  - Audit trail for all decisions
  - Faster decision-making
- **Success Metrics:**
  - Evaluation completion within 24 hours of interview
  - 100% structured feedback capture
  - Decision communicated within 48 hours
- **Dependencies:** Evaluation framework, decision workflow

---

#### BR-6: Background Verification Workflow
- **Requirement ID:** BR-6
- **Category:** Compliance
- **Priority:** HIGH
- **Business Need:** Track background verification status until clearance
- **Current Gap:** Manual tracking, no visibility, delays in offer
- **Proposed Solution:**
  - Manual background verification initiation by HR
  - Status tracking (Pending, In Progress, Cleared, Failed)
  - Document collection and verification
  - Final approval by HR manager
  - Conditional offer (subject to BG clearance)
- **Business Value:**
  - Complete visibility on BG status
  - Faster turnaround time
  - Reduced hiring risk
  - Audit trail for compliance
- **Success Metrics:**
  - BG completion time < 14 days
  - 100% BG completion before joining
  - Zero post-joining BG failures
- **Dependencies:** BG verification vendor coordination

---

#### BR-7: Offer Letter Management
- **Requirement ID:** BR-7
- **Category:** Core
- **Priority:** HIGH
- **Business Need:** Generate, deliver, and track offer letters professionally
- **Current Gap:** Manual offer letter creation, delayed delivery, no tracking
- **Proposed Solution:**
  - Automated offer letter PDF generation with candidate details
  - Email delivery with digital tracking
  - Offer acceptance/rejection tracking
  - Offer validity period management
  - Integration with onboarding workflow
- **Business Value:**
  - Professional offer delivery
  - Clear offer records
  - Faster offer turnaround
  - Better acceptance tracking
- **Success Metrics:**
  - Offer generation time < 30 minutes
  - Offer acceptance rate > 85%
  - Zero offer letter errors
- **Dependencies:** Document template, PDF generation, email service

---

#### BR-8: Onboarding Checklist & Task Management
- **Requirement ID:** BR-8
- **Category:** Enhancement
- **Priority:** MEDIUM
- **Business Need:** Manage post-selection onboarding tasks and activities
- **Current Gap:** Ad-hoc onboarding, inconsistent experience, tasks forgotten
- **Proposed Solution:**
  - Form-4: Final onboarding details collection
  - Pre-induction checklist (IT setup, desk allocation, paperwork)
  - Post-induction checklist (orientation, training, system access)
  - Task assignment and completion tracking
  - Milestone-based status updates
- **Business Value:**
  - Consistent onboarding experience
  - Smooth joining process
  - Reduced first-day issues
  - Better new hire retention
- **Success Metrics:**
  - Onboarding completion rate 100%
  - New hire satisfaction > 4.5/5
  - Zero first-day issues
- **Dependencies:** Task management system, checklist templates

---

#### BR-9: Multi-Channel Communication
- **Requirement ID:** BR-9
- **Category:** Core
- **Priority:** HIGH
- **Business Need:** Notify candidates and staff through preferred channels
- **Current Gap:** Manual communication, delayed updates, poor reach
- **Proposed Solution:**
  - **WhatsApp Notifications:** Application status, interview invites, offer letters
  - **Email Notifications:** Detailed forms, documents, formal communication
  - **SMS Notifications:** Critical alerts (optional)
  - Templated, personalized messages
  - Delivery tracking and retry mechanism
- **Business Value:**
  - Timely communication
  - Professional touchpoints
  - Improved candidate experience
  - Better engagement
- **Success Metrics:**
  - Message delivery rate > 98%
  - Candidate response time < 24 hours
  - Communication satisfaction > 4.0/5
- **Dependencies:** n8n automation, WhatsApp API, email service

---

#### BR-10: Dashboard & Reporting
- **Requirement ID:** BR-10
- **Category:** Analytics
- **Priority:** HIGH
- **Business Need:** Provide HR visibility into recruitment pipeline and metrics
- **Current Gap:** No real-time visibility, manual report compilation
- **Proposed Solution:**
  - **HR Manager Dashboard:** Application overview, interview schedule, pending decisions
  - **Recruiter Dashboard:** Assigned candidates, QR management
  - **Candidate Dashboard:** Application status timeline, document checklist
  - **Analytics Reports:** Time-to-hire, source effectiveness, offer acceptance rate
- **Business Value:**
  - Real-time visibility
  - Data-driven decisions
  - Process optimization
  - Performance tracking
- **Success Metrics:**
  - Dashboard load time < 2 seconds
  - 20+ KPIs tracked automatically
  - Monthly reports automated
- **Dependencies:** Database views, reporting framework

---

#### BR-11: Document Management & KYC
- **Requirement ID:** BR-11
- **Category:** Compliance
- **Priority:** HIGH
- **Business Need:** Centralize document storage and verification
- **Current Gap:** Documents scattered across emails, WhatsApp, no verification tracking
- **Proposed Solution:**
  - Secure upload of resume, certificates, ID proofs
  - Document verification status tracking
  - Version control and audit trail
  - Compliance with data protection regulations
  - Searchable document repository
- **Business Value:**
  - Complete hiring records
  - Regulatory compliance
  - Easy audit preparation
  - Reduced verification time
- **Success Metrics:**
  - 100% documents stored centrally
  - Document verification time < 3 days
  - Zero document loss
- **Dependencies:** Supabase Storage, encryption

---

#### BR-12: Compliance & Audit Trail
- **Requirement ID:** BR-12
- **Category:** Compliance
- **Priority:** HIGH
- **Business Need:** Maintain complete audit logs and compliance records
- **Current Gap:** No audit trail, compliance risk, manual record-keeping
- **Proposed Solution:**
  - User action logging (who, what, when, where)
  - Data access logs
  - Change history for all records
  - Deletion and archival logs
  - Compliance reports (data retention, GDPR/DPDP compliance)
- **Business Value:**
  - Legal compliance
  - Fraud prevention
  - Dispute resolution
  - Audit readiness
- **Success Metrics:**
  - 100% action logging
  - Zero compliance incidents
  - Audit logs retained 7 years
- **Dependencies:** Database audit framework

---

### 4.2 NON-FUNCTIONAL BUSINESS REQUIREMENTS

#### NBR-1: Scalability
- **Requirement:** System should support business growth without major rework
- **Business Need:** Organization expects 50% YoY growth in hiring volume
- **Specifications:**
  - Handle 100+ concurrent users simultaneously
  - Support 10 years of candidate records (100K+ candidates)
  - Database query performance stable with large datasets
- **Success Criteria:** 
  - No performance degradation up to 100K records
  - Support 2-3x current hiring volume
- **Business Value:** Future-proof investment, avoid system replacement

---

#### NBR-2: Availability & Reliability
- **Requirement:** System must be available during business hours with minimal downtime
- **Business Need:** Recruitment is time-sensitive, downtime causes candidate loss
- **Specifications:**
  - 99.5% uptime target for HR team operations
  - 99% uptime for candidate portal during business hours
  - Automated daily backups
  - Disaster recovery: RTO 4 hours, RPO 1 hour
- **Success Criteria:**
  - Max downtime < 3.6 hours per month
  - Zero data loss incidents
- **Business Value:** Business continuity, candidate satisfaction

---

#### NBR-3: Performance
- **Requirement:** Fast, responsive system for good user experience
- **Business Need:** Slow systems lead to abandonment and frustration
- **Specifications:**
  - Page load time < 2 seconds for all interfaces
  - Database query response < 500ms
  - Bulk operations (export, reporting) < 30 seconds
- **Success Criteria:**
  - 95th percentile response time < 500ms
  - Zero timeout errors
- **Business Value:** Better user adoption, higher completion rates

---

#### NBR-4: Security
- **Requirement:** Protect sensitive candidate and business data
- **Business Need:** Data breaches damage reputation and incur penalties
- **Specifications:**
  - Data encryption in transit and at rest
  - Role-based access control (RBAC)
  - Multi-factor authentication for HR managers
  - Regular security audits
- **Success Criteria:**
  - Zero security incidents
  - Pass annual penetration testing
- **Business Value:** Trust, compliance, risk mitigation

---

#### NBR-5: Usability
- **Requirement:** Intuitive interface for all user types
- **Business Need:** Easy adoption without extensive training
- **Specifications:**
  - Intuitive mobile-first design for candidates
  - Desktop-friendly interface for HR
  - Multilingual support (English, Hindi, Bengali)
  - Accessibility compliance (WCAG 2.1 AA)
- **Success Criteria:**
  - User satisfaction > 4.0/5
  - < 5% support tickets for usability issues
- **Business Value:** Higher adoption, lower training costs

---

#### NBR-6: Maintainability
- **Requirement:** Easy to maintain, enhance, and troubleshoot
- **Business Need:** Minimize ongoing operational costs
- **Specifications:**
  - Clean, well-documented code
  - Modular design for easy feature additions
  - Automated testing coverage > 80%
  - Comprehensive documentation
- **Success Criteria:**
  - New feature development time reduced by 30%
  - Bug fix time < 24 hours
- **Business Value:** Lower TCO, faster enhancements

---

## 5. BUSINESS PROCESS FLOW

### 5.1 HIGH-LEVEL RECRUITMENT LIFECYCLE

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    RECRUITMENT & ONBOARDING LIFECYCLE                   │
└─────────────────────────────────────────────────────────────────────────┘

PHASE 1: AWARENESS & APPLICATION (Day 0-2)
├─ Vacancy Identified by Department
├─ WhatsApp Campaign Launched by HR
├─ Candidate Submits CV or Sees Campaign
├─ System Sends Form-1 Link
├─ Candidate Fills Form-1 (Basic Details)
└─ System Acknowledgment Sent

PHASE 2: SCREENING & ELIGIBILITY (Day 2-4)
├─ Eligibility Check (Qualification, Experience, 30-day rule)
├─ HR Recruiter Reviews Application
├─ Screened Candidate Path OR Walk-in Path Decision
├─ Shortlist or Reject Decision
└─ Interview Scheduled & Confirmed

PHASE 3: INTERVIEW & EVALUATION (Day 5-8)
├─ QR Code Generated for Interview Venue
├─ Interview Reminder Sent (1 day before)
├─ Candidate Arrives and Scans QR at Venue
├─ System Validates QR and Logs Check-in
├─ Form Presentation Based on Type:
│   ├─ Screened: Form-2 only
│   └─ Walk-in: Form-1 + Form-2
├─ Candidate Completes Required Forms
├─ Interview Panel Conducts Evaluation
├─ Form-3 (Evaluation) Submitted by Interviewer(s)
└─ HR Reviews All Evaluations

PHASE 4: DECISION & BACKGROUND VERIFICATION (Day 8-15)
├─ HR Manager Makes Decision (Select/Reject/Hold)
├─ Decision Communicated to Candidate
├─ If Rejected: Process Ends, Data Archived
├─ If Selected: BG Verification Initiated
├─ Document Collection & Verification (Manual Process)
├─ Status Tracked (Pending → In Progress → Cleared/Failed)
├─ If BG Failed: Offer Withdrawn, Candidate Notified
└─ If BG Cleared: HR Manager Final Approval

PHASE 5: OFFER & ACCEPTANCE (Day 15-22)
├─ Offer Letter Generated (Automated)
├─ Offer Sent to Candidate (Email + WhatsApp)
├─ Candidate Reviews Offer
├─ Candidate Accepts or Rejects
├─ If Rejected: Reason Captured, Process Ends
├─ If Accepted: Joining Date Confirmed
├─ Data Exported to HRMS/Octane
└─ Onboarding Workflow Initiated

PHASE 6: ONBOARDING & INDUCTION (Day 22-30)
├─ Welcome Message & Onboarding Checklist Sent
├─ Pre-induction Tasks Assigned:
│   ├─ IT Equipment Preparation
│   ├─ Desk Allocation
│   ├─ Access Card Generation
│   └─ System Account Creation
├─ Candidate Joins at Office on DOJ
├─ Induction QR Check-in at Reception
├─ Form-4: Final Onboarding Details Collection
├─ Post-induction Tasks:
│   ├─ Orientation Session
│   ├─ Department Introduction
│   ├─ Buddy Assignment
│   └─ First Project Assignment
├─ Task Completion Tracked
└─ Onboarding Marked Complete

PHASE 7: COMPLETION & ARCHIVAL (Day 30+)
├─ All Onboarding Records Verified
├─ Data Transferred to HRMS
├─ Recruitment Analytics Updated
├─ Recruitment Record Archived
└─ Process Complete
```

### 5.2 PROCESS DETAILS BY STAKEHOLDER

#### 5.2.1 Candidate Journey

**Discovery Stage (Day 0)**
1. Sees WhatsApp campaign, job portal post, or referral message
2. Interested in position, wants to apply

**Application Stage (Day 0-1)**
1. Sends message to WhatsApp bot or clicks application link
2. Receives Form-1 link via WhatsApp
3. Opens Form-1 on mobile/desktop
4. Fills basic details: Name, Email, Phone, Qualification, Experience, Desired Role
5. Submits Form-1
6. Receives acknowledgment message

**Waiting Stage (Day 1-5)**
1. System performs eligibility check
2. Receives status update: Shortlisted or Rejected
3. If rejected: Receives reason and alternative role suggestions
4. If shortlisted: Receives interview invitation with date, time, venue

**Interview Preparation (Day 5-6)**
1. Receives interview details via email and WhatsApp
2. Reviews venue location, parking instructions, reporting time
3. Prepares for interview (reviews job description, company info)
4. Receives reminder notification 1 day before

**Interview Day (Day 7)**
1. Arrives at venue 15 minutes early
2. Scans QR code at reception using mobile phone
3. System validates QR and confirms check-in
4. Receives form link based on candidate type:
   - **If Screened:** Form-2 link (Address, Qualifications, Documents)
   - **If Walk-in:** Form-1 + Form-2 links
5. Fills required forms while waiting
6. Uploads documents (Resume, Certificates)
7. Proceeds to interview room
8. Interviewed by panel
9. Thanks interviewer(s) and leaves
10. Receives "Thank You" message via WhatsApp

**Post-Interview Waiting (Day 7-10)**
1. Waits for interview result
2. Receives status updates in candidate portal
3. Can check application timeline anytime

**Decision Communication (Day 10)**
1. Receives interview result via email and WhatsApp
2. **If Rejected:** Receives empathetic rejection message with reason
3. **If Selected:** Receives congratulations and next steps (BG verification)

**Background Verification (Day 10-17)**
1. Receives document request for BG verification
2. Submits required documents
3. Receives BG clearance notification

**Offer Stage (Day 17-22)**
1. Receives offer letter via email (PDF)
2. Reviews offer details: Role, Salary, Benefits, DOJ
3. Logs into candidate portal
4. Accepts or rejects offer (or requests changes)
5. If accepted: Confirms joining date

**Pre-Joining (Day 22-30)**
1. Receives welcome message and onboarding checklist
2. Can view checklist progress in portal
3. Receives reminders for documents to bring
4. Receives venue and reporting time for Day 1

**Joining Day (Day 30)**
1. Arrives at office
2. Scans induction QR code at reception
3. Fills Form-4: Bank details, Emergency contact, Health info
4. Meets reception, HR, and manager
5. Receives IT equipment (laptop, access card)
6. Office tour and team introduction
7. Orientation session

**First Week**
1. Completes onboarding tasks
2. Assigned buddy mentor
3. Department onboarding and training
4. First project assignment
5. Onboarding marked complete

---

#### 5.2.2 Recruiter Workflow

**Recruitment Setup (Day 0)**
1. Receives recruitment requisition from HR Manager or Department Head
2. Understands role requirements: Skills, Experience, Qualifications
3. Creates vacancy posting in system
4. Launches WhatsApp campaign or job portal posting

**Application Review (Day 1-3)**
1. Logs into Recruiter Dashboard
2. Reviews applications in "Form-1 Submitted" status
3. Filters by: Role, Experience Level, Location, Submission Date
4. For each candidate:
   - Quick views profile summary
   - Checks eligibility (auto-validated by system)
   - Makes decision: Shortlist or Reject
5. For rejected candidates: Selects rejection reason from template
6. System automatically sends rejection notification to candidate

**Interview Coordination (Day 3-5)**
1. For shortlisted candidates:
   - Selects interview date and time
   - Checks interviewer availability
   - Assigns interview panel (Technical + HR + Manager)
   - Selects venue and adds details (parking, reporting time)
   - Submits interview schedule
2. System automatically:
   - Generates unique QR code for interview
   - Sends interview invite to candidate
   - Notifies assigned interviewers
3. Monitors interview schedule on calendar view
4. Manages any rescheduling requests

**QR Management (Day 6-7)**
1. Reviews QR codes for upcoming interviews
2. Prints QR codes for venue display (optional)
3. Ensures QR scanner is ready at reception
4. Coordinates with office admin for venue setup

**Interview Day (Day 7)**
1. Arrives at venue early
2. Ensures QR check-in system is working
3. Greets candidates as they arrive
4. Assists with any QR scanning issues
5. Ensures interviewers have candidate profiles
6. Tracks interview completion

**Post-Interview Follow-up (Day 7-10)**
1. Reminds interviewers to submit Form-3 evaluations
2. Tracks evaluation completion status
3. Escalates to HR Manager if evaluations pending > 48 hours
4. Monitors decision pending list

**Ongoing Tracking**
1. Updates candidate status as they progress
2. Responds to candidate queries
3. Maintains recruitment pipeline visibility
4. Generates weekly recruitment reports

---

#### 5.2.3 Interviewer Process

**Interview Assignment (Day 5)**
1. Receives interview assignment notification via email and in-app
2. Reviews notification details: Candidate, Date, Time, Venue, Role
3. Accepts or declines assignment (if scheduling conflict)
4. Logs into system to review candidate profile

**Pre-Interview Preparation (Day 5-6)**
1. Downloads candidate resume
2. Reviews Form-1 basic details
3. Prepares interview questions based on role requirements
4. Reviews evaluation rubric (Form-3)
5. Blocks calendar for interview time

**Interview Day (Day 7)**
1. Arrives at venue 10 minutes before interview time
2. Checks candidate QR check-in status in system
3. Reviews candidate Form-2 if available (address, qualifications)
4. Meets candidate in interview room
5. Conducts structured interview:
   - Technical assessment
   - Problem-solving questions
   - Communication and culture-fit assessment
6. Takes notes during interview
7. Thanks candidate and concludes interview

**Post-Interview Evaluation (Day 7)**
1. Logs into system immediately after interview (or within 24 hours)
2. Opens Form-3 evaluation form for candidate
3. Fills evaluation scores:
   - Technical Skills: 1-5 (with rubric guidance)
   - Communication: 1-5
   - Problem-Solving: 1-5
   - Cultural Fit: 1-5
   - Overall Assessment: 1-5
4. Writes strengths and areas for development
5. Selects recommendation: Select / Borderline / Reject
6. Adds panel feedback (internal notes for HR)
7. Submits evaluation
8. System sends confirmation and notifies HR Manager

**Follow-up (If Needed)**
1. Available for HR Manager clarifications
2. Participates in panel discussion if decision is borderline
3. Provides additional input as requested

---

#### 5.2.4 HR Manager Workflow

**Strategic Planning (Continuous)**
1. Reviews recruitment KPIs on dashboard:
   - Time-to-hire trend
   - Offer acceptance rate
   - Hiring pipeline by department
   - Quality metrics
2. Identifies bottlenecks and improvement areas
3. Plans recruitment campaigns
4. Sets targets for recruiters

**Application Oversight (Day 2-5)**
1. Reviews overall application pipeline
2. Monitors recruiter screening progress
3. Reviews high-priority or sensitive positions
4. Approves interview schedules
5. Ensures panel composition is appropriate

**Evaluation Review & Decision (Day 8-10)**
1. Logs into HR Manager Dashboard
2. Reviews "Pending Decision" list
3. For each candidate:
   - Views all panel member evaluations (Form-3)
   - Reviews aggregated scores
   - Checks for score outliers or inconsistencies
   - Reviews strengths and development areas
   - Considers business need and team fit
4. Makes final decision: Select / Reject / Hold
5. If rejected:
   - Selects reason from template or writes custom
   - System sends rejection notification
6. If selected:
   - Initiates background verification workflow
   - Assigns BG officer
   - System sends conditional offer message

**Background Verification Management (Day 10-15)**
1. Monitors BG verification status
2. Reviews documents submitted by BG officer
3. Reviews any flags or concerns
4. Makes final BG approval decision
5. If BG failed: Withdraws offer, notifies candidate
6. If BG cleared: Approves for offer generation

**Offer Management (Day 15-22)**
1. Reviews candidate details for offer letter
2. Confirms salary, designation, DOJ with Finance and Department Head
3. Generates offer letter (automated from template)
4. Reviews offer letter PDF for accuracy
5. Approves and sends offer
6. Tracks offer status: Sent → Viewed → Accepted/Rejected
7. If offer rejected: Contacts candidate for reason, considers counter-offer
8. If offer accepted: Confirms joining arrangements

**Onboarding Preparation (Day 22-30)**
1. Creates onboarding checklist for new employee
2. Assigns pre-joining tasks:
   - IT equipment preparation → IT Team
   - Desk allocation → Office Admin
   - Access card → Security Team
   - System accounts → IT Team
3. Monitors task completion status
4. Sends welcome message to candidate
5. Notifies department manager about new joinee

**Joining Day & Post-Joining (Day 30+)**
1. Welcomes new employee
2. Validates induction QR check-in
3. Ensures Form-4 completion
4. Reviews onboarding checklist progress
5. Conducts first-day orientation
6. Assigns buddy mentor
7. Tracks post-joining task completion
8. Marks onboarding as complete
9. Exports data to HRMS

**Analytics & Reporting (Monthly)**
1. Reviews monthly recruitment analytics
2. Generates reports:
   - Recruitment summary (applications, interviews, offers, joins)
   - Time-to-hire by department and role
   - Source effectiveness
   - Offer acceptance and joining rates
   - Recruiter performance
3. Presents insights to leadership
4. Plans process improvements

---

## 6. KEY PERFORMANCE INDICATORS (KPIs)

### 6.1 RECRUITMENT EFFICIENCY KPIs

| KPI | Current (AS-IS) | Target (TO-BE) | Measurement Formula | Reporting Frequency |
|-----|-----------------|----------------|---------------------|---------------------|
| **Time-to-Hire** | 30 days | 21 days (30% reduction) | Days from application to offer acceptance | Weekly/Monthly |
| **Time-to-Interview** | 7-10 days | 3 days | Days from application to interview scheduled | Weekly |
| **Time-to-Decision** | 5-7 days | 2 days | Days from interview to hiring decision | Weekly |
| **Application Drop-off Rate** | 35% | < 10% | % candidates starting but not completing Form-1 | Monthly |
| **Form Completion Rate** | N/A (Manual) | > 85% | % candidates completing all required forms | Monthly |
| **Interview Scheduling Time** | 2-3 days | < 24 hours | Hours from shortlist to interview scheduled | Weekly |
| **QR Check-in Rate** | N/A (New) | > 95% | % of scheduled candidates checking in via QR | Weekly |
| **Interview-to-Decision Time** | 5 days | < 3 days | Days from interview completion to decision | Weekly |
| **Evaluation Submission Time** | N/A | < 24 hours | Hours from interview to Form-3 submission | Weekly |
| **Offer Acceptance Rate** | 75% | > 85% | % of candidates accepting offers | Monthly |
| **Offer-to-Join Conversion** | 80% | > 90% | % of candidates joining after accepting offer | Monthly |
| **Joining Rate** | 60% (of selected) | > 85% | % of selected candidates actually joining | Monthly |

### 6.2 HIRING QUALITY KPIs

| KPI | Current | Target | Measurement Formula | Reporting Frequency |
|-----|---------|--------|---------------------|---------------------|
| **Candidate Quality Score** | N/A | > 4.0/5 | Average Form-3 evaluation score | Monthly |
| **Technical Score** | N/A | > 4.0/5 | Average technical skills rating | Monthly |
| **Cultural Fit Score** | N/A | > 4.2/5 | Average cultural fit rating | Monthly |
| **BG Clearance Rate** | 85% | > 95% | % of candidates clearing background verification | Monthly |
| **BG Clearance Time** | 20 days | < 14 days | Days for background verification completion | Monthly |
| **First-Year Retention Rate** | 75% | > 85% | % of hires retained after 1 year | Quarterly |
| **90-Day Retention** | 80% | > 90% | % of hires retained after 90 days | Quarterly |
| **Performance Rating (6 months)** | N/A | > 3.5/5 | Average manager performance rating at 6 months | Quarterly |
| **New Hire Productivity** | N/A | Baseline | Time to reach 80% productivity | Quarterly |
| **Manager Satisfaction** | N/A | > 4.0/5 | Hiring manager satisfaction with quality of hire | Quarterly |

### 6.3 PROCESS QUALITY KPIs

| KPI | Current | Target | Measurement Formula | Reporting Frequency |
|-----|---------|--------|---------------------|---------------------|
| **Data Accuracy** | 70% | > 98% | % of records with correct/complete data | Monthly |
| **Data Completeness** | 60% | > 95% | % of mandatory fields filled | Monthly |
| **Audit Trail Completeness** | 0% | 100% | % of actions with complete audit logs | Daily |
| **System Uptime** | N/A | > 99.5% | % of time system available during business hours | Daily |
| **System Response Time** | N/A | < 2 sec | Average page load time | Daily |
| **User Satisfaction (HR)** | N/A | > 4.0/5 | NPS score for HR users | Quarterly |
| **User Satisfaction (Candidates)** | N/A | > 4.0/5 | NPS score for candidates | Quarterly |
| **Error/Exception Rate** | High | < 2% | % of processes requiring manual intervention | Monthly |
| **Document Verification Time** | 7 days | < 3 days | Days to verify uploaded documents | Monthly |
| **Communication Delivery Rate** | 85% | > 98% | % of emails/WhatsApp delivered successfully | Weekly |
| **Support Ticket Volume** | N/A | Baseline | Number of support tickets per 100 applications | Monthly |

### 6.4 BUSINESS IMPACT KPIs

| KPI | Current | Target | Measurement Formula | Reporting Frequency |
|-----|---------|--------|---------------------|---------------------|
| **Manual Data Entry Reduction** | Baseline | 90% | Hours saved on manual data entry | Quarterly |
| **Cost per Hire** | $2000 | $1200 (40% reduction) | Total recruitment cost / number of hires | Quarterly |
| **HR Productivity** | 20 candidates/month | 35 candidates/month | Candidates processed per HR per month | Monthly |
| **Recruiter Productivity** | 15 candidates/month | 25 candidates/month | Candidates screened per recruiter per month | Monthly |
| **Interview No-Show Rate** | 20% | < 5% | % of scheduled candidates not showing up | Monthly |
| **Candidate Satisfaction (NPS)** | N/A | > 70 | Net Promoter Score from candidate survey | Quarterly |
| **Employer Brand Score** | N/A | Baseline | Glassdoor/LinkedIn ratings improvement | Semi-annually |
| **Compliance Incidents** | Unknown | 0 | Number of data/compliance violations | Quarterly |
| **Audit Findings** | Unknown | 0 | Number of audit issues identified | Annually |
| **Process Automation Rate** | 10% | 80% | % of recruitment tasks automated | Quarterly |

### 6.5 ADOPTION & USAGE KPIs

| KPI | Target | Measurement Formula | Reporting Frequency |
|-----|--------|---------------------|---------------------|
| **User Adoption Rate (HR)** | 100% | % of HR staff actively using system | Monthly |
| **User Adoption Rate (Candidates)** | > 90% | % of candidates completing digital forms | Monthly |
| **Mobile Usage Rate** | > 70% | % of candidates using mobile for application | Monthly |
| **WhatsApp Response Rate** | > 85% | % of candidates responding to WhatsApp notifications | Monthly |
| **Email Open Rate** | > 60% | % of recruitment emails opened | Monthly |
| **Dashboard Usage** | Daily | Login frequency of HR managers | Weekly |
| **Feature Utilization** | > 80% | % of key features actively used | Quarterly |

---

## 7. BUSINESS BENEFITS

### 7.1 QUANTIFIABLE BENEFITS

#### 7.1.1 Time Savings

| Benefit | Current State | Future State | Savings | Annual Value |
|---------|--------------|--------------|---------|--------------|
| **Recruitment Cycle Time** | 30 days | 10 days | 20 days (67%) | 20 days × 200 hires = 4000 person-days saved |
| **Manual Data Entry** | 50 hrs per 100 applications | 5 hrs per 100 applications | 45 hrs (90%) | 45 hrs × 20 batches = 900 hrs/year saved |
| **Interview Scheduling** | 2 hrs per interview | 15 min per interview | 1.75 hrs (87%) | 1.75 hrs × 200 interviews = 350 hrs/year |
| **Document Collection** | 3 hrs per candidate | 30 min per candidate | 2.5 hrs (83%) | 2.5 hrs × 200 candidates = 500 hrs/year |
| **Report Generation** | 8 hrs/month | 30 min/month | 7.5 hrs (94%) | 7.5 hrs × 12 months = 90 hrs/year |
| **Offer Letter Creation** | 2 hrs per offer | 15 min per offer | 1.75 hrs (87%) | 1.75 hrs × 150 offers = 262 hrs/year |
| **TOTAL TIME SAVINGS** | - | - | - | **~2100 hours/year** |

**Monetary Value of Time Savings:**
- Average HR hourly cost: $30/hour
- Annual savings: 2100 hours × $30 = **$63,000/year**

#### 7.1.2 Cost Savings

| Cost Category | Current Annual Cost | Projected Annual Cost | Savings | % Reduction |
|---------------|---------------------|----------------------|---------|-------------|
| **Manual Processing** | $45,000 | $5,000 | $40,000 | 89% |
| **Paper & Printing** | $3,000 | $300 | $2,700 | 90% |
| **Document Storage** | $2,000 | $0 | $2,000 | 100% |
| **Communication (calls, SMS)** | $5,000 | $1,500 (WhatsApp) | $3,500 | 70% |
| **External Recruitment** | $80,000 (fees) | $60,000 | $20,000 | 25% |
| **Hiring Mistakes (attrition)** | $100,000 | $60,000 | $40,000 | 40% |
| **TOTAL COST SAVINGS** | **$235,000** | **$126,800** | **$108,200** | **46%** |

#### 7.1.3 Revenue Impact

| Metric | Current | Target | Impact | Annual Value |
|--------|---------|--------|--------|--------------|
| **Time-to-Productivity** | 90 days | 60 days | 30 days faster | 30 days × 200 hires × $150/day productivity = $900,000 |
| **Vacancy Cost** | 30 days open | 10 days open | 20 days faster filling | 20 days × 200 positions × $500/day = $2,000,000 |
| **Quality of Hire** | 75% success rate | 90% success rate | 15% improvement | Reduced replacement cost: $80,000 |
| **TOTAL REVENUE IMPACT** | - | - | - | **~$2,980,000** |

#### 7.1.4 ROI Calculation

**Investment:**
- Development Cost (Phase 1-3): $150,000
- Infrastructure (Annual): $15,000
- Training & Change Management: $10,000
- **Total Year 1 Investment:** $175,000

**Returns:**
- Time Savings: $63,000/year
- Cost Savings: $108,200/year
- **Total Direct Savings:** $171,200/year

**ROI:**
- **Payback Period:** 12.3 months
- **Year 1 ROI:** -2% (breakeven)
- **Year 2 ROI:** 98%
- **Year 3 ROI:** 195%
- **3-Year Total ROI:** 194%

*Note: Revenue impact not included in ROI calculation (conservative estimate)*

### 7.2 QUALITATIVE BENEFITS

#### 7.2.1 Enhanced Employer Branding

**Current Challenges:**
- Manual, paper-based process perceived as outdated
- Poor candidate communication leads to negative reviews
- Inconsistent candidate experience

**Future Benefits:**
- **Professional Digital Experience:** Modern, mobile-first application process
- **Timely Communication:** Real-time status updates via WhatsApp and email
- **Positive Candidate Feedback:** Improved NPS and online reviews
- **Competitive Advantage:** Stand out in talent market

**Impact:**
- 30-40% improvement in employer brand ratings
- Increased referrals from candidates
- Easier attraction of top talent

---

#### 7.2.2 Better Decision Making

**Current Challenges:**
- No structured evaluation data
- Decisions based on intuition and incomplete information
- No historical hiring trend analysis

**Future Benefits:**
- **Data-Driven Hiring:** Structured evaluation scores and analytics
- **Historical Insights:** Trend analysis on time-to-hire, source effectiveness, quality of hire
- **Predictive Analytics:** Forecast hiring needs based on pipeline data
- **Informed Strategy:** Optimize recruitment channels and process

**Impact:**
- 25% improvement in hiring quality
- Better alignment of hiring with business needs
- Optimized recruitment budget allocation

---

#### 7.2.3 Improved Compliance & Risk Mitigation

**Current Challenges:**
- No audit trail for hiring decisions
- Manual document handling prone to loss
- Compliance risks with data protection laws

**Future Benefits:**
- **Complete Audit Trail:** Every action logged with timestamp and user
- **Document Retention:** Secure, version-controlled document management
- **Regulatory Compliance:** DPDP Act 2023 compliance built-in
- **Risk Reduction:** Reduced legal exposure from hiring disputes

**Impact:**
- Zero compliance violations
- Reduced legal risk
- Faster audit preparation (from weeks to hours)

---

#### 7.2.4 Scalability Without Proportional Cost Increase

**Current Challenges:**
- Manual process doesn't scale
- Adding hiring volume requires more HR staff

**Future Benefits:**
- **Process Automation:** Handle 2-3x volume without additional headcount
- **Consistent Process:** Same quality regardless of volume
- **Geographic Expansion:** Support multiple locations seamlessly

**Impact:**
- Support 50% YoY growth without HR expansion
- Consistent process across all departments and locations
- Reduced marginal cost per hire as volume increases

---

#### 7.2.5 Enhanced Employee Experience

**Current Challenges:**
- Ad-hoc onboarding leads to confusion
- New hires feel lost on first day
- Inconsistent onboarding across departments

**Future Benefits:**
- **Structured Onboarding:** Clear checklist and expectations
- **Smooth First Day:** All logistics pre-arranged
- **Better Integration:** Buddy system and clear task tracking
- **Positive First Impression:** Professional, organized process

**Impact:**
- 20% reduction in early attrition (< 90 days)
- 25% faster time-to-productivity
- Higher new hire satisfaction scores

---

#### 7.2.6 Organizational Insights & Continuous Improvement

**Current Challenges:**
- No visibility into recruitment bottlenecks
- Cannot measure effectiveness of recruitment channels
- Process improvements based on gut feel

**Future Benefits:**
- **Pipeline Visibility:** Identify where candidates drop off
- **Source Analysis:** ROI of each recruitment channel
- **Trend Analysis:** Seasonal hiring patterns, time-to-hire trends
- **Continuous Improvement:** Data-driven process optimization

**Impact:**
- 30% improvement in recruitment process efficiency over 2 years
- Better resource allocation
- Proactive talent pipeline management

---

## 8. STAKEHOLDER ANALYSIS

### 8.1 PRIMARY STAKEHOLDERS

| Stakeholder | Role | Interest | Influence | Engagement Strategy |
|------------|------|----------|-----------|---------------------|
| **HR Manager** | Decision Maker, Primary User | High - Daily system user, needs efficiency | High - Final approval authority | Weekly demos, continuous feedback |
| **Recruiters** | Primary User | High - Daily workflow impact | Medium - Input on features | Training, user testing, feedback sessions |
| **Interviewers** | Periodic User | Medium - Occasional use for Form-3 | Low - Limited system interaction | Simple training, quick reference guide |
| **Candidates** | End User | High - Direct application experience | Low - No system decisions | User-friendly design, support channel |
| **IT Team** | System Owner, Support | Medium - Infrastructure responsibility | Medium - Technical feasibility | Technical documentation, handover |
| **Finance Team** | Data Consumer | Low - Payroll data recipient | Low - Downstream consumer | Data export format alignment |
| **Department Heads** | Beneficiary | High - Quality hires faster | High - Business need drivers | Executive dashboard, monthly reports |
| **CEO/Leadership** | Sponsor | High - Business impact, ROI | High - Final budget approval | Executive summary, ROI presentation |

### 8.2 SECONDARY STAKEHOLDERS

| Stakeholder | Role | Interest | Engagement Strategy |
|------------|------|----------|---------------------|
| **Background Verification Vendor** | External Service | Medium - Status tracking | Integration planning, API coordination |
| **HRMS/Octane Team** | System Integration | Medium - Data import | Export format specification, testing |
| **Legal/Compliance Team** | Risk Management | High - Regulatory compliance | Compliance review, sign-off |
| **Office Admin** | Venue Coordination | Low - Interview logistics | Simple communication plan |
| **Security Team** | Access Control | Low - Access card generation | Onboarding checklist integration |

---

## 9. ASSUMPTIONS & CONSTRAINTS

### 9.1 BUSINESS ASSUMPTIONS

1. **Hiring Volume:** Organization will maintain or increase current hiring volume (200+ hires/year)
2. **HR Commitment:** HR team will dedicate 20% time to system testing and feedback
3. **Candidate Technology Access:** 95%+ candidates have smartphone with camera and internet
4. **Interviewer Participation:** Interviewers will complete Form-3 evaluations within 24 hours
5. **Data Migration:** Legacy data (if any) will be provided in structured format (Excel/CSV)
6. **Process Adherence:** All stakeholders will follow the new digital process (no parallel manual process)
7. **Internet Connectivity:** Office venues have stable internet for QR check-in
8. **WhatsApp Availability:** Candidates and HR have active WhatsApp accounts
9. **Email Accessibility:** Candidates regularly check email for formal communication
10. **Budget Availability:** Approved budget will be released as per project milestones

### 9.2 TECHNICAL CONSTRAINTS

1. **Technology Stack:** Must use Python (FastAPI, Streamlit), PostgreSQL, Supabase, n8n
2. **Infrastructure:** AWS India region for data localization
3. **Integration Limitations:** n8n integration capabilities for WhatsApp and email
4. **Database Size:** PostgreSQL storage limits and query performance considerations
5. **API Rate Limits:** WhatsApp Business API rate limits for messaging
6. **File Storage:** Supabase Storage limits for document uploads
7. **Concurrent Users:** System designed for 100 concurrent users initially
8. **Browser Support:** Chrome, Safari, Firefox (latest 2 versions)
9. **Mobile OS:** Android 8+ and iOS 13+ support
10. **Network Dependency:** System requires internet connectivity (no offline mode in Phase 1)

### 9.3 RESOURCE CONSTRAINTS

1. **Development Team:** 1 Technical Lead + 2 Developers for 6 months
2. **HR Testing:** Max 2 weeks for UAT with 3-4 HR staff
3. **Budget Cap:** $175,000 for complete implementation (Phases 1-3)
4. **Timeline:** 6 months total (3 + 2 + 1 months for phases)
5. **Training Time:** 1 week for HR staff training
6. **Support:** Limited to business hours (9 AM - 6 PM IST) initially

### 9.4 REGULATORY CONSTRAINTS

1. **DPDP Act 2023:** Compliance with India's Digital Personal Data Protection Act
2. **Data Localization:** Candidate data must be stored in India
3. **Consent Management:** Explicit consent required for data processing
4. **Right to Deletion:** GDPR-like right to be forgotten implementation
5. **Labor Laws:** Compliance with Indian employment and hiring regulations
6. **Audit Requirements:** Maintain audit logs for 7 years minimum
7. **Equal Opportunity:** No discriminatory practices in hiring process

---

## 10. APPROVAL & SIGN-OFF

### 10.1 DOCUMENT APPROVAL

This Business Requirements Document has been reviewed and approved by the following stakeholders:

| Name | Role | Signature | Date |
|------|------|-----------|------|
| [To be filled] | CEO / Business Sponsor | ________________ | ______ |
| [To be filled] | HR Manager / Primary Stakeholder | ________________ | ______ |
| [To be filled] | IT Manager / Technical Lead | ________________ | ______ |
| [To be filled] | Finance Head / Budget Approver | ________________ | ______ |
| [To be filled] | Legal/Compliance Officer | ________________ | ______ |

### 10.2 DOCUMENT CHANGE CONTROL

| Version | Date | Author | Changes | Approved By |
|---------|------|--------|---------|-------------|
| 0.1 | [Date] | [Author] | Initial Draft | - |
| 0.2 | [Date] | [Author] | Stakeholder Feedback Incorporated | - |
| 1.0 | January 05, 2026 | AI Assistant | Final Version | Pending |

### 10.3 NEXT STEPS

Upon approval of this BRD:

1. **Week 1-2:** Develop detailed Software Requirements Specification (SRS)
2. **Week 2-3:** Technical architecture design and database schema finalization
3. **Week 3-4:** Project kickoff, team onboarding, development environment setup
4. **Month 2-4:** Phase 1 Development (MVP)
5. **Month 4:** Phase 1 UAT and Deployment
6. **Month 5-6:** Phase 2 Development (Onboarding & Advanced Features)
7. **Month 6:** Phase 3 Optimization, Testing, Training, Go-Live

### 10.4 SUCCESS CRITERIA FOR BRD ACCEPTANCE

This BRD will be considered accepted when:
- ✅ All primary stakeholders have reviewed and signed off
- ✅ Budget approval received from Finance
- ✅ Legal/Compliance approval for data protection approach
- ✅ IT infrastructure feasibility confirmed
- ✅ Project timeline and resource allocation approved
- ✅ Risk mitigation strategies agreed upon

---

**Document Status:** FINAL  
**Version:** 1.0  
**Date:** January 05, 2026  
**Prepared By:** AI Assistant  
**For:** Sampurna Financial Services Pvt. Ltd. (SFSPL)

---

**CONFIDENTIAL:** This document contains proprietary business information and is intended solely for the use of authorized personnel at SFSPL.

---
