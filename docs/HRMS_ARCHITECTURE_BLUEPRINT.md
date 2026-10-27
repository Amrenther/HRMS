# HRMS (Human Resource Management System) Master Architecture & Delivery Blueprint

**Organization:** Adithiya Solutions  
**Target Delivery Window:** 30 Calendar Days  
**Architecture:** Monorepo MERN Stack (TypeScript)  
**Security Model:** 3-Tier Granular RBAC with HttpOnly JWT Token Rotation  
**Hosting Cost Target:** ₹0 Incremental Cloud Infra (Self-contained local file storage, embedded MongoDB persistence, pure Node vector PDF generation)

---

## 1. System Topology & Monorepo Structure

```
HRMS/
├── apps/
│   ├── server/                         # Express.js + TypeScript REST API
│   │   ├── src/
│   │   │   ├── config/                 # DB, Mailer, Environment configuration
│   │   │   ├── constants/              # Roles, Permissions, Status Enums
│   │   │   ├── controllers/            # Request handlers (Leave, Payroll, etc.)
│   │   │   ├── middleware/             # Auth, RBAC, Validate(Zod), ErrorHandler
│   │   │   ├── models/                 # Mongoose Data Models & Schemas
│   │   │   ├── routes/                 # Express API Route Definitions
│   │   │   ├── services/               # Core business logic (Payroll computation, PDF gen)
│   │   │   ├── jobs/                   # Node-cron / Agenda scheduled workers
│   │   │   └── utils/                  # Excel exporter, calculation helpers
│   │   ├── uploads/                    # Local protected storage (Avatars, Docs, Payslips)
│   │   └── package.json
│   │
│   ├── admin-portal/                   # React 19 + Vite + Tailwind + RTK Query
│   │   ├── src/
│   │   │   ├── app/                    # Redux store & root reducers
│   │   │   ├── features/               # Module slices (employees, leaves, payroll, appraisals)
│   │   │   ├── components/ui/          # Shadcn / Radix UI design tokens
│   │   │   ├── layouts/                # Admin sidebar, header, notification drawer
│   │   │   └── pages/                  # Super User & Sub-User management views
│   │   └── package.json
│   │
│   └── employee-portal/                # React 19 + Vite + Tailwind + RTK Query
│       ├── src/
│       │   ├── app/                    # Redux store
│       │   ├── features/               # Self-service slices (daily tasks, my leaves, payslips)
│       │   ├── components/ui/          # Shadcn / Radix primitives
│       │   ├── layouts/                # Employee app layout & mobile bottom bar
│       │   └── pages/                  # My Profile, Attendance Clock, Leave Apply, Tasks
│       └── package.json
│
├── packages/                           # Shared workspace code
│   └── shared-types/                   # Shared TypeScript Interfaces, Enums & Zod Schemas
├── docs/                               # SRS, User Manual, API Specs, Database ERD
└── package.json                        # Root npm/pnpm workspace orchestrator
```

---

## 2. Complete Feature Matrix by Application

### 📱 A. Employee Self-Service App (`apps/employee-portal`)
| Module | Features & Capabilities |
| :--- | :--- |
| **Authentication & Profile** | • Secure login with email & password + password reset workflow.<br>• View personal profile: Contact details, Emergency contacts, Bank account details, Job role, Reporting manager.<br>• Profile change request submission for HR approval. |
| **Attendance & Clock-In** | • One-click daily Web Clock-In and Clock-Out with timestamp verification.<br>• Monthly calendar view showing Present, Absent, Half-Day, Late-In, and Holiday markers.<br>• Monthly summary card (Total Working Days, Present Days, Late marks, Overtime). |
| **Leave Management** | • Real-time Leave Balance cards (Casual, Sick, Earned, Comp-off).<br>• Leave application modal with single-day, multi-day, or half-day options.<br>• Live application tracking status (*Pending Stage-1 Manager*, *Pending Stage-2 HR*, *Approved*, *Rejected*).<br>• Organization Holiday Calendar view.<br>• Download leave application history. |
| **Daily Productivity & Tasks** | • Daily Task Logger: Submit task title, category/project, description, hours spent, and status (*In Progress*, *Completed*, *Blocked*).<br>• Historical timesheet log and editable entries within a same-day cutoff window.<br>• Weekly productivity summary view with manager feedback notes. |
| **Performance & Goals** | • View active quarterly/annual goals assigned by manager with completion progress bars.<br>• Periodic Self-Appraisal submission form (rating on organizational metrics + qualitative self-review).<br>• View published appraisal scorecards, manager ratings, and historical performance trends. |
| **Payroll & Payslips** | • Download automated monthly payslip as password-protected / signed PDF.<br>• Interactive Payslip Viewer: Earnings breakdown (Basic, HRA, Allowances), Deductions breakdown (PF, ESI, Tax, LOP days), and Net Take-home.<br>• Annual Earnings & Tax deduction projection statement. |
| **Notifications** | • Real-time notification center (bell icon) for leave approval/rejection updates, appraisal reminders, and payslip publication. |

