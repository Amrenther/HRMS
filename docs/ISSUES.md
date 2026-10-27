# HRMS Project — GitHub Issues Backlog & Task Catalog

## Document Metadata
- **Project:** Human Resource Management System (HRMS)
- **Client Organization:** Adhithiya Solutions
- **Source Documents:** [docs/SRS.md](docs/SRS.md) (v1.4.0) & [docs/MILESTONES.md](docs/MILESTONES.md)
- **Total Issues:** 24 Well-Organized End-to-End Issues
- **Target Execution Duration:** 30 Calendar Days (October 28, 2026 – November 26, 2026)
- **Document Status:** Refined Baseline Task Catalog for AI-Assisted Implementation

---

## Executive Summary & Milestone Distribution

This document translates the complete functional, technical, non-functional, and compliance requirements from the HRMS SRS and Milestone Plan into **24 actionable, full-stack GitHub issues**. Each issue is structured as an end-to-end vertical slice containing database schemas, backend API endpoints, frontend UI components, authorization guards, validation logic, audit hooks, and testable acceptance criteria.

> **Schedule risk:** October 28–November 26, 2026 is the proposed 30-calendar-day schedule, not a completion guarantee. Milestones 1 and 3 are particularly tight; timely client decisions on leave policy, approval routing, payroll divisor/rounding, statutory rules, and SMTP access are required before the related acceptance gates can close.

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              30-DAY ISSUE DISTRIBUTION                                │
├────────────────────────────────────────────────────────────────────────────────────────┤
│ • Milestone 1 (Days 01–10: Oct 28 – Nov 06): Issues #01 to #07 (7 Issues)               │
│   Theme: Monorepo Foundation, 3-Tier RBAC, Organization Settings & Leave Management     │
│   Review Checkpoint: Friday, November 06, 2026 (Client Demonstration)                  │
│                                                                                        │
│ • Milestone 2 (Days 11–17: Nov 07 – Nov 13): Issues #08 to #13 (6 Issues)               │
│   Theme: Daily Attendance Capture, Timesheet Logger, Goal Setting & Appraisals         │
│   Review Checkpoint: Friday, November 13, 2026 (Client Demonstration)                  │
│                                                                                        │
│ • Milestone 3 (Days 18–24: Nov 14 – Nov 20): Issues #14 to #19 (6 Issues)               │
│   Theme: Attendance Precedence Reconciliation, Payroll Engine, LOP & PDF Payslips       │
│   Review Checkpoint: Friday, November 20, 2026 (Client Demonstration)                  │
│                                                                                        │
│ • Milestone 4 (Days 25–30: Nov 21 – Nov 26): Issues #20 to #24 (5 Issues)               │
│   Theme: System Audit Viewer, Security Hardening, Usability QA, Seed Scripts & Handover │
│   Final Handover Sign-off: Thursday, November 26, 2026                                 │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Table of Contents

