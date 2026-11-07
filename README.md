# EnterpriseFlow
## Product Requirements Document (PRD)

**Version:** 1.1  
**Status:** Ready for Development  
**Product:** Expense Management System  
**Backend:** Python / Django  
**Database:** PostgreSQL  
**API:** Django REST Framework

---

# 1. Product Overview

EnterpriseFlow is a web-based expense management system that allows organizations to manage employee expenses through a centralized platform.

Employees can submit expense requests with receipt attachments. Managers and administrators can review and approve expenses based on predefined approval rules.

Administrators can manage users, expense categories, budgets, reports, and system activities.

# 2. Problem Statement

Businesses often manage employee expenses using spreadsheets, paper receipts, and messaging applications.

This creates problems such as:

- Difficulty tracking expense requests.
- Missing receipts.
- Delayed approvals.
- Uncontrolled department spending.
- Lack of financial visibility.
- Difficulty tracking approval history.

EnterpriseFlow aims to simplify expense management through a centralized system.

# 3. Project Objectives

1. Provide employee registration and authentication.
2. Implement role-based access control.
3. Allow employees to submit expenses with receipts.
4. Implement manager and administrator approvals.
5. Support multi-level approval workflows.
6. Manage expense categories and budgets.
7. Generate financial reports.
8. Maintain audit logs.
9. Provide in-app notifications.
10. Provide administrative dashboard APIs.

# 4. User Roles

## Employee
- Register and log in.
- Submit expense requests.
- Upload expense receipts.
- View personal expense history.
- Track approval status.
- Receive notifications.

## Manager
- View expenses submitted by assigned employees.
- Review expense details and receipts.
- Approve or reject expenses.
- Provide rejection reasons.
- View team expense history.
- Receive approval notifications.

## Administrator
- Manage users and roles.
- Manage expense categories.
- Manage organizational budgets.
- Perform second-level approvals.
- View all expense requests.
- Access financial reports.
- View audit logs.
- Access administrative dashboard data.

# 5. Functional Requirements

## FR-01: Employee Registration and Authentication

- Employees can register using their name, email, and password.
- Email addresses must be unique.
- Users can log in and log out.
- Users can change their passwords.
- Administrators can deactivate accounts.
- Deactivated accounts cannot access the application.

## FR-02: Role-Based Access Control

- Every user must have an assigned role.
- The system supports Employee, Manager, and Administrator roles.
- Employees can only manage their own expenses.
- Managers can access expenses belonging to their assigned team.
- Administrators can access organizational records.
- All permissions must be enforced on the backend.

## FR-03: Expense Submission and Receipt Attachments

Employees can submit expenses with the following information:

- Expense title.
- Amount.
- Expense date.
- Expense category.
- Description.
- Receipt attachment.

Business rules:

- Expense amounts must be greater than zero.
- Receipt attachments must use supported file formats.
- Employees can edit their own pending expenses.
- Employees cannot edit approved or rejected expenses.
- Every new expense starts with Pending status.

## FR-04: Manager Approval and Rejection

- Managers can view pending expense requests from their assigned team.
- Managers can approve expenses.
- Managers can reject expenses.
- Rejection reasons are required.
- The system records the reviewer and decision timestamp.
- Only pending expenses can be processed.

## FR-05: Multi-Level Approval Workflows

Approval requirements depend on the expense amount.

**Approval rules:**

| Expense amount | Required approval |
|---|---|
| ₱1 – ₱5,000 | Manager |
| Above ₱5,000 | Manager + Administrator |

Workflow:

1. Employee submits an expense.
2. Manager reviews the expense.
3. If approved and the amount is ₱5,000 or less, the expense becomes Approved.
4. If approved and the amount exceeds ₱5,000, it proceeds to administrator approval.
5. Administrator reviews the expense.
6. Once approved, the expense becomes Approved.

Additional rules:

- Either approval level can reject an expense.
- Rejected expenses become Rejected immediately.
- The system records every approval decision.
- Users cannot approve their own expenses.
- Duplicate approval actions must be prevented.

