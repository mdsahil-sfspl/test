# HR Onboarding Agent
## Software Requirements Specification (SRS)

**Document Version:** 2.0 (Cleaned - Code Removed)  
**Created Date:** January 05, 2026  
**Updated Date:** January 09, 2026  
**Organization:** Sampurna Financial Services Pvt. Ltd. (SFSPL)

---

## TABLE OF CONTENTS

1. [Introduction](#1-introduction)
2. [Functional Requirements](#2-functional-requirements)
3. [Non-Functional Requirements](#3-non-functional-requirements)
4. [System Architecture Requirements](#4-system-architecture-requirements)
5. [Data Requirements](#5-data-requirements)
6. [Security & Compliance Requirements](#6-security--compliance-requirements)
7. [Interface Requirements](#7-interface-requirements)
8. [User Roles & Permissions](#8-user-roles--permissions)
9. [Acceptance Criteria](#9-acceptance-criteria)
10. [Delivery Phases](#10-delivery-phases)

---

## 1. INTRODUCTION

### 1.1 PURPOSE

This Software Requirements Specification (SRS) document defines the functional and non-functional requirements for the HR Onboarding Agent system at Sampurna Financial Services Pvt. Ltd. (SFSPL).

**Document Scope:**
- High-level requirements specification (WHAT needs to be built)
- Functional requirements for all system features
- Non-functional quality requirements (performance, security, usability)
- Data specifications
- System-level requirements

**NOT Included in SRS (Belong to separate Design/Implementation Documents):**
- ❌ Source code or code examples
- ❌ Detailed algorithm implementation
- ❌ SQL queries or database triggers
- ❌ UI component code (HTML/CSS/JavaScript)
- ❌ API implementation details beyond specification

**Intended Audience:**
- Business analysts and stakeholders
- Test engineers and QA teams
- System architects (for high-level design)
- Project managers
- Technical leads

### 1.2 SCOPE

**In Scope:**
- Complete candidate lifecycle management (application → offer → onboarding)
- Multi-stage digital forms (Form-1 through Form-4)
- QR-based check-in system for interview venues
- Dual candidate paths (Screened vs Walk-in)
- Interview scheduling and evaluation
- Background verification workflow
- Offer letter generation and management
- Onboarding checklist and task management
- Multi-channel notifications (WhatsApp, Email, SMS)
- Real-time dashboards and analytics
- Document management and KYC
- Audit logging and compliance

**Out of Scope:**
- Full background verification automation (manual process with status tracking)
- Direct auto-sync with Octane HRMS (manual export)
- AI-based candidate ranking
- Video interview platform integration
- Multi-company/multi-tenant support

### 1.3 DOCUMENT STRUCTURE

**Definition Levels:**
- **Requirement ID (FR-1.1):** Unique identifier for traceability
- **Priority:** HIGH, MEDIUM, LOW
- **Description:** One-line summary
- **Functional Specifications:** Detailed WHAT is required
- **Business Rules:** Conditions and constraints
- **Acceptance Criteria:** How to verify the requirement is met

### 1.4 KEY DEFINITIONS

| Term | Definition |
|------|-----------|
| **Candidate** | Person applying for a position at SFSPL |
| **Application** | Candidate's submission for a specific role |
| **Screened Candidate** | Pre-qualified candidate selected by recruiter |
| **Walk-in Candidate** | Candidate applying on-the-spot at interview venue |
| **QR Check-in** | Candidate scans QR code at interview venue |
| **Form-1** | Basic personal and professional details |
| **Form-2** | Address, qualifications, skills, documents |
| **Form-3** | Interview evaluation by interviewers |
| **Form-4** | Onboarding details (bank, emergency contact) |
| **Offer Letter** | Official employment offer document |
| **Onboarding** | Process of integrating new employee into organization |
| **RBAC** | Role-Based Access Control |
| **OTP** | One-Time Password for authentication |

---

## 2. FUNCTIONAL REQUIREMENTS

### 2.1 AUTHENTICATION & AUTHORIZATION (FR-1)

#### FR-1.1: Candidate Authentication via OTP
- **Requirement ID:** FR-1.1
- **Priority:** HIGH
- **Description:** Enable passwordless login for candidates using mobile OTP

**Functional Specifications:**

**Candidate Login Flow:**
1. Candidate navigates to login page
2. Enters 10-digit mobile number (Indian format)
3. System validates phone number format
4. System sends 6-digit OTP via WhatsApp
5. OTP valid for 5 minutes (single-use)
6. Candidate enters OTP on verification screen
7. System validates OTP (max 3 failed attempts)
8. On success: System creates session and redirects to dashboard
9. On failure: Display error message, allow retry (cooldown after 3 failures: 15 minutes)

**Key Requirements:**
- Mobile number format: 10 digits, starts with 6-9
- OTP format: 6 digits, numeric only
- OTP validity: 5 minutes
- Max retry attempts: 3
- Cooldown period: 15 minutes after max failures
- Session duration: 24 hours
- Session timeout: On browser close or manual logout

**Error Handling:**
- Invalid mobile format: "Please enter a valid 10-digit mobile number"
- OTP expired: "OTP has expired. Please request a new one"
- Invalid OTP: "Invalid OTP. {attempts_remaining} attempts remaining"
- Max attempts exceeded: "Too many failed attempts. Please try again after 15 minutes"
- WhatsApp delivery failure: "Unable to send OTP. Please try again"

---

#### FR-1.2: HR Staff Authentication with Email/Password
- **Requirement ID:** FR-1.2
- **Priority:** HIGH
- **Description:** Enable secure login for HR staff using email and password

**Functional Specifications:**

**HR Staff Login Flow:**
1. Staff member navigates to login page
2. Enters email address
3. Enters password
4. System validates credentials against database
5. If MFA enabled: Request 6-digit TOTP code from authenticator app
6. On success: System creates session and redirects to role-specific dashboard
7. On failure: Display error message

**Password Requirements:**
- Minimum 8 characters
- Must contain uppercase letter (A-Z)
- Must contain lowercase letter (a-z)
- Must contain digit (0-9)
- Must contain special character (@$!%*?&)
- Cannot match last 3 passwords
- Must be changed every 90 days
- Password reset link valid for 30 minutes

**Session Management:**
- Session duration: 8 hours
- Idle timeout: 2 hours for regular staff, 30 minutes for HR Manager
- Concurrent session limit: 3 devices maximum
- Automatic logout on idle timeout

**Multi-Factor Authentication (MFA):**
- Method: TOTP (Time-based One-Time Password, RFC 6238)
- QR code provided for secret key setup
- 6-digit code required every login
- Backup codes: 10 single-use codes provided during setup
- Mandatory for: HR Manager role
- Optional for: Other HR staff

**Error Handling:**
- Invalid email format: "Please enter a valid email address"
- Invalid credentials: "Invalid email or password"
- Account locked: "Account locked due to multiple failed attempts. Contact admin"
- MFA code invalid: "Invalid authentication code. Please try again"
- MFA code expired: "Authentication code expired. Please try again"
- Session expired: "Your session has expired. Please login again"

---

#### FR-1.3: Role-Based Access Control (RBAC)
- **Requirement ID:** FR-1.3
- **Priority:** HIGH
- **Description:** Enforce role-based permissions across all system features

**Functional Specifications:**

**System Roles (7 Total):**

1. **Super Admin**
   - System configuration and settings management
   - User provisioning (create, edit, delete users)
   - Complete audit log access
   - Global data access (all candidates, all departments)
   - Role and permission management

2. **HR Manager**
   - Hiring decision approval/rejection
   - Offer letter generation and approval
   - Background verification approval and tracking
   - Onboarding checklist creation and monitoring
   - Dashboard access (all or assigned departments)
   - Report generation and analytics
   - Department-level data visibility

3. **Recruiter**
   - Candidate screening and shortlist/reject decisions
   - Interview scheduling and coordination
   - QR code generation for interviews
   - Candidate communication (email, WhatsApp)
   - Data access: Only assigned candidates
   - Basic reporting

4. **Interviewer**
   - Form-3 (interview evaluation) submission only
   - QR code validation at interview venue
   - View candidate profiles for assigned interviews only
   - No data modification permissions

5. **Background Verifier**
   - Background verification status updates
   - Document collection and verification
   - Data access: Only assigned candidates
   - Background verification report submission
   - No hiring decisions

6. **Compliance Officer**
   - Read-only access to all data
   - Audit log review and export
   - Compliance report generation
   - No data modification permissions

7. **Candidate**
   - View own profile and application status
   - Form submission (Form-1, Form-2, Form-4)
   - Document upload and management (own documents only)
   - Offer acceptance/rejection
   - Cannot view other candidates' data

**Access Control Implementation:**
- Role-based permissions enforced at API level
- Row-level security: Data access restricted by role
- Principle of least privilege: Default deny, explicit allow
- Permission check on every API request
- All access attempts logged in audit trail
- Quarterly access review and certification

**Data Scope by Role:**

| Role | Candidate Data Access | Scope |
|------|----------------------|-------|
| Super Admin | All candidates | Global |
| HR Manager | All or department-specific | Department/Global |
| Recruiter | Assigned candidates | Assigned only |
| Interviewer | Interview-assigned candidates | Interview-specific |
| BG Verifier | Assigned candidates | Assigned only |
| Compliance | All candidates | Global (read-only) |
| Candidate | Own profile only | Self only |

---

### 2.2 CANDIDATE MANAGEMENT (FR-2)

#### FR-2.1: Candidate Registration via WhatsApp
- **Requirement ID:** FR-2.1
- **Priority:** HIGH
- **Description:** Enable candidates to initiate application via WhatsApp bot message

**Functional Specifications:**

**Registration Trigger:**
- Candidate sends any message (e.g., "Hi", "Apply", "Job") to WhatsApp business number
- System receives webhook from WhatsApp Business API
- System extracts phone number from message

**Registration Process:**
1. Extract phone number from WhatsApp message
2. Normalize phone format to +91XXXXXXXXXX
3. Check if phone number exists in candidate database
   - If exists: Retrieve candidate_id, update last_contact_at
   - If new: Create new candidate record
4. Check 30-day cooldown rule:
   - Query for applications from same phone number for same role within last 30 days
   - If found: Send cooldown message with wait date
   - If not found: Send Form-1 link
5. Create candidate_applications record with status "Initiated"
6. Generate Form-1 URL with secure token
7. Send WhatsApp message with Form-1 link and instructions

**30-Day Cooldown Rule:**
- Same candidate cannot apply for same role within 30 days
- Different roles are allowed within 30 days
- Cooldown resets 30 days after initial application
- User receives message: "You have already applied for this role. Please wait until [date]"

**WhatsApp Message Format:**
```
Hi! Thank you for your interest in [Role] at SFSPL.

Please fill out this form to complete your application:
[Form-1 Link]

This should take about 5-7 minutes.

Need help? Reply with "Help"
```

**Acceptance Criteria:**
- Form-1 link successfully sent to valid phone numbers
- Cooldown rule prevents duplicate applications
- WhatsApp delivery confirmed
- Error handling for invalid numbers or API failures

---

#### FR-2.2: Form-1 - Basic Personal & Professional Details
- **Requirement ID:** FR-2.2
- **Priority:** HIGH
- **Description:** Collect candidate's basic information through Form-1

**Functional Specifications:**

**Form-1 Fields:**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Name | Text | Yes | 2-100 chars, letters only |
| Email | Email | Yes | Valid email format |
| Phone Number | Text | Yes | 10 digits, pre-filled from WhatsApp |
| Date of Birth | Date | Yes | Age between 18-65 years |
| Gender | Select | Yes | Male, Female, Other |
| Current Location | Text | Yes | 1-50 chars |
| Current Company | Text | No | Max 100 chars |
| Current Designation | Text | Yes | Max 100 chars |
| Years of Experience | Number | Yes | 0-50 years |
| Desired Role | Select | Yes | Dropdown from roles table |
| Highest Qualification | Select | Yes | 12th, Graduate, Post-Graduate, Doctorate |
| Notice Period | Select | No | Immediate, 15d, 1m, 2m, 3m |

**Eligibility Check (On Form-1 Submission):**

System must validate the following criteria:

1. **Qualification Match:** Candidate's qualification meets role requirement
2. **Experience Range:** Candidate's experience within role requirement (e.g., 2-5 years)
3. **Age Validation:** Candidate age between 18-65 years
4. **30-Day Cooldown:** No application for same role within 30 days

**Eligibility Results:**

**If All Checks Pass:**
- Status updated to "Eligible - Pending Screening"
- Confirmation email sent to candidate
- WhatsApp message sent: "✅ Application received! We'll review and get back within 2-3 days"
- Data stored in database
- Recruiter receives notification to screen

**If Any Check Fails:**
- Status updated to "Rejected - [Reason]"
- Reason displayed to candidate
- Email sent with rejection reason
- WhatsApp message sent: "Thank you for applying. Unfortunately, you don't meet requirements for this role at this time"
- System suggests alternative roles if applicable

**Form Features:**
- Mobile-responsive Streamlit interface
- Progress indicator: "Step 1 of 4"
- Auto-save draft every 30 seconds
- Field-level validation with inline error messages
- Submit button disabled until all required fields valid
- Ability to resume from draft if form incomplete

**User Experience Requirements:**
- Form should load in < 2 seconds
- Each field should validate immediately on blur
- Error messages should be clear and actionable
- Progress should be visible to user
- Draft should survive browser refresh

---

#### FR-2.3: Form-2 - Address, Qualifications & Skills
- **Requirement ID:** FR-2.3
- **Priority:** HIGH
- **Description:** Collect detailed address, education, skills, and supporting documents

**Functional Specifications:**

**When Form-2 is Presented:**
- **For Screened Candidates:** After interview scheduled, before interview (via email/WhatsApp)
- **For Walk-in Candidates:** After QR check-in at interview venue (same day as interview)

**Form-2 Sections:**

**Section 1: Address Details**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Current Address Line 1 | Text | Yes | 1-200 chars |
| Current Address Line 2 | Text | No | 1-200 chars |
| Current City | Text | Yes | 1-50 chars |
| Current State | Select | Yes | Dropdown of Indian states |
| Current Pincode | Text | Yes | Exactly 6 digits |
| Permanent Same as Current | Checkbox | - | If checked, copy current to permanent |
| Permanent Address Line 1 | Text | Conditional | Required if not same as current |
| Permanent Address Line 2 | Text | No | 1-200 chars |
| Permanent City | Text | Conditional | Required if not same as current |
| Permanent State | Select | Conditional | Required if not same as current |
| Permanent Pincode | Text | Conditional | Required if not same as current |

**Section 2: Educational Qualifications** (Multiple entries allowed)

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Degree/Qualification | Select | Yes | 12th, Graduate, Post-Grad, Doctorate |
| Degree Name | Text | Yes | 1-100 chars (e.g., "B.Tech CSE") |
| University/Institute | Text | Yes | 1-100 chars |
| Year of Passing | Number | Yes | 1970 to current year |
| CGPA/Percentage | Number | Yes | 0-100 or 0-10 based on type |
| Grade Type | Select | Yes | Percentage or CGPA |

**Section 3: Skills** (Multiple selections)

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Skill Name | Multi-select | Yes | Predefined skill list |
| Proficiency | Select | Yes | Beginner, Intermediate, Advanced, Expert |

**Predefined Skills:**
- Technical: Python, Java, SQL, AWS, Data Analysis, Excel, etc.
- Soft Skills: Communication, Leadership, Teamwork, Problem-solving, etc.
- Domain: Finance, HR, IT, Operations, etc.

**Section 4: Document Uploads**

| Document Type | Required | File Types | Max Size | Purpose |
|---------------|----------|-----------|----------|---------|
| Resume | Yes | PDF, DOC, DOCX | 5 MB | Employment history |
| Photo | Yes | JPG, PNG | 2 MB | Identity verification |
| Qualification Certificates | Yes | PDF, JPG, PNG | 5 MB each | Education proof |
| Experience Letter | No | PDF, JPG | 5 MB | Employment verification |
| ID Proof | Yes | PDF, JPG, PNG | 2 MB | Identity document |

**Document Upload Requirements:**
- Drag-and-drop interface
- File type validation
- File size validation
- Upload progress bar
- Preview capability
- Multiple file support (for certificates)
- Virus scan (optional, Phase 2)

**Form-2 Business Rules:**
- All required documents must be uploaded before submission
- File formats limited to specified types
- File sizes must not exceed limits
- Pincode must be exactly 6 digits
- Year of passing must be realistic (not future dates)
- Cannot upload duplicates of same document type

**Acceptance Criteria:**
- Form-2 data persists in database
- Document URLs stored with metadata
- Verification status set to "Unverified"
- Candidate receives confirmation email/WhatsApp
- HR can view all collected information

---

#### FR-2.4: Form-4 - Onboarding & Final Details
- **Requirement ID:** FR-2.4
- **Priority:** MEDIUM
- **Description:** Collect final onboarding details post-induction (Form-4)

**Functional Specifications:**

**When Form-4 is Shown:**
- After candidate successfully scans induction QR code on joining day
- One-time submission (final form)
- Must be completed before day-end

**Form-4 Sections:**

**Section 1: Bank Account Details**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Account Number | Text | Yes | 9-18 digits |
| Confirm Account Number | Text | Yes | Must match account number |
| IFSC Code | Text | Yes | 11 chars, format: XXXX0XXXXXX |
| Account Holder Name | Text | Yes | 1-100 chars |
| Bank Name | Text | Yes | 1-100 chars |
| Branch Name | Text | Yes | 1-100 chars |
| Account Type | Select | Yes | Savings or Current |

**Section 2: Emergency Contact**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Contact Person Name | Text | Yes | 1-100 chars |
| Relationship | Select | Yes | Spouse, Parent, Sibling, Friend, Other |
| Phone Number | Text | Yes | 10 digits |
| Address | Text | No | 1-200 chars |

**Section 3: Address Confirmation**

| Field | Type | Required | Purpose |
|-------|------|----------|---------|
| Permanent Address Confirmed | Checkbox | Yes | Confirm address accuracy |
| Address Update (if changed) | Text | No | Update if address changed |

**Section 4: Health Declaration** (Optional)

| Field | Type | Required | Max Length |
|-------|------|----------|-----------|
| Blood Group | Select | No | A+, A-, B+, B-, AB+, AB-, O+, O- |
| Medical Conditions | Text | No | 500 chars |
| Allergies | Text | No | 300 chars |
| Emergency Medical Info | Text | No | 500 chars |

**Section 5: IT Preferences** (Optional)

| Field | Type | Required |
|-------|------|----------|
| Laptop Preference | Select | No (Options: Windows, Mac, Linux) |
| Monitor Preference | Select | No (Options: Single, Dual, Triple) |
| Keyboard/Mouse Type | Select | No (Options: Wired, Wireless) |
| Software Requirements | Text | No (Max 300 chars) |

**Form-4 Requirements:**
- All bank fields must be filled and validated
- Bank account numbers must be confirmed (match check)
- IFSC code must follow Indian standard format
- Emergency contact phone must be valid
- Form cannot be submitted until all required fields completed
- Data must be encrypted before storage (bank details, phone)

**Post-Submission Actions:**
- Update candidate status to "Onboarding Complete"
- Export data to HRMS/Payroll system
- Send congratulatory message to candidate
- Send completion notification to HR Manager
- Generate employment letter (optional)
- Archive candidate record from active pipeline

**Acceptance Criteria:**
- Form-4 data successfully stored in database
- Sensitive fields (bank account, phone) encrypted
- Data exported to HRMS within 1 hour
- Candidate receives confirmation
- Onboarding marked 100% complete

---

#### FR-2.5: Candidate Status Tracking
- **Requirement ID:** FR-2.5
- **Priority:** MEDIUM
- **Description:** Provide real-time status visibility to candidates with timeline view

**Functional Specifications:**

**Status Lifecycle:**

The system must support the following status flow:

1. **Initiated** → 2. **Form-1 Submitted** → 3. **Eligible - Pending Screening** → 4. **Screened (Shortlisted/Rejected)** → 5. **Interview Scheduled** → 6. **Interview Complete - Forms Pending** → 7. **Interview Complete - Evaluation Pending** → 8. **Evaluation Complete - Decision Pending** → 9. **Selected/Rejected** → 10. **BG Verification** → 11. **Offer Sent** → 12. **Offer Accepted/Rejected** → 13. **Onboarding** → 14. **Onboarding Complete**

**Status Display Requirements:**

**Timeline View:**
- Vertical timeline showing all status milestones
- Each milestone displays: Status name, Date/Time, Description
- Completed stages marked with green checkmark
- Current stage highlighted with blue indicator
- Pending stages shown in gray
- Clear visual distinction between stages

**Status Badge:**
- Color-coded badge at top of page
- Green: Success states (Selected, Offer Accepted, Onboarding Complete)
- Blue: In-progress states (Interviews, Evaluation)
- Orange: Pending action needed
- Red: Failure states (Rejected, BG Failed)

**Next Action Indicator:**
- Clear call-to-action based on current status
- Examples:
  - "Upload Documents" (if Form-2 pending)
  - "Wait for Interview Schedule" (if shortlisted)
  - "View Interview Details" (if interview scheduled)
  - "Accept Offer" (if offer sent)
  - "Complete Form-4" (if onboarding started)

**Rejection Display:**
- If status = "Rejected": Show empathetic message
- Display rejection reason (template or custom)
- Suggest alternatives:
  - Apply for different role
  - Reapply after 30 days
  - Provide feedback/appeal option

**Status Refresh:**
- Status refreshes automatically every 30 seconds
- Manual refresh button available
- Timestamp of last update shown
- Network error handling (show cached status with warning)

**Acceptance Criteria:**
- All status changes visible within 30 seconds
- Timeline displays all milestones with dates
- Rejection reasons clearly communicated
- Next action always clear to candidate
- Mobile-responsive display

---

#### FR-2.6: Document Management & Verification
- **Requirement ID:** FR-2.6
- **Priority:** HIGH
- **Description:** Centralized secure document storage with verification tracking

**Functional Specifications:**

**Document Types & Requirements:**

| Document Type | Required | Uploader | Verifier | Retention |
|---------------|----------|----------|----------|-----------|
| Resume | Yes | Candidate | Recruiter | 2 years |
| Photo | Yes | Candidate | Recruiter | 2 years |
| Qualification Certificate | Yes | Candidate | BG Verifier | 2 years |
| Experience Letter | No | Candidate | BG Verifier | 2 years |
| ID Proof | Yes | Candidate | BG Verifier | 2 years |
| Offer Letter Signed | Yes | Candidate | HR Manager | 7 years |
| Onboarding Documents | Varies | Candidate/HR | HR Manager | 7 years |

**Document Upload Process:**

1. User selects document type from dropdown
2. User uploads file (drag-and-drop or file picker)
3. System validates: File type, file size, magic number
4. System generates signed URL for direct upload to storage
5. User uploads file directly to Supabase Storage
6. System stores document metadata (name, URL, size, timestamp)
7. Document status set to "Unverified"
8. Confirmation message displayed to user

**Upload Validations:**
- File type must match allowed types (PDF, DOC, DOCX, JPG, PNG)
- File size must not exceed limits (max 5 MB)
- File must not be corrupted or empty
- Virus scan performed (future enhancement)
- Duplicate document type replaces previous version (with version history)

**Document Verification Process:**

1. HR/BG Officer views document list
2. Clicks "Verify" on document
3. Document preview opens (PDF viewer or image viewer)
4. Officer reviews document content
5. Officer performs one of: Verify, Reject, Request Reupload
6. If Verify: Status changed to "Verified", notes added
7. If Reject: Status changed to "Rejected", reason provided, candidate notified
8. If Reupload Requested: Candidate notified, document marked pending
9. Verification timestamp and officer ID recorded

**Document Version Control:**
- When candidate reuploads same document type, new version created
- Previous versions retained with "Superseded" status
- Version numbering: resume_v1.pdf, resume_v2.pdf
- Access to all versions available to HR/Compliance

**Access Control:**
- Candidate: View/download own documents
- Recruiter: View documents of assigned candidates
- HR Manager: View all documents
- BG Verifier: View assigned candidates' documents
- Compliance Officer: Read-only access to all documents
- Document download requires authentication

**Document Storage Requirements:**
- Location: Supabase Storage (S3-compatible)
- Encryption: AES-256 at rest
- Access: Private (signed URLs for access)
- Folder structure: `/candidate_id/application_id/document_type/filename`
- Automatic backups: Daily
- Virus scanning: Optional, Phase 2

**Auto-Cleanup & Retention:**
- Rejected candidates: Documents archived after 2 years
- Hired employees: Documents retained until 2 years post-exit
- Documents marked for deletion move to archive table
- Complete deletion after 7-year retention
- Audit trail maintained for all document actions

**Acceptance Criteria:**
- All documents securely stored in Supabase
- Document verification workflow functional
- Version history maintained
- Access control enforced
- Automatic cleanup after retention period
- All document actions audited

---

### 2.3 HR SCREENING & SCHEDULING (FR-3)

#### FR-3.1: Candidate Screening Dashboard
- **Requirement ID:** FR-3.1
- **Priority:** HIGH
- **Description:** Enable recruiters to review and make screening decisions on applications

**Functional Specifications:**

**Dashboard Components:**

**1. Application List:**
- Displays all applications in "Form-1 Submitted" or "Eligible" status
- Shows candidates assigned to recruiter
- Sortable columns: Name, Applied Role, Experience, Applied Date, Status
- Filterable by: Role, Experience Level, Location, Applied Date Range, Status
- Pagination: 20 records per page

**2. Candidate Quick View:**
- Name and contact information
- Applied role and experience
- Qualification level
- Current location
- Application date
- Eligibility check result
- Resume download link

**3. Bulk Actions:**
- Select multiple candidates using checkboxes
- Bulk shortlist or reject action
- Bulk download resume zip file
- Confirmation dialog before bulk action

**4. Quick Stats:**
- Total applications (this week)
- Pending review count
- Shortlisted (this week)
- Rejected (this week)

**Screening Decision Actions:**

**For Each Candidate:**

1. **View Profile:** Open full candidate details in modal
   - All Form-1 data
   - Resume preview/download
   - Application date and status
   - Eligibility check results

2. **Shortlist Decision:**
   - Click "Shortlist" button
   - Candidate status changed to "Shortlisted"
   - Interview scheduling form opens
   - Or "Schedule Later" to shortlist without scheduling

3. **Reject Decision:**
   - Click "Reject" button
   - Modal opens with rejection reason dropdown
   - Predefined reasons: Insufficient Experience, Qualification Mismatch, Location Preference Mismatch, Overqualified, Other
   - Optional custom reason text field
   - On confirm: Status changed to "Rejected", automatic rejection email/WhatsApp sent to candidate

**Dashboard Features:**
- Search candidates by name or phone
- Export candidates list to Excel
- Download bulk resumes
- Interview scheduling from dashboard
- Reassign candidates to other recruiters (admin only)
- View candidate history/notes

**Acceptance Criteria:**
- Recruiter can view assigned applications
- Filtering and sorting work correctly
- Shortlist/reject decisions saved immediately
- Rejection notifications sent automatically
- Dashboard loads in < 2 seconds
- Bulk actions execute successfully

---

#### FR-3.2: Interview Scheduling
- **Requirement ID:** FR-3.2
- **Priority:** HIGH
- **Description:** Schedule interviews with date/time, interviewer assignment, and venue details

**Functional Specifications:**

**Interview Scheduling Form:**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| Interview Date | Date | Yes | Future date, not weekend |
| Interview Time | Time | Yes | Business hours 9 AM - 6 PM |
| Interview Duration | Select | Yes | 30min, 45min, 1h, 1.5h |
| Venue Location | Select | Yes | Head Office, Branch 1, Branch 2, etc. |
| Venue Address | Text | Auto-filled | Based on location |
| Room/Cabin Number | Text | No | Conference Room A, Meeting Room 3, etc. |
| Parking Available | Checkbox | - | Tick if parking available |
| Parking Instructions | Text | No | Max 200 chars |
| Reporting Time | Time | Yes | Default: 15 min before interview |
| Primary Interviewer | Select | Yes | Dropdown of available interviewers |
| Secondary Interviewer | Select | No | Optional second interviewer |
| Tertiary Interviewer | Select | No | Optional third interviewer |
| Interview Type | Select | Yes | Technical, HR, Managerial, Panel |
| Internal Notes | Text | No | Max 500 chars (visible to interviewers) |

**Scheduling Business Rules:**

1. **Date Rules:**
   - Interview date must be minimum 2 days from today
   - Maximum 30 days in future
   - No interviews on weekends (Saturday/Sunday)
   - No interviews on company holidays

2. **Time Rules:**
   - Business hours only: 9 AM to 6 PM
   - No overlapping interview times in same venue
   - Minimum 30 minutes between consecutive interviews in same venue

3. **Interviewer Availability:**
   - Max 4 interviews per interviewer per day
   - Check for schedule conflicts
   - Prevent double-booking
   - Show alternative available slots if conflict detected

4. **Venue Capacity:**
   - Check venue availability for selected date/time
   - Show available venues if selected venue unavailable

**Panel Composition Rules:**

| Interview Type | Panel Requirements |
|----------------|-------------------|
| Technical | 1 Technical Expert (required) |
| HR | 1 HR Manager (required) + 1 optional |
| Managerial | Hiring Manager (required) + Senior Manager (optional) |
| Panel | 2-3 members (Tech + HR + Manager) |

**Scheduling Workflow:**

1. Recruiter selects candidate to schedule
2. Opens interview scheduling form with candidate details
3. Fills all required fields
4. System checks interviewer availability in real-time
5. System validates all business rules
6. On submit: Interview record created
7. QR code generated (see FR-4.1)
8. Notifications triggered (see FR-3.2.1)

**Rescheduling:**
- Recruiters can reschedule up to 24 hours before interview
- Same form with prefilled data
- Updates interview record
- Sends reschedule notification to all parties

**Interview Status:**
- **Scheduled:** Interview created and confirmed
- **In Progress:** During interview (after QR check-in)
- **Completed:** Interview finished, evaluation pending
- **Cancelled:** Interview cancelled by HR

**Acceptance Criteria:**
- Interview scheduled with all details
- Interviewer availability validated
- Business rules enforced
- Interview record created in database
- Notifications sent to all parties
- Interviewer conflicts prevented
- Rescheduling works within 24-hour window

---

#### FR-3.2.1: Interview Scheduling Notifications
- **Requirement ID:** FR-3.2.1
- **Priority:** HIGH
- **Description:** Automated notifications sent on interview scheduling

**Functional Specifications:**

**Notification Recipients & Content:**

**1. To Candidate (WhatsApp + Email):**

WhatsApp Content:
- Interview scheduled notification
- Date, Time, Venue Address
- Parking instructions
- Reporting time
- QR code image for check-in
- Documents to bring
- Contact information for queries

Email Content:
- Professional HTML email format
- All details in table format
- QR code embedded as image
- Venue map link (if available)
- Contact information
- Professional signature

**2. To Interviewers (Email):**

Email Content:
- Interview assignment confirmation
- Candidate details (name, experience, current role)
- Interview date, time, venue, room
- Candidate profile link
- Resume link
- Panel member names and roles
- Internal notes from recruiter
- Evaluation form link

**3. Interview Reminders (Auto-scheduled):**

- **24 Hours Before:** WhatsApp + Email reminder to candidate
- **4 Hours Before:** Email reminder to interviewers
- **15 Minutes Before:** SMS reminder to candidate (optional)

**Notification Delivery:**
- Via n8n automation workflows
- WhatsApp Business API for WhatsApp messages
- Email service for emails
- SMS service for SMS (if enabled)
- All notifications logged in database
- Retry mechanism: 3 automatic retries on failure

**Acceptance Criteria:**
- Interview invitation sent to candidate within 5 minutes of scheduling
- Interviewer assignment emails sent to all panel members
- Reminders scheduled and delivered on time
- All notifications logged with delivery status
- Failed notifications queued for retry

---

#### FR-3.3: Interview Panel Management
- **Requirement ID:** FR-3.3
- **Priority:** MEDIUM
- **Description:** Manage interviewer availability, panel composition, and interview load

**Functional Specifications:**

**Interviewer Master Data:**

| Information | Type | Purpose |
|-------------|------|---------|
| Name | Text | Identification |
| Department | Select | Department assignment |
| Expertise/Skills | Multi-select | Technical/domain skills |
| Interview Types | Multi-select | Technical, HR, Managerial |
| Max Interviews/Day | Number | Load balancing (default: 4) |
| Available Days | Multi-select | Mon-Fri by default |
| Status | Select | Active/Inactive |

**Availability Management:**

1. **Regular Availability:**
   - Define available days (Mon-Fri by default)
   - Available time slots (9 AM - 6 PM by default)
   - Max interviews per day (default: 4)

2. **Unavailability Management:**
   - Mark as unavailable for date ranges
   - Reasons: Leave, OOO, Training, etc.
   - System prevents scheduling during unavailable dates

3. **Availability View:**
   - Calendar showing available/unavailable slots
   - Interview count for each day
   - Real-time availability check during scheduling

**Panel Composition Features:**

1. **Panel Assignment:**
   - Primary interviewer (required)
   - Secondary interviewer (optional)
   - Tertiary interviewer (optional)
   - Role assignment for each interviewer (Technical, HR, Manager)

2. **Load Balancing:**
   - System suggests interviewers based on:
     - Expertise match with role requirements
     - Current workload (prefer less loaded)
     - Department alignment
     - Availability

3. **Conflict Detection:**
   - Prevent same interviewer double-booking
   - Show warning if conflict detected
   - Suggest alternative dates/times
   - Suggest alternative interviewers

**Interviewer Performance Metrics:**

| Metric | Description | Tracking |
|--------|-------------|----------|
| Total Interviews | Number of interviews conducted | Count |
| Evaluation Timeliness | % evaluations submitted on time | Percentage |
| Evaluation Quality | Completeness and consistency of evaluations | Score |
| Consistency Score | Deviation from panel average scores | Score |
| Feedback Quality | Quality of written feedback | Qualitative |

**HR Manager Dashboard for Panel:**
- Interviewer workload by week/month
- Interview load distribution
- Evaluation submission status
- Performance metrics per interviewer
- Recommendations for load balancing

**Acceptance Criteria:**
- Interviewer availability checked in real-time
- Panel conflicts prevented
- Load balancing suggestions provided
- Interviewer metrics tracked and reported
- Unavailability periods respected

---

### 2.4 QR CHECK-IN SYSTEM (FR-4)

#### FR-4.1: QR Code Generation
- **Requirement ID:** FR-4.1
- **Priority:** HIGH
- **Description:** Generate unique encrypted QR codes for each interview

**Functional Specifications:**

**QR Code Requirements:**

1. **Uniqueness:**
   - One QR code per interview session
   - Each QR contains encrypted interview data
   - QR becomes single-use after first scan

2. **Data Contained in QR:**
   - Interview ID (unique identifier)
   - Candidate ID (for identification)
   - Application ID (for record linking)
   - Interview date
   - Interview time
   - Venue location
   - Generation timestamp
   - Expiration timestamp
   - Cryptographic signature

3. **Encryption:**
   - Encryption method: AES-256
   - Signed with HMAC for tampering detection
   - Encrypted data embedded in QR code

4. **Validity Rules:**
   - Activation window: 30 minutes before interview time
   - Valid duration: 1 hour (30 min before to 30 min after)
   - Single-use: Invalid after first successful scan
   - Status tracking: Active → Used / Expired / Invalidated

**QR Code Properties:**

| Property | Specification |
|----------|-------------|
| Format | QR Code (2D barcode) |
| Error Correction | Level H (30% recovery capacity) |
| Size | 250x250 pixels |
| File Format | PNG image |
| Encoding | UTF-8 |
| Data Capacity | ~500 bytes |

**QR Generation Process:**

1. Interview scheduled (trigger point)
2. System creates QR code record
3. Generate encrypted payload with interview data
4. Create digital signature for integrity
5. Generate QR code image (250x250 PNG)
6. Save QR image to Supabase Storage
7. Store QR metadata in database
8. Generate signed URL with 7-day expiry
9. Provide QR for download/display/sharing

**QR Code Display Options:**

1. **HR Dashboard:**
   - View QR code image in interview details
   - Download QR code as PNG
   - Print QR code on A4 paper

2. **Email to Candidate:**
   - QR image embedded in HTML email
   - Clickable QR code (optional)

3. **WhatsApp Message:**
   - QR code image sent as attachment
   - Text instructions with QR

4. **SMS (Optional):**
   - Link to QR image

**QR Code Invalidation:**
- HR Manager can manually invalidate QR if interview cancelled
- QR auto-invalidates after expiration time
- Invalidated QR code cannot be scanned

**Acceptance Criteria:**
- QR code generated on interview scheduling
- QR contains encrypted interview data
- QR code image generated and stored
- Single-use enforcement working
- Expiry validation working
- Signed URL provided with correct expiry

---

#### FR-4.2: QR Check-in at Venue
- **Requirement ID:** FR-4.2
- **Priority:** HIGH
- **Description:** Candidate scans QR code at interview venue for check-in

**Functional Specifications:**

**Check-in Interface:**

1. **Access Point:**
   - Mobile web browser: `https://portal.sfspl.com/checkin`
   - Works on all mobile phones and tablets
   - Works on tablet at reception desk

2. **Camera Interface:**
   - Automatic camera access request
   - Visual guide for QR positioning
   - Auto-detection and reading
   - Processing indicator during scan

**QR Validation Process:**

System must perform the following validations:

1. **Decrypt QR Data:**
   - Decrypt encrypted payload from QR
   - Error if decryption fails: "Invalid QR code"

2. **Signature Verification:**
   - Verify HMAC signature
   - Error if signature invalid: "QR code tampered or invalid"

3. **Expiry Check:**
   - Verify current time is within validity window
   - Validity window: 30 min before interview to 30 min after
   - Error if expired: "QR code has expired"

4. **Single-Use Check:**
   - Query database for QR usage history
   - Error if already used: "QR code already scanned"

5. **Status Check:**
   - Verify QR status is "Active"
   - Error if invalidated: "QR code has been cancelled"

6. **Geolocation Verification (Optional):**
   - Capture GPS coordinates
   - Verify within 500m radius of venue
   - Warning if outside venue radius

**Successful Check-in Actions:**

1. **Mark QR as Used:**
   - Update QR status to "Used"
   - Record scan timestamp
   - Record IP address and device type

2. **Update Application Status:**
   - Change status to "Interview In Progress - Checked In"
   - Log check-in event in status history

3. **Determine Candidate Type:**
   - Query application details
   - If pre-screened: Type = "Screened"
   - If walk-in or no Form-2: Type = "Walk-in"

4. **Display Success Message:**
   - "✅ Check-in Successful!"
   - Welcome message with candidate name
   - Show which forms need to be completed
   - Provide next action instructions

5. **Load Required Forms:**
   - **For Screened:** Show Form-2 only (address, qualifications)
   - **For Walk-in:** Show Form-1 + Form-2

6. **Send Notifications:**
   - WhatsApp to HR: "Candidate [Name] has checked in"
   - Email to interviewers: "Candidate has arrived"

**Error Handling:**

| Error | Message to Candidate | Action |
|-------|---------------------|--------|
| Invalid QR | "Invalid QR code. Please ensure you're scanning the correct code" | Show help option |
| Expired QR | "QR code has expired. Please contact reception" | Alert HR receptionist |
| Already Used | "You have already checked in. Please proceed to [Room]" | Show interview details |
| Too Early | "Check-in opens at [Time]. Please wait" | Show countdown timer |
| Cancelled Interview | "This interview has been cancelled. Please contact HR" | Show HR contact details |
| Camera Access Denied | "Camera access required. Please enable in settings" | Show device instructions |
| Network Error | "Connection lost. Retrying..." | Retry automatically 3 times |
| Outside Venue | "You seem to be outside venue. Please ensure you're at [Address]" | Warning (not blocking) |

**Mobile Responsiveness:**
- QR scanner works on iPhone and Android
- Works on all screen sizes
- Touch-friendly buttons
- Landscape and portrait orientation

**Acceptance Criteria:**
- QR scan validation successful
- Check-in timestamp recorded
- Correct forms displayed based on candidate type
- Notifications sent to HR
- Check-in status updated in database
- Error messages clear and actionable

---

#### FR-4.3: QR Access Logs & Audit
- **Requirement ID:** FR-4.3
- **Priority:** LOW
- **Description:** Maintain audit logs of all QR validation attempts

**Functional Specifications:**

**Log Entry Contents:**

For each QR scan attempt (success or failure):

| Field | Recorded Data |
|-------|---------------|
| Timestamp | Exact date and time of scan |
| QR ID | Identifier of QR code scanned |
| Interview ID | Associated interview |
| Candidate ID | Candidate attempting check-in |
| Scan Status | Success, Invalid, Expired, Already Used, Outside Venue, etc. |
| IP Address | Source IP of scan request |
| Device Type | Browser, OS, device model |
| Geolocation | GPS coordinates (if captured) |
| Error Message | Reason for failure (if applicable) |
| Validation Duration | Milliseconds to complete validation |

**Logging Events:**

System must log:
- Every successful QR scan
- Every failed validation attempt
- Multiple failed attempts from same IP
- Unusual patterns (QR scanned from different city)
- QR code generation
- QR code invalidation by HR
- Manual checks of QR status

**Analytics & Fraud Detection:**

1. **QR Usage Statistics:**
   - Total QR codes generated (by date range)
   - Total successful check-ins
   - Failed validation attempts (by error type)
   - Average check-in time before interview
   - Check-in rate (% of scheduled candidates)

2. **Fraud Detection Alerts:**
   - Flag if > 5 failed attempts from same IP in 10 min
   - Flag if QR scanned from > 50km away from venue
   - Flag if same QR scanned from multiple IPs
   - Alert admin for suspicious patterns

3. **Venue-wise Analytics:**
   - Check-in rate per venue
   - No-show rate (scheduled but not checked in)
   - Average check-in time per venue

4. **Reporting:**
   - Generate fraud alerts report
   - QR usage analytics report
   - Venue-wise check-in statistics

**Data Retention:**
- QR validation logs retained for 2 years
- After 2 years, archive to cold storage
- Personal identifiers anonymized after retention
- Deletion policy defined in compliance doc

**Acceptance Criteria:**
- All QR scan events logged
- Logs immutable (no deletion)
- Analytics queries available for HR
- Fraud alerts triggered for suspicious patterns
- Data retained per policy

---

### 2.5 INTERVIEW EVALUATION (FR-5)

#### FR-5.1: Form-3 - Interview Evaluation Form
- **Requirement ID:** FR-5.1
- **Priority:** HIGH
- **Description:** Capture structured interview evaluation from interviewers

**Functional Specifications:**

**Form-3 Availability:**
- Available only to assigned interviewers
- Can be filled immediately after interview or within 7 days
- One form per interviewer per interview
- Form cannot be edited after submission

**Scoring Dimensions:**

System must capture scores on 5 dimensions (1-5 scale):

| Dimension | Description | Guidance |
|-----------|-------------|----------|
| **Technical Skills** | Domain knowledge, expertise, technical proficiency | 1=No skills, 2=Below avg, 3=Average, 4=Good, 5=Excellent |
| **Communication** | Clarity, listening, articulation, confidence | 1=Poor, 2=Below avg, 3=Average, 4=Good, 5=Excellent |
| **Problem-Solving** | Analytical thinking, approach, creativity | 1=Weak, 2=Below avg, 3=Average, 4=Good, 5=Excellent |
| **Cultural Fit** | Alignment with company values, team compatibility | 1=Poor fit, 2=Below avg, 3=Average fit, 4=Good fit, 5=Excellent fit |
| **Overall Assessment** | Holistic evaluation considering all factors | 1=Poor, 2=Below avg, 3=Average, 4=Good, 5=Excellent |

**Qualitative Feedback:**

| Field | Type | Max Length | Required | Purpose |
|-------|------|-----------|----------|---------|
| Strengths | Textarea | 200 chars | Yes | Key strengths observed |
| Areas for Development | Textarea | 200 chars | Yes | Growth areas identified |
| Specific Examples | Textarea | 300 chars | No | Supporting examples from interview |

**Recommendation:**

| Option | Meaning |
|--------|---------|
| Strong Recommend | Definitely hire, exceptional candidate |
| Recommend | Good fit, would be good hire |
| Borderline | Could work with proper guidance |
| Do Not Recommend | Not suitable for role |

**Panel Feedback** (Internal, visible to HR only):

| Field | Type | Max Length | Purpose |
|-------|------|-----------|---------|
| Panel Feedback | Textarea | 500 chars | Internal notes for HR discussion |
| Red Flags | Textarea | 300 chars | Concerns or warning signs |

**Auto-Captured Information:**

| Field | Source |
|-------|--------|
| Interview Duration | Calculated from QR check-in to form submission |
| Evaluation Submitted At | Form submission timestamp |
| Interviewer ID | From session/login |
| Interview ID | From form parameters |

**Form Features:**

1. **User Interface:**
   - Rating inputs for scores (1-5 stars or sliders)
   - Clear rubric guidance on hover
   - Character count for text fields
   - Auto-save draft every 60 seconds
   - Submit confirmation modal
   - Progress indicator

2. **Validation:**
   - All scoring fields required
   - All text fields required (min 10 chars)
   - At least one of 5 ratings must be provided
   - Overall score should be within 1.5 points of average

3. **Form Workflow:**
   - Interviewer logs in
   - Opens completed interview from "My Interviews" list
   - Clicks "Submit Evaluation"
   - Form-3 loads with interview details pre-filled
   - Fills scores and feedback
   - Submits form
   - Confirmation: "Evaluation submitted successfully"
   - Email notification sent

**Reminder System:**
- 24 hours after interview: Email reminder if not submitted
- 48 hours after interview: Escalation email to HR Manager
- 7 days after interview: Auto-marked as "Evaluation Overdue"

**Acceptance Criteria:**
- Form-3 loads for assigned interviews only
- All scores captured (1-5 range)
- Qualitative feedback recorded
- Recommendation selected
- Red flags tracked
- Submission timestamp recorded
- HR Manager notified

---

#### FR-5.2: Scoring & Aggregation
- **Requirement ID:** FR-5.2
- **Priority:** MEDIUM
- **Description:** Aggregate scores from multiple interviewers for fair decision-making

**Functional Specifications:**

**Aggregation Methods:**

1. **Simple Average (Default):**
   - Calculate mean for each dimension
   - Example: Technical scores [4, 4, 5] = Average 4.3
   - Calculate overall average score

2. **Weighted Average (Optional):**
   - Apply custom weights to dimensions
   - Example: Technical 40%, Communication 20%, Problem-solving 20%, Cultural-fit 20%
   - Weighted overall score calculated

3. **Role-Based Weighting (Optional):**
   - Interviewer role weights dimensions
   - Technical interviewer's technical score weighted 2x
   - HR interviewer's cultural-fit score weighted 2x

**Outlier Detection:**

System must flag significant score deviations:

1. **Detection Method:**
   - Calculate mean for each dimension
   - Flag any score deviating > 1.5 points from mean
   - Example: If average is 4.0 and one score is 5.0, flag (deviation > 1)

2. **Outlier Display:**
   - Highlight outlier scores in report
   - Show which interviewer gave outlier score
   - Explain the deviation ("This score is significantly higher than panel average")
   - Recommend HR review for consensus

3. **Handling:**
   - HR Manager reviews outliers
   - Consider if legitimate or scoring error
   - May request interviewer clarification

**Aggregate Report Contents:**

For each dimension and overall:

| Item | Contents |
|------|----------|
| Average Score | Mean of all scores |
| Min Score | Lowest score |
| Max Score | Highest score |
| Individual Scores | All 3 scores listed |
| Outliers | List of outlier scores if any |
| Standard Deviation | Measure of score consistency |

**Recommendation Summary:**

| Item | Contents |
|------|----------|
| Strong Recommend Count | Number of interviewers voting strong |
| Recommend Count | Number recommending |
| Borderline Count | Number borderline |
| Do Not Recommend Count | Number recommending rejection |
| Consensus | Majority recommendation (if consensus exists) |

**Benchmark Comparison:**

1. **Role Benchmark:**
   - Query all interviews for same role (last 6 months)
   - Calculate average score for role
   - Compare candidate to benchmark

2. **Percentile Ranking:**
   - Where does candidate score rank among similar roles?
   - Percentile display (e.g., 75th percentile)

3. **Trend Analysis:**
   - Score trend over time (if multiple rounds)
   - Improvement/decline across dimensions

**Visualization Requirements:**

System must support these visualizations:

1. **Radar Chart:**
   - 5 dimensions as axes
   - Overlay: Individual scores + Average + Benchmark
   - Visual comparison easy to understand

2. **Score Distribution:**
   - Bar chart showing distribution per dimension
   - Highlight outliers in different color

3. **Recommendation Breakdown:**
   - Pie chart: % Strong Recommend, Recommend, Borderline, Do Not Recommend

**Acceptance Criteria:**
- Aggregate scores calculated correctly
- Outliers detected and flagged
- Benchmark comparison shows percentile
- Visualizations render correctly
- All 3 evaluations aggregated
- HR can make decision based on aggregates

---

(Continuing with remaining sections: FR-6 through FR-10, NFR-1 through NFR-6, System Architecture, Data Requirements, Security, Interface, Roles, Acceptance Criteria, and Delivery Phases...)

---

### 2.6 HIRING DECISION & OFFER MANAGEMENT (FR-6)

#### FR-6.1: Hiring Decision Workflow
- **Requirement ID:** FR-6.1
- **Priority:** HIGH
- **Description:** Enable HR Manager to make hiring decisions with structured process

**Functional Specifications:**

**Decision Dashboard:**

HR Manager views:
- List of candidates with "Evaluation Pending" status
- All Form-3 evaluations for each candidate
- Aggregated scores and recommendations
- Candidate profile summary
- Interview feedback

**Decision Options:**

| Decision | Outcome | Next Step |
|----------|---------|-----------|
| **Select (Hire)** | Candidate marked as "Selected" | BG verification workflow starts |
| **Reject** | Candidate marked as "Rejected" | Rejection email sent to candidate |
| **Hold** | Candidate kept in pipeline | Reviewed in future rounds |

**Decision Form:**

HR Manager enters:
1. **Decision:** Select, Reject, or Hold
2. **Decision Reason:**
   - Predefined templates: "Excellent fit", "Lacks experience", "Better candidates available"
   - Custom reason text (optional)
3. **Decision Notes:** Additional context (max 500 chars)
4. **Hiring Manager Approval:** (optional) Get hiring manager sign-off before final decision

**Workflow:**

1. HR Manager opens "Pending Decisions" dashboard
2. Reviews candidate profile, all evaluations, scores
3. Selects "Make Decision"
4. Decision form opens
5. Selects decision (Select/Reject/Hold)
6. Enters reason and notes
7. Confirms decision
8. System updates database
9. Automated notifications triggered

**Auto-Triggered Actions:**

**If Selected:**
- Status changed to "Selected"
- BG verification workflow initiated (see FR-6.2)
- Department manager notified
- Candidate notified (generic "Good news coming" message)

**If Rejected:**
- Status changed to "Rejected"
- Rejection email automatically sent to candidate
- Rejection WhatsApp sent to candidate
- Candidate can request feedback (optional)
- HR can provide feedback (optional)

**If Hold:**
- Status changed to "Hold"
- Candidate remains in system for future consideration
- Automatically moved to "Archive" after 90 days if not reactivated

**Acceptance Criteria:**
- Decision form submitted successfully
- Status updated in database
- Notifications sent to appropriate parties
- Decision logged with timestamp and user
- Rejection reasons recorded

---

#### FR-6.2: Background Verification Workflow
- **Requirement ID:** FR-6.2
- **Priority:** HIGH
- **Description:** Track and manage background verification process

**Functional Specifications:**

**BG Verification Process:**

1. **Initiation:** On candidate selection, BG workflow starts
2. **Assignment:** HR Manager assigns to Background Verifier
3. **Status Tracking:** Track status through verification process
4. **Document Collection:** Verify required documents
5. **Final Approval:** HR Manager approves clearance
6. **Offer Generation:** Trigger offer letter generation after clearance

**BG Status States:**

| Status | Meaning | Duration |
|--------|---------|----------|
| Not Initiated | BG not started yet | - |
| Pending | BG initiated, awaiting documents | 0-3 days |
| In Progress | BG officer reviewing documents | 3-10 days |
| Cleared | All checks passed, cleared | Final |
| Failed | Checks failed, candidate rejected | Final |

**BG Verification Requirements:**

Documents/Checks to Verify:

| Item | Required | Verifier |
|------|----------|----------|
| **Address Verification** | Yes | BG Officer |
| **ID Proof Validation** | Yes | BG Officer |
| **Employment History** | Yes | BG Officer |
| **Education Verification** | Yes | BG Officer |
| **Police Verification** | No | BG Officer |
| **Reference Checks** | No | BG Officer |

**BG Officer Dashboard:**

Shows:
- Candidates assigned for BG verification
- Current status of each
- Documents uploaded by candidate
- Checklist of items to verify
- Days elapsed since initiation
- Overdue alerts (> 14 days)

**BG Verification Steps:**

1. **HR Manager Initiates:**
   - Selects "Start BG Verification" on selected candidate
   - System sends message to candidate: "Your background verification has started"
   - BG Officer assigned

2. **BG Officer Reviews Documents:**
   - Views all documents uploaded by candidate
   - Verifies authenticity and completeness
   - Checks for discrepancies

3. **BG Officer Updates Status:**
   - Mark each verification item: Verified, Rejected, In Progress
   - Add notes/findings
   - Upload verification documents (if needed)

4. **HR Manager Reviews:**
   - Reviews BG Officer findings
   - Decides: Clear, Fail, or Need More Info

5. **Clear Decision:**
   - Status changed to "Cleared"
   - Offer letter generation triggered (see FR-6.3)
   - Candidate notified: "Background verification cleared"

6. **Fail Decision:**
   - Status changed to "Failed"
   - Offer withdrawn
   - Candidate notified with reason
   - Candidate can appeal (optional)

**Escalation:**
- If BG not completed within 14 days: Auto-alert HR Manager
- If BG not completed within 21 days: Critical alert to HR Head
- Default: BG completion target = 10 days

**Offer Status During BG:**
- Offer letter marked as "Conditional - Pending BG Clearance"
- Candidate cannot accept offer until BG cleared
- Offer becomes unconditional once BG cleared

**Acceptance Criteria:**
- BG workflow initiated on candidate selection
- BG officer assigned
- Status tracked and updated
- HR Manager reviews findings
- Final clearance decision made
- Escalation alerts triggered

---

#### FR-6.3: Offer Letter Generation & Management
- **Requirement ID:** FR-6.3
- **Priority:** HIGH
- **Description:** Generate, deliver, and track offer letters

**Functional Specifications:**

**Offer Letter Generation:**

Trigger: After BG verification cleared

**Offer Letter Contents:**
- Candidate name and address
- Role and designation
- Department and reporting manager
- Salary and benefits summary
- Date of joining
- Terms and conditions
- Company policies reference
- Offer validity period
- Signature line (scanned employer signature)

**Generation Process:**

1. **Template:** Pre-defined offer letter template (Word or PDF)
2. **Merge:** System merges candidate data into template
3. **Review:** HR Manager reviews generated letter
4. **Corrections:** HR can make corrections before sending
5. **Preview:** PDF preview shown to HR
6. **Approval:** HR Manager approves and sends

**Delivery:**

1. **Email:** Offer letter PDF attached to email
   - Professional email template
   - Clear acceptance/rejection instructions
   - Offer validity date highlighted
   - Contact information for queries

2. **WhatsApp:** Link to offer letter + notification
   - WhatsApp message with offer details
   - Link to download offer PDF
   - Instructions to accept/reject

3. **Portal:** Candidate can view offer in portal
   - Download offer letter
   - View all offer details
   - Accept/reject offer online
   - Request modifications (optional)

**Offer Status Tracking:**

| Status | Meaning | Duration |
|--------|---------|----------|
| **Draft** | Created, not sent yet | - |
| **Sent** | Delivered to candidate | 0-7 days |
| **Viewed** | Candidate opened/viewed | - |
| **Accepted** | Candidate accepted | Final |
| **Rejected** | Candidate rejected | Final |
| **Expired** | Validity period passed | Final |

**Validity Management:**

- Default validity: 7 days from sending
- Configurable by HR Manager
- Auto-expiration: Status changes to "Expired" after validity ends
- Candidate cannot accept after expiration
- HR can extend validity if needed

**Acceptance Process:**

1. Candidate views offer in portal
2. Candidate can accept or reject
3. If accept:
   - Status changed to "Accepted"
   - Confirmation email sent to candidate
   - Onboarding workflow triggered
   - HR Manager notified
   - Data exported to HRMS
4. If reject:
   - Status changed to "Rejected"
   - Reason captured (optional)
   - HR Manager notified
   - System suggests next candidates

**Offer Modifications:**

- Candidate can request modifications (optional feature)
- Request goes to HR Manager
- HR can approve, deny, or propose counter-offer
- If approved, new offer generated and sent

**Acceptance Criteria:**
- Offer letter generated from template
- All merge fields populated correctly
- Offer sent via email and WhatsApp
- Candidate can accept/reject online
- Offer expiry enforced
- Acceptance triggers onboarding

---

(Document continues with FR-7 through FR-10, NFR-1 through NFR-6, System Architecture, Data Requirements, Security, Interface, Roles, Acceptance Criteria, and Delivery Phases...)

Due to length constraints, I'll provide a summary of remaining sections and create them in the next part if needed. Would you like me to:

1. **Continue** with remaining functional requirements (FR-7 to FR-10)?
2. **Include** all non-functional requirements (NFR-1 to NFR-6)?
3. **Add** system architecture, data requirements, interface requirements?
4. **Include** acceptance criteria and delivery phases?

Or should I save this cleaner version now and you can use it as the template for the rest?