- [Milestone 1: Foundation, Access Control & Complete Leave Management](#milestone-1-foundation-access-control--complete-leave-management)
  - [Issue #01: Monorepo Scaffolding, Shared Types & Database Configuration](#issue-01-monorepo-scaffolding-shared-types--database-configuration)
  - [Issue #02: Authentication System, JWT in HttpOnly Cookies & Session Management](#issue-02-authentication-system-jwt-in-httponly-cookies--session-management)
  - [Issue #03: 3-Tier RBAC, Super User Permission Builder & Employee Management](#issue-03-3-tier-rbac-super-user-permission-builder--employee-management)
  - [Issue #04: Organization Settings & Centralized Holiday Calendar](#issue-04-organization-settings--centralized-holiday-calendar)
  - [Issue #05: Leave Policy Engine, Dynamic Leave Types & Baseline Seeding](#issue-05-leave-policy-engine-dynamic-leave-types--baseline-seeding)
  - [Issue #06: Leave Reservation Engine, Application Portal & Balance Tracking](#issue-06-leave-reservation-engine-application-portal--balance-tracking)
  - [Issue #07: Multi-Mode Leave Approval Workflow & Transactional Notifications](#issue-07-multi-mode-leave-approval-workflow--transactional-notifications)
- [Milestone 2: Performance Management & Daily Attendance](#milestone-2-performance-management--daily-attendance)
  - [Issue #08: Daily Attendance Web Clock-In/Clock-Out System](#issue-08-daily-attendance-web-clock-inclock-out-system)
  - [Issue #09: Attendance Missed Punch Regularization Workflow](#issue-09-attendance-missed-punch-regularization-workflow)
  - [Issue #10: Daily Task Logger, Timesheet Validation & Same-Day Edit Lock](#issue-10-daily-task-logger-timesheet-validation--same-day-edit-lock)
  - [Issue #11: Manager Timesheet Review Console & Weekly Coaching Rating](#issue-11-manager-timesheet-review-console--weekly-coaching-rating)
  - [Issue #12: Goal Setting & Progress Tracking Workflow](#issue-12-goal-setting--progress-tracking-workflow)
  - [Issue #13: Appraisal Parameter Builder, Periodic Cycles & Evaluation Orchestration](#issue-13-appraisal-parameter-builder-periodic-cycles--evaluation-orchestration)
- [Milestone 3: Attendance Reconciliation & Payroll Engine](#milestone-3-attendance-reconciliation--payroll-engine)
  - [Issue #14: Monthly Attendance Precedence, Auto-Aggregation & Audit Override Sheet](#issue-14-monthly-attendance-precedence-auto-aggregation--audit-override-sheet)
  - [Issue #15: Salary Component Builder & Employee Salary Structure Assignment](#issue-15-salary-component-builder--employee-salary-structure-assignment)
  - [Issue #16: Unified Attendance- and Leave-Linked Salary & LOP Computation Engine](#issue-16-unified-attendance--and-leave-linked-salary--lop-computation-engine)
  - [Issue #17: Pre-Payroll Review Grid, Manual Adjustments & Monthly Batch Freeze](#issue-17-pre-payroll-review-grid-manual-adjustments--monthly-batch-freeze)
  - [Issue #18: Vector PDF Payslip Generator, Authenticated Streaming & Individual Regeneration](#issue-18-vector-pdf-payslip-generator-authenticated-streaming--individual-regeneration)
  - [Issue #19: Batch Payslip Email Dispatcher & Bank Payment Reconciliation Reports](#issue-19-batch-payslip-email-dispatcher--bank-payment-reconciliation-reports)
- [Milestone 4: Integration, Security, Audit & Final Handover](#milestone-4-integration-security-audit--final-handover)
  - [Issue #20: System Audit Log Engine & Super User Read-Only Viewer](#issue-20-system-audit-log-engine--super-user-read-only-viewer)
  - [Issue #21: Centralized In-App Notification Center & Background Cron Reminders](#issue-21-centralized-in-app-notification-center--background-cron-reminders)
  - [Issue #22: Comprehensive Security Audit, Route Protection & Rate Limiting](#issue-22-comprehensive-security-audit-route-protection--rate-limiting)
  - [Issue #23: Cross-Browser Compatibility, Mobile Responsiveness & Usability QA](#issue-23-cross-browser-compatibility-mobile-responsiveness--usability-qa)
  - [Issue #24: Seed Data Script, Production Configuration, API Collection & User Manuals](#issue-24-seed-data-script-production-configuration-api-collection--user-manuals)
- [Traceability Matrix: Requirements to Issues](#traceability-matrix-requirements-to-issues)

---

## Milestone 1: Foundation, Access Control & Complete Leave Management
**Timeline:** Days 01–10 (October 28, 2026 – November 06, 2026)  
**Deliverable Checkpoint:** Friday, November 06, 2026 (Client Demonstration)

---

### Issue #01: Monorepo Scaffolding, Shared Types & Database Configuration
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-ORG-001`, Section 1.2, Section 8, Section 10.3
- **Suggested Labels:** `milestone-1`, `foundation`, `backend`, `frontend`, `devops`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`, `packages/shared-types`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Initialize the production monorepo workspace using npm workspaces (Turborepo or other orchestrators remain optional technical proposals). Scaffold the Express.js API backend and two distinct React/Vite frontend applications: the **Admin & Manager Portal** and the **Employee Self-Service Portal**. Use TypeScript, Tailwind CSS, MongoDB/Mongoose, and Zod as selected. Do not introduce Next.js. Configure shared contracts, environment validation, local storage folders, and MongoDB health monitoring.

#### 2. Technical Scope
- **Directory Structure (npm workspaces):**
  - `apps/api`: Node.js LTS version confirmed at kickoff, Express.js, TypeScript, MongoDB/Mongoose, and Zod.
  - `apps/admin-portal`: React, Vite, TypeScript, and Tailwind CSS.
  - `apps/employee-portal`: React, Vite, TypeScript, and Tailwind CSS.
  - `packages/shared-types`: Common TypeScript DTOs, Enums, Zod validation schemas, and API response wrappers.
- **Backend Infrastructure:**
  - Express setup with strict CORS whitelist, Helmet security headers, JSON parser, and cookie parser.
  - Mongoose connection helper with auto-reconnect and index creation.
  - Zod-based environment variable validation on boot (`process.env` schema verifying `MONGO_URI`, `PORT`, `JWT_SECRET`, etc.; halts if variables are missing).
  - Global error handler returning structured JSON (`{ success: false, error: { code, message } }`).
  - Provisioning of storage directories for local file uploads: `/uploads/avatars`, `/uploads/logos`, and private `/uploads/payslips` (ensuring payslips are not publicly served).
- **Frontend Infrastructure:**
  - Vite configurations with path aliases (`@/...`).
  - Axios or Fetch client instance configured with base URL, credential support (`credentials: 'include'`), and response error interceptors.

#### 3. Acceptance Criteria
- [ ] Running `npm run dev` from root concurrently launches API (port 5000), Admin Portal (port 5173), and Employee Portal (port 5174) cleanly without compilation errors.
- [ ] Health check endpoint `GET /api/health` returns `HTTP 200` with uptime, database status `connected`, and memory metrics.
- [ ] Shared TypeScript interfaces and Zod schemas in `packages/shared-types` are consumable by both backend and frontends without build-step friction.
- [ ] Missing required environment variables cause immediate startup failure with clear console error.
- [ ] Local folders `/uploads/avatars`, `/uploads/logos`, and private `/uploads/payslips` are automatically created on startup with proper permissions.

#### 4. Dependencies
- **Blocked By:** None
- **Blocks:** Issue #02, Issue #03, Issue #04

---

### Issue #02: Authentication System, JWT in HttpOnly Cookies & Session Management
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-AUTH-001`, `FR-AUTH-002`, `FR-AUTH-003`, `FR-AUTH-004`, `FR-AUTH-006`, `NFR-SEC-001`, `NFR-SEC-002`, `NFR-SEC-003`, `NFR-SEC-004`, `NFR-SEC-005`
- **Suggested Labels:** `milestone-1`, `security`, `auth`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Deliver secure email-and-password authentication using JWTs stored in `HttpOnly`, `SameSite=Strict` cookies. Implement `bcryptjs` password hashing at 12 rounds, session validation, password reset using a 15-minute email token, password-change token invalidation, and protected portal entry points. CSRF-control mechanics and account-level lockout are implementation proposals, not confirmed SRS requirements.

#### 2. Technical Scope
- **Database Schema (`User`):**
  ```typescript
  {
    email: { type: String, required: true, unique: true, lowercase: true, trim: true },
    passwordHash: { type: String, required: true },
    role: { type: String, enum: ['super_user', 'sub_user', 'employee'], required: true },
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee' },
    isActive: { type: Boolean, default: true },
    tokenVersion: { type: Number, default: 1 }, // Used to invalidate tokens on password change
    failedLoginAttempts: { type: Number, default: 0 },
    lockUntil: { type: Date },
    passwordChangedAt: { type: Date },
    mustChangePassword: { type: Boolean, default: false },
    passwordResetTokenHash: String,
    passwordResetExpiresAt: Date
  }
  ```
- **Backend API Endpoints:**
  - `POST /api/v1/auth/login`: Validates input with Zod, checks lock status, verifies bcrypt hash (>= 12 rounds), signs JWT (payload: userId, role, employeeId, tokenVersion), sets `auth_token` HttpOnly cookie.
  - `POST /api/v1/auth/logout`: Clears auth cookie with matching path/domain/flags.
  - `GET /api/v1/auth/me`: Validates cookie and returns sanitized user profile (omitting password hash).
  - `PUT /api/v1/auth/password`: Verifies current password, updates to new hash, increments `tokenVersion` (invalidating active sessions across all devices).
  - `POST /api/v1/auth/password-reset/request` and `POST /api/v1/auth/password-reset/confirm`: Implement `FR-AUTH-004` with a hashed, single-use 15-minute reset token.
- **Security & CSRF Controls:**
  - Cookies set with `httpOnly: true`, `sameSite: 'strict'`, `secure: process.env.NODE_ENV === 'production'`.
  - [Proposed security control — pending technical approval] Use an appropriate CSRF defence for cookie-authenticated state-changing requests.
  - [Proposed business/security control — pending client approval] Optional account-level lockout may use `failedLoginAttempts` and `lockUntil`; it must not change the confirmed IP-based rate-limit response.
  - IP-based rate limiting on `/api/v1/auth/login`: maximum 10 requests per 15 minutes per IP, then `HTTP 429 Too Many Requests` (`NFR-SEC-005`).
- **Frontend Screens:** Modern, branded login pages in both portals with validation, error states, and session context provider.

#### 3. Acceptance Criteria
- [ ] Passwords stored using bcrypt with >= 12 salt rounds; plaintext passwords never logged or returned.
- [ ] Successful login sets an `HttpOnly`, `SameSite=Strict` cookie; JavaScript `document.cookie` cannot access it.
- [ ] Protected endpoints return `HTTP 401 Unauthorized` when cookie is missing, tampered with, or expired.
- [ ] The 11th login request from one IP within 15 minutes receives `HTTP 429`; this is the confirmed SRS control.
- [ ] Password-reset tokens expire after 15 minutes and are single-use; a seeded user with `mustChangePassword: true` may authenticate only to complete a password change until the flag is cleared.
- [ ] [Proposed — pending approval] If account lockout is enabled, its threshold, duration, response, and interaction with IP rate limiting are separately approved and tested.
- [ ] Changing password invalidates previous JWT tokens via `tokenVersion` check.
- [ ] Unauthenticated requests cannot access any portal view; redirect to `/login` is automatic.

#### 4. Dependencies
- **Blocked By:** Issue #01
- **Blocks:** Issue #03, Issue #04, Issue #06

---

### Issue #03: 3-Tier RBAC, Super User Permission Builder & Employee Management
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-AUTH-005`, `FR-EMP-001`, `FR-EMP-002`, `FR-EMP-003`, `FR-EMP-004`, `FR-AUDIT-001`, `NFR-PRIV-001`
- **Suggested Labels:** `milestone-1`, `rbac`, `employee-management`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 2.0 Days

#### 1. Description & Objective
Implement the 3-tier Role-Based Access Control model and the dynamic Super User Permission Builder. The Super User can create Sub-Users (HR/Department Managers) and assign granular permissions via 12 modular boolean flags scoped by department. Build the complete Employee Directory with profile attributes, reporting manager hierarchy, and the `isEligibleForEarnedLeave` flag. Enforce data protection: sensitive bank details and statutory numbers must never be exposed to unauthorized users or logged.

#### 2. Technical Scope
- **Database Schema (`Employee`):**
  ```typescript
  {
    employeeCode: { type: String, required: true, unique: true },
    firstName: { type: String, required: true },
    lastName: { type: String, required: true },
    email: { type: String, required: true, unique: true },
    phone: String,
    department: { type: String, required: true },
    designation: { type: String, required: true },
    joiningDate: { type: Date, required: true },
    confirmationDate: Date,
    reportingManagerId: { type: Schema.Types.ObjectId, ref: 'Employee' },
    isEligibleForEarnedLeave: { type: Boolean, default: false },
    earnedLeaveQuota: { type: Number, default: 12 }, // Applied only when eligibility is true
    bankDetails: {
      accountName: String,
      accountNumber: String,
      bankName: String,
      ifscCode: String
    },
    statutoryDetails: {
      panNumber: String,
      uanNumber: String,
      pfNumber: String,
      esiNumber: String
    },
    isDeleted: { type: Boolean, default: false }
  }
  ```
- **Permission Builder Flags (Sub-User Model):**
  `canManageEmployees`, `canApproveLeaves`, `canManageLeavePolicy`, `canAdjustLeaveBalances`, `canManageAttendance`, `canReviewProductivity`, `canManageGoals`, `canConfigureAppraisalParams`, `canManageAppraisals`, `canConfigureSalary`, `canProcessPayroll`, `canExportReports`.
- **Backend API:**
  - `POST/GET/PUT/DELETE /api/v1/employees` (department query filtering, soft-delete via `isDeleted: true`).
  - `POST/GET/PUT /api/v1/sub-users` (manage Sub-User accounts, departmental scope, and permission flags).
  - Middleware: `requirePermission(permissionFlag)` checking active Sub-User rights and departmental boundary.
- **Frontend UI (Admin Portal):**
  - Sub-User Management Console with interactive 12-checkbox permission builder matrix.
  - Employee Directory with search, department filtering, pagination, and Create/Edit drawers.
- **Audit Logging:** Permission updates, employee creation, and changes to `isEligibleForEarnedLeave` write immutable records to `FR-AUDIT-001` (excluding sensitive bank/statutory numbers from diff payloads).

#### 3. Acceptance Criteria
- [ ] Super User has unrestricted access across all endpoints; Sub-Users without the required permission flag are blocked with `HTTP 403 Forbidden`.
- [ ] Department scoping: Sub-Users with departmental restrictions can only view/modify employees in their assigned departments.
- [ ] Employees are initialized with `isEligibleForEarnedLeave: false`; an ineligible employee has an EL allocation of 0 even though the per-employee `earnedLeaveQuota` default is 12.
- [ ] Soft delete is enforced: deleting an employee sets `isDeleted: true` and retains all historical foreign key relationships.
- [ ] Sensitive data protection: Bank details and statutory IDs are stripped from responses unless requested by authorized Super User/HR.
- [ ] Permission updates on Sub-Users write immutable records to the audit log.

#### 4. Dependencies
- **Blocked By:** Issue #02
- **Blocks:** Issue #04, Issue #05, Issue #06, Issue #08

---

### Issue #04: Organization Settings & Centralized Holiday Calendar
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-ORG-001`, `FR-ORG-002`, `FR-ORG-003`, `FR-LEAVE-009`, `FR-REP-005`
- **Suggested Labels:** `milestone-1`, `org-settings`, `holidays`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Build the Organization Settings management module and Annual Holiday Calendar. The Super User configures organization details, company logo (stored locally in `/uploads/logos/` and stamped on future payslips), weekly-off schedule (e.g. Saturday/Sunday), and leave/financial year calendar boundaries. Super Users create and publish the organization Holiday Calendar, which exports to PDF and feeds downstream leave and attendance calculations.

#### 2. Technical Scope
- **Database Schema:**
  - `OrganizationSettings` (singleton): `companyName`, `companyAddress`, `taxIdNumber`, `companyLogoPath`, `weeklyOffDays` (array of numbers: 0=Sun, 6=Sat), `leaveYearStartMonth` (1–12), `financialYearStartMonth` (1–12).
  - `Holiday`: `name`, `date`, `isOptional`, `description`, `year`.
- **Backend API:**
  - `GET /api/v1/organization/settings`, `PUT /api/v1/organization/settings`.
  - `POST /api/v1/organization/logo`: Handles multipart logo upload, saves to `/uploads/logos/` with strict size/type validation.
  - `GET/POST/PUT/DELETE /api/v1/holidays`.
  - `GET /api/v1/holidays/export/pdf`: Generates clean PDF schedule using `PDFKit`.
- **Frontend UI:**
  - Admin Portal: Organization Profile tab with logo uploader; Holiday Calendar editor.
  - Employee Portal: Read-only visual Holiday Calendar schedule with "Download PDF" button.
- **Audit Logging:** Modifications to Organization Settings or Holiday Calendar write change records to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] Logo upload rejects non-image MIME types and files > 2 MB; valid upload saves to `/uploads/logos/` and updates DB path.
- [ ] Weekly-off configuration (e.g., `[0, 6]` for Sat/Sun) is accessible via API and consumed by attendance calculation modules.
- [ ] Holiday Calendar PDF export downloads a branded, cleanly formatted annual schedule.
- [ ] Organization setting modifications write before/after change records to the audit trail.

#### 4. Dependencies
- **Blocked By:** Issue #03
- **Blocks:** Issue #05, Issue #07, Issue #08, Issue #14, Issue #18

---

### Issue #05: Leave Policy Engine, Dynamic Leave Types & Baseline Seeding
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-LEAVE-001`, `FR-LEAVE-002`, `FR-LEAVE-003`, `FR-LEAVE-004`, `FR-EMP-002`
- **Suggested Labels:** `milestone-1`, `leave-management`, `policy-engine`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Implement the Leave Policy Engine and Dynamic Leave Type Builder. Model the stated baseline entitlements: 12 Sick Leave (SL) and 12 Casual Leave (CL) for active employees, plus EL only for employees where `isEligibleForEarnedLeave === true`, using `earnedLeaveQuota` (default 12). Do not claim a confirmed allocation schedule: annual upfront credit, monthly accrual, mid-year prorating, carry-forward, encashment, and EL eligibility timing remain pending client confirmation.

#### 2. Technical Scope
- **Database Schema:**
  - `LeaveType`: `name`, `code` (`SL`, `CL`, `EL`, or custom), `description`, `annualQuota`, `isPaid` (boolean), `isCarryForwardAllowed` (boolean), `maxCarryForwardDays`, `requiresProofThresholdDays`.
  - `EmployeeLeaveBalance`: `employeeId`, `leaveTypeId`, `year`, `totalAllocated`, `usedDays`, `reservedDays`, `availableDays`.
- **Backend API:**
  - `GET/POST/PUT/DELETE /api/v1/leave/types`.
  - `GET /api/v1/leave/balances/employee/:id`.
  - Service: `LeaveBalanceService.initializeEmployeeBalances(employeeId)`.
- **Frontend UI (Admin Portal):**
  - Leave Policy Configuration screen showing system leave types and custom leave builder modal.
- **Client Decision Note (D2, Q2, Q3, Q7) [Pending Client Confirmation]:** The baseline quantities are confirmed, but allocation timing is not. Support a configurable proposal for upfront annual credit; do not enable monthly accrual, any prorating formula, carry-forward, encashment, or EL eligibility rule until the client confirms each rule.

#### 3. Acceptance Criteria
- [ ] Given an approved allocation policy, 12 SL and 12 CL are allocated to eligible active employees and EL is allocated as `earnedLeaveQuota` only when `isEligibleForEarnedLeave === true`; otherwise EL is 0.
- [ ] Until D2/Q2/Q3/Q7 are decided, tests demonstrate the configured upfront-credit proposal without representing it as a client-approved accrual, prorating, carry-forward, encashment, or EL-eligibility rule.
- [ ] Admin can add custom leave types (e.g. "Bereavement Leave", 5 days, Paid); newly created types become available in application forms.
- [ ] Balance integrity rule enforced: `availableDays = totalAllocated - (usedDays + reservedDays)`. Available days can never be negative.
- [ ] Leave policy edits write an audit event to `FR-AUDIT-001`.

#### 4. Dependencies
- **Blocked By:** Issue #03, Issue #04
- **Blocks:** Issue #06, Issue #07

---

### Issue #06: Leave Reservation Engine, Application Portal & Balance Tracking
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-LEAVE-005`, `FR-LEAVE-006`, `FR-LEAVE-008`, `FR-AUDIT-001`, SRS Section 9.4
- **Suggested Labels:** `milestone-1`, `leave-management`, `employee-portal`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/employee-portal`, `apps/admin-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Implement the unified Leave Balance Reservation Lifecycle and the Employee Self-Service Leave Application interface. When an employee submits a leave request, requested days are immediately placed in a **Reserved/Held** state, preventing double-booking. If approved, reserved days transition to **Confirmed/Used**; if rejected or cancelled, reserved days are immediately released back to **Available**. Implement manual balance adjustments by Super Users with mandatory recorded audit reasons.

#### 2. Technical Scope
- **Database Schema (`LeaveApplication`):**
  ```typescript
  {
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    leaveTypeId: { type: Schema.Types.ObjectId, ref: 'LeaveType', required: true },
    startDate: { type: Date, required: true },
    endDate: { type: Date, required: true },
    totalDays: { type: Number, required: true },
    isHalfDay: { type: Boolean, default: false },
    halfDaySession: { type: String, enum: ['first_half', 'second_half'] },
    reason: { type: String, required: true },
    status: { type: String, enum: ['pending', 'approved', 'rejected', 'cancelled'], default: 'pending' },
    currentStage: { type: Number, default: 1 },
    approverTimeline: [{ approverId: Schema.Types.ObjectId, stage: Number, action: String, comments: String, actionDate: Date }]
  }
  ```
- **Backend API:**
  - `POST /api/v1/leave/apply`: Atomically moves days from `availableDays` to `reservedDays` using Mongo transaction session.
  - `GET /api/v1/leave/my-applications`: Fetches paginated history for logged-in employee.
  - `POST /api/v1/leave/cancel/:id`: Releases reserved days back to available balance (allowed only before leave start date).
  - `POST /api/v1/leave/balances/adjust`: Adjusts balances; requires mandatory audit reason.
- **Frontend UI:**
  - Employee Portal: 3-click Leave Application Drawer on dashboard; real-time balance summary cards.
  - Admin Portal: Manual Balance Adjustment dialog with mandatory reason text input.

#### 3. Acceptance Criteria
- [ ] Submitting a 3-day leave request immediately decreases `availableDays` by 3 and increases `reservedDays` by 3.
- [ ] Validation blocks application if `requestedDays > availableDays`, returning a descriptive validation message.
- [ ] Cancellation prior to start date immediately restores reserved days to available balance.
- [ ] [Proposed Usability Target - Confirmed by SRS Section 9.4]: Newly onboarded employee can submit a leave request in <= 3 clicks from home dashboard.
- [ ] Manual balance adjustment without a reason string is rejected (`HTTP 400`); valid adjustment writes an immutable record to `FR-AUDIT-001`.

#### 4. Dependencies
- **Blocked By:** Issue #05
- **Blocks:** Issue #07

---

### Issue #07: Multi-Mode Leave Approval Workflow & Transactional Notifications
- **Milestone:** Milestone 1 (Foundation & Leave)
- **SRS Reference:** `FR-LEAVE-006`, `FR-LEAVE-007`, `FR-LEAVE-010`, `FR-LEAVE-011`, `FR-REP-001`, `FR-REP-005`, `FR-AUDIT-001`
- **Suggested Labels:** `milestone-1`, `workflow`, `approval-engine`, `reports`, `notifications`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Deliver the confirmed leave approval, reporting, and notification requirements for Milestone 1. `FR-LEAVE-007` confirms a configurable organization-level 1- or 2-stage hierarchy; `FR-LEAVE-011` confirms in-app and SMTP notifications for leave lifecycle events. The named routing modes and no-manager fallback below are baseline proposals from the planning documents, pending client confirmation of departmental, leave-type, and 3+ stage needs.

#### 2. Technical Scope
- **Approval Routing Engine:**
  - [Proposed baseline] Mode 1 routes to the reporting manager; Mode 2 routes to HR; Mode 3 routes manager then HR.
  - [Proposed fallback] Where no reporting manager is assigned, route to HR/Super User. Confirm this and any department-specific, per-leave-type, or 3+ stage workflow under Q1/D13 before acceptance.
- **Notification Dispatcher:**
  - In-app notification creation with unread badges.
  - Transactional email dispatch via `nodemailer` (dumps to console logger if SMTP credentials unconfigured; see D14).
- **Backend API:**
  - `GET /api/v1/leave/pending-approvals`: Scoped by approver role.
  - `POST /api/v1/leave/:id/approve`, `POST /api/v1/leave/:id/reject`.
  - `GET /api/v1/reports/leave/utilization` (supports `.xlsx` and `.csv` stream).
- **Frontend UI (Admin & Manager Portal):**
  - Manager Pending Approvals Inbox with 1-click Approve/Reject buttons and comment modal.
  - Department Leave Utilization Report table with download buttons.
- **Audit Logging:** Every approval, rejection, or cancellation writes an audit entry to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] Configured approved hierarchy routes each request through its required stage(s); final approval confirms reserved days and any rejection releases them.
- [ ] [Proposed baseline — pending Q1/D13] The documented manager-only, HR-only, and manager-then-HR modes, including no-manager fallback, behave as configured.
- [ ] Rejection at any stage immediately releases reserved days back to the employee's available balance.
- [ ] In-app badge count updates immediately upon submission for the assigned approver.
- [ ] Department Leave Utilization Report exports accurately to `.xlsx` and `.csv` matching UI data.
- [ ] **Milestone 1 Handover Gate:** All M1 acceptance criteria met; software ready for client demonstration on Friday, November 06, 2026.

#### 4. Dependencies
- **Blocked By:** Issue #06
- **Blocks:** Issue #08, Issue #09, Issue #14

---

## Milestone 2: Performance Management & Daily Attendance
**Timeline:** Days 11–17 (November 07, 2026 – November 13, 2026)  
**Deliverable Checkpoint:** Friday, November 13, 2026 (Client Demonstration)

---

### Issue #08: Daily Attendance Web Clock-In/Clock-Out System
- **Milestone:** Milestone 2 (Performance & Attendance)
- **SRS Reference:** `FR-ATT-002`, `FR-ORG-002`, `NFR-SEC-004`
- **Suggested Labels:** `milestone-2`, `attendance`, `employee-portal`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Implement web-based daily attendance capture in the Employee Portal. Employees record daily clock-in and clock-out timestamps with calculated duration. Store shift start/end times, late-arrival grace periods (default 15 mins), and half-day vs. full-day working hour thresholds (default 4 hrs / 8 hrs) as configurable parameters in system settings.

#### 2. Technical Scope
- **Database Schema (`DailyAttendance`):**
  ```typescript
  {
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    date: { type: Date, required: true },
    clockInTime: { type: Date, required: true },
    clockOutTime: Date,
    totalWorkingHours: { type: Number, default: 0 },
    status: { type: String, enum: ['present', 'half_day', 'late', 'absent'], default: 'present' },
    isRegularized: { type: Boolean, default: false },
    ipAddress: String
  }
  ```
- **Backend API:**
  - `POST /api/v1/attendance/clock-in`: Records clock-in with server timestamp.
  - `POST /api/v1/attendance/clock-out`: Calculates total hours worked and sets status.
  - `GET /api/v1/attendance/my-daily-logs`: Returns monthly logs for logged-in user.
- **Frontend UI (Employee Portal):**
  - Clock-In / Clock-Out widget on dashboard with live timer and status badge.
  - Monthly attendance punch history table with color-coded status badges.
- **Client Decision Note (D8 / Q6) [Proposed Technical Default - Pending Client Confirmation]:** Standard shift hours (9:00 AM – 6:00 PM) and 15-min grace window are configurable technical baselines pending client confirmation.

#### 3. Acceptance Criteria
- [ ] Clock-in and clock-out timestamps are generated by the server, preventing client-side device tampering.
- [ ] With client-configured thresholds (default proposal: 4 hours half-day, 8 hours full-day, 15-minute grace), the computed attendance outcome is reproducible from server timestamps. Do not introduce an unsupported `< 1 hour` rule.
- [ ] System blocks duplicate clock-ins on the same calendar date for the same employee.
- [ ] Employees can only access their own attendance logs (IDOR protected; returns `HTTP 403` on cross-employee access attempts).

#### 4. Dependencies
- **Blocked By:** Issue #03, Issue #04
- **Blocks:** Issue #09, Issue #14

---

### Issue #09: Attendance Missed Punch Regularization Workflow
- **Milestone:** Milestone 2 (Performance & Attendance)
- **SRS Reference:** `FR-ATT-003`, `FR-LEAVE-007`, `FR-AUDIT-001`
- **Suggested Labels:** `milestone-2`, `attendance`, `regularization`, `workflow`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Implement the Attendance Regularization workflow allowing employees to rectify missed clock-ins, missed clock-outs, or erroneous attendance statuses. Requests route through the configured approval hierarchy (Manager -> HR). Upon approval, the daily attendance record is updated and logged to the audit trail.

#### 2. Technical Scope
- **Database Schema (`AttendanceRegularization`):**
  ```typescript
  {
    attendanceId: { type: Schema.Types.ObjectId, ref: 'DailyAttendance' },
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    date: { type: Date, required: true },
    proposedClockIn: { type: Date, required: true },
    proposedClockOut: { type: Date, required: true },
    reason: { type: String, required: true },
    status: { type: String, enum: ['pending', 'approved', 'rejected'], default: 'pending' },
    approverId: { type: Schema.Types.ObjectId, ref: 'User' },
    actionDate: Date
  }
  ```
- **Backend API:**
  - `POST /api/v1/attendance/regularize`: Submits regularization request with reason.
  - `GET /api/v1/attendance/regularizations/pending`: Scoped pending queue for approvers.
  - `POST /api/v1/attendance/regularizations/:id/action`: Approves or rejects request.
- **Frontend UI:**
  - Employee Portal: "Regularize Punch" action button in attendance log table with modal form.
  - Admin & Manager Portal: Regularization review inbox in manager dashboard.
- **Audit Logging:** Regularization approvals update attendance and write an immutable event to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] Employee can select past date and submit proposed punch times with a mandatory reason text.
- [ ] Regularization routes through configured approval hierarchy matching leave approval mode.
- [ ] Approval updates the corresponding `DailyAttendance` record to `status: 'present'`, sets `isRegularized: true`, and writes an immutable audit record to `FR-AUDIT-001`.

#### 4. Dependencies
- **Blocked By:** Issue #08, Issue #07
- **Blocks:** Issue #14

---

### Issue #10: Daily Task Logger, Timesheet Validation & Same-Day Edit Lock
- **Milestone:** Milestone 2 (Performance & Attendance)
- **SRS Reference:** `FR-PROD-001`, `FR-PROD-002`
- **Suggested Labels:** `milestone-2`, `productivity`, `timesheet`, `employee-portal`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Build the Daily Productivity Task Logger in the Employee Portal. Employees log daily activities by specifying project/category name, task title, hours spent (supporting decimals, e.g. 2.5 hrs), completion status (*In Progress*, *Completed*, *Blocked*), and self-reported productivity notes. Enforce same-day editing lock at 23:59:59 local time.

#### 2. Technical Scope
- **Database Schema (`DailyTimesheet`):**
  ```typescript
  {
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    workDate: { type: Date, required: true },
    tasks: [{
      projectName: { type: String, required: true },
      taskTitle: { type: String, required: true },
      hoursSpent: { type: Number, required: true, min: 0.25, max: 16 },
      status: { type: String, enum: ['in_progress', 'completed', 'blocked'], required: true },
      notes: String
    }],
    totalDailyHours: { type: Number, required: true },
    isLocked: { type: Boolean, default: false }
  }
  ```
- **Backend API:**
  - `POST /api/v1/productivity/timesheet`: Validates hours and saves daily entries.
  - `GET /api/v1/productivity/my-timesheets`: Retrieves history by date range.
  - `PUT /api/v1/productivity/timesheet/:id`: Allows editing only on same calendar day (< 23:59:59).
- **Frontend UI (Employee Portal):**
  - Interactive Daily Timesheet table with dynamic row addition, live hours counter, and status badges.

#### 3. Acceptance Criteria
- [ ] System validates that total logged daily hours are > 0 and <= 16 hours per day.
- [ ] Same-day edit rule: Employees can update entries until 23:59:59 of entry date; past dates are strictly locked and read-only.
- [ ] Attempting to modify a locked timesheet returns `HTTP 403 Forbidden`.

#### 4. Dependencies
- **Blocked By:** Issue #03
- **Blocks:** Issue #11

---

### Issue #11: Manager Timesheet Review Console & Weekly Coaching Rating
- **Milestone:** Milestone 2 (Performance & Attendance)
- **SRS Reference:** `FR-PROD-003`, `FR-PROD-004`, `FR-REP-002`
- **Suggested Labels:** `milestone-2`, `productivity`, `manager-portal`, `feedback`, `reports`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Build the Manager Productivity Review Console and Weekly Rating mechanism. Department Managers view daily task submissions for their direct reports in a weekly summary view, evaluate hours spent against projects, and submit a weekly performance rating (1 to 5 scale) with constructive coaching comments.

#### 2. Technical Scope
- **Database Schema (`WeeklyProductivityReview`):**
  ```typescript
  {
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    managerId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    weekStartDate: { type: Date, required: true },
    weekEndDate: { type: Date, required: true },
    weeklyRating: { type: Number, min: 1, max: 5, required: true },
    feedbackComments: { type: String, required: true },
    reviewedAt: { type: Date, default: Date.now }
  }
  ```
- **Backend API:**
  - `GET /api/v1/productivity/team-timesheets`: Aggregates team logs by week.
  - `POST /api/v1/productivity/weekly-rating`: Submits 1–5 score with comments.
  - `GET /api/v1/reports/productivity/export`: Exports summary to `.xlsx` and `.csv`.
- **Frontend UI (Admin & Manager Portal):**
  - Team Timesheet weekly summary matrix with expandable daily task details and rating submission dialog.

#### 3. Acceptance Criteria
- [ ] Managers can only view and rate timesheets for employees assigned to their team/department scope.
- [ ] Rating field accepts integers 1 to 5 with mandatory feedback comments.
- [ ] Submitting a weekly review triggers an in-app notification to the employee.
- [ ] Productivity data exports cleanly to Excel (`.xlsx`) and CSV (`.csv`).

#### 4. Dependencies
- **Blocked By:** Issue #10
- **Blocks:** Issue #13

---

### Issue #12: Goal Setting & Progress Tracking Workflow
- **Milestone:** Milestone 2 (Performance & Attendance)
- **SRS Reference:** `FR-PERF-001`, `FR-REP-002`
- **Suggested Labels:** `milestone-2`, `performance`, `goals`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/employee-portal`, `apps/admin-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Implement the Goal Setting and Performance Tracking module. Managers or Employees can establish specific goals for an active cycle (Title, Target Completion Date, Description, Priority/Weight). Employees update self-reported progress percentage (0% to 100%) and milestones; managers review ongoing progress and post interim coaching comments.

#### 2. Technical Scope
- **Database Schema (`Goal`):**
  ```typescript
  {
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    createdBy: { type: Schema.Types.ObjectId, ref: 'User', required: true },
    cycleName: String,
    title: { type: String, required: true },
    description: String,
    targetDate: { type: Date, required: true },
    priority: { type: String, enum: ['low', 'medium', 'high'], default: 'medium' },
    weightage: { type: Number, default: 0 },
    progressPercentage: { type: Number, min: 0, max: 100, default: 0 },
    status: { type: String, enum: ['active', 'completed', 'deferred'], default: 'active' },
    comments: [{ authorId: Schema.Types.ObjectId, comment: String, createdAt: Date }]
  }
  ```
- **Backend API:**
  - `POST/GET/PUT /api/v1/performance/goals`.
  - `PUT /api/v1/performance/goals/:id/progress`: Updates percentage and notes.
  - `POST /api/v1/performance/goals/:id/comments`: Adds review comment.
- **Frontend UI:**
  - Employee Portal: Goals Dashboard with visual percentage sliders, status indicators, and comment feed.
  - Admin & Manager Portal: Team Goals tracker with rollups.

#### 3. Acceptance Criteria
- [ ] Employees can adjust progress percentage from 0% to 100% and log milestone notes.
- [ ] Managers can add feedback comments on any assigned goal.
- [ ] Visual progress bars update in real time with status colors (green = completed, blue = on track, red = overdue).

#### 4. Dependencies
- **Blocked By:** Issue #03
- **Blocks:** Issue #13

---

### Issue #13: Appraisal Parameter Builder, Periodic Cycles & Evaluation Orchestration
- **Milestone:** Milestone 2 (Performance & Attendance)
- **SRS Reference:** `FR-PERF-002`, `FR-PERF-003`, `FR-PERF-004`, `FR-PERF-005`, `FR-PERF-006`, `FR-REP-003`, `FR-AUDIT-001`
- **Suggested Labels:** `milestone-2`, `performance`, `appraisals`, `workflow`, `reports`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 2.0 Days

#### 1. Description & Objective
Complete Milestone 2 by delivering the full Performance Appraisal Cycle. Build the Appraisal Parameter Builder allowing Super Users to configure competencies, 1–5 rating scales, and weights summing to 100%. Orchestrate the 3-step appraisal workflow: (1) Employee Self-Appraisal, (2) Manager Evaluation & Scoring, and (3) Super User Calibration & Final Sign-Off. Note: Goals and Appraisals follow their fixed review flows and are not routed through the dynamic leave approval hierarchy.

#### 2. Technical Scope
- **Database Schema:**
  - `AppraisalParameter`: `name`, `category`, `description`, `maxScore` (default 5), `weightage` (number).
  - `AppraisalCycle`: `name`, `startDate`, `endDate`, `selfReviewDeadline`, `managerReviewDeadline`, `status` (`draft`|`active`|`under_review`|`closed`).
  - `EmployeeAppraisal`: `cycleId`, `employeeId`, `selfScores`: [{ parameterId, score, comments }], `managerScores`: [{ parameterId, score, comments }], `finalCalibratedScore`: Number, `status` (`pending_self`|`pending_manager`|`pending_signoff`|`published`).
- **Backend API:**
  - `GET/POST/PUT /api/v1/performance/parameters`.
  - `POST /api/v1/performance/cycles`.
  - `POST /api/v1/performance/appraisals/self-submit`.
  - `POST /api/v1/performance/appraisals/manager-submit`.
  - `POST /api/v1/performance/appraisals/sign-off`.
- **Frontend UI:**
  - Admin Portal: Parameter Builder; Appraisal Launch Console; Score Calibration grid.
  - Employee Portal: Structured Self-Appraisal form with scorecards and text commentary.
- **Audit Logging:** Score calibrations and final publication by Super User write an audit record to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] Parameter builder enforces that active evaluation criteria weights sum exactly to 100%.
- [ ] Strict sequential workflow: Employee self-appraisal must be submitted before Manager review unlocks; Super User must sign off before score becomes visible to employee.
- [ ] Score calibrations and final sign-off write an audit event to `FR-AUDIT-001`.
- [ ] Department appraisal summary report exports cleanly to Excel (`.xlsx`).
- [ ] **Milestone 2 Handover Gate:** All M2 acceptance criteria met; software ready for client demonstration on Friday, November 13, 2026.

#### 4. Dependencies
- **Blocked By:** Issue #11, Issue #12
- **Blocks:** Issue #20

---

## Milestone 3: Attendance Reconciliation & Payroll Engine
**Timeline:** Days 18–24 (November 14, 2026 – November 20, 2026)  
**Deliverable Checkpoint:** Friday, November 20, 2026 (Client Demonstration)

---

### Issue #14: Monthly Attendance Precedence, Auto-Aggregation & Audit Override Sheet
- **Milestone:** Milestone 3 (Reconciliation & Payroll)
- **SRS Reference:** `FR-ATT-001`, `FR-ATT-004`, `FR-ATT-005`, `FR-AUDIT-001`
- **Suggested Labels:** `milestone-3`, `attendance`, `reconciliation`, `payroll-prerequisite`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Implement the Monthly Attendance Precedence and Aggregation Engine. The system aggregates clock-in/out records, weekly-offs (`FR-ORG-002`), public holidays (`FR-LEAVE-009`), and approved leaves (`FR-LEAVE-005`) to automatically pre-fill the monthly attendance sheet. Define an "absence" as a working day with no punch, no approved leave, and not a holiday/weekly-off. Allow HR Sub-Users to review and manually override figures, requiring a mandatory recorded audit reason.

#### 2. Technical Scope
- **Database Schema (`MonthlyAttendanceSummary`):**
  ```typescript
  {
    employeeId: { type: Schema.Types.ObjectId, ref: 'Employee', required: true },
    month: { type: Number, required: true },
    year: { type: Number, required: true },
    totalCalendarDays: Number,
    scheduledWorkingDays: Number,
    presentDays: Number,
    paidLeaveDays: Number,
    holidayDays: Number,
    weeklyOffDays: Number,
    unexcusedAbsentDays: Number,
    totalLOPDays: Number,
    isConfirmed: { type: Boolean, default: false },
    overrides: [{ field: String, oldValue: Number, newValue: Number, reason: String, updatedBy: Schema.Types.ObjectId, timestamp: Date }]
  }
  ```
- **Backend API:**
  - `POST /api/v1/payroll/attendance/pre-fill`: Runs aggregation query for specified month/year.
  - `GET /api/v1/payroll/attendance/sheet`: Returns tabular reconciliation grid.
  - `PUT /api/v1/payroll/attendance/override`: Overrides present/leave/LOP days with mandatory audit reason.
- **Frontend UI (Admin Portal):**
  - Monthly Attendance Grid with pre-populated values, color-coded cells, inline edit fields, and audit reason modal.
- **Audit Logging:** Overrides write before/after values with the mandatory user reason to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] Aggregation computes `presentDays`, `paidLeaveDays`, `unexcusedAbsentDays`, and `totalLOPDays` from raw attendance and approved leave records; an absence is only a scheduled working day with no punch and no approved leave.
- [ ] Public holidays and configured weekly-off days are excluded from unexcused absence/LOP calculation.
- [ ] Any manual override requires an audit reason string; writes before/after values to `FR-AUDIT-001`.

#### 4. Dependencies
- **Blocked By:** Issue #07, Issue #08, Issue #09
- **Blocks:** Issue #16, Issue #17

---

### Issue #15: Salary Component Builder & Employee Salary Structure Assignment
- **Milestone:** Milestone 3 (Reconciliation & Payroll)
- **SRS Reference:** `FR-PAY-001`, `FR-PAY-002`, `FR-AUDIT-001`
- **Suggested Labels:** `milestone-3`, `payroll`, `salary-structure`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Build the flexible Salary Component Builder and Salary Structure Assignment module. Super Users configure recurring Earnings (Basic, HRA, Special Allowance, Conveyance, Bonus) and Deductions (Provident Fund, ESI, Professional Tax, TDS/Income Tax, Custom Deductions). Assign custom salary structures to employee profiles linking individual monthly gross amounts and itemized breakdowns. Protect sensitive salary information from unauthorized access.

#### 2. Technical Scope
- **Database Schema:**
  - `SalaryComponent`: `name`, `code`, `type` (`earning` | `deduction`), `calculationType` (`flat` | `percentage_of_basic`), `percentageValue`, `isTaxable`, `isStatutory`.
  - `EmployeeSalaryStructure`: `employeeId`, `effectiveFromDate`, `ctcAnnual`, `monthlyGross`, `earnings`: [{ componentId, amount }], `deductions`: [{ componentId, amount }], `netBasePay`: Number, `isCurrent`: Boolean.
- **Backend API:**
  - `GET/POST/PUT /api/v1/payroll/components`.
  - `GET/POST/PUT /api/v1/payroll/structures/:employeeId`.
- **Frontend UI (Admin Portal):**
  - Salary Component management console.
  - Employee Salary Assignment wizard with real-time component breakdown calculation and Gross-to-Net simulator.
- **Client Decision Note (D12 / Q5) [Proposed Technical Default - Pending Client Confirmation]:** Flat configurable amounts per employee are used as baseline; structure supports formulaic percentage of Basic.
- **Audit Logging:** Salary structure creation and edits write audit entries to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] Admin can define custom earnings and deductions with descriptive names, codes, and calculation rules.
- [ ] Assigning salary structure computes monthly gross, total deductions, and net base pay.
- [ ] Changes to employee salary structures are versioned with effective dates and logged to audit trail.
- [ ] Salary structures are accessible only to Super User and authorized HR Sub-Users (`HTTP 403` for Employees).

#### 4. Dependencies
- **Blocked By:** Issue #03
- **Blocks:** Issue #16

---

### Issue #16: Unified Attendance- and Leave-Linked Salary & LOP Computation Engine
- **Milestone:** Milestone 3 (Reconciliation & Payroll)
- **SRS Reference:** `FR-PAY-003`, SRS Section 5.2, Q4 / Milestones D10–D11
- **Suggested Labels:** `milestone-3`, `payroll`, `calculation-engine`, `math-logic`, `backend`
- **Target Apps:** `apps/api`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Implement the core payroll calculation engine. Compute monthly payable days by subtracting confirmed Loss of Pay (LOP) days (from approved unpaid leaves and unregularized absences) while treating approved paid leaves ($L_{paid}$) and public holidays ($H_{pub}$) as fully paid. Implement the daily salary rate divisor using Option A (Actual calendar days in the month: 28, 29, 30, or 31) as the configurable temporary technical working assumption.

#### 2. Technical Scope
- **Mathematical Specification (Section 5.2):**
  ```text
  Daily Rate (R_daily) = Monthly Gross Base / Divisor (D)
  LOP Deduction = R_daily * Total LOP Days
  Earned Gross = Monthly Gross Base - LOP Deduction
  Total Deductions = LOP Deduction + PF + ESI + PT + TDS + Other Deductions
  Net Pay = Earned Gross - (PF + ESI + PT + TDS + Other Deductions) + Reimbursements / Bonuses
  ```
- **Engine Architecture:**
  - `PayrollCalculationService` with strategy pattern supporting divisor modes:
    - *Option A:* Actual Calendar Days (28–31) — [Proposed technical default — pending client confirmation].
    - *Option B:* Fixed 26 days.
    - *Option C:* Net working days in the month.
- **Backend API:**
  - `POST /api/v1/payroll/compute-draft`: Runs batch calculation for specified month/year.
  - `GET /api/v1/payroll/draft/:month/:year`: Fetches draft payroll results.
- **Client Decision Note (D10 / Q4) [Proposed Technical Default - Pending Client Confirmation]:** Option A is implemented as a temporary technical working assumption to ensure testability, pending client sign-off.

#### 3. Acceptance Criteria
- [ ] Approved paid leaves and public holidays incur zero deduction ($0.00 LOP).
- [ ] LOP days accurately deduct gross pay proportional to the daily rate divisor.
- [ ] Monetary calculations use a documented two-decimal rounding method at the designated calculation boundary, with deterministic results in approved sample cases. The SRS does not prescribe a rounding algorithm; client/accounting confirmation is required.
- [ ] Divisor strategy supports the three SRS options without code refactoring once the client selects one; Option A remains a temporary proposed default.

#### 4. Dependencies
- **Blocked By:** Issue #14, Issue #15
- **Blocks:** Issue #17

---

### Issue #17: Pre-Payroll Review Grid, Manual Adjustments & Monthly Batch Freeze
- **Milestone:** Milestone 3 (Reconciliation & Payroll)
- **SRS Reference:** `FR-PAY-004`, `FR-AUDIT-001`
- **Suggested Labels:** `milestone-3`, `payroll`, `admin-portal`, `audit`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Build the Pre-Payroll Review Grid in the Admin Portal. HR Sub-Users review draft payroll computations, inspect employee breakdown cards (payable days, LOP deductions, gross, net), apply manual ad-hoc bonuses or one-off deductions with mandatory audit reasons, and formally **Freeze** the monthly payroll batch. Once frozen, the payroll period is locked against further edits. Clearly identify client policy regarding whether frozen batches can ever be reopened.

#### 2. Technical Scope
- **Database Schema:**
  - `PayrollBatch`: `month`, `year`, `totalEmployees`, `totalGross`, `totalNet`, `totalLOPDeductions`, `status` (`draft` | `frozen` | `disbursed`), `frozenBy`, `frozenAt`.
  - `PayrollRecord`: `batchId`, `employeeId`, `earningsBreakdown`: [{ name, amount }], `deductionsBreakdown`: [{ name, amount }], `lopDays`, `lopAmount`, `adHocBonus`, `adHocDeduction`, `netPay`, `isFrozen`.
- **Backend API:**
  - `GET /api/v1/payroll/batches/:id`.
  - `PUT /api/v1/payroll/records/:id/adjust`: Applies ad-hoc adjustments with reason.
  - `POST /api/v1/payroll/batches/freeze`: Transitions status to `frozen` and locks month.
- **Frontend UI (Admin Portal):**
  - Pre-Payroll Dashboard with aggregate summary tiles, search/filter table, adjustment modal, and Freeze confirmation dialog.
- **Client Decision Note (D11) [Pending Client Confirmation]:** Freeze is confirmed by `FR-PAY-004`; post-freeze effects and any unfreeze policy are not. Default proposal: disallow editing the frozen payroll batch, and require an explicit Super User unfreeze action with an audit reason only if approved.
- **Audit Logging:** Pre-payroll adjustments and the final batch freeze action write immutable audit events to `FR-AUDIT-001`.

#### 3. Acceptance Criteria
- [ ] HR can view full calculation breakdown for every employee prior to batch freezing.
- [ ] Manual adjustments require an audit reason and update net pay dynamically.
- [ ] Freezing locks payroll batch records and rejects subsequent payroll-record adjustments. Whether it also locks source attendance or leave records, and the response status, requires client policy confirmation.
- [ ] Freeze action logs an immutable audit event to `FR-AUDIT-001`.

#### 4. Dependencies
- **Blocked By:** Issue #16
- **Blocks:** Issue #18, Issue #19

---

### Issue #18: Vector PDF Payslip Generator, Authenticated Streaming & Individual Regeneration
- **Milestone:** Milestone 3 (Reconciliation & Payroll)
- **SRS Reference:** `FR-PAY-005`, `FR-PAY-006`, `FR-ORG-001`, `NFR-SEC-003`, `NFR-PRIV-002`, `NFR-PERF-004`
- **Suggested Labels:** `milestone-3`, `payroll`, `pdf-generation`, `security`, `backend`, `frontend`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Build the automated vector PDF payslip generation engine using pure Node.js `PDFKit` (maintaining ₹0 cloud software cost). Generate branded, professional payslip PDFs stamped with the organization logo (`FR-ORG-001`), company details, employee information, payable days, itemized earnings, itemized deductions, and net pay in words. Save payslips to private `/uploads/payslips/<year>/<month>/` and provide secure authenticated streaming with strict IDOR protection (employees can only download their own payslips). Support both batch generation and individual payslip regeneration.

#### 2. Technical Scope
- **Services (`PayslipPdfService`):**
  - Pure Node.js `PDFKit` vector document layout.
  - Embeds company logo, tabular earnings/deductions, border styling, and currency number-to-words generator.
- **Storage & Security:**
  - File path: `/uploads/payslips/:year/:month/:employeeCode_payslip.pdf`.
  - Privacy guard: `/uploads/payslips/` is NOT mounted as a public static Express route.
  - Streaming controller checking JWT: Super User / HR can download all; Employee can ONLY download their own (`employeeId === req.user.employeeId`).
- **Backend API:**
  - `POST /api/v1/payroll/generate-payslips/:batchId`: Batch generates all PDFs.
  - `POST /api/v1/payroll/regenerate-payslip/:recordId`: Re-renders individual PDF after adjustment.
  - `GET /api/v1/payroll/payslips/:id/download`: Secure streaming route.
- **Frontend UI:**
  - Employee Portal: Payslip download table with "Download PDF" action.
  - Admin Portal: Batch generation progress bar and individual regenerate buttons.

#### 3. Acceptance Criteria
- [ ] Generated PDF displays company logo, tax IDs, itemized earnings/deductions, and clean formatting without rendering bugs.
- [ ] Direct unauthenticated requests for any uploaded/payslip file return `HTTP 401 Unauthorized`; the payslip directory is not publicly mounted or browsable.
- [ ] Cross-employee IDOR security: Employee attempting to download another employee's payslip receives `HTTP 403 Forbidden`.
- [ ] A single PDF completes in under 500 ms and an asynchronous batch of 100 completes in under 45 seconds, measured under agreed test conditions (`NFR-PERF-004`).
- [ ] Admin can regenerate an individual payslip on-demand after an adjustment.

#### 4. Dependencies
- **Blocked By:** Issue #17
- **Blocks:** Issue #19

---

### Issue #19: Batch Payslip Email Dispatcher & Bank Payment Reconciliation Reports
- **Milestone:** Milestone 3 (Reconciliation & Payroll)
- **SRS Reference:** `FR-PAY-007`, `FR-REP-004`, `FR-REP-005`
- **Suggested Labels:** `milestone-3`, `payroll`, `email-dispatch`, `reports`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Complete Milestone 3 by delivering the automated batch payslip email dispatcher and restricted payroll reconciliation exports. Distribute generated payslip PDFs as SMTP attachments. Export the Monthly Payroll Summary and Bank Disbursement Sheet to `.xlsx` and `.csv` only for Super Users and Sub-Users with both payroll-processing and report-export authority (or an explicitly approved equivalent); never expose bank account data to employees or unauthorized users.

#### 2. Technical Scope
- **Email Worker:**
  - Asynchronous batch dispatcher with delay pacing (preventing SMTP connection throttling).
  - Polite error handling: logs failed recipient emails without halting batch execution.
- **Backend API:**
  - `POST /api/v1/payroll/batches/:id/dispatch-emails`: Triggers background dispatch.
  - `GET /api/v1/reports/payroll/summary`: Exports gross, deductions, LOP, and net pay to `.xlsx`.
  - `GET /api/v1/reports/payroll/bank-sheet`: Streams a bank transfer `.csv` after the bank-data authorization check.
- **Frontend UI (Admin Portal):**
  - Email Dispatch console with progress bar (e.g. 45/50 sent) and retry button.
  - Bank Reconciliation Export buttons.
- **Client Decision Note (D14) [Proposed Technical Default - Pending Client Confirmation]:** If SMTP credentials are not provided, emails are dumped to console logger without crashing the process.

#### 3. Acceptance Criteria
- [ ] Batch email worker dispatches payslip PDFs as attachments with polite error handling if SMTP fails.
- [ ] If SMTP credentials are not configured, emails are dumped to console logs without crashing the process.
- [ ] Only Super Users and appropriately authorized HR users can export a Bank Disbursement Sheet containing Employee Name, Bank Account Number, IFSC, and Net Amount; unauthorized access receives `HTTP 403` and exports are not audit payloads.
- [ ] **Milestone 3 Handover Gate:** All M3 acceptance criteria met; software ready for client demonstration on Friday, November 20, 2026.

#### 4. Dependencies
- **Blocked By:** Issue #18
- **Blocks:** Issue #20, Issue #22

---

## Milestone 4: Integration, Security, Audit & Final Handover
**Timeline:** Days 25–30 (November 21, 2026 – November 26, 2026)  
**Deliverable Checkpoint:** Thursday, November 26, 2026 (Final Project Handover & Sign-off)

---

### Issue #20: System Audit Log Engine & Super User Read-Only Viewer
- **Milestone:** Milestone 4 (Audit & Handover)
- **SRS Reference:** `FR-AUDIT-001`, `FR-AUDIT-002`
- **Suggested Labels:** `milestone-4`, `audit`, `security`, `admin-portal`, `backend`, `frontend:admin`
- **Target Apps:** `apps/api`, `apps/admin-portal`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Finalize the System Audit Log engine and build the read-only Audit Log Viewer in the Admin Portal. Verify that critical events across all modules (balance adjustments, permission changes, approval hierarchy edits, attendance overrides, payroll freezes, appraisal calibrations) write immutable records capturing Actor ID, Action, Entity, Before/After values, Reason, IP, and Timestamp. Provide Super Users with multi-criteria search and filtering. Ensure that sensitive data (passwords, JWT secrets, full bank account numbers) is never written into audit diffs.

#### 2. Technical Scope
- **Database Schema (`AuditLog`):**
  ```typescript
  {
    actorId: { type: Schema.Types.ObjectId, ref: 'User', required: true },
    actorRole: { type: String, required: true },
    action: { type: String, required: true },
    entityType: { type: String, required: true },
    entityId: Schema.Types.ObjectId,
    beforeValue: Schema.Types.Mixed,
    afterValue: Schema.Types.Mixed,
    reason: String,
    ipAddress: String,
    timestamp: { type: Date, default: Date.now, immutable: true }
  }
  ```
- **Integrity Guarantee:**
  - Guarantees **application-level append-only / read-only** behavior through Express route restrictions and Mongoose middleware preventing `update` or `delete` on this collection. (Does not claim cryptographic hardware-level immutability against direct database administrator access).
- **Backend API:**
  - `GET /api/v1/audit-logs`: Multi-criteria query endpoint (date range, actor, action, entity).
  - Explicit omission of `PUT`, `PATCH`, or `DELETE` endpoints for audit records.
- **Frontend UI (Admin Portal):**
  - Super User Audit Log Viewer with date pickers, actor filter, action dropdown, and expandable JSON before/after state diff inspector.

#### 3. Acceptance Criteria
- [ ] Audit log entries are strictly immutable through the application layer (no edit/delete endpoints).
- [ ] Multi-criteria filtering by Date Range, Action Type, and Actor works accurately.
- [ ] State diffs clearly highlight changed values between previous and updated records.
- [ ] Sensitive fields (passwords, tokens, bank account numbers) are masked or excluded from audit records.

#### 4. Dependencies
- **Blocked By:** Issue #03, Issue #06, Issue #09, Issue #14, Issue #17
- **Blocks:** Issue #22, Issue #24

---

### Issue #21: Centralized In-App Notification Center & Background Cron Reminders
- **Milestone:** Milestone 4 (Audit & Handover)
- **SRS Reference:** `FR-NOTIF-001`, `FR-NOTIF-002`
- **Suggested Labels:** `milestone-4`, `notifications`, `background-jobs`, `frontend`, `backend`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Implement the centralized In-App Notification Center and automated background reminder jobs. Deliver a unified notification drawer in both portals displaying unread count badges, categorized notifications (Leave, Attendance, Goals, Appraisals, Payslips), and "Mark as Read" actions. Configure lightweight embedded `node-cron` background tasks for daily attendance submission reminders and pending approval alerts.

#### 2. Technical Scope
- **Database Schema (`Notification`):**
  ```typescript
  {
    recipientId: { type: Schema.Types.ObjectId, ref: 'User', required: true },
    title: { type: String, required: true },
    message: { type: String, required: true },
    category: { type: String, enum: ['leave', 'attendance', 'goal', 'appraisal', 'payroll', 'system'] },
    linkUrl: String,
    isRead: { type: Boolean, default: false },
    createdAt: { type: Date, default: Date.now }
  }
  ```
- **Backend API:**
  - `GET /api/v1/notifications`, `PATCH /api/v1/notifications/:id/read`, `PATCH /api/v1/notifications/read-all`.
- **Background Cron Jobs (`node-cron`):**
  - Daily check for leave requests pending > 48 hours.
  - Monthly reminder before payroll cutoff date.
- **Frontend UI:**
  - Top navigation Notification Bell with unread counter pill and slide-over notification drawer.

#### 3. Acceptance Criteria
- [ ] Unread notification badge updates dynamically when actions occur.
- [ ] Clicking a notification navigates directly to the relevant action screen (e.g. pending leave approval).
- [ ] "Mark All as Read" clears badge count instantly.

#### 4. Dependencies
- **Blocked By:** Issue #01, Issue #02 (shared notification primitives/auth); leave lifecycle notifications are delivered in Issue #07 without waiting for the centralized viewer.
- **Blocks:** Issue #24

---

### Issue #22: Comprehensive Security Audit, Route Protection & Rate Limiting
- **Milestone:** Milestone 4 (Audit & Handover)
- **SRS Reference:** `NFR-SEC-001` through `NFR-SEC-005`, `NFR-PRIV-001`, `NFR-PRIV-002`, `NFR-PERF-001`, `NFR-PERF-003`, `NFR-PERF-004`
- **Suggested Labels:** `milestone-4`, `security`, `hardening`, `performance`, `testing`
- **Target Apps:** `apps/api`, `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Conduct a comprehensive security audit and perimeter hardening across the application stack. Verify the confirmed login IP limit (maximum 10 requests per 15 minutes per IP, then `HTTP 429`), 401/403 route protection, IDOR safeguards, private uploads, validation, and performance requirements. `express-rate-limit`, a global limiter, exact index selections, and “95%” framing are implementation proposals; performance must instead be measured against the SRS condition of standard reads under 300 ms for up to 100 concurrent users.

#### 2. Technical Scope
- **Hardening Middleware:**
  - Rate limiting on `/api/v1/auth/login` (maximum 10 requests per 15 minutes per IP; the next request returns `HTTP 429`).
  - [Proposed — pending technical approval] Apply a separately configured global API limiter where it does not interfere with authenticated operational workflows.
  - Strict CORS origin whitelisting.
- **Automated Integration Security Tests:**
  - Jest / Supertest suite asserting HTTP 401 on missing cookies.
  - Test asserting HTTP 403 when Employee token requests `/api/v1/payroll/*` or `/api/v1/admin/*`.
  - Test asserting HTTP 403 on IDOR cross-employee payslip access.
- **Database Optimization:**
  - Compound indexes on `EmployeeLeaveBalance` (`employeeId`, `year`), `DailyAttendance` (`employeeId`, `date`), and `PayrollRecord` (`batchId`, `employeeId`).

#### 3. Acceptance Criteria
- [ ] `HTTP 401` returned for any unauthenticated request to protected endpoints.
- [ ] `HTTP 403` returned when an employee account requests admin routes (`/api/v1/admin/*`, `/api/v1/payroll/*`).
- [ ] `HTTP 429` is returned on the 11th login request from one IP within 15 minutes; account-level lockout is not treated as an SRS requirement.
- [ ] Zod rejects malformed inbound requests with `HTTP 400` field-level errors (`NFR-PERF-001`).
- [ ] Standard REST reads complete in under 300 ms for up to 100 concurrent users under an agreed reproducible test profile (`NFR-PERF-003`).

#### 4. Dependencies
- **Blocked By:** Preceding Milestones 1–3
- **Blocks:** Issue #23, Issue #24

---

### Issue #23: Cross-Browser Compatibility, Mobile Responsiveness & Usability QA
- **Milestone:** Milestone 4 (Audit & Handover)
- **SRS Reference:** `NFR-PERF-002`, SRS Section 9.4
- **Suggested Labels:** `milestone-4`, `qa`, `cross-browser`, `usability`, `a11y`
- **Target Apps:** `apps/admin-portal`, `apps/employee-portal`
- **Estimated Duration:** 1.0 Day

#### 1. Description & Objective
Perform cross-browser compatibility verification, viewport responsiveness testing, and end-to-end usability validation. Test both portals across Google Chrome, Mozilla Firefox, Apple Safari, and Microsoft Edge. Verify responsive CSS layouts across Desktop (1280px+), Tablet (768px–1024px), and Mobile (375px+) viewports. Execute the mandatory usability test: confirm that a newly onboarded employee can submit a leave request in <= 3 clicks from the home dashboard.

#### 2. Technical Scope
- **Testing Scope:**
  - Google Chrome (v120+), Mozilla Firefox (v120+), Apple Safari (v17+), Microsoft Edge (v120+).
  - Responsive breakpoints: Mobile (375px+), Tablet (768px–1024px), Desktop (1280px+).
  - Accessibility check: WCAG 2.1 Level AA color contrast and keyboard navigation.
  - Usability test script for leave submission workflow.

#### 3. Acceptance Criteria
- [ ] Layout renders cleanly without broken elements or horizontal scrolling at the SRS-supported desktop, tablet, and mobile viewport ranges (`NFR-PERF-002`).
- [ ] Mobile navigation drawer operates smoothly on viewports down to 375px width.
- [ ] Leave application is completed successfully in ≤ 3 clicks from the dashboard (SRS Section 9.4).
- [ ] [Proposed accessibility baseline — pending approval] Core screens meet WCAG 2.1 AA contrast and keyboard-accessibility checks; this is not assigned an SRS requirement ID.
- [ ] All high-severity and critical UI defects resolved.

#### 4. Dependencies
- **Blocked By:** Issue #22
- **Blocks:** Issue #24

---

### Issue #24: Seed Data Script, Production Configuration, API Collection & User Manuals
- **Milestone:** Milestone 4 (Audit & Handover)
- **SRS Reference:** Section 1.1, Section 8, Section 10.2, Section 12 (Handover Assets)
- **Suggested Labels:** `milestone-4`, `handover`, `documentation`, `seed-scripts`, `manuals`
- **Target Apps:** Root repository, `docs/`
- **Estimated Duration:** 1.5 Days

#### 1. Description & Objective
Prepare and verify the complete final client handover package to achieve formal project sign-off on Thursday, November 26, 2026. Deliver the automated one-command database seed script (`npm run seed`), complete `.env.example` templates, production deployment instructions, Postman/Bruno API test collection, illustrated Employee User Manual (PDF/Markdown), and illustrated Admin & Manager User Manual (PDF/Markdown). Note: Documentation drafting occurs incrementally across milestones; Issue #24 handles final compilation, screenshots, review, and handover sign-off.

#### 2. Technical Scope
- **Deliverables Package:**
  - Automated seed script: `apps/api/src/scripts/seed.ts` provisioning Organization Settings, standard leave types, sample departments/default roles, an initial Super User, and optionally non-production demo users. The number and leave balances of demo users are proposed test fixtures, not SRS commitments; EL seed balance is 0 unless the employee is eligible and the allocation policy has been confirmed.
  - Security in seed data: if demo accounts are included, create credentials from required deployment-time inputs (never hard-code or publish them) and set `mustChangePassword: true`; Issue #02 must block normal access until first-password change clears this flag.
  - Production documentation: `docs/DEPLOYMENT_GUIDE.md` and `.env.example`.
  - Illustrated User Manuals: `docs/EMPLOYEE_USER_MANUAL.md` and `docs/ADMIN_USER_MANUAL.md`.
  - Exported Postman/Bruno API Collection covering all authenticated endpoints.
  - Final Handover and Acceptance Sign-off document.

#### 3. Acceptance Criteria
- [ ] Running `npm run seed` on a fresh MongoDB instance executes cleanly and seeds the required master data; any demo users are explicitly labelled non-production fixtures and use the confirmed leave-allocation policy.
- [ ] Seed script does not expose hardcoded permanent credentials; forces password change on first login.
- [ ] Employee User Manual covers login, leave applications, timesheets, goal updates, self-appraisals, and payslip downloads with clear illustrations.
- [ ] Admin User Manual covers Sub-User permission builder, approval hierarchy modes, attendance reconciliation, payroll freeze, and audit viewer.
- [ ] **Proposed Final Handover Gate:** Client handover review is scheduled for Thursday, November 26, 2026; completion/sign-off remains subject to accepted criteria, client decisions, and no blocking defects.

#### 4. Dependencies
- **Blocked By:** Issue #20, Issue #21, Issue #22, Issue #23 (Documentation drafting proceeds in parallel; Issue #24 executes final packaging and handover review).
- **Blocks:** Project Completion

---

## Traceability Matrix: Requirements to Issues

| Functional Domain | SRS Requirement IDs | Primary Assigned GitHub Issue |
| :--- | :--- | :---: |
| **Organization Settings** | `FR-ORG-001`, `FR-ORG-002`, `FR-ORG-003` | **Issue #01, Issue #04** |
| **Authentication & RBAC** | `FR-AUTH-001`, `FR-AUTH-002`, `FR-AUTH-003`, `FR-AUTH-004`, `FR-AUTH-005`, `FR-AUTH-006` | **Issue #02, Issue #03** |
| **Employee Directory** | `FR-EMP-001`, `FR-EMP-002`, `FR-EMP-003`, `FR-EMP-004` | **Issue #03** |
| **Leave Policy & Types** | `FR-LEAVE-001` through `FR-LEAVE-004` | **Issue #05** |
| **Holiday Calendar** | `FR-LEAVE-009`, `FR-REP-005` | **Issue #04** |
| **Leave Reservation & Booking** | `FR-LEAVE-005`, `FR-LEAVE-006`, `FR-LEAVE-008` | **Issue #06** |
| **Leave Approvals, Reports & Lifecycle Notifications** | `FR-LEAVE-007`, `FR-LEAVE-010`, `FR-LEAVE-011`, `FR-REP-001`, `FR-REP-005` | **Issue #07** |
| **Attendance Clock-In/Out** | `FR-ATT-002` | **Issue #08** |
| **Attendance Regularization** | `FR-ATT-003` | **Issue #09** |
| **Productivity Timesheets** | `FR-PROD-001`, `FR-PROD-002` | **Issue #10** |
| **Manager Coaching Reviews** | `FR-PROD-003`, `FR-PROD-004` | **Issue #11** |
| **Goal Setting & Tracking** | `FR-PERF-001` | **Issue #12** |
| **Appraisal Cycle Orchestration & Reports** | `FR-PERF-002` through `FR-PERF-007`, `FR-REP-003` | **Issue #13** |
| **Attendance Reconciliation** | `FR-ATT-001`, `FR-ATT-004`, `FR-ATT-005` | **Issue #14** |
| **Salary Components** | `FR-PAY-001`, `FR-PAY-002` | **Issue #15** |
| **Payroll Calculation & LOP** | `FR-PAY-003` | **Issue #16** |
| **Pre-Payroll Review & Freeze**| `FR-PAY-004` | **Issue #17** |
| **PDF Payslip Generation** | `FR-PAY-005`, `FR-PAY-006` | **Issue #18** |
| **Email Payslips & Bank Reports**| `FR-PAY-007`, `FR-REP-004` | **Issue #19** |
| **System Audit Log** | `FR-AUDIT-001`, `FR-AUDIT-002` | **Issue #20** (capture is implemented incrementally in #03, #04, #06, #07, #09, #13, #14, #15, and #17) |
| **Notification Engine** | `FR-NOTIF-001`, `FR-NOTIF-002` | **Issue #07** (Leave alerts), **Issue #21** (Central) |
| **Security, Privacy & Performance NFRs** | `NFR-SEC-001`, `NFR-SEC-002`, `NFR-SEC-003`, `NFR-SEC-004`, `NFR-SEC-005`, `NFR-PRIV-001`, `NFR-PRIV-002`, `NFR-PERF-001`, `NFR-PERF-002`, `NFR-PERF-003`, `NFR-PERF-004` | **Issue #02, Issue #03, Issue #18, Issue #19, Issue #22, Issue #23** |
| **Responsive QA & Usability** | `NFR-PERF-002`, SRS Section 9.4 | **Issue #23** |
| **Handover Deliverables** | Section 12, Handover List | **Issue #24** |
