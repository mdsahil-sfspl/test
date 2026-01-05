# HR Onboarding Agent
## Software Requirements Specification (SRS)

**Document Version:** 1.0  
**Created Date:** January 05, 2026  
**Organization:** Sampurna Financial Services Pvt. Ltd. (SFSPL)  
**Last Updated:** January 05, 2026

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

This Software Requirements Specification (SRS) document provides a detailed description of the HR Onboarding Agent system for Sampurna Financial Services Pvt. Ltd. (SFSPL). It defines the functional and non-functional requirements, system architecture, data models, security specifications, and acceptance criteria necessary for successful system development, testing, and deployment.

This document is intended for:
- **Development Team:** Developers, architects, and technical leads
- **Quality Assurance Team:** Test engineers and QA analysts
- **Project Management:** Project managers and scrum masters
- **Stakeholders:** HR managers, IT managers, and business sponsors

### 1.2 SCOPE

The HR Onboarding Agent is a comprehensive digital recruitment and onboarding platform that:

**In Scope:**
- End-to-end candidate lifecycle management (application → offer → onboarding)
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
- Full background verification automation (manual process with tracking)
- Direct auto-sync with Octane HRMS (manual export)
- AI-based candidate ranking
- Video interview platform integration
- Multi-company/multi-tenant support

### 1.3 DEFINITIONS, ACRONYMS, AND ABBREVIATIONS

| Term | Definition |
|------|------------|
| **API** | Application Programming Interface |
| **BG** | Background (Verification) |
| **BRD** | Business Requirements Document |
| **CI/CD** | Continuous Integration / Continuous Deployment |
| **CORS** | Cross-Origin Resource Sharing |
| **CRUD** | Create, Read, Update, Delete |
| **CSV** | Comma-Separated Values |
| **DOJ** | Date of Joining |
| **DPDP Act** | Digital Personal Data Protection Act 2023 (India) |
| **ERD** | Entity-Relationship Diagram |
| **GDPR** | General Data Protection Regulation |
| **HR** | Human Resources |
| **HRMS** | Human Resource Management System |
| **HTTPS** | Hypertext Transfer Protocol Secure |
| **JWT** | JSON Web Token |
| **KPI** | Key Performance Indicator |
| **KYC** | Know Your Customer |
| **MFA** | Multi-Factor Authentication |
| **NPS** | Net Promoter Score |
| **OTP** | One-Time Password |
| **PDF** | Portable Document Format |
| **PII** | Personally Identifiable Information |
| **QR** | Quick Response (Code) |
| **RBAC** | Role-Based Access Control |
| **REST** | Representational State Transfer |
| **RLS** | Row-Level Security |
| **RPO** | Recovery Point Objective |
| **RTO** | Recovery Time Objective |
| **SFSPL** | Sampurna Financial Services Pvt. Ltd. |
| **SLA** | Service Level Agreement |
| **SMS** | Short Message Service |
| **SQL** | Structured Query Language |
| **SRS** | Software Requirements Specification |
| **TLS** | Transport Layer Security |
| **UAT** | User Acceptance Testing |
| **UI/UX** | User Interface / User Experience |
| **UUID** | Universally Unique Identifier |
| **WCAG** | Web Content Accessibility Guidelines |

### 1.4 REFERENCES

- Business Requirements Document (BRD) v1.0 - January 05, 2026
- HR Onboarding Agent High-Level Design (HLD) - December 2025
- DPDP Act 2023 - Indian Data Protection Regulations
- WCAG 2.1 Accessibility Guidelines
- FastAPI Documentation - https://fastapi.tiangolo.com/
- Streamlit Documentation - https://docs.streamlit.io/
- PostgreSQL 14 Documentation
- Supabase Documentation
- n8n Automation Documentation

### 1.5 TECHNOLOGY STACK OVERVIEW

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Backend API** | FastAPI | 0.104+ | REST API, business logic, validation |
| **Frontend** | Streamlit | 1.28+ | Web UI for candidates and HR |
| **Database** | PostgreSQL | 14+ | Primary data store |
| **Document Storage** | Supabase Storage | Latest | File uploads, documents |
| **Automation** | n8n | Latest | Notifications, workflows |
| **Authentication** | JWT + OTP | - | Stateless auth |
| **Caching** | Redis | 7+ | Session storage, rate limiting |
| **Deployment** | AWS EC2/ECS | - | Cloud infrastructure |
| **Monitoring** | CloudWatch | - | Logs, metrics, alerts |

---

## 2. FUNCTIONAL REQUIREMENTS

### 2.1 AUTHENTICATION & AUTHORIZATION

#### FR-1.1: Candidate Authentication
- **Requirement ID:** FR-1.1
- **Priority:** HIGH
- **Description:** Passwordless authentication for candidates using mobile OTP

**Detailed Specifications:**

**Input:**
- Mobile number (10 digits, Indian format)
- OTP (6 digits, numeric)

**Process:**
1. Candidate enters mobile number on login screen
2. System validates format: `^[6-9]\d{9}$`
3. System generates 6-digit OTP using secure random
4. OTP sent via WhatsApp using n8n webhook
5. OTP stored in Redis with 5-minute TTL
6. Candidate enters OTP
7. System validates OTP against Redis
8. On success: Generate JWT token with 24-hour expiry
9. On failure: Increment retry counter, allow max 3 attempts
10. After 3 failures: 15-minute cooldown period

**Output:**
- JWT access token (24-hour validity)
- Session created in database
- Redirect to candidate dashboard

**Validation Rules:**
- Mobile number: 10 digits, starts with 6-9
- OTP: 6 digits, numeric only
- OTP expiry: 5 minutes
- Max retry attempts: 3
- Cooldown period: 15 minutes after 3 failures

**Error Handling:**
- Invalid mobile format: "Please enter a valid 10-digit mobile number"
- OTP expired: "OTP has expired. Please request a new one"
- Invalid OTP: "Invalid OTP. {attempts_remaining} attempts remaining"
- Max attempts exceeded: "Too many failed attempts. Please try again after 15 minutes"
- WhatsApp delivery failure: "Unable to send OTP. Please try again"

**Database Tables:**
- `candidates` (candidate_id, phone_number)
- `sessions` (session_id, candidate_id, created_at, expires_at)