## FR-06: Expense Categories and Budgets

Administrators can:

- Create expense categories.
- Update category names.
- Deactivate categories.
- Create organizational or department budgets.
- Define budget amounts and periods.

The system must:

- Track approved expenses against budgets.
- Calculate remaining budget.
- Display budget utilization.
- Allow administrators to view spending by category.

Budget calculation:

Remaining Budget = Total Budget - Approved Expenses

## FR-07: Financial Reports

Administrators can view financial reports containing:

- Total submitted expenses.
- Total approved expenses.
- Total rejected expenses.
- Total pending expenses.
- Total approved spending.
- Expenses by category.
- Expenses by date range.
- Department spending.

Reports must support filtering by date and category.

## FR-08: Audit Logs

The system must maintain records of important activities.

Examples:

- User registration.
- Expense submission.
- Expense modification.
- Expense approval.
- Expense rejection.
- Category modification.
- Budget modification.
- User deactivation.

Each audit record must contain:

- User who performed the action.
- Action performed.
- Affected record.
- Timestamp.

Audit records must not be editable through normal application operations.

## FR-09: Notifications

The system must provide in-app notifications.

Examples:

- Managers receive notifications when employees submit expenses.
- Administrators receive notifications when second-level approval is required.
- Employees receive notifications when their expenses are approved or rejected.
- Managers receive notifications when their approval is required.

Users can view their notifications and mark them as read.

## FR-10: Administrative Dashboard APIs

The backend must provide API endpoints for administrative dashboard information.

Dashboard information includes:

- Total expenses.
- Pending expenses.
- Approved expenses.
- Rejected expenses.
- Total approved spending.
- Budget utilization.
- Recent expense activities.
- Expenses grouped by category.

All dashboard endpoints must require administrator authorization.

# 6. User Stories

## Employee Stories

### US-01: Register an Account
As an employee, I want to register an account so that I can access EnterpriseFlow.

Acceptance criteria:
- I can register with my name, email, and password.
- Duplicate email addresses are rejected.
- Passwords are securely stored.
- I can log in after successful registration.

### US-02: Submit an Expense
As an employee, I want to submit an expense so that my company can review it.

Acceptance criteria:
- I can provide expense details.
- I can upload a receipt.
- The expense starts with Pending status.
- The system records the submission timestamp.

### US-03: View My Expenses
As an employee, I want to view my expenses so that I can track their progress.

Acceptance criteria:
- I can see my submitted expenses.
- I can see their current status.
- I can view approval history.
- I can see rejection reasons.

### US-04: Edit a Pending Expense
As an employee, I want to edit my pending expense so that I can correct mistakes.

Acceptance criteria:
- I can edit my own pending expenses.
- I cannot edit approved or rejected expenses.
- Other employees cannot modify my expenses.

## Manager Stories

### US-05: Review Team Expenses
As a manager, I want to review my team's expense requests so that I can verify their validity.

Acceptance criteria:
- I can see pending expenses from my assigned team.
- I can view expense details and receipts.
- I cannot access unrelated teams' expenses.

### US-06: Approve an Expense
As a manager, I want to approve an expense so that it can proceed through the approval workflow.

Acceptance criteria:
- I can approve pending expenses.
- The system records my decision.
- Expenses above ₱5,000 proceed to administrator approval.
- Expenses of ₱5,000 or less become Approved.

### US-07: Reject an Expense
As a manager, I want to reject an expense so that invalid requests do not proceed.

Acceptance criteria:
- I can reject pending expenses.
- A rejection reason is mandatory.
- The expense becomes Rejected.
- The employee receives a notification.

## Administrator Stories

### US-08: Manage Users
As an administrator, I want to manage users so that I can control system access.

Acceptance criteria:
- I can view users.
- I can create and deactivate accounts.
- I can assign roles.
- I can assign employees to managers.

### US-09: Perform Second-Level Approval
As an administrator, I want to review high-value expenses so that large expenses receive additional authorization.

