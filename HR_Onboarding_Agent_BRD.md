# Business Requirements Document (BRD)
# HR Onboarding Agent System

**Document Version Control**

| Version | Date       | Author   | Change Description                                      |
|---------|------------|----------|--------------------------------------------------------|
| 1.0     | 2026-01-09 | Md Sahil | Initial BRD document for HR Onboarding Agent System |

---

## Document Approval

| Role                          | Name      | Signature | Date       |
|-------------------------------|-----------|-----------|------------|
| Executive Sponsor             |           |           |            |
| Managing Director             |           |           |            |
| Head of Human Resources       |           |           |            |
| Chief Technology Officer      |           |           |            |
| Project Manager               | Md Sahil  |           | 2026-01-09 |
| Finance Controller            |           |           |            |

---

## Executive Summary

### Business Challenge

Sampurna Financial Services Pvt. Ltd. (SFSPL) currently processes approximately **1,500 job applications monthly** through a predominantly manual recruitment process. This approach relies on WhatsApp messaging, Excel spreadsheets, and email communications, resulting in significant operational inefficiencies, data loss, and inability to make data-driven hiring decisions.

**Current Pain Points:**
- **Data Loss:** 30-40% of candidate information lost during manual handoffs
- **Time Inefficiency:** Average 45 days time-to-hire (industry standard: 30 days)
- **No Visibility:** Management lacks real-time insights into recruitment pipeline
- **Compliance Risk:** Incomplete audit trails and data retention issues
- **Poor Candidate Experience:** Delayed communications and unclear status updates
- **Resource Drain:** HR team spends 60% of time on administrative tasks vs. strategic hiring

### Proposed Solution

Implementation of a comprehensive **HR Onboarding Agent System** - a digital platform that automates and streamlines the entire recruitment lifecycle from initial candidate contact through successful employee onboarding.

**Solution Highlights:**
- **Digital Forms:** Four-stage form capture (Forms 1-4) ensuring complete data collection
- **QR-Based Check-in:** Innovative venue check-in with automatic candidate path routing
- **Automated Communications:** WhatsApp and Email integration for timely notifications
- **Real-time Tracking:** Complete visibility of candidate progress for all stakeholders
- **Analytics Dashboard:** Data-driven insights for recruitment optimization
- **Multilingual Support:** English, Hindi, and Bengali for diverse candidate base

### Expected Business Outcomes

| Metric | Current State | Target State | Improvement |
|--------|--------------|--------------|-------------|
| **Data Capture** | 60-70% complete | 100% complete | 30-40% increase |
| **Time-to-Hire** | 45 days | 22 days | 51% reduction |
| **HR Admin Time** | 60% of work hours | 15% of work hours | 75% reduction |
| **Candidate Satisfaction** | Not measured | 80%+ satisfaction | New capability |
| **Process Visibility** | 0% real-time | 100% real-time | Complete visibility |
| **Compliance** | Partial audit trail | 100% audit trail | Full compliance |

### Investment Summary

| Category | Amount (INR) |
|----------|--------------|
| **Development Costs** | 8,00,000 - 12,00,000 |
| **Infrastructure (Annual)** | 2,40,000 - 3,60,000 |
| **Training & Change Management** | 1,00,000 |
| **Total First Year Investment** | 11,40,000 - 16,60,000 |
| **Annual Operating Cost (Year 2+)** | 3,00,000 - 4,20,000 |

**Return on Investment (ROI):**
- **Payback Period:** x-y months
- **3-Year Net Savings:** ₹n1-n2 lakhs
- **ROI (3 years):** r1-r2%

### Recommendation