**API Endpoints:**
- `POST /api/auth/candidate/request-otp` - Request OTP
- `POST /api/auth/candidate/verify-otp` - Verify OTP and login
- `POST /api/auth/candidate/logout` - End session

---

#### FR-1.2: HR Staff Authentication
- **Requirement ID:** FR-1.2
- **Priority:** HIGH
- **Description:** Email/password authentication for HR staff with optional MFA

**Detailed Specifications:**

**Input:**
- Email address
- Password (min 8 chars, complexity requirements)
- MFA code (6 digits, if enabled)

**Process:**
1. User enters email and password
2. System validates email format
3. System retrieves user record from database
4. Password hash compared using bcrypt
5. If MFA enabled: Request TOTP code
6. Validate TOTP using user's secret key
7. On success: Generate JWT tokens (access + refresh)
8. Access token: 8-hour expiry
9. Refresh token: 7-day expiry
10. Session created with IP, user agent logging

**Output:**
- JWT access token (8-hour validity)
- JWT refresh token (7-day validity)
- User profile data
- Redirect to role-specific dashboard

**Password Requirements:**
- Minimum 8 characters
- At least 1 uppercase letter
- At least 1 lowercase letter
- At least 1 digit
- At least 1 special character (@$!%*?&)
- Cannot be same as last 3 passwords
- Must be changed every 90 days

**MFA Specifications:**
- TOTP algorithm: RFC 6238
- Time step: 30 seconds
- Code length: 6 digits
- QR code generation for secret key setup
- Backup codes: 10 single-use codes

**Session Management:**
- Access token expiry: 8 hours
- Refresh token expiry: 7 days
- Idle timeout: 2 hours for regular staff, 30 min for HR Manager
- Automatic session refresh using refresh token
- Concurrent session limit: 3 devices

**Error Handling:**
- Invalid email format: "Please enter a valid email address"
- Invalid credentials: "Invalid email or password"
- Account locked: "Account locked due to multiple failed attempts. Contact admin"
- MFA code invalid: "Invalid authentication code"
- Password expired: "Your password has expired. Please reset"
- Session expired: "Session expired. Please login again"

**Database Tables:**
- `users` (user_id, email, password_hash, role_id, mfa_enabled, mfa_secret)
- `sessions` (session_id, user_id, access_token, refresh_token, ip_address, user_agent)
- `password_history` (user_id, password_hash, created_at)

**API Endpoints:**
- `POST /api/auth/staff/login` - Login with email/password
- `POST /api/auth/staff/mfa/setup` - Setup MFA
- `POST /api/auth/staff/mfa/verify` - Verify MFA code
- `POST /api/auth/staff/refresh` - Refresh access token
- `POST /api/auth/staff/logout` - End session
- `POST /api/auth/staff/password/reset` - Reset password

---

#### FR-1.3: Role-Based Access Control (RBAC)
- **Requirement ID:** FR-1.3
- **Priority:** HIGH
- **Description:** Enforce role-based permissions for all system features

**Detailed Specifications:**

**Roles:**

1. **Super Admin**
   - System configuration and settings
   - User provisioning (create, edit, delete users)
   - Audit log access (all users, all actions)
   - Global data access (all candidates, all departments)
   - Role and permission management

2. **HR Manager**
   - Hiring decision approval
   - Offer letter generation and approval
   - Background verification approval
   - Dashboard access (all departments or assigned)
   - Report generation
   - Onboarding checklist creation

3. **Recruiter**
   - Candidate screening (shortlist/reject)
   - Interview scheduling
   - QR code generation
   - Candidate communication
   - Data access: Assigned candidates only
   - Basic reporting

4. **Interviewer**
   - Form-3 submission (interview evaluation)
   - QR code validation at venue
   - Candidate profile view (assigned interviews only)
   - No candidate data modification

5. **Background Verifier**
   - BG verification status updates
   - Document collection and verification
   - Data access: Assigned candidates only
   - BG report upload

6. **Compliance Officer**
   - Read-only access to all data
   - Audit log review
   - Compliance report generation
   - No data modification

7. **Candidate**
   - Self-profile view and edit
   - Application status tracking
   - Form submission (Form-1, Form-2, Form-4)
   - Document upload
   - Offer acceptance/rejection

**Permission Matrix:**

| Resource | Super Admin | HR Manager | Recruiter | Interviewer | BV Officer | Candidate | Compliance |
|----------|------------|-----------|-----------|------------|-----------|----------|-----------|
| **Candidates** |
| View All | ✓ | ✓ | ✓ (Assigned) | ✓ (Assigned) | ✓ (Assigned) | ✓ (Self) | ✓ (Read) |
| Create | ✓ | - | - | - | - | ✓ (Self) | - |
| Edit | ✓ | ✓ | ✓ (Minor) | - | - | ✓ (Self) | - |
| Delete | ✓ | - | - | - | - | - | - |
| **Applications** |
| View | ✓ | ✓ | ✓ (Assigned) | ✓ (Assigned) | ✓ (Assigned) | ✓ (Own) | ✓ (Read) |
| Shortlist/Reject | ✓ | ✓ | ✓ | - | - | - | - |
| **Interviews** |
| Schedule | ✓ | ✓ | ✓ | - | - | - | - |
| Conduct | ✓ | - | - | ✓ | - | - | - |
| Evaluate (Form-3) | ✓ | - | - | ✓ | - | - | - |
| **Decisions** |
| Make Decision | ✓ | ✓ | - | - | - | - | - |
| View Decisions | ✓ | ✓ | ✓ (Own) | ✓ (Own) | - | ✓ (Own) | ✓ (Read) |
| **Offers** |
| Generate | ✓ | ✓ | - | - | - | - | - |
| Send | ✓ | ✓ | - | - | - | - | - |
| Accept/Reject | ✓ | - | - | - | - | ✓ (Own) | - |
| **BG Verification** |
| Initiate | ✓ | ✓ | - | - | - | - | - |
| Perform | ✓ | - | - | - | ✓ | - | - |
| Approve | ✓ | ✓ | - | - | - | - | - |
| **Onboarding** |
| Create Checklist | ✓ | ✓ | - | - | - | - | - |
| Assign Tasks | ✓ | ✓ | - | - | - | - | - |
| Complete Tasks | ✓ | ✓ | - | - | - | ✓ (Own) | - |
| **Documents** |
| Upload | ✓ | - | - | - | - | ✓ | - |
| Download | ✓ | ✓ | ✓ (Assigned) | ✓ (Assigned) | ✓ (Assigned) | ✓ (Own) | - |
| Verify | ✓ | ✓ | - | - | ✓ | - | - |
| **Reports** |
| Generate | ✓ | ✓ | ✓ (Limited) | - | - | - | ✓ |
| Export Data | ✓ | ✓ | - | - | - | - | ✓ |
| **Admin** |
| User Management | ✓ | - | - | - | - | - | - |
| Audit Logs | ✓ | - | - | - | - | - | ✓ |
| System Config | ✓ | - | - | - | - | - | - |