Acceptance criteria:
- I can view expenses awaiting administrator approval.
- I can approve or reject them.
- Rejection requires a reason.
- The system records my decision.
- The employee receives a notification.

### US-10: Manage Expense Categories
As an administrator, I want to manage expense categories so that expenses are properly classified.

Acceptance criteria:
- I can create categories.
- I can update categories.
- I can deactivate categories.

### US-11: Manage Budgets
As an administrator, I want to manage budgets so that I can monitor company spending.

Acceptance criteria:
- I can create budgets.
- I can define budget periods.
- I can view approved spending.
- I can view remaining budget.

### US-12: View Financial Reports
As an administrator, I want to view financial reports so that I can monitor company expenses.

Acceptance criteria:
- I can filter by date.
- I can filter by category.
- I can view spending totals.
- I can view expense status summaries.

### US-13: View Audit Logs
As an administrator, I want to view audit logs so that I can investigate important system activities.

Acceptance criteria:
- I can view the user responsible for an action.
- I can view the action performed.
- I can view the affected record.
- I can view the timestamp.

### US-14: View Dashboard
As an administrator, I want to view a dashboard so that I can understand the organization's financial activity.

Acceptance criteria:
- I can view total expenses.
- I can view pending approvals.
- I can view approved and rejected expenses.
- I can view budget utilization.
- I can view recent activities.

# 7. Expense Status Workflow

An expense can have the following statuses:

- Pending Manager Approval
- Pending Administrator Approval
- Approved
- Rejected

Possible transitions:

- Pending Manager Approval → Pending Administrator Approval
- Pending Manager Approval → Approved
- Pending Manager Approval → Rejected
- Pending Administrator Approval → Approved
- Pending Administrator Approval → Rejected

Approved and rejected expenses are final in version 1.0.

# 8. Non-Functional Requirements

## Security
- Enforce backend authorization.
- Secure password storage.
- Validate uploaded files.
- Protect against unauthorized data access.
- Keep sensitive configuration outside source code.

## Performance
- Use database indexes where appropriate.
- Implement pagination for expense listings.
- Avoid unnecessary database queries.
- Optimize report queries.

## Reliability
- Use database transactions for critical operations.
- Prevent duplicate approval actions.
- Log application errors.
- Handle failed notification delivery gracefully.

## Maintainability
- Follow Django conventions.
- Separate business logic from API views.
- Use reusable components.
- Write automated tests.

## Data Integrity
- Validate expense amounts.
- Preserve approval history.
- Maintain accurate budget calculations.
- Prevent unauthorized changes to finalized expenses.

# 9. Technology Stack

| Component | Technology |
|---|---|
| Language | Python |
| Backend | Django |
| API | Django REST Framework |
| Database | PostgreSQL |
| ORM | Django ORM |
| Authentication | Django Authentication |
| File Storage | Local storage initially |
| Testing | pytest / Django Test Framework |
| Version Control | Git and GitHub |
| Deployment | Docker and cloud hosting |

# 10. Out of Scope — Version 1.0

To keep development manageable, these features will not be implemented initially:

- Actual bank transfers and reimbursements.
- Subscription and billing management.
- External accounting integrations.
- Mobile applications.
- AI-powered receipt processing.
- Microservices.
- Complex configurable workflow engines.
- External email and SMS notifications.

# 11. Definition of Done

EnterpriseFlow v1.0 is complete when:

1. Employees can register and authenticate.
2. Role-based permissions work correctly.
3. Employees can submit expenses and receipts.
4. Managers can approve and reject expenses.
5. Multi-level approvals work based on expense amount.
6. Categories and budgets can be managed.
7. Financial reports produce accurate results.
8. Audit logs record important activities.
9. In-app notifications work.
10. Administrative dashboard APIs return accurate data.
11. Automated tests cover core workflows and security rules.
12. The application is deployed and accessible.

---

**Final Product Goal:**

Build a maintainable Django expense management platform that demonstrates real-world backend engineering, database design, business logic, security, testing, and deployment capabilities.