---

### 🛡️ B. Admin & Manager Portal (`apps/admin-portal`)
| Module | Features & Capabilities |
| :--- | :--- |
| **Organization & Configuration** | • **Super User Control Center**: Company branding (Name, Logo, Address, Tax IDs).<br>• Dynamic Leave Policy Builder: Configure leave types, annual allowances, accrual rules, carry-forward limits.<br>• Configurable Approval Hierarchies: Choose 1-Stage (Manager or HR) or 2-Stage (Manager then HR).<br>• Salary Component Builder: Add custom Earning types (fixed/formula) & Deduction types (PF, ESI, Tax slabs).<br>• Appraisal Parameter Builder: Define custom evaluation criteria, rating scales (1–5 or 1–10), and weights. |
| **3-Tier User & Role Management** | • **Super User**: Global access, system audit logs, database backup triggers.<br>• **Sub-User Management**: Create HR Managers and Department Heads with modular permission toggles (`canManageEmployees`, `canApproveLeaves`, `canReviewPerformance`, `canProcessPayroll`) scoped to specific departments.<br>• Employee Directory: Full CRUD operations, onboarding wizard, employee status toggle (*Active*, *Probation*, *Notice*, *Terminated*). |
| **Attendance & Leave Administration** | • Daily Attendance Live Dashboard: Who is In, Who is On Leave, Who is Late.<br>• CSV / Excel Bulk Attendance Upload for biometric / punch machine logs.<br>• Manual Attendance Overrides / Regularization requests approval.<br>• Leave Request Approval Queue: Approve / Reject with mandatory comment trail.<br>• Leave balance manual credit/debit adjustments with audit reason. |
| **Productivity & Performance Console** | • Departmental Daily Productivity Feed: Review timesheet entries submitted by team members.<br>• Manager Weekly Rating Interface: Rate employee daily logs and provide constructive coaching notes.<br>• Appraisal Cycle Orchestrator: Launch new appraisal cycles (Quarterly / Annual), track submission rates, complete Manager reviews, and finalize Super User sign-offs.<br>• Departmental performance bell-curve distribution and reporting. |
| **Payroll Processing Engine** | • Attendance-linked Auto Payroll Compute: Automatically calculates Working Days, Paid Leaves, and Loss of Pay (LOP) days.<br>• Pre-run Payroll Review Grid: Adjust one-off bonuses, reimbursements, or penalties before freezing.<br>• 1-Click Automated Batch Payslip Generation via PDFKit vector engine.<br>• Bulk Email Dispatcher: Email payslips directly to employee inboxes via SMTP.<br>• Monthly Payroll Summary Export in Excel (`.xlsx`) & CSV for bank disbursements. |
| **Analytics & Reporting** | • Comprehensive Export Center: Leave utilization reports, Monthly attendance logs, Payroll variance reports, and Appraisal rating sheets.<br>• Executive Dashboard charts: Headcount growth, Monthly salary payouts, Absenteeism rate. |

---

## 3. Technology Stack & 2026 Verified Package Ecosystem

### Backend Stack (`apps/server`)
| Category | Library / Tool | Target Version | Rationale |
| :--- | :--- | :--- | :--- |
| **Runtime & Core** | `Node.js` (Active LTS) | `v22.x LTS` | Native fetch, modern V8 optimizations, long-term enterprise stability. |
| **Web Framework** | `express` | `^4.21.x` / `5.x` | Industry standard, minimal overhead, robust middleware ecosystem. |
| **Language** | `typescript` | `^5.7.x` | Strict compile-time safety and unified typings across backend & frontends. |
| **Database ODM** | `mongoose` | `^8.10.x` | Strongly-typed schemas, aggregation pipelines, validation hooks. |
| **Authentication** | `jsonwebtoken` + `bcryptjs` | `^9.0.x` / `^2.4.x` | Industry-standard JWT encryption and salted password hashing. |
| **Security & Headers** | `helmet` + `cors` + `cookie-parser` | `^8.0.x` / `^2.8.x` | Strict HTTP security headers, CORS origin whitelisting, signed cookies. |
| **Validation** | `zod` | `^3.24.x` | Universal schema validation with automated TypeScript type inference. |
| **PDF Engine** | `pdfkit` | `^0.15.x` / `0.16.x` | Ultra-fast vector PDF rendering in pure Node.js; zero Chromium/RAM bloat. |
| **Excel Export** | `exceljs` | `^4.4.x` | High-performance generation of formatted `.xlsx` spreadsheets and `.csv`. |
| **Job Scheduling** | `node-cron` | `^3.0.x` | Embedded cron runner for daily auto-absent, leave accruals, and payroll runs. |
| **Email Service** | `nodemailer` | `^6.10.x` | Zero-cost SMTP integration (works with Gmail, Outlook, or custom SMTP). |
| **File Handling** | `multer` | `^1.4.x` | Streamed multipart file uploads with MIME-type and file-size validation. |