**Implementation:**

**Row-Level Security (RLS):**
```sql
-- Example: Recruiter sees only assigned candidates
CREATE POLICY recruiter_candidates ON candidate_applications
  FOR SELECT
  USING (
    recruiter_assigned_id = current_user_id() 
    OR current_user_role() = 'HR Manager'
    OR current_user_role() = 'Super Admin'
  );
```

**API Middleware:**
- Every API endpoint checks user role and permissions
- Decorator: `@require_role(["HR Manager", "Super Admin"])`
- Decorator: `@require_permission("candidates.edit")`

**Database Tables:**
- `roles` (role_id, role_name, description)
- `permissions` (permission_id, resource, action, description)
- `role_permissions` (role_id, permission_id)
- `users` (user_id, role_id)

**API Endpoints:**
- `GET /api/auth/me` - Get current user profile and permissions
- `GET /api/auth/permissions` - Get current user's permissions
- `GET /api/roles` - List all roles (admin only)
- `POST /api/roles/{role_id}/permissions` - Assign permission to role (admin only)

**Error Handling:**
- Insufficient permissions: `403 Forbidden - "You do not have permission to perform this action"`
- Invalid role: `400 Bad Request - "Invalid role specified"`
- Data access violation: `403 Forbidden - "Access denied to this resource"`

---

### 2.2 CANDIDATE MANAGEMENT

#### FR-2.1: Candidate Registration via WhatsApp
- **Requirement ID:** FR-2.1
- **Priority:** HIGH
- **Description:** Candidate initiates application by sending message to WhatsApp bot

**Detailed Specifications:**

**Trigger:**
- Candidate sends any message (e.g., "Hi", "Apply", "Job") to WhatsApp business number

**Process Flow:**
1. n8n receives webhook from WhatsApp Business API
2. Webhook payload contains: `from` (phone number), `message` (text), `timestamp`
3. n8n forwards to FastAPI endpoint: `POST /api/webhooks/whatsapp/incoming`
4. FastAPI extracts phone number, normalizes format (+91XXXXXXXXXX)
5. Check if phone number exists in `candidates` table:
   - **If exists:** Retrieve candidate_id, update last_contact_at
   - **If new:** Create new candidate record with status "Initiated"
6. Check 30-day cooldown: Query `candidate_applications` for same phone + role in last 30 days
   - **If found:** Send message: "You have already applied for this role recently. Please wait until [date]"
   - **If not found:** Proceed
7. Generate Form-1 URL with candidate_id token: `https://portal.sfspl.com/form1?token={encrypted_candidate_id}`
8. Send WhatsApp message via n8n:
   ```
   Hi! Thank you for your interest in [Role] at SFSPL.
   
   Please fill out this form to complete your application:
   [Form-1 Link]
   
   This should take about 5-7 minutes.
   
   Need help? Reply with "Help"
   ```
9. Log interaction in `candidate_interactions` table

**Output:**
- Candidate record created/updated
- Form-1 link sent via WhatsApp
- Application status: "Initiated"

**30-Day Cooldown Logic:**
```sql
SELECT COUNT(*) FROM candidate_applications
WHERE phone_number = :phone
  AND role_id = :role_id
  AND created_at > NOW() - INTERVAL '30 days';
```

**Database Tables:**
- `candidates` (candidate_id, phone_number, created_at, last_contact_at)
- `candidate_applications` (application_id, candidate_id, role_id, status, created_at)
- `candidate_interactions` (interaction_id, candidate_id, channel, message, timestamp)

**API Endpoints:**
- `POST /api/webhooks/whatsapp/incoming` - Receive WhatsApp messages
- `POST /api/candidates/initiate` - Manual initiation (admin)

**n8n Workflow:**
1. WhatsApp Trigger Node
2. HTTP Request Node → FastAPI
3. Conditional Node (based on FastAPI response)
4. WhatsApp Send Node → Form-1 link or cooldown message
5. Log Node → Supabase log table

**Error Handling:**
- Invalid phone format: Log error, send "Invalid phone number" message
- Database error: Retry 3 times, alert admin
- WhatsApp API error: Queue message for retry (up to 24 hours)

---

#### FR-2.2: Form-1 - Basic Details
- **Requirement ID:** FR-2.2
- **Priority:** HIGH
- **Description:** Candidate fills basic personal and professional details

**Detailed Specifications:**

**Form Fields:**

| Field Name | Type | Required | Validation | Default |
|-----------|------|----------|-----------|---------|
| `name` | Text | Yes | Min 2, Max 100 chars, alphabets only | - |
| `email` | Email | Yes | Valid email format | - |
| `phone_number` | Text | Yes | 10 digits, auto-filled from WhatsApp | Pre-filled |
| `date_of_birth` | Date | Yes | Age between 18-65 years | - |
| `gender` | Select | Yes | Options: Male, Female, Other | - |
| `current_location` | Text | Yes | City name, max 50 chars | - |
| `current_company` | Text | No | Max 100 chars | - |
| `current_designation` | Text | Yes | Max 100 chars | - |
| `years_of_experience` | Number | Yes | 0-50 years | - |
| `desired_role` | Select | Yes | Dropdown from `roles` table | - |
| `qualification` | Select | Yes | Options: 12th, Graduate, Post-Graduate, Doctorate | - |
| `notice_period` | Select | No | Options: Immediate, 15 days, 1 month, 2 months, 3 months | - |

