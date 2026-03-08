# Loan Management System

## Domain Model Document

### 1. Overview
This document describes the **domain model** for the Loan Management System (LMS). The domain model defines the core business entities,
their responsibilities, and the relationships between them. It represents the conceptual structure of the system before defining database 
tables or implementation details. The goal of the domain model is to ensure that the system accurately reflects 
the real-world loan management process used by financial institutions.

# 2. Domain Scope
The Loan Management System supports the complete lifecycle of a loan, including:
* Customer registration and authentication
* Loan application submission
* Document verification
* Credit risk evaluation
* Loan approval workflow
* Loan disbursement
* Repayment scheduling
* Notifications and audit tracking

# 3. Core Domain Entities
## 3.1 User
Represents a person interacting with the system.
Users may belong to different roles such as customers, loan officers, or administrators.

### Attributes
* userId
* username
* email
* accountStatus
* createdAt

### Responsibilities
* Submit loan applications
* Upload loan documents
* Track loan application status
* Receive system notifications

## 3.2 Role
Defines the access level and permissions associated with a user.

### Attributes
* roleId
* roleName
* description

### Example Roles
* CUSTOMER
* LOAN_OFFICER
* ADMIN

---

## 3.3 LoanApplication
Represents a request submitted by a customer to obtain a loan.
This entity is the central object of the loan processing workflow.

### Attributes
* applicationId
* applicantId
* loanType
* requestedAmount
* purpose
* status
* createdAt

### Status Values
* SUBMITTED
* UNDER_REVIEW
* APPROVED
* REJECTED
* DISBURSED

### Responsibilities
* Capture loan request details
* Manage loan processing status
* Link documents and approval workflow

---

## 3.4 LoanDocument
Represents documents submitted by a customer to support a loan application.

### Attributes
* documentId
* applicationId
* documentType
* fileLocation
* uploadedAt

### Example Document Types
* Identity Proof
* Income Statement
* Bank Statement
* Employment Verification

---

## 3.5 CreditAssessment
Represents the credit evaluation performed on a loan applicant.

### Attributes
* assessmentId
* applicationId
* creditScore
* riskCategory
* evaluationDate

### Responsibilities
* Assess financial risk
* Provide decision input for loan approval

---

## 3.6 Approval
Represents a decision taken by a loan officer or system workflow.

### Attributes
* approvalId
* applicationId
* approverId
* decision
* comments
* approvalDate

### Decision Types
* APPROVED
* REJECTED
* NEED_MORE_INFORMATION

---

## 3.7 Loan
Represents the approved financial agreement created after a loan application is accepted.
### Attributes

* loanId
* applicationId
* approvedAmount
* interestRate
* loanTermMonths
* startDate
* loanStatus

### Responsibilities
* Track loan lifecycle
* Manage repayment schedule

---

## 3.8 Disbursement
Represents the release of funds to the borrower after loan approval.

### Attributes
* disbursementId
* loanId
* disbursedAmount
* disbursementDate
* paymentMethod

---

## 3.9 PaymentSchedule
Represents the repayment structure of an approved loan.

### Attributes
* scheduleId
* loanId
* installmentNumber
* dueDate
* installmentAmount
* paymentStatus

### Payment Status Values
* PENDING
* PAID
* OVERDUE

---

## 3.10 Notification
Represents messages sent to users regarding system events.

### Attributes
* notificationId
* userId
* message
* notificationType
* sentAt

### Example Notifications
* Loan application submitted
* Loan approved or rejected
* Payment reminder

---

## 3.11 AuditLog
Tracks system actions for compliance and traceability.

### Attributes
* auditId
* entityType
* entityId
* actionPerformed
* performedBy
* timestamp

### Responsibilities
* Maintain audit trail
* Support regulatory compliance

---

# 4. Domain Relationships
The main relationships between domain entities are as follows:

* A **User** can submit multiple **LoanApplications**
* A **LoanApplication** may contain multiple **LoanDocuments**
* A **LoanApplication** has one **CreditAssessment**
* A **LoanApplication** may go through multiple **Approval** steps
* An approved **LoanApplication** results in a **Loan**
* A **Loan** has one **Disbursement**
* A **Loan** contains multiple **PaymentSchedules**
* A **User** can receive multiple **Notifications**
* System actions are recorded in **AuditLog**

---

# 5. Conceptual Domain Structure

User
│
├── LoanApplication
│     ├── LoanDocument
│     ├── CreditAssessment
│     ├── Approval
│     └── Loan
│           ├── Disbursement
│           └── PaymentSchedule
│
└── Notification

AuditLog records events across all entities.

---

# 6. Domain Boundaries for Microservices
The domain model can be divided into the following service boundaries:

### Identity Service
* User
* Role

### Loan Service
* LoanApplication
* Loan
* LoanDocument

### Credit Service
* CreditAssessment

### Approval Workflow Service
* Approval

### Payment Service

* PaymentSchedule
* Disbursement

### Notification Service
* Notification

### Audit Service
* AuditLog