### Frontend Stack (`apps/employee-portal` & `apps/admin-portal`)
| Category | Library / Tool | Target Version | Rationale |
| :--- | :--- | :--- | :--- |
| **UI Library** | `react` & `react-dom` | `^19.0.x` | React 19 compiler optimizations, Actions, and enhanced form transitions. |
| **Build Tool** | `vite` | `^6.x` | Sub-second HMR, optimized tree-shaking, lightweight bundle sizes. |
| **Language** | `typescript` | `^5.7.x` | Type synchronization with backend API DTO contracts. |
| **Styling** | `tailwindcss` | `^3.4.x` / `^4.0.x` | Utility-first CSS, responsive styling, dark/light theme support. |
| **Component Primitives** | `Radix UI` + `lucide-react` | Latest | Accessible, keyboard-navigable UI components and modern iconography. |
| **State & API Layer** | `@reduxjs/toolkit` (RTK Query)| `^2.5.x` | Centralized global state, automated caching, deduplication, optimistic updates. |
| **Form Handling** | `react-hook-form` + `@hookform/resolvers` | `^7.54.x` | Uncontrolled high-performance forms with integrated Zod validation. |
| **Data Visualization** | `recharts` | `^2.15.x` | Responsive SVG charts for attendance rates, productivity graphs, salary trends. |
| **Dates & Formatting** | `date-fns` | `^4.1.x` | Lightweight, immutable date arithmetic for leave and payroll calculations. |

---

## 4. Database Schema Design (MongoDB / Mongoose Models)

### Core Collections Overview:
1. `users` (Employees, Sub-Users, Super User)
2. `organizations` (Global settings, leave policies, salary component definitions, holiday list)
3. `attendances` (Clock-in/out records, status: Present, Late, Half-Day, Absent)
4. `leaves` (Leave applications, approval history, stage status)
5. `leave_balances` (Yearly quota, used, accrued, carried over)
6. `daily_tasks` (Productivity logs, hours, status, manager review notes)
7. `appraisal_cycles` & `appraisal_submissions` (Goals, self-evaluation, manager score)
8. `salary_structures` (Base salary, fixed earnings, deductions assigned to employee)
9. `payrolls` & `payslips` (Generated monthly records, computed earnings/deductions, PDF path)
10. `notifications` (In-app notifications for both portals)

---

## 5. 30-Day Step-by-Step Delivery Roadmap

| Phase / Window | Key Milestones & Deliverables | Exit Criteria |
| :--- | :--- | :--- |
| **Days 1 – 5: Foundation, DB & Auth** | • Monorepo initialization (pnpm / npm workspaces).<br>• Mongoose schemas, indexes, and seed scripts.<br>• Express auth controllers (JWT in HttpOnly cookies, refresh token rotation).<br>• 3-tier RBAC middleware.<br>• Base UI shell for Admin & Employee portals (Tailwind, Redux store, Login screens). | Working authentication flow for Super User, Sub-User, and Employee across both portals. |
| **Days 6 – 11: Core HR & Leave Management** | • Organization Settings & Holiday Calendar CRUD.<br>• Dynamic Leave Policy configuration in Admin.<br>• Employee Leave Application & Balance widget.<br>• 1-to-2 stage Leave Approval Workflow with email notification hooks.<br>• Leave reporting dashboard with Excel export. | Employees can apply for leaves; Sub-Users/HR can approve/reject; balances auto-deduct. |
| **Days 12 – 17: Attendance & Daily Productivity** | • Web Clock-In/Clock-Out with daily status resolution.<br>• Biometric CSV upload & manual regularization workflow.<br>• Employee Daily Task / Timesheet logger.<br>• Manager Timesheet review and weekly rating console.<br>• Daily attendance summary charts. | Timesheets & attendance feed directly into the system database without errors. |
| **Days 18 – 22: Performance Management & Appraisals** | • Goal setting & KPI tracking interface.<br>• Configurable Appraisal cycle orchestrator.<br>• Multi-parameter Self-Appraisal form & Manager scoring interface.<br>• Super User final sign-off & scorecard publishing.<br>• Performance summary reports. | Full appraisal cycle can be launched, completed, scored, and archived. |
| **Days 23 – 27: Payroll Engine & Automated Payslip PDF** | • Salary structure assignment (Earnings & Deductions builder).<br>• Attendance & Leave-linked salary computation service (auto-LOP deductions).<br>• PDFKit vector payslip generator with company logo and dynamic breakdown.<br>• Bulk payslip generation and batch SMTP email dispatch.<br>• Monthly Payroll reconciliation export (`.xlsx` & `.csv`). | One-click payroll generates accurate payslips and downloadable PDFs. |
| **Days 28 – 30: QA, Hardening, Documentation & Handover** | • End-to-end integration testing and input validation hardening.<br>• Audit trail validation and security checks.<br>• Generation of User Manual (PDF/Markdown) for Admin and Employees.<br>• Database Schema documentation & API collection (Postman/Bruno).<br>• Final deployment handover to client. | Complete source code, working dual apps, documentation, and user manual delivered. |