**UI Components:**
- Mobile-responsive Streamlit form
- Progress indicator: "Step 1 of 4"
- Auto-save draft every 30 seconds
- Field-level validation with inline error messages
- Submit button disabled until all required fields valid

**Process Flow:**
1. Candidate clicks Form-1 link from WhatsApp
2. System validates token in URL, retrieves candidate_id
3. Form loads with phone number pre-filled
4. Candidate fills remaining fields
5. On field blur: Client-side validation
6. On form submit:
   - Final validation (client + server)
   - Create/update record in `personal_details` table
   - Create/update record in `candidate_applications` table with status "Form-1 Submitted"
   - Eligibility check (see FR-2.3)
7. Success message displayed
8. Redirect to status page

**Eligibility Check (on Form-1 submit):**

| Criterion | Rule | Fail Action |
|-----------|------|-------------|
| **Qualification** | Must match role requirement | Reject with reason |
| **Experience** | Must be within role range (e.g., 2-5 years) | Reject with reason |
| **30-Day Cooldown** | No application for same role in 30 days | Reject with date |
| **Age** | 18-65 years | Reject with reason |

**Eligibility Pass:**
- Status updated to "Eligible - Pending Screening"
- Email sent: "Application received. Our team will review and contact you soon"
- WhatsApp sent: "✅ Application received! We'll review and get back within 2-3 days"

**Eligibility Fail:**
- Status updated to "Rejected - {Reason}"
- Email sent with detailed rejection reason and suggestions
- WhatsApp sent: "Thank you for applying. Unfortunately, you don't meet requirements for this role at this time"

**Auto-Save Draft:**
- Every 30 seconds, form data saved to `application_drafts` table
- On page reload, draft retrieved and form populated
- Draft expires after 7 days

**Database Tables:**
- `personal_details` (detail_id, application_id, name, email, phone_number, dob, gender, current_location, current_company, current_designation, years_of_experience, qualification, submitted_at)
- `candidate_applications` (application_id, candidate_id, role_id, status, created_at, updated_at)
- `application_drafts` (draft_id, candidate_id, form_data_json, saved_at, expires_at)

**API Endpoints:**
- `GET /api/forms/form1?token={token}` - Load Form-1
- `POST /api/forms/form1/draft` - Save draft
- `GET /api/forms/form1/draft?candidate_id={id}` - Retrieve draft
- `POST /api/forms/form1/submit` - Submit Form-1

**Validation Rules (Backend):**
```python
class Form1Schema(BaseModel):
    name: str = Field(min_length=2, max_length=100, regex="^[a-zA-Z ]+$")
    email: EmailStr
    phone_number: str = Field(regex="^[6-9]\d{9}$")
    date_of_birth: date
    gender: Literal["Male", "Female", "Other"]
    current_location: str = Field(max_length=50)
    current_designation: str = Field(max_length=100)
    years_of_experience: int = Field(ge=0, le=50)
    desired_role: int  # role_id
    qualification: Literal["12th", "Graduate", "Post-Graduate", "Doctorate"]
    
    @validator('date_of_birth')
    def validate_age(cls, v):
        age = (date.today() - v).days // 365
        if not (18 <= age <= 65):
            raise ValueError('Age must be between 18 and 65')
        return v
```

**Error Handling:**
- Invalid token: "Invalid or expired link. Please request a new one"
- Validation errors: Field-specific error messages
- Database error: "Unable to save. Please try again"
- Network error: "Connection lost. Your progress is saved. Please retry"

---

#### FR-2.3: Form-2 - Address & Qualifications
- **Requirement ID:** FR-2.3
- **Priority:** HIGH
- **Description:** Candidate fills address, education, skills, and document uploads

**Detailed Specifications:**

**When Shown:**
- **Screened Candidates:** After interview scheduled, before interview (via email/WhatsApp link)
- **Walk-in Candidates:** After QR check-in at interview venue (same day as interview)

**Form Sections:**

**Section 1: Address Details**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `current_address_line1` | Text | Yes | Max 200 chars |
| `current_address_line2` | Text | No | Max 200 chars |
| `current_city` | Text | Yes | Max 50 chars |
| `current_state` | Select | Yes | Dropdown of Indian states |
| `current_pincode` | Text | Yes | 6 digits |
| `permanent_same_as_current` | Checkbox | - | If checked, copy current to permanent |
| `permanent_address_line1` | Text | Conditional | Required if not same as current |
| `permanent_address_line2` | Text | No | Max 200 chars |
| `permanent_city` | Text | Conditional | Required if not same as current |
| `permanent_state` | Select | Conditional | Required if not same as current |
| `permanent_pincode` | Text | Conditional | Required if not same as current |

**Section 2: Educational Qualifications**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `qualification_level` | Select | Yes | 12th, Graduate, Post-Graduate, Doctorate |
| `degree_name` | Text | Yes | E.g., "B.Tech CSE", Max 100 chars |
| `university` | Text | Yes | Max 100 chars |
| `year_of_passing` | Number | Yes | 1970 to current year |
| `cgpa_percentage` | Number | Yes | 0-100 (if percentage) or 0-10 (if CGPA) |
| `grade_type` | Select | Yes | Percentage, CGPA |

*(Allow multiple qualifications: + Add Another Qualification)*

**Section 3: Skills**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `skills` | Multi-select | Yes | Select from predefined list + "Other" option |
| `skill_proficiency` | Select per skill | Yes | Beginner, Intermediate, Advanced, Expert |

Predefined skill categories (examples):
- **Technical:** Python, Java, SQL, AWS, Data Analysis, Project Management
- **Soft Skills:** Communication, Leadership, Teamwork, Problem-solving

**Section 4: Document Uploads**

| Document Type | Required | File Types | Max Size |
|--------------|----------|-----------|----------|
| `resume` | Yes | PDF, DOC, DOCX | 5 MB |
| `photo` | Yes | JPG, PNG | 2 MB |
| `qualification_certificates` | Yes | PDF, JPG (multiple) | 5 MB each |
| `experience_letter` | No | PDF, JPG | 5 MB |
| `id_proof` | Yes | PDF, JPG | 2 MB |

**UI Components:**
- Collapsible sections for better UX
- Progress indicator: "Step 2 of 4"
- File upload with drag-and-drop
- Upload progress bar
- Preview for uploaded files
- Auto-save draft