**Approval Requested** for immediate project initiation with Phase 1 implementation targeted for completion within 3 months. The investment will deliver substantial operational efficiency gains, improved candidate experience, enhanced compliance, and strong financial returns.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Business Objectives and Goals](#2-business-objectives-and-goals)
3. [Current State Assessment](#3-current-state-assessment)
4. [Business Requirements](#4-business-requirements)
5. [Stakeholder Analysis](#5-stakeholder-analysis)
6. [Scope Definition](#6-scope-definition)
7. [Success Criteria and KPIs](#7-success-criteria-and-kpis)
8. [Cost-Benefit Analysis](#8-cost-benefit-analysis)
9. [Risk Assessment](#9-risk-assessment)
10. [Project Timeline and Phases](#10-project-timeline-and-phases)
11. [Assumptions and Dependencies](#11-assumptions-and-dependencies)
12. [Appendices](#12-appendices)

---

## 1. Project Overview

### 1.1 Project Background

Sampurna Financial Services Pvt. Ltd. (SFSPL) is experiencing significant growth in its business operations, necessitating regular recruitment of qualified personnel across multiple roles and locations. The current recruitment process, while functional, is heavily manual and cannot scale effectively to meet the organization's growing needs.

**Current Process Overview:**
1. Candidates send CVs via WhatsApp to HR team
2. HR manually reviews CVs and conducts phone screenings
3. Eligible candidates invited for in-person interviews via WhatsApp
4. Interview feedback captured in Excel sheets
5. Selection decisions made based on Excel data
6. Manual background verification coordination
7. Offer letters created in Word and sent via email
8. Onboarding information collected on joining day
9. Data manually entered into Octane HRMS

**Processing Volume:**
- **1,500+ applications per month**
- **x-y interviews per month**
- **h1-h2 hires per month**

### 1.2 Business Drivers

**Strategic Drivers:**
1. **Business Growth:** SFSPL expanding operations requires efficient talent acquisition at scale
2. **Digital Transformation:** Organizational initiative to digitize core business processes
3. **Competitive Advantage:** Attract top talent through superior candidate experience
4. **Data-Driven Decisions:** Enable analytics-based recruitment strategy optimization

**Operational Drivers:**
1. **Efficiency:** Reduce time and effort spent on manual administrative tasks
2. **Quality:** Ensure complete and accurate candidate data collection
3. **Compliance:** Maintain complete audit trails for regulatory requirements
4. **Scalability:** Support growing recruitment volume without proportional resource increase

**Risk Mitigation Drivers:**
1. **Data Loss Prevention:** Eliminate information loss in manual handoffs
2. **Compliance Risk:** Address audit trail gaps and data retention issues
3. **Reputation Risk:** Improve candidate experience to protect employer brand

### 1.3 Project Vision

**Vision Statement:**
"To establish SFSPL as an employer of choice through a world-class digital recruitment experience that enables data-driven hiring decisions while maximizing HR team productivity."

**Strategic Alignment:**
This project aligns with SFSPL's broader digital transformation initiative and supports the organization's growth objectives by:
- Enabling scalable talent acquisition processes
- Freeing HR team to focus on strategic activities
- Building data foundation for predictive workforce planning
- Enhancing employer brand through superior candidate experience

---

## 2. Business Objectives and Goals

### 2.1 Primary Business Objectives

**Objective 1: Operational Efficiency**
- **Goal:** Reduce HR administrative workload by 75%
- **Measure:** Time spent on data entry, communication, and status tracking
- **Target:** From 60% of HR time to 15% within 6 months of implementation
- **Business Value:** HR team can focus on strategic hiring and candidate engagement

**Objective 2: Data Quality and Completeness**
- **Goal:** Achieve 100% complete candidate data capture
- **Measure:** Percentage of required fields populated in candidate records
- **Target:** From 60-70% to 100% within 3 months
- **Business Value:** Better hiring decisions, improved HRMS data quality, enhanced analytics

**Objective 3: Time-to-Hire Reduction**
- **Goal:** Reduce average time-to-hire by 50%
- **Measure:** Days from CV submission to offer acceptance
- **Target:** From 45 days to 22 days within 6 months
- **Business Value:** Faster access to talent, reduced risk of candidate dropout, lower vacancy costs

**Objective 4: Process Visibility and Control**
- **Goal:** Provide real-time visibility into recruitment pipeline
- **Measure:** Percentage of stakeholders with access to real-time data
- **Target:** 100% of relevant stakeholders within 1 month of go-live
- **Business Value:** Better resource planning, proactive bottleneck management, informed decisions

**Objective 5: Candidate Experience Improvement**
- **Goal:** Achieve 80%+ candidate satisfaction rating
- **Measure:** Post-process candidate satisfaction survey
- **Target:** 80% satisfaction score within 6 months
- **Business Value:** Enhanced employer brand, reduced candidate dropout, positive word-of-mouth

**Objective 6: Compliance and Audit Readiness**
- **Goal:** Maintain 100% audit trail for all recruitment activities
- **Measure:** Percentage of activities with complete audit records
- **Target:** 100% from day 1 of implementation
- **Business Value:** Regulatory compliance, risk mitigation, defense against legal challenges

### 2.2 Secondary Business Objectives

**Objective 7: Cost Optimization**
- **Goal:** Reduce overall cost-per-hire by 30%
- **Target:** Within 12 months through efficiency gains
- **Value:** Direct financial savings, improved recruitment ROI

**Objective 8: Analytics Capability**
- **Goal:** Enable data-driven recruitment optimization
- **Target:** Monthly analytics reviews identifying improvement opportunities
- **Value:** Continuous process improvement, source effectiveness analysis, quality hiring

**Objective 9: Scalability**
- **Goal:** Support 2x recruitment volume without proportional resource increase
- **Target:** System capable of handling 3,000+ applications monthly
- **Value:** Business growth enablement, future-proofing

**Objective 10: Employee Onboarding Quality**
- **Goal:** Reduce first-day administrative time by 60%
- **Target:** From 4 hours to 1.5 hours through pre-collected data
- **Value:** Better new hire experience, faster productivity ramp-up

### 2.3 Strategic Goals Alignment

| Corporate Goal | Project Contribution | Expected Impact |
|----------------|---------------------|-----------------|
| **Digital Transformation** | Digitize complete recruitment process | High - flagship HR digital initiative |
| **Operational Excellence** | Automate manual tasks, reduce errors | High - 75% efficiency gain |
| **Customer Centricity** | Improve candidate experience | Medium - candidates as customers |
| **Data-Driven Organization** | Enable recruitment analytics | High - foundation for HR analytics |
| **Talent Excellence** | Better hiring decisions through data | Medium - improved hire quality |
| **Cost Leadership** | Reduce cost-per-hire | Medium - 30% cost reduction |

---

## 3. Current State Assessment

### 3.1 Current Process Description

**Step 1: Candidate Sourcing and Initial Contact**
- **Method:** Job postings on social media, candidates WhatsApp CVs to HR number
- **Challenges:** 
  - No structured data collection
  - CVs lost in WhatsApp threads
  - No tracking of source effectiveness
  - Delayed responses to candidates

**Step 2: Preliminary Screening**
- **Method:** HR manually reviews CVs, calls candidates for basic screening
- **Challenges:**
  - Time-intensive (15-20 minutes per candidate)
  - No standardized evaluation criteria
  - Screening notes lost or incomplete
  - Inability to track screening outcomes

**Step 3: Interview Scheduling**
- **Method:** HR manually coordinates dates/times via WhatsApp, updates Excel tracker
- **Challenges:**
  - Back-and-forth messaging (average 8-10 messages per candidate)
  - Calendar conflicts and no-shows
  - No automated reminders
  - Excel sheet becomes version control nightmare

**Step 4: Interview Day Management**
- **Method:** Candidates arrive, manual sign-in sheet, paper forms
- **Challenges:**
  - Walk-in candidates with no prior registration
  - Duplicate data collection
  - Lost or incomplete forms
  - No real-time tracking of interview progress

**Step 5: Interview Evaluation**
- **Method:** Panel members verbally discuss, HR records notes in Excel
- **Challenges:**
  - Inconsistent evaluation criteria
  - Subjective and non-standardized feedback
  - Evaluation notes incomplete
  - Difficult to compare candidates

**Step 6: Selection Decision**
- **Method:** HR reviews Excel sheet, consults with management
- **Challenges:**
  - Excel data incomplete or outdated
  - No audit trail of decision rationale
  - Delayed decisions (candidates wait days/weeks)
  - Inability to quickly retrieve decision history

**Step 7: Background Verification**
- **Method:** HR manually coordinates with third-party vendors
- **Challenges:**
  - No system tracking of BG status
  - Delays due to manual follow-up
  - Lost documentation
  - No centralized repository

**Step 8: Offer Letter Generation**
- **Method:** HR creates Word documents, manually emails
- **Challenges:**
  - Time-intensive (30-45 minutes per offer)
  - Errors in manual data entry
  - No tracking of offer acceptance/rejection
  - Lost email threads

**Step 9: Onboarding**
- **Method:** Paper forms on joining day, manual data entry to HRMS
- **Challenges:**
  - Repetitive data collection (asked same info 3-4 times)
  - First day spent on paperwork (3-4 hours)
  - Errors in HRMS data entry
  - Poor new hire experience

### 3.2 Pain Points Summary

| Category | Pain Point | Impact | Frequency |
|----------|-----------|--------|-----------|
| **Data Loss** | Candidate information lost between steps | High | 30-40% of candidates |
| **Time Waste** | Manual data entry and re-entry | High | Daily, all HR staff |
| **Communication Delays** | Manual WhatsApp/email coordination | Medium | Every candidate interaction |
| **No Visibility** | Management cannot see pipeline status | High | Continuous |
| **Excel Chaos** | Version control, concurrent editing issues | Medium | Weekly |
| **Candidate Frustration** | Unclear status, delayed responses | Medium | 40% of candidates |
| **Compliance Gaps** | Incomplete audit trails | High | Continuous |
| **Quality Issues** | Inconsistent evaluations | Medium | Every interview |
| **Scalability Limits** | Process breaks down at higher volumes | High | Monthly (during peaks) |
| **HRMS Data Quality** | Incomplete/incorrect data in HRMS | Medium | 20% of new hires |

### 3.3 Current State Metrics

| Metric | Current Performance | Industry Benchmark |
|--------|--------------------|--------------------|
| **Average Time-to-Hire** | 45 days | 30 days |
| **HR Admin Time** | 60% of total work | 20-30% |
| **Data Completeness** | 60-70% | 95%+ |
| **Candidate Satisfaction** | Not measured | 75-85% |
| **Cost-per-Hire** | ₹15,000 | ₹10,000 |
| **Offer Acceptance Rate** | 65% | 80-85% |
| **New Hire Turnover (90 days)** | 18% | 10-12% |
| **Interview-to-Hire Ratio** | 5:1 | 3:1 |
| **Process Compliance** | 40% | 100% |

### 3.4 Stakeholder Feedback

**HR Team:**
- "We spend most of our time on data entry instead of actually engaging with candidates"
- "Excel sheets are a nightmare - we never know which version is current"
- "Candidates constantly ask for status updates, and we don't have good answers"

**Hiring Managers:**
- "I have no visibility into the recruitment pipeline for my team"
- "Selection decisions are delayed because we can't quickly access candidate information"
- "Interview feedback is incomplete, making comparisons difficult"

**Management:**
- "We need data to understand our recruitment effectiveness, but we don't have it"
- "The current process doesn't scale - how will we handle double the volume?"
- "Compliance is a major concern with our current approach"

**Candidates (Informal Feedback):**
- "I applied 3 weeks ago and still haven't heard back"
- "I had to provide the same information multiple times"
- "The interview process was disorganized and unprofessional"

---

## 4. Business Requirements

### 4.1 Functional Business Requirements

#### BR-F-001: Digital Candidate Registration
**Business Need:** Capture complete candidate information at first contact
**Requirement:** System must provide web-based registration form accessible via WhatsApp link
**Business Value:** 100% data capture, elimination of manual data entry, improved data quality
**Priority:** CRITICAL
**Acceptance Criteria:**
- Form accessible on mobile devices
- All mandatory fields validated before submission
- Confirmation sent to candidate upon submission
- Data automatically stored in centralized database

#### BR-F-002: Interview Scheduling Automation
**Business Need:** Reduce manual coordination effort and improve scheduling efficiency
**Requirement:** System must enable one-click interview scheduling with automated candidate notification
**Business Value:** 80% reduction in scheduling time, reduced no-shows through automated reminders
**Priority:** CRITICAL
**Acceptance Criteria:**
- HR can schedule interviews in < 2 minutes
- Automated WhatsApp/Email notification sent to candidate
- Automated reminder sent 24 hours before interview
- Calendar integration (optional future enhancement)

#### BR-F-003: QR-Based Interview Check-in
**Business Need:** Streamline interview day logistics and eliminate paper forms
**Requirement:** System must provide QR code-based check-in at interview venue
**Business Value:** Faster check-in process, automatic attendance tracking, paperless operation
**Priority:** HIGH
**Acceptance Criteria:**
- Candidates can scan QR code using personal mobile devices or venue tablets
- Check-in completes in < 30 seconds
- System automatically routes to appropriate forms based on candidate status
- Real-time check-in notification to HR team

#### BR-F-004: Standardized Interview Evaluation
**Business Need:** Ensure consistent and objective candidate assessment
**Requirement:** System must provide structured evaluation form for interview panels
**Business Value:** Objective comparisons, audit trail, quality hiring decisions
**Priority:** CRITICAL
**Acceptance Criteria:**
- Evaluation form with predefined criteria and rating scales
- Mandatory fields to ensure completeness
- Automatic score calculation
- Panel member feedback aggregation for multi-interviewer scenarios

#### BR-F-005: Selection Workflow Management
**Business Need:** Streamline decision-making and maintain audit trail
**Requirement:** System must guide selection decisions through structured workflow
**Business Value:** Faster decisions, complete audit trail, compliance assurance
**Priority:** CRITICAL
**Acceptance Criteria:**
- HR can review all candidate information on single screen
- One-click selection/rejection with mandatory justification
- Automatic candidate notification of decision
- Complete audit log of who, what, when, why

#### BR-F-006: Background Verification Tracking
**Business Need:** Monitor BG verification status and prevent delays
**Requirement:** System must track background verification status with alerts
**Business Value:** Reduced BG processing time, proactive delay management, audit trail
**Priority:** HIGH
**Acceptance Criteria:**
- BG verification status visible in candidate record
- HR can update status with notes and documents
- Automated alerts for pending verifications > 7 days
- Integration points for future automation

#### BR-F-007: Automated Offer Letter Generation
**Business Need:** Reduce offer letter creation time and eliminate errors
**Requirement:** System must auto-generate offer letters from templates with candidate data
**Business Value:** 90% time reduction (from 30 min to 3 min), elimination of data entry errors
**Priority:** HIGH
**Acceptance Criteria:**
- Offer letter generated from template in < 1 minute
- All candidate data auto-populated
- PDF generated and emailed automatically
- Offer acceptance tracking via online link

#### BR-F-008: Onboarding Data Collection
**Business Need:** Collect onboarding information before first day to reduce administrative time
**Requirement:** System must enable pre-joining data collection (bank details, emergency contacts, etc.)
**Business Value:** 60% reduction in first-day admin time, better new hire experience
**Priority:** MEDIUM
**Acceptance Criteria:**
- Form sent to candidate after offer acceptance
- Data collected before joining day
- Data exportable to HRMS
- Onboarding checklist tracking

#### BR-F-009: Recruitment Analytics Dashboard
**Business Need:** Enable data-driven recruitment optimization
**Requirement:** System must provide real-time analytics dashboard for HR and management
**Business Value:** Visibility into recruitment effectiveness, proactive bottleneck management
**Priority:** HIGH
**Acceptance Criteria:**
- Real-time pipeline visibility (candidates at each stage)
- Time-to-hire tracking and trending
- Source effectiveness analysis
- Interview quality metrics
- Exportable reports for monthly reviews

#### BR-F-010: Multilingual Support
**Business Need:** Serve diverse candidate base across different regions
**Requirement:** System must support English, Hindi, and Bengali for candidate-facing interfaces
**Business Value:** Improved candidate experience, wider candidate reach, reduced support calls
**Priority:** MEDIUM
**Acceptance Criteria:**
- Language selection option on all candidate forms
- Professional translations (not machine-translated)
- Consistent terminology across languages
- Email/WhatsApp templates in all languages

### 4.2 Non-Functional Business Requirements

#### BR-NF-001: System Availability
**Business Need:** System accessible during business hours for uninterrupted operations
**Requirement:** 99.5% uptime during business hours (9 AM - 6 PM IST, Mon-Fri)
**Business Value:** No disruption to recruitment activities, candidate satisfaction
**Priority:** HIGH

#### BR-NF-002: Performance
**Business Need:** Fast response times to maintain user productivity
**Requirement:** 
- Page load times < 3 seconds
- Form submissions process in < 2 seconds
- Support 100 concurrent users without degradation
**Business Value:** User satisfaction, productivity maintenance
**Priority:** MEDIUM

#### BR-NF-003: Data Security
**Business Need:** Protect sensitive candidate personal information
**Requirement:** 
- Encryption of data in transit and at rest
- Role-based access controls
- Complete audit logging
**Business Value:** Regulatory compliance, risk mitigation, candidate trust
**Priority:** CRITICAL

#### BR-NF-004: Scalability
**Business Need:** Support business growth without system limitations
**Requirement:** System must handle 3,000+ applications monthly without performance degradation
**Business Value:** Business growth enablement, future-proofing
**Priority:** MEDIUM

#### BR-NF-005: User-Friendliness
**Business Need:** Minimize training requirements and maximize adoption
**Requirement:**
- Intuitive interfaces requiring minimal training
- 90% of candidates complete forms without assistance
- HR personnel productive after 1-hour training
**Business Value:** Rapid adoption, reduced training costs, user satisfaction
**Priority:** HIGH

#### BR-NF-006: Mobile Accessibility
**Business Need:** Serve mobile-first candidate population
**Requirement:** All candidate-facing interfaces must be fully functional on mobile devices
**Business Value:** Candidate convenience, higher completion rates
**Priority:** HIGH

### 4.3 Integration Requirements

#### BR-I-001: HRMS Data Export
**Business Need:** Transfer successful candidate data to Octane HRMS
**Requirement:** System must support CSV/Excel export in Octane-compatible format
**Business Value:** Eliminate double data entry, ensure HRMS data quality
**Priority:** HIGH
**Note:** Phase 1 = manual export; Phase 2 = API integration

#### BR-I-002: WhatsApp Integration
**Business Need:** Leverage existing candidate communication channel
**Requirement:** System must send notifications via WhatsApp Business API
**Business Value:** High message open rates (95%+), candidate preference alignment
**Priority:** HIGH

#### BR-I-003: Email Integration
**Business Need:** Formal communication channel for official correspondence
**Requirement:** System must send emails for offer letters and formal notifications
**Business Value:** Professional communication, documentation trail
**Priority:** HIGH

### 4.4 Compliance and Regulatory Requirements

#### BR-C-001: Data Privacy
**Business Need:** Comply with Indian data protection laws
**Requirement:** 
- Obtain explicit candidate consent for data collection
- Provide privacy policy accessible from all candidate interfaces
- Enable candidate data access and correction rights
**Business Value:** Legal compliance, risk mitigation, candidate trust
**Priority:** CRITICAL

#### BR-C-002: Audit Trail
**Business Need:** Maintain complete record of all recruitment activities for compliance
**Requirement:** System must log all user actions with timestamp, user ID, and details
**Business Value:** Compliance assurance, legal defense capability, process transparency
**Priority:** CRITICAL

#### BR-C-003: Data Retention
**Business Need:** Comply with legal data retention requirements
**Requirement:**
- Retain successful candidate data for employment period + 7 years
- Retain rejected candidate data for 1 year minimum
- Provide data deletion capability post-retention period
**Business Value:** Legal compliance, risk mitigation
**Priority:** HIGH

---

## 5. Stakeholder Analysis

### 5.1 Stakeholder Identification

| Stakeholder Group | Key Representatives | Interest Level | Influence Level | Engagement Strategy |
|-------------------|--------------------|--------------------|-----------------|---------------------|
| **Executive Sponsor** | Managing Director | High | Very High | Monthly steering committee, decision escalation |
| **Primary Beneficiaries** | Head of HR, HR Team | Very High | High | Weekly meetings, daily communication, UAT participation |
| **Secondary Beneficiaries** | Hiring Managers | Medium | Medium | Monthly updates, feedback sessions |
| **End Users - Candidates** | Job Applicants | High | Low | User testing, feedback surveys |
| **End Users - Interview Panels** | Department Heads, Senior Staff | Medium | Medium | Training sessions, feedback collection |
| **Technology Team** | CTO, IT Team | Medium | High | Weekly sync, technical decision collaboration |
| **Finance** | CFO, Finance Controller | Medium | High | ROI reviews, budget approvals |
| **Compliance/Legal** | Compliance Officer | Medium | Medium | Quarterly compliance reviews |

### 5.2 Stakeholder Needs and Expectations

**HR Team:**
- **Primary Need:** Reduce time spent on manual administrative tasks
- **Key Expectations:**
  - Intuitive, easy-to-use interface
  - Significant time savings (75% reduction in admin work)
  - Reliable system with minimal downtime
  - Comprehensive training and support
- **Success Metric:** Reduction in admin time from 24 hours/week to 6 hours/week per HR person

**Hiring Managers:**
- **Primary Need:** Faster access to qualified candidates
- **Key Expectations:**
  - Real-time visibility into recruitment pipeline for their positions
  - Faster time-to-hire (from 45 days to < 25 days)
  - Better quality candidates through improved screening
  - Easy access to candidate evaluation data
- **Success Metric:** Reduction in vacancy days by 40%

**Management:**
- **Primary Need:** Data-driven insights and strategic control
- **Key Expectations:**
  - Real-time dashboard access to recruitment metrics
  - Ability to identify bottlenecks and optimization opportunities
  - Strong ROI and cost savings
  - Compliance assurance
- **Success Metric:** Monthly analytics reviews leading to process improvements

**Job Candidates:**
- **Primary Need:** Transparent and efficient recruitment experience
- **Key Expectations:**
  - Easy-to-complete application forms
  - Timely communication and status updates
  - Professional interview experience
  - Minimal repetitive data entry
- **Success Metric:** 80%+ candidate satisfaction score

**IT Team:**
- **Primary Need:** Maintainable, secure, and stable system
- **Key Expectations:**
  - Well-documented architecture and code
  - Manageable operational workload
  - Security best practices implemented
  - Clear escalation procedures
- **Success Metric:** < 2 hours MTTR for critical issues

### 5.3 Change Management Considerations

**Key Change Impacts:**

1. **HR Team - High Impact**
   - Transition from familiar Excel/WhatsApp to new digital system
   - New workflows and procedures
   - Initial learning curve
   - **Mitigation:** Comprehensive training, phased rollout, super-user designation

2. **Hiring Managers - Medium Impact**
   - New interview evaluation process
   - Dashboard access for pipeline visibility
   - **Mitigation:** Simple interface design, quick training sessions

3. **Interview Panels - Low to Medium Impact**
   - Digital evaluation forms instead of verbal feedback
   - **Mitigation:** User-friendly forms, training during first use

4. **Candidates - Low Impact (Positive)**
   - Better experience through improved process
   - Digital forms instead of paper
   - **Mitigation:** Minimal, primarily ensure mobile-friendly design

**Change Readiness Assessment:**
- **Executive Support:** Strong (MD and HR Head championing)
- **HR Team Readiness:** Medium (some resistance expected, but generally positive)
- **Technology Readiness:** High (IT team has bandwidth and expertise)
- **Resource Availability:** Adequate (budget approved, team allocated)

**Change Management Plan:**
- **Pre-Launch:** Stakeholder communication campaign, benefit articulation
- **Launch:** Pilot with limited user group, gather feedback, refine
- **Post-Launch:** Regular feedback sessions, continuous improvement, success celebration

---

## 6. Scope Definition

### 6.1 In-Scope (Phase 1)

**Module 1: Candidate Registration (Form-1)**
- Web-based registration form
- Mobile-responsive design
- Multilingual support (English, Hindi, Bengali)
- Automatic WhatsApp link distribution
- Data validation and storage
- Duplicate checking (mobile number)

**Module 2: Interview Scheduling**
- HR interface for scheduling interviews
- Date, time, venue, panel member assignment
- QR code generation for each interview
- Automated WhatsApp/Email notifications with QR code
- Interview reminders (24 hours before)
- Rescheduling capability (max 2 times)

**Module 3: QR-Based Check-in**
- QR code scanning at interview venue
- Candidate type detection (screened vs. walk-in)
- Dual path routing:
  - Screened candidates → Form-2 only
  - Walk-in candidates → Form-1 + Form-2 sequentially
- Check-in metadata logging (time, device, IP, location)

**Module 4: Form-2 Submission**
- Qualifications and experience capture
- Skills and competencies
- Document upload (Aadhaar, PAN, certificates, photo)
- File validation and secure storage

**Module 5: Interview Evaluation (Form-3)**
- Panel member authentication
- Structured evaluation form with rating scales
- Text areas for detailed remarks
- Automatic score calculation
- Multi-panel aggregation
- Form locking after submission

**Module 6: Selection and BG Verification**
- Selection decision interface for HR
- Rejection workflow with notifications
- Background verification status tracking
- BG cleared/failed workflows
- Complete audit trail

**Module 7: Offer Management**
- Offer letter template management
- Automatic data population
- PDF generation with company branding
- Email delivery
- Online offer acceptance/rejection
- Offer expiry tracking

**Module 8: Onboarding (Form-4)**
- Induction date communication
- Induction day QR check-in
- Bank account details collection
- Emergency contact capture
- Employee preferences
- Onboarding checklist tracking
- Onboarding completion confirmation

**Module 9: Data Export to HRMS**
- CSV/Excel export generation
- Field mapping to Octane HRMS format
- Bulk document export (ZIP)
- Export history logging

**Module 10: Analytics and Reporting**
- Recruitment funnel dashboard
- Time-to-hire metrics
- Interview quality analytics
- Source effectiveness reports
- Custom report builder
- Report exports (PDF, Excel, CSV)

**Module 11: Security and Administration**
- User authentication (JWT-based)
- Role-based access control (6 user roles)
- Audit logging (all actions)
- Data encryption (at rest and in transit)
- User management interface
- System configuration

**Infrastructure and Integrations:**
- Azure VM deployment (Docker containerized)
- Supabase PostgreSQL database
- Supabase Blob Storage for documents
- n8n workflow automation
- WhatsApp Business API integration
- Email SMTP integration

### 6.2 Out-of-Scope (Phase 1)

**Deferred to Phase 2 (6-12 months):**
1. **Automated Background Verification** - Third-party API integration for automated BG checks
2. **Direct HRMS API Integration** - Real-time sync with Octane (Phase 1 = manual export)
3. **Two-Factor Authentication (2FA)** - Enhanced security for user logins
4. **Offline Mode** - QR check-in functionality without internet connection
5. **High Availability Setup** - Load balancing and redundant servers
6. **Advanced Analytics** - Predictive hiring models using AI/ML

**Deferred to Phase 3 (12-18 months):**
1. **Video Interview Platform** - Integrated video conferencing for remote interviews
2. **Native Mobile Apps** - iOS and Android apps (Phase 1 = mobile web)
3. **Full ATS Features** - Job posting management, candidate sourcing tools
4. **Calendar Integration** - Sync with Outlook/Google Calendar

**Explicitly Out-of-Scope:**
1. **Payroll Integration** - Remains separate HRMS function
2. **Performance Management** - Separate system for employee performance
3. **Learning Management** - Employee training and development separate
4. **Existing Data Migration** - Historical data not migrated (clean start)

### 6.3 Boundaries and Interfaces

**System Boundaries:**
- **Starts:** CV submission via WhatsApp (system sends Form-1 link)
- **Ends:** Data exported to Octane HRMS and onboarding complete
- **Handles:** Everything between initial contact and HRMS handoff

**External System Interfaces:**
- **WhatsApp Business API:** Outbound notifications only (no inbound message processing)
- **Email (SMTP):** Outbound emails only
- **Octane HRMS:** One-way data export (CSV file), no API integration in Phase 1
- **Supabase:** Fully managed database and storage (no self-hosting)

**Organizational Boundaries:**
- **Users:** SFSPL employees and job applicants only
- **Geography:** India only (data residency compliance)
- **Departments:** HR department is primary user; hiring managers are secondary

---

## 7. Success Criteria and KPIs

### 7.1 Critical Success Factors

**CSF-1: User Adoption**
- **Criterion:** 95% of HR team actively using system for all recruitment activities within 1 month of go-live
- **Measurement:** System usage logs, manual process observation
- **Importance:** Without adoption, benefits cannot be realized

**CSF-2: Data Quality**
- **Criterion:** 100% of candidate records have all mandatory fields completed
- **Measurement:** Database completeness reports
- **Importance:** Foundation for all downstream benefits (analytics, HRMS quality, etc.)

**CSF-3: Time-to-Hire Reduction**
- **Criterion:** Average time-to-hire reduces from 45 days to 25 days within 6 months
- **Measurement:** System-tracked time from CV submission to offer acceptance
- **Importance:** Primary efficiency metric and business value driver

**CSF-4: HR Productivity Improvement**
- **Criterion:** HR admin time reduces from 60% to 20% of total work hours
- **Measurement:** Time tracking survey (monthly)
- **Importance:** Frees HR for strategic work, core project objective

**CSF-5: System Stability**
- **Criterion:** 99.5% uptime during business hours, MTTR < 2 hours for critical issues
- **Measurement:** Uptime monitoring, incident logs
- **Importance:** Reliability is essential for mission-critical recruitment process

### 7.2 Key Performance Indicators (KPIs)

#### Efficiency KPIs

| KPI | Baseline | Target (6 mo) | Target (12 mo) | Measurement Frequency |
|-----|----------|---------------|----------------|----------------------|
| **Average Time-to-Hire** | 45 days | 25 days | 22 days | Weekly |
| **HR Admin Time %** | 60% | 25% | 20% | Monthly |
| **Interview Scheduling Time** | 20 min | 3 min | 2 min | Per transaction |
| **Offer Letter Creation Time** | 35 min | 5 min | 3 min | Per transaction |
| **First-Day Admin Time** | 4 hours | 2 hours | 1.5 hours | Per new hire |

#### Quality KPIs

| KPI | Baseline | Target (6 mo) | Target (12 mo) | Measurement Frequency |
|-----|----------|---------------|----------------|----------------------|
| **Data Completeness** | 65% | 95% | 100% | Weekly |
| **Candidate Satisfaction** | N/A | 75% | 80% | Quarterly |
| **Offer Acceptance Rate** | 65% | 75% | 80% | Monthly |
| **90-Day New Hire Retention** | 82% | 88% | 90% | Quarterly |
| **Interview Quality Score** | N/A | 3.5/5 | 4.0/5 | Monthly |

#### Process KPIs

| KPI | Baseline | Target (6 mo) | Target (12 mo) | Measurement Frequency |
|-----|----------|---------------|----------------|----------------------|
| **Process Compliance %** | 40% | 95% | 100% | Weekly |
| **No-Show Rate** | 25% | 12% | 10% | Weekly |
| **Candidate Dropout Rate** | 35% | 20% | 15% | Monthly |
| **CV-to-Interview Ratio** | 3.5:1 | 3.0:1 | 2.5:1 | Monthly |
| **Interview-to-Hire Ratio** | 5:1 | 4:1 | 3.5:1 | Monthly |

#### Financial KPIs

| KPI | Baseline | Target (6 mo) | Target (12 mo) | Measurement Frequency |
|-----|----------|---------------|----------------|----------------------|
| **Cost-per-Hire** | ₹15,000 | ₹12,000 | ₹10,500 | Quarterly |
| **HR Cost as % of Total Hiring Cost** | 45% | 35% | 30% | Quarterly |
| **ROI** | N/A | 50% | 120% | Quarterly |

#### System KPIs

| KPI | Baseline | Target (6 mo) | Target (12 mo) | Measurement Frequency |
|-----|----------|---------------|----------------|----------------------|
| **System Uptime** | N/A | 99.5% | 99.5% | Weekly |
| **Average Response Time** | N/A | < 2 sec | < 1.5 sec | Daily |
| **User Satisfaction** | N/A | 4.0/5 | 4.3/5 | Quarterly |
| **Support Tickets per Week** | N/A | < 5 | < 3 | Weekly |

### 7.3 Success Milestones

**Month 1 (Implementation Phase):**
- ✅ All HR team members trained
- ✅ 50% of new candidates processed through system
- ✅ System uptime > 95%

**Month 2 (Ramp-up Phase):**
- ✅ 100% of new candidates processed through system
- ✅ Zero use of old Excel/WhatsApp process
- ✅ Data completeness > 90%

**Month 3 (Stabilization Phase):**
- ✅ System uptime > 99%
- ✅ All KPIs being tracked and reported
- ✅ First analytics-driven process improvement implemented

**Month 6 (Optimization Phase):**
- ✅ Time-to-hire reduced to < 25 days
- ✅ HR admin time reduced to < 25%
- ✅ Candidate satisfaction > 75%
- ✅ ROI > 50%

**Month 12 (Maturity Phase):**
- ✅ All target KPIs achieved
- ✅ ROI > 100%
- ✅ Phase 2 planning initiated based on lessons learned

---

## 8. Cost-Benefit Analysis

### 8.1 Cost Breakdown

#### One-Time Costs

| Category | Description | Cost (INR) | Notes |
|----------|-------------|------------|-------|
| **Software Development** | | | |
| - System Design | Architecture, UI/UX design | 1,50,000 | 2 weeks |
| - Backend Development | FastAPI, database, APIs | 3,50,000 | 6 weeks |
| - Frontend Development | Streamlit interfaces | 2,50,000 | 4 weeks |
| - Integration | WhatsApp, Email, Supabase | 1,00,000 | 2 weeks |
| - Testing & QA | UAT, bug fixes | 1,50,000 | 3 weeks |
| **Project Management** | | 1,00,000 | 3 months |
| **Training & Change Mgmt** | | 1,00,000 | |
| **Total Development** | | **11,00,000** | |
| **Contingency (10%)** | | 1,10,000 | |
| **TOTAL ONE-TIME** | | **12,10,000** | |

#### Recurring Annual Costs

| Category | Description | Annual Cost (INR) | Monthly Cost (INR) |
|----------|-------------|-------------------|-------------------|
| **Infrastructure** | | | |
| - Azure VM | 4 CPU, 16GB RAM | 1,80,000 | 15,000 |
| - Supabase | Database + Storage | 60,000 | 5,000 |
| **Services** | | | |
| - WhatsApp Business API | ~1,500 candidates/mo | 36,000 | 3,000 |
| - Email Service | SMTP | 12,000 | 1,000 |
| **Support & Maintenance** | | | |
| - System Administration | Part-time | 60,000 | 5,000 |
| - Bug Fixes & Updates | As needed | 48,000 | 4,000 |
| **Licenses & Tools** | | | |
| - n8n (self-hosted) | Free | 0 | 0 |
| - Monitoring Tools | | 12,000 | 1,000 |
| **TOTAL ANNUAL (Year 2+)** | | **4,08,000** | **34,000** |

**First Year Total Cost:**
- Development: ₹12,10,000
- Operations (assuming 9 months live): ₹3,06,000
- **Total Year 1: ₹15,16,000**

**Subsequent Years:**
- **Annual Operating Cost: ₹4,08,000**

### 8.2 Benefit Quantification

#### Direct Cost Savings (Annual)

| Benefit Category | Calculation | Annual Savings (INR) |
|------------------|-------------|---------------------|
| **HR Staff Time Savings** | | |
| - 3 HR staff | 1,800 hrs/yr savings each @ ₹500/hr | 27,00,000 |
| - Partial redeployment | -40% (still need HR oversight) | -10,80,000 |
| **Net HR Labor Savings** | | **16,20,000** |
| **Reduced External Costs** | | |
| - WhatsApp data charges | Eliminate personal phone usage | 36,000 |
| - Printing & Stationery | Paperless operations | 60,000 |
| - Courier & Postage | Digital offer letters | 48,000 |
| **Reduced Time-to-Fill Costs** | | |
| - Vacancy costs | 23 days savings × 200 hires × ₹2,000/day | 92,00,000 |
| - Temp staffing reduction | Lower temporary staffing needs | 3,00,000 |
| **Reduced Cost-per-Hire** | | |
| - Efficiency gains | ₹4,500 savings × 2,400 hires | 108,00,000 |
| **Total Direct Annual Savings** | | **220,64,000** |

*Note: Cost-per-hire includes allocated HR time, so there's overlap. Conservative estimate focuses on HR time savings and vacancy cost reduction.*

**Conservative Annual Savings (avoiding double-counting): ₹25,00,000**

#### Indirect Benefits (Not Quantified)

| Benefit | Description | Value |
|---------|-------------|-------|
| **Improved Candidate Quality** | Better screening and evaluation leads to higher quality hires | High |
| **Enhanced Employer Brand** | Superior candidate experience improves reputation | Medium |
| **Compliance Assurance** | Complete audit trail reduces legal/regulatory risk | High |
| **Data-Driven Optimization** | Analytics enable continuous process improvement | Medium |
| **Scalability** | Support 2x growth without proportional resource increase | High |
| **Strategic HR Focus** | HR team freed for talent strategy vs. admin | High |
| **Reduced New Hire Turnover** | Better hiring decisions → better retention | Medium |

### 8.3 Return on Investment (ROI) Analysis

**3-Year Financial Projection:**

| Year | Investment (INR) | Savings (INR) | Net Benefit (INR) | Cumulative Net (INR) |
|------|------------------|---------------|-------------------|----------------------|
| **Year 0** | -12,10,000 | 0 | -12,10,000 | -12,10,000 |
| **Year 1** | -3,06,000 | +18,75,000 | +15,69,000 | +3,59,000 |
| **Year 2** | -4,08,000 | +25,00,000 | +20,92,000 | +24,51,000 |
| **Year 3** | -4,08,000 | +25,00,000 | +20,92,000 | +45,43,000 |

**ROI Metrics:**
- **Payback Period:** 10 months (within Year 1)
- **3-Year ROI:** 225% (₹45.43L return on ₹20.24L total investment)
- **Annual ROI (steady state):** 512% (₹20.92L annual benefit on ₹4.08L annual cost)

**Sensitivity Analysis:**

| Scenario | Assumption | 3-Year Net Benefit |
|----------|-----------|-------------------|
| **Best Case** | 30% higher savings | ₹59 lakhs |
| **Base Case** | As projected | ₹45 lakhs |
| **Conservative** | 30% lower savings | ₹32 lakhs |
| **Worst Case** | 50% lower savings | ₹22 lakhs |

**Even in worst-case scenario, project delivers positive ROI within 2 years.**

### 8.4 Intangible Benefits

**Strategic Value:**
1. **Foundation for HR Digital Transformation:** First major HR technology initiative, sets precedent
2. **Competitive Advantage:** Superior recruitment process differentiates SFSPL as employer of choice
3. **Organizational Learning:** Builds internal digital capability and change management muscle
4. **Data Asset Creation:** Builds valuable dataset for future predictive analytics

**Risk Mitigation:**
1. **Compliance Risk Reduction:** Complete audit trail protects against legal challenges
2. **Reputation Risk Mitigation:** Professional process reduces negative candidate feedback
3. **Business Continuity:** Reduces dependence on key individuals (knowledge in system)

---

## 9. Risk Assessment

### 9.1 Project Risks

| Risk ID | Risk Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|------------------|-------------|--------|---------------------|-------|
| **R-001** | **User Adoption Resistance** - HR team resists change, continues using Excel/WhatsApp | Medium | High | - Involve HR in design phase<br>- Comprehensive training<br>- Executive sponsorship<br>- Quick wins demonstration | Project Manager |
| **R-002** | **Technical Complexity Underestimation** - Development takes longer than planned | Medium | Medium | - Experienced development team<br>- Agile sprints with regular reviews<br>- 10% contingency buffer<br>- Clear scope management | Technical Lead |
| **R-003** | **Candidate Device Compatibility** - Candidates unable to scan QR or access forms on devices | Low | Medium | - Extensive mobile testing<br>- Manual backup process<br>- HR assistance at venue<br>- Clear instructions | Development Team |
| **R-004** | **Third-Party Service Failures** - WhatsApp API, Supabase outages | Low | High | - Email backup for WhatsApp<br>- Monitor service status<br>- Escalation procedures<br>- Local caching where possible | System Admin |
| **R-005** | **Data Migration Issues** - Problems exporting data to Octane HRMS | Low | Medium | - Early testing of export format<br>- Octane team collaboration<br>- Manual reconciliation process<br>- Dry runs before go-live | HR Lead |
| **R-006** | **Security Breach** - Unauthorized access to candidate data | Low | Critical | - Security best practices<br>- Regular security audits<br>- Penetration testing<br>- Incident response plan | CTO |
| **R-007** | **Budget Overrun** - Costs exceed approved budget | Medium | Medium | - Regular budget tracking<br>- Change control process<br>- Prioritized feature list<br>- Phase 2 for non-critical features | Project Manager |
| **R-008** | **Timeline Delays** - Project extends beyond 3-month target | Medium | Medium | - Agile methodology<br>- MVP approach<br>- Weekly progress reviews<br>- Clear acceptance criteria | Project Manager |
| **R-009** | **Key Resource Unavailability** - Critical team members unavailable | Low | High | - Knowledge documentation<br>- Cross-training<br>- Backup resources identified<br>- Contractor relationships | Project Manager |
| **R-010** | **Regulatory Changes** - New data protection laws impact design | Low | Medium | - Legal consultation<br>- Flexible architecture<br>- Regular compliance reviews | Compliance Officer |

### 9.2 Operational Risks (Post Go-Live)

| Risk ID | Risk Description | Probability | Impact | Mitigation Strategy | Owner |
|---------|------------------|-------------|--------|---------------------|-------|
| **O-001** | **System Downtime During Peak** - System unavailable during high-recruitment period | Low | High | - High availability architecture (Phase 2)<br>- Daily backups<br>- 24-hour support SLA<br>- Communication plan | System Admin |
| **O-002** | **Data Quality Issues** - Incomplete or incorrect data entered | Medium | Medium | - Mandatory field validation<br>- Real-time error checking<br>- Regular data audits<br>- User training reinforcement | HR Manager |
| **O-003** | **Process Compliance Drift** - Users revert to old manual methods | Medium | Medium | - Regular process audits<br>- Management reinforcement<br>- Make system easier than manual<br>- Disable old processes | HR Head |
| **O-004** | **Scalability Issues** - System struggles with growth | Low | High | - Performance monitoring<br>- Capacity planning<br>- Infrastructure scaling plan<br>- Load testing | System Admin |
| **O-005** | **User Turnover** - New HR staff not trained on system | Medium | Low | - Comprehensive documentation<br>- Self-service training materials<br>- Super-user program<br>- Onboarding checklist | HR Manager |

### 9.3 Risk Response Summary

**Risk Tolerance:**
- **Critical Risks:** Zero tolerance - must be mitigated before go-live
- **High Risks:** Acceptable only with robust mitigation in place
- **Medium Risks:** Accept with monitoring and response plans
- **Low Risks:** Accept and monitor

**Monitoring Approach:**
- Monthly risk review during implementation
- Quarterly risk review post go-live
- Real-time monitoring of technical risks (uptime, performance)
- Regular stakeholder feedback on adoption and usage

---

## 10. Project Timeline and Phases

### 10.1 Phase 1: Implementation (Months 0-3)

**Month 1: Requirements and Design**

| Week | Activities | Deliverables |
|------|-----------|--------------|
| **Week 1-2** | - Kickoff meeting<br>- Stakeholder interviews<br>- Requirement validation<br>- Process mapping | - Project charter<br>- Detailed requirements document<br>- Current process map |
| **Week 3-4** | - System architecture design<br>- Database schema design<br>- UI/UX wireframes<br>- Technical stack finalization | - System architecture document<br>- Database design<br>- UI mockups<br>- Development environment setup |

**Month 2: Development**

| Week | Activities | Deliverables |
|------|-----------|--------------|
| **Week 5-6** | - Backend API development (Forms 1-2)<br>- Database implementation<br>- Supabase integration<br>- Authentication module | - Working Forms 1-2 APIs<br>- Database tables<br>- User authentication |
| **Week 7-8** | - Frontend development (Candidate Portal, Form-1, Form-2)<br>- QR code generation<br>- Interview scheduling module<br>- Document upload | - Candidate Portal UI<br>- Interview scheduling interface<br>- QR functionality |

**Month 3: Development Completion & Testing**

| Week | Activities | Deliverables |
|------|-----------|--------------|
| **Week 9-10** | - Form-3 evaluation module<br>- Selection workflow<br>- Offer management<br>- Analytics dashboard | - Complete evaluation workflow<br>- Offer letter generation<br>- Basic analytics |
| **Week 11** | - Integration testing<br>- User acceptance testing (UAT)<br>- Bug fixes<br>- Performance testing | - Test results report<br>- Bug fix log<br>- UAT sign-off |
| **Week 12** | - Training delivery<br>- Production deployment<br>- Go-live preparation<br>- Soft launch | - Trained users<br>- Production environment<br>- Go-live checklist<br>- System live |

### 10.2 Phase 2: Stabilization and Optimization (Months 4-6)

**Month 4-5:**
- Monitor system performance and stability
- Address user feedback and minor enhancements
- Refine processes based on real-world usage
- Complete transition from manual processes
- Begin collecting KPI data

**Month 6:**
- First comprehensive KPI review
- Identify optimization opportunities
- Plan Phase 2 enhancements based on learnings
- Cost-benefit validation
- Celebration of success with stakeholders

### 10.3 Phase 2 Roadmap (Months 7-12)

**Potential Phase 2 Features (Prioritized):**
1. **Automated Background Verification** - API integration with BG check providers
2. **Two-Factor Authentication (2FA)** - Enhanced security
3. **Direct HRMS API Integration** - Real-time sync with Octane
4. **Advanced Analytics** - Predictive models, hiring forecasts
5. **High Availability Setup** - Load balancing, redundancy

**Phase 2 Initiation:** Subject to Phase 1 success and budget approval

### 10.4 Critical Path and Dependencies

**Critical Path:**
1. Requirements Finalization → System Design → Backend Development → Frontend Development → Integration Testing → UAT → Deployment

**Key Dependencies:**
- **Requirement Sign-off:** Must be complete before design starts (Week 2)
- **Supabase Setup:** Must be ready before database implementation (Week 5)
- **UAT Availability:** HR team must be available for UAT (Week 11)
- **Production Environment:** Must be ready 2 weeks before go-live (Week 10)

**Parallel Tracks:**
- Backend and Frontend development can proceed in parallel (Weeks 5-10)
- Training material development can occur during testing phase (Week 11)

---

## 11. Assumptions and Dependencies

### 11.1 Project Assumptions

**Technical Assumptions:**
1. **ASM-001:** Azure VM infrastructure will be available and stable (99.5% uptime)
2. **ASM-002:** Supabase platform will continue to operate without major changes
3. **ASM-003:** WhatsApp Business API will remain accessible and within pricing expectations
4. **ASM-004:** Interview venues will have stable Wi-Fi or 4G connectivity
5. **ASM-005:** Candidates will have access to smartphones with cameras and internet
6. **ASM-006:** Current technology stack (Python, FastAPI, Streamlit) will remain supported

**Business Assumptions:**
1. **ASM-007:** Recruitment volume will remain in range of 1,200-1,800 applications per month
2. **ASM-008:** Current HR team size (3 members) will be maintained
3. **ASM-009:** Octane HRMS will continue to accept CSV imports
4. **ASM-010:** No major changes to recruitment process during implementation
5. **ASM-011:** Management support will remain strong throughout project

**User Assumptions:**
1. **ASM-012:** HR team willing to adopt new system and discontinue manual processes
2. **ASM-013:** Candidates will prefer digital forms over paper
3. **ASM-014:** Interview panel members will complete digital evaluations
4. **ASM-015:** Hiring managers will access dashboards for pipeline visibility

**Regulatory Assumptions:**
1. **ASM-016:** No major data protection regulation changes during implementation
2. **ASM-017:** Current data retention requirements (1-7 years) will remain stable
3. **ASM-018:** WhatsApp usage for business communication remains compliant

### 11.2 Project Dependencies

**External Dependencies:**
1. **DEP-001:** **Supabase** - Database and storage platform availability and performance
   - **Impact if unavailable:** Critical - system cannot function
   - **Mitigation:** Monitor status, have backup/restore procedures

2. **DEP-002:** **n8n Workflow Engine** - Automation platform for WhatsApp/Email
   - **Impact if unavailable:** High - notifications will not be sent
   - **Mitigation:** Self-hosted instance, manual backup process

3. **DEP-003:** **WhatsApp Business API** - Candidate communication channel
   - **Impact if unavailable:** Medium - can fallback to email
   - **Mitigation:** Email as primary backup

4. **DEP-004:** **Email Service Provider (SMTP)** - Email delivery
   - **Impact if unavailable:** High - cannot send offers or formal communications
   - **Mitigation:** Secondary SMTP provider configuration

5. **DEP-005:** **Azure Cloud Platform** - Infrastructure hosting
   - **Impact if unavailable:** Critical - system cannot be accessed
   - **Mitigation:** Daily backups, disaster recovery plan

6. **DEP-006:** **Octane HRMS** - Target system for data export
   - **Impact if unavailable:** Low - export can be queued
   - **Mitigation:** Store export files for later import

**Internal Dependencies:**
1. **DEP-007:** **HR Team Availability** - For requirements, UAT, and training
   - **Impact if unavailable:** High - cannot validate system meets needs
   - **Mitigation:** Schedule well in advance, executive mandate for participation

2. **DEP-008:** **IT Team Support** - For infrastructure setup and support
   - **Impact if unavailable:** High - deployment and operations impacted
   - **Mitigation:** External contractor backup identified

3. **DEP-009:** **Budget Approval** - Timely release of funds
   - **Impact if unavailable:** Critical - project cannot proceed
   - **Mitigation:** Secure approval before project kickoff

4. **DEP-010:** **Executive Sponsorship** - MD and HR Head active support
   - **Impact if unavailable:** High - change management will fail
   - **Mitigation:** Regular executive briefings, clear escalation path

**Vendor Dependencies:**
1. **DEP-011:** **Development Team** - Availability and performance of development resources
   - **Impact if unavailable:** Critical - project cannot be delivered
   - **Mitigation:** Contractual SLAs, backup contractor relationships

### 11.3 Constraints

**Budget Constraints:**
- Total approved budget: ₹16,00,000 for Year 1
- Must stay within +/- 10% of budget
- No additional funds available for Phase 1

**Timeline Constraints:**
- Hard deadline: 3 months from project kickoff
- No flexibility due to recruitment cycle planning
- UAT must complete in Week 11 (HR team availability)

**Resource Constraints:**
- HR team can allocate max 10 hours/week during development
- IT team has 1 person part-time (20 hours/week)
- Development team: 3-4 developers maximum (budget)

**Technical Constraints:**
- Must use existing Azure subscription
- Must be compatible with Octane HRMS CSV format
- Cannot modify Octane system (no API available Phase 1)
- Must run on Ubuntu 24 (company standard)

**Operational Constraints:**
- System must be fully operational by Month 4 (no soft launch extension)
- Cannot disrupt ongoing recruitment during implementation
- Must support 1,500 applications/month from day 1
- Zero data loss acceptable - must have rollback plan

---

## 12. Appendices

### 12.1 Appendix A: Glossary of Terms

| Term | Definition |
|------|------------|
| **Background Verification (BG)** | Process of verifying candidate's credentials, employment history, and criminal record |
| **Cost-per-Hire** | Total recruitment costs divided by number of hires |
| **Form-1** | Initial candidate registration form (basic personal details) |
| **Form-2** | Detailed qualifications, experience, and document upload form |
| **Form-3** | Interview evaluation form completed by interview panel |
| **Form-4** | Final onboarding form (bank details, emergency contacts) |
| **KPI** | Key Performance Indicator - metric to measure success |
| **MTTR** | Mean Time To Repair - average time to fix an issue |
| **Octane** | HRMS (Human Resource Management System) used by SFSPL |
| **QR Code** | Quick Response code - 2D barcode scannable by mobile devices |
| **ROI** | Return on Investment - financial return relative to investment |
| **Screened Candidate** | Candidate who submitted Form-1 before interview date |
| **Time-to-Hire** | Days from CV submission to offer acceptance |
| **UAT** | User Acceptance Testing - testing by end users before go-live |
| **Walk-in Candidate** | Candidate appearing at interview without prior Form-1 submission |

### 12.2 Appendix B: References

1. SFSPL HR Policy Manual (Internal Document)
2. Octane HRMS Data Import Specifications
3. Indian IT Act 2000 - Data Protection Provisions
4. Industry Benchmarks - Recruitment Metrics (SHRM, LinkedIn Talent Solutions)
5. HR Onboarding Agent - High Level Design Document v2.1 (Dec 2025)
6. HR Onboarding Agent - Software Requirements Specification v1.0 (Jan 2026)

### 12.3 Appendix C: Stakeholder Contact Information

| Role | Name | Email | Phone |
|------|------|-------|-------|
| **Executive Sponsor** | [MD Name] | [email] | [phone] |
| **Project Sponsor** | [HR Head Name] | [email] | [phone] |
| **Project Manager** | Md Sahil | [email] | [phone] |
| **Technical Lead** | [Name] | [email] | [phone] |
| **HR Team Lead** | [Name] | [email] | [phone] |

### 12.4 Appendix D: Change Log

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| 2026-01-09 | 1.0 | Md Sahil | Initial BRD document creation |

### 12.5 Appendix E: Approval History

*To be completed upon stakeholder review and approval*

---

## Document Review and Approval

### Review Cycle

| Review Round | Start Date | End Date | Status |
|--------------|-----------|----------|---------|
| **Draft Review** | 2026-01-09 | 2026-01-13 | In Progress |
| **Stakeholder Comments** | 2026-01-14 | 2026-01-18 | Pending |
| **Final Review** | 2026-01-20 | 2026-01-22 | Pending |
| **Approval** | 2026-01-23 | 2026-01-23 | Pending |

### Approval Sign-Off

**By signing below, I acknowledge that I have reviewed this Business Requirements Document and:**
1. Understand the project scope, objectives, and expected outcomes
2. Agree with the cost estimates and benefit projections
3. Commit to providing necessary resources and support
4. Approve proceeding with project implementation as described

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Executive Sponsor (MD)** | | | |
| **Project Sponsor (Head of HR)** | | | |
| **Chief Technology Officer** | | | |
| **Finance Controller** | | | |
| **Project Manager** | Md Sahil | | 2026-01-09 |

---

**Document Status:** DRAFT - Pending Executive Review and Approval

**Next Action:** Circulate to Executive Sponsor and key stakeholders for review

**Approval Deadline:** January 23, 2026

**Project Kickoff (Conditional):** January 27, 2026 (upon approval)

---

## Important Notes for Reviewers

1. **Investment Decision:** This document requests approval for ₹16 lakhs investment with projected 3-year ROI of 225%

2. **Timeline Commitment:** 3-month delivery timeline is aggressive but achievable with dedicated resources

3. **Resource Requirements:** Requires HR team availability for UAT (Week 11) - please confirm availability

4. **Change Impact:** Significant change for HR team - executive sponsorship critical for success

5. **Risk Acceptance:** All identified risks have mitigation plans; residual risks within acceptable tolerance

6. **Phase 2 Planning:** Automated BG verification and direct HRMS integration deferred to Phase 2 (6-12 months)

7. **Success Metrics:** KPIs defined and will be tracked monthly; first review at 6-month mark

**For Questions or Clarifications:** Contact Md Sahil, Project Manager

---

**END OF BUSINESS REQUIREMENTS DOCUMENT**

---

*Document Prepared By:* Md Sahil, Project Manager  
*Preparation Date:* January 09, 2026  
*Document Version:* 1.0 (Draft)  
*Next Review Date:* January 13, 2026  
*Classification:* Internal - Management Review