**Process Flow:**
1. Candidate receives Form-2 link (email/WhatsApp)
2. Loads form with application_id in token
3. Fills sections 1-4
4. On file upload:
   - Client requests signed URL from FastAPI: `POST /api/storage/signed-url`
   - Client uploads directly to Supabase Storage
   - Client sends file URL to FastAPI: `POST /api/documents`
   - Document metadata stored in `documents` table
5. On form submit:
   - Validate all fields
   - Insert records into `addresses`, `qualifications`, `skills` tables
   - Update `candidate_applications` status to "Form-2 Submitted"
   - Send confirmation email/WhatsApp
6. Redirect to status page

**Database Tables:**
- `addresses` (address_id, application_id, type, line1, line2, city, state, pincode)
- `qualifications` (qualification_id, application_id, level, degree_name, university, year_of_passing, cgpa_percentage, grade_type)
- `skills` (skill_id, application_id, skill_name, proficiency)
- `documents` (document_id, application_id, document_type, file_name, file_url, file_size, uploaded_at, verification_status)

**Supabase Storage:**
- Bucket: `candidate-documents`
- Folder structure: `{candidate_id}/{application_id}/{document_type}/{filename}`
- Encryption: AES-256 at rest
- Access: Private, signed URLs with 1-hour expiry

**API Endpoints:**
- `GET /api/forms/form2?token={token}` - Load Form-2
- `POST /api/forms/form2/draft` - Save draft
- `POST /api/storage/signed-url` - Get signed upload URL
- `POST /api/documents` - Store document metadata
- `POST /api/forms/form2/submit` - Submit Form-2

**Validation Rules:**
```python
class AddressSchema(BaseModel):
    line1: str = Field(max_length=200)
    line2: Optional[str] = Field(max_length=200)
    city: str = Field(max_length=50)
    state: str
    pincode: str = Field(regex="^\d{6}$")

class QualificationSchema(BaseModel):
    level: Literal["12th", "Graduate", "Post-Graduate", "Doctorate"]
    degree_name: str = Field(max_length=100)
    university: str = Field(max_length=100)
    year_of_passing: int = Field(ge=1970, le=date.today().year)
    cgpa_percentage: float = Field(ge=0, le=100)
    grade_type: Literal["Percentage", "CGPA"]
    
    @validator('cgpa_percentage')
    def validate_grade(cls, v, values):
        if values.get('grade_type') == 'CGPA' and v > 10:
            raise ValueError('CGPA cannot exceed 10')
        return v
```

**Error Handling:**
- File upload failure: Retry 3 times, then show error message
- Invalid file type: "Please upload PDF, DOC, or DOCX files only"
- File size exceeded: "File size should not exceed 5 MB"
- Validation error: Field-specific inline error messages
- Network error: "Upload paused. Will resume automatically"

---

#### FR-2.4: Form-4 - Onboarding Details
- **Requirement ID:** FR-2.4
- **Priority:** MEDIUM
- **Description:** Candidate fills final onboarding details post-induction

**Detailed Specifications:**

**When Shown:**
- After candidate scans induction QR code on joining day (DOJ)
- One-time form, submitted once

**Form Sections:**

**Section 1: Bank Details**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `bank_account_number` | Text | Yes | 9-18 digits, numeric |
| `bank_account_number_confirm` | Text | Yes | Must match above |
| `ifsc_code` | Text | Yes | 11 chars, alphanumeric, format: `^[A-Z]{4}0[A-Z0-9]{6}$` |
| `account_holder_name` | Text | Yes | Max 100 chars |
| `bank_name` | Text | Yes | Max 100 chars |
| `branch_name` | Text | Yes | Max 100 chars |
| `account_type` | Select | Yes | Savings, Current |

**Section 2: Emergency Contact**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `emergency_contact_name` | Text | Yes | Max 100 chars |
| `emergency_contact_relation` | Select | Yes | Options: Spouse, Parent, Sibling, Friend, Other |
| `emergency_contact_phone` | Text | Yes | 10 digits |
| `emergency_contact_address` | Text | No | Max 200 chars |

**Section 3: Final Address Confirmation**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `permanent_address_confirmed` | Checkbox | Yes | Confirm permanent address is correct |
| `permanent_address_update` | Text | No | If address changed, update here |

**Section 4: Health Declaration**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `blood_group` | Select | No | A+, A-, B+, B-, AB+, AB-, O+, O- |
| `medical_conditions` | Textarea | No | Max 500 chars |
| `allergies` | Textarea | No | Max 300 chars |
| `emergency_medical_info` | Textarea | No | Max 500 chars |

**Section 5: IT Preferences**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `laptop_preference` | Select | No | Windows, Mac, Linux |
| `monitor_preference` | Select | No | Single, Dual |
| `keyboard_mouse_type` | Select | No | Wired, Wireless |
| `software_requirements` | Textarea | No | Max 300 chars |

**UI Components:**
- Step-by-step wizard UI
- Progress: "Step 4 of 4 - Final Details"
- Section collapsibles
- Bank account verification (future: Penny drop API)
- Submit confirmation modal

**Process Flow:**
1. Candidate scans induction QR at reception on DOJ
2. QR validation (see FR-7.2)
3. Upon successful QR scan, Form-4 link sent via WhatsApp
4. Candidate opens Form-4 link
5. Fills all sections
6. On submit:
   - Validate all fields
   - Encrypt sensitive data (bank account, emergency contact phone)
   - Insert into `onboarding_details` table
   - Update `candidate_applications` status to "Onboarding Complete"
   - Trigger data export to HRMS (see FR-7.3)
7. Success message: "Congratulations! Your onboarding is complete. Welcome to SFSPL!"
8. Send confirmation email and WhatsApp

**Data Export to HRMS:**
- Triggered automatically on Form-4 submission
- Fields exported: Name, Email, Phone, DOJ, Designation, Bank Details, Emergency Contact
- Export format: JSON API call to Octane HRMS
- Fallback: CSV file generation for manual upload

**Database Tables:**
- `onboarding_details` (onboarding_id, application_id, bank_account_number_encrypted, ifsc_code, account_holder_name, bank_name, branch_name, account_type, emergency_contact_name, emergency_contact_relation, emergency_contact_phone_encrypted, permanent_address, blood_group, medical_conditions, allergies, laptop_preference, monitor_preference, submitted_at)

**API Endpoints:**
- `GET /api/forms/form4?token={token}` - Load Form-4
- `POST /api/forms/form4/submit` - Submit Form-4
- `POST /api/hrms/export` - Export to HRMS

**Encryption:**
- Fields encrypted: `bank_account_number`, `emergency_contact_phone`
- Algorithm: AES-256
- Key management: AWS KMS or HashiCorp Vault

**Validation Rules:**
```python
class BankDetailsSchema(BaseModel):
    bank_account_number: str = Field(regex="^\d{9,18}$")
    bank_account_number_confirm: str
    ifsc_code: str = Field(regex="^[A-Z]{4}0[A-Z0-9]{6}$")
    account_holder_name: str = Field(max_length=100)
    bank_name: str = Field(max_length=100)
    branch_name: str = Field(max_length=100)
    account_type: Literal["Savings", "Current"]
    
    @validator('bank_account_number_confirm')
    def accounts_match(cls, v, values):
        if 'bank_account_number' in values and v != values['bank_account_number']:
            raise ValueError('Account numbers do not match')
        return v
```

**Error Handling:**
- IFSC validation failure: "Invalid IFSC code. Please check and try again"
- Bank account mismatch: "Account numbers do not match"
- Encryption error: Log error, retry, alert admin
- HRMS export failure: Queue for retry, alert admin

---

#### FR-2.5: Candidate Status Tracking
- **Requirement ID:** FR-2.5
- **Priority:** MEDIUM
- **Description:** Candidate views real-time application status with timeline

**Detailed Specifications:**

**Status Flow:**

```
Initiated 
  ↓
Form-1 Submitted 
  ↓
Eligible - Pending Screening
  ↓
Shortlisted
  ↓
Interview Scheduled
  ↓
Interview Complete - QR Checked In
  ↓
Interview Complete - Form-2 Submitted
  ↓
Interview Complete - Evaluation Pending
  ↓
Evaluation Complete - Decision Pending
  ↓
Selected / Rejected / Hold
  ↓ (if Selected)
Background Verification - Initiated
  ↓
Background Verification - In Progress
  ↓
Background Verification - Cleared / Failed
  ↓ (if Cleared)
Offer Sent
  ↓
Offer Accepted / Rejected / Expired
  ↓ (if Accepted)
Onboarding Started
  ↓
Onboarding - Induction Pending
  ↓
Onboarding - Induction Complete
  ↓
Onboarding - Form-4 Pending
  ↓
Onboarding Complete
```

**UI Components:**

**Timeline View:**
- Vertical timeline with icons for each stage
- Completed stages: Green checkmark
- Current stage: Blue indicator with pulse animation
- Pending stages: Gray outline
- Each stage shows: Status, Date/Time, Description

**Status Badge:**
- Color-coded badge at top of page
- Green: Success states (Offer Accepted, Onboarding Complete)
- Blue: In-progress states
- Orange: Pending action from candidate
- Red: Rejected or Failed states

**Next Action Indicator:**
- Clear CTA based on current status
- Examples:
  - "Upload Documents" (if Form-2 pending)
  - "Wait for Interview Schedule" (if shortlisted)
  - "Check Interview Details" (if interview scheduled)
  - "Accept Offer" (if offer sent)
  - "Complete Form-4" (if onboarding started)

**Process Flow:**
1. Candidate logs in
2. Dashboard loads with current status
3. Timeline query: `SELECT * FROM application_status_log WHERE application_id = :app_id ORDER BY timestamp`
4. Display timeline with all status changes
5. Highlight current status
6. Show next action if applicable

**Rejection Display:**
- If status = "Rejected":
  - Show empathetic message
  - Display rejection reason (from template or custom)
  - Suggest alternative actions:
    - Apply for different role
    - Reapply after 30 days
    - Provide feedback link

**Database Tables:**
- `candidate_applications` (application_id, candidate_id, status, updated_at)
- `application_status_log` (log_id, application_id, status, timestamp, reason, updated_by_user_id)

**API Endpoints:**
- `GET /api/candidates/status?application_id={id}` - Get current status
- `GET /api/candidates/timeline?application_id={id}` - Get status timeline

**Real-Time Updates:**
- Status refreshes every 30 seconds (polling)
- Alternative: WebSocket for real-time push (future enhancement)

**Error Handling:**
- Load failure: Show cached status with "Unable to refresh" message
- Network error: Retry with exponential backoff

---

#### FR-2.6: Document Management
- **Requirement ID:** FR-2.6
- **Priority:** HIGH
- **Description:** Secure storage and management of candidate documents

**Detailed Specifications:**

**Document Types:**

| Type | Required | Uploaded By | Verified By | Retention |
|------|----------|-------------|-------------|-----------|
| `resume` | Yes | Candidate | Recruiter | 2 years |
| `photo` | Yes | Candidate | Recruiter | 2 years |
| `qualification_certificate` | Yes | Candidate | BV Officer | 2 years |
| `experience_letter` | No | Candidate | BV Officer | 2 years |
| `id_proof` | Yes | Candidate | BV Officer | 2 years |
| `offer_letter_signed` | Yes | Candidate | HR Manager | 7 years |
| `form_16` | No | HR | - | 7 years |
| `onboarding_documents` | Varies | Candidate | HR | 7 years |

**Upload Process:**
1. Candidate clicks "Upload Document"
2. Selects document type from dropdown
3. Chooses file (drag-and-drop or file picker)
4. File validation: Type, size, virus scan (future)
5. Request signed URL from FastAPI: `POST /api/storage/signed-url`
   ```json
   {
     "application_id": "uuid",
     "document_type": "resume",
     "file_name": "john_doe_resume.pdf",
     "file_size": 1048576
   }
   ```
6. FastAPI generates signed URL from Supabase Storage (1-hour expiry)
7. Client uploads directly to Supabase using signed URL (reduces server load)
8. On upload success, client sends metadata to FastAPI: `POST /api/documents`
   ```json
   {
     "application_id": "uuid",
     "document_type": "resume",
     "file_name": "john_doe_resume.pdf",
     "file_url": "https://supabase.co/storage/...",
     "file_size": 1048576
   }
   ```
9. Document record created in `documents` table with status "Unverified"
10. Success toast: "Document uploaded successfully"

**Verification Process:**
1. HR/BV Officer views document list
2. Clicks "Verify" on document
3. Document opens in modal (PDF viewer or image preview)
4. Officer reviews document
5. Actions:
   - **Verify:** Mark as "Verified", add verification notes
   - **Reject:** Mark as "Rejected", add rejection reason (e.g., "Blurry image", "Invalid document")
   - **Request Reupload:** Send notification to candidate
6. Status updated, candidate notified

**Version Control:**
- If candidate reuploads same document type, create new version
- Previous versions retained with status "Superseded"
- Version number incremented: `resume_v1.pdf`, `resume_v2.pdf`

**Document Access Control:**
- Candidate: View/download own documents
- HR/Recruiter: View/download documents of assigned candidates
- BV Officer: View/download documents of assigned candidates (for BG verification)
- Compliance: Read-only access to all documents

**Download:**
- Document download via signed URL (30-minute expiry)
- Audit log: Record who downloaded which document and when

**Automatic Cleanup:**
- Rejected candidates: Documents archived after 2 years
- Hired employees: Documents retained until 2 years post-exit
- Soft delete: Move to `documents_archived` table, retain for 7 years total

**Database Tables:**
- `documents` (document_id, application_id, document_type, file_name, file_url, file_size, version, uploaded_at, uploaded_by, verification_status, verified_by, verified_at, verification_notes, rejection_reason)
- `documents_archived` (same schema, for soft-deleted documents)

**API Endpoints:**
- `POST /api/storage/signed-url` - Get signed upload URL
- `POST /api/documents` - Save document metadata
- `GET /api/documents?application_id={id}` - List documents for application
- `GET /api/documents/{document_id}/download` - Get signed download URL
- `PUT /api/documents/{document_id}/verify` - Verify document
- `PUT /api/documents/{document_id}/reject` - Reject document
- `DELETE /api/documents/{document_id}` - Soft delete document

**Supabase Storage Configuration:**
- Bucket: `candidate-documents`
- Folder structure: `{candidate_id}/{application_id}/{document_type}/{file_name}`
- Encryption: AES-256 at rest
- Access: Private, signed URLs only
- Versioning: Enabled
- Lifecycle policy: Archive to cold storage after 1 year

**Error Handling:**
- Upload failure: Retry 3 times, show error message
- Invalid file type: "Only PDF, DOC, DOCX, JPG, PNG files allowed"
- File size exceeded: "Maximum file size is 5 MB"
- Virus detected: "File contains malware and cannot be uploaded"
- Storage quota exceeded: Alert admin, block uploads

---

### 2.3 HR SCREENING & SCHEDULING

#### FR-3.1: Candidate Screening Dashboard
- **Requirement ID:** FR-3.1
- **Priority:** HIGH
- **Description:** Recruiter reviews submitted Form-1 applications and makes shortlist decision

**Detailed Specifications:**

**Dashboard Components:**

**1. Application List Table:**

| Column | Description | Sortable | Filterable |
|--------|-------------|----------|------------|
| `Candidate Name` | Full name from Form-1 | Yes | Yes (search) |
| `Applied For` | Desired role | Yes | Yes (dropdown) |
| `Experience` | Years of experience | Yes | Yes (range) |
| `Qualification` | Highest qualification | Yes | Yes (dropdown) |
| `Location` | Current location | Yes | Yes (search) |
| `Applied On` | Form-1 submission date | Yes | Yes (date range) |
| `Status` | Current application status | Yes | Yes (dropdown) |
| `Actions` | Quick actions (View, Shortlist, Reject) | - | - |

**2. Filters:**
- Department: Dropdown
- Role: Dropdown (filtered by department)
- Experience: Range slider (0-30 years)
- Qualification: Multi-select (12th, Graduate, Post-Graduate)
- Location: Multi-select (city dropdown)
- Submission Date: Date range picker
- Status: Multi-select (Form-1 Submitted, Eligible, etc.)

**3. Quick Stats Cards:**
- Total Applications (this week)
- Pending My Review
- Shortlisted (this week)
- Rejected (this week)

**4. Actions:**
- **View Profile:** Opens modal with full candidate details (Form-1 data, resume link)
- **Shortlist:** Mark for interview scheduling, opens scheduling form
- **Reject:** Mark as rejected, select reason from dropdown + optional custom text
- **Bulk Actions:** Select multiple candidates, bulk shortlist or reject

**Process Flow:**

**1. Recruiter Login:**
- Lands on Screening Dashboard
- See applications assigned to them (by department/branch)

**2. Review Application:**
- Click "View Profile" on candidate
- Modal opens with:
  - Personal details (Name, Email, Phone, DOB, Gender, Location)
  - Professional details (Company, Designation, Experience, Desired Role)
  - Qualification
  - Resume download link
  - Application date and status
  - Eligibility check result (auto-populated)
- Recruiter reviews information

**3. Shortlist Decision:**
- Click "Shortlist" button
- Opens interview scheduling form (see FR-3.2)
- Or click "Schedule Later" to shortlist without scheduling

**4. Reject Decision:**
- Click "Reject" button
- Modal opens with rejection reason dropdown:
  - Insufficient experience
  - Qualification mismatch
  - Location preference mismatch
  - Overqualified
  - Other (custom text)
- Confirm rejection
- System updates status to "Rejected - {Reason}"
- Automated rejection email/WhatsApp sent to candidate

**5. Bulk Actions:**
- Select multiple candidates using checkboxes
- Click "Bulk Shortlist" or "Bulk Reject"
- Confirm action
- System processes in background

**Database Tables:**
- `candidate_applications` (application_id, candidate_id, role_id, recruiter_assigned_id, status, rejection_reason)
- `application_status_log` (log_id, application_id, status, timestamp, reason, updated_by_user_id)

**API Endpoints:**
- `GET /api/applications?recruiter_id={id}&status=Form-1 Submitted` - Get applications for screening
- `GET /api/applications/{application_id}` - Get full application details
- `PUT /api/applications/{application_id}/shortlist` - Shortlist candidate
- `PUT /api/applications/{application_id}/reject` - Reject candidate with reason
- `POST /api/applications/bulk-action` - Bulk shortlist or reject

**Rejection Notification (Automated):**

**Email Template:**
```
Subject: Application Update - [Role] at SFSPL

Dear [Candidate Name],

Thank you for your interest in the [Role] position at Sampurna Financial Services.

After careful review of your application, we regret to inform you that we are unable to move forward with your candidacy at this time.

Reason: [Rejection Reason]

We encourage you to apply for other positions that match your profile. You can view current openings at [Careers Portal Link].

We wish you the best in your job search.

Best regards,
HR Team
SFSPL
```

**WhatsApp Template:**
```
Hi [Name],

Thank you for applying to SFSPL. Unfortunately, we're unable to proceed with your application for [Role] at this time.

We encourage you to explore other opportunities on our careers page: [Link]

Best wishes for your job search!
```

**Error Handling:**
- No applications found: "No applications pending review at this time"
- Load failure: Retry 3 times, show error message
- Rejection email failure: Queue for retry, alert admin

---

#### FR-3.2: Interview Scheduling
- **Requirement ID:** FR-3.2
- **Priority:** HIGH
- **Description:** Schedule interview with candidate, assign interviewer, set venue details

**Detailed Specifications:**

**UI Components:**

**1. Interview Scheduling Form:**

| Field | Type | Required | Validation |
|-------|------|----------|-----------|
| `interview_date` | Date | Yes | Future date, not weekend (configurable) |
| `interview_time` | Time | Yes | Business hours (9 AM - 6 PM) |
| `interview_duration` | Select | Yes | 30 min, 45 min, 1 hour, 1.5 hours |
| `venue_location` | Select | Yes | Dropdown: Head Office, Branch 1, Branch 2, etc. |
| `venue_address` | Text | Auto-filled | Based on location selection |
| `venue_room` | Text | No | E.g., "Conference Room A" |
| `parking_available` | Checkbox | - | Show parking instructions if checked |
| `parking_instructions` | Text | No | Max 200 chars |
| `reporting_time` | Time | Yes | Default: 15 min before interview |
| `interviewer_1` | Select | Yes | Dropdown of interviewers (filtered by availability) |
| `interviewer_2` | Select | No | Optional second interviewer |
| `interviewer_3` | Select | No | Optional third interviewer |
| `interview_type` | Select | Yes | Technical, HR, Managerial, Panel |
| `notes` | Textarea | No | Internal notes for interviewers, max 500 chars |

**2. Calendar View (Alternative UI):**
- Month/Week/Day view toggle
- Shows scheduled interviews
- Drag-and-drop to reschedule
- Color-coded by status (Scheduled, Completed, Cancelled)
- Click on slot to schedule new interview

**3. Interviewer Availability Check:**
- Real-time availability checking
- Shows conflicting interviews
- Suggests next available slot

**Process Flow:**

**1. Initiate Scheduling:**
- Recruiter shortlists candidate (from FR-3.1)
- Opens interview scheduling form
- Or clicks "Schedule Interview" from dashboard

**2. Fill Scheduling Form:**
- Select interview date and time
- System checks interviewer availability
- If conflict: Show warning "Interviewer has another interview at this time"
- Select venue and room
- Assign interviewers (1-3 panel members)
- Add internal notes if needed

**3. Submit Schedule:**
- Validate all fields
- Insert record into `interviews` table
- Generate unique QR code for interview (see FR-4.1)
- Update `candidate_applications` status to "Interview Scheduled"
- Trigger notifications (see FR-3.2.1)

**4. Notifications Triggered:**

**To Candidate (WhatsApp + Email):**
```
🎯 Interview Scheduled!

Dear [Name],

Your interview for [Role] is scheduled:

📅 Date: [Date]
🕐 Time: [Time]
📍 Venue: [Address]
🚗 Parking: [Instructions]

⏰ Please arrive by [Reporting Time]

📲 On arrival, scan this QR code at reception:
[QR Code Image]

Documents to bring:
- Valid ID proof
- Printed resume
- Certificates (if available)

For queries, contact [HR Contact]

Best of luck!
HR Team, SFSPL
```

**To Interviewers (Email):**
```
Subject: Interview Assigned - [Candidate Name] for [Role]

Dear [Interviewer Name],

You have been assigned to interview [Candidate Name] for the [Role] position.

Interview Details:
Date: [Date]
Time: [Time]
Duration: [Duration]
Venue: [Location], [Room]

Candidate Profile:
[View Profile Link]
[Download Resume]

Panel Members:
- [Interviewer 1]
- [Interviewer 2]

Please review the candidate profile and prepare accordingly.

Notes: [Internal Notes]

Thanks,
HR Team
```

**5. Rescheduling:**
- Recruiter/HR can reschedule up to 24 hours before interview
- Opens same form with prefilled data
- Updates interview record
- Sends reschedule notification to candidate and interviewers

**Database Tables:**
- `interviews` (interview_id, application_id, interview_date, interview_time, interview_duration, venue_location, venue_address, venue_room, reporting_time, interview_type, scheduled_by_user_id, candidate_type, status, created_at, updated_at)
- `interview_panel` (panel_id, interview_id, interviewer_user_id, role)
- `interview_status_log` (log_id, interview_id, status, timestamp, updated_by)

**API Endpoints:**
- `GET /api/interviewers/availability?date={date}&time={time}` - Check interviewer availability
- `POST /api/interviews` - Schedule interview
- `GET /api/interviews?recruiter_id={id}` - Get interviews scheduled by recruiter
- `PUT /api/interviews/{interview_id}` - Reschedule interview
- `DELETE /api/interviews/{interview_id}` - Cancel interview

**Business Rules:**
- Interview date: Min 2 days from today, max 30 days
- Interview time: Business hours only (9 AM - 6 PM)
- No interviews on weekends (configurable)
- No interviews on company holidays (from holidays table)
- Interviewer availability: Max 4 interviews per day
- Interview duration: Min 30 min, max 2 hours

**Error Handling:**
- Interviewer conflict: "Interviewer not available at this time. Suggested slots: [List]"
- Past date selected: "Interview date must be in the future"
- Notification failure: Queue for retry, show warning to recruiter

---

(Continued in next response due to length...)

Would you like me to continue with the remaining sections of the SRS document?