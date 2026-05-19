# Patient Referral & Triage System — Domain Scope

## 1. Project Purpose

This project simulates a real-world healthcare referral workflow, where patient referrals are submitted, clinically reviewed, prioritised through triage, and routed to the appropriate healthcare department for further care.

### It enables:
- Referral submission
- Clinical review
- Priority assignment
- Approval/rejection/escalation
- Department routing
- Audit tracking

## 2. Business Problem
Healthcare providers need an efficient and reliable way to assess incoming patient referrals and ensure they are directed to the right clinical department based on urgency and specialist care requirements.

In many healthcare settings, referral workflows can be slowed down by manual triage processes, limited visibility into referral progress, and inconsistent routing decisions. These challenges can lead to delays in patient care, reduced operational efficiency, and difficulties in maintaining clear audit trails for clinical accountability.

### Key Challenges

- Delays caused by manual triage and review processes
- Limited visibility into the current status of referrals
- Lack of clear audit tracking for referral decisions
- Inefficient routing to appropriate clinical departments

## 3. Core Workflow

GP submits referral
      ↓
Clinical review queue
      ↓
Triage assessment
      ↓
Decision outcome
 ↙     ↓      ↘
Approve Reject Escalate

## 4. Workflow Summary

A referral begins when a GP submits a request for specialist care. The referral is placed into a clinical review queue, where it is assessed by a clinician and assigned a priority level based on urgency and clinical need.
Following review, the referral may be:
- **Approved**, allowing it to be routed to the appropriate department
- **Rejected**, with feedback returned to the requester
- **Escalated**, requiring further assessment by a senior clinician

## 5. Core Domain Entities

### Patient
Represents the individual receiving healthcare services through the referral process.

**Responsibilities**
- Stores patient contact and identifying information
- Maintain referral historty for continuity of care
- Links referrals to the appropriate clinical pathway

### Referral

Represents a request for specialist clinical review submitted on behalf of a patient.

**Responsibilities**
- Tracks the current status of the referral throuhout its lifecycle.
- Manages state transitions such as submitted,under review,approved,rejected, or escalated
- Holds all relevant clinical and administrative details required for decision-making

### Clinician

Represents a healthcare professional responsible for reviewing patient referrals and making clinical decisions.

**Responsibilities**
- Review patient referrals as part of the clinical triage process
- Makes decisions to approve,reject, or escalate referrals based on clinical assessment
- Ensures referrals are directed to the appropriate care pathway or senior review when required

### Triage Assessment

A triage assessment captures the clinician’s evaluation of the referral, including the clinical reasoning behind the decision and the assigned level of priority.

**Responsibilities**
- Record the outcome of the clinical review(approved/rejected or escalated)
- Stores clinical notes and supporting observations made during assessment
- Assigns a priority level based on clinical urgency and patient need

### Department

A department acts as the destination within the referral pathway, ensuring patients are directed to the correct area of care based on their clinical needs.

**Responsibilites**
- Receives and processes referrals that have been approved through triage
- Manages incoming referral flow and ensures appropriate allocation within the team

### AuditLog

The audit log captures key actions performed within the system, helping to maintain accountability for changes made to referrals and related clinical decisions.

**Responsibilities**
- Records who performed an action and what changes were made
- Maintain a history of system events for auditing purposes

## 6. Value Objects

- PriorityLevel
- ReferralReason
- NHSNumber
- ContactDetails
- DecisionReason

## 7. Business Rules

- Referrals must belong to a patient
- Cancelled referrals cannot be approved
- Only assigned clinician may triage
- Emergecy referrals bypass standard queue
- Approved referrals must route to department

## 8. Referral State Lifecycle

A referral moves through a controlled workflow as it progresses from submission to a final outcome. Each stage represents a key step in the clinical decision-making process.

Submitted
   ↓
UnderReview
   ↓
Approved / Rejected / Escalated

### Invalid Transitions
- A rejected referral cannot be moved back to approved
- A cancelled referral cannot transition to approved

## 9. Architecture Intent

This project is designed with a focus on clean separation of concerns and maintainable domain modelling. It follows a structured architectural approach to ensure the system remains testable, scalable, and easy to evolve over time.

The system will be built using the following principles and patterns:

- Clean Architecture to separate domain, application, and infrastructure concerns
- Domain-Driven Design (DDD) to model the healthcare referral process around real business concepts
- CQRS to clearly separate read and write operations
- MediatR to decouple request handling and improve maintainability
- Unit Testing to ensure business rules and domain logic are reliably validated
- In-memory persistence in the initial phase to keep the system simple and focused on domain modelling

## 10. Out of Scope (Phase 1)

To keep the initial implementation focused on core domain modelling and workflow design, certain features are intentionally excluded from the first phase of the project.

The following areas are not included in Phase 1:

- Authentication and user security management  
- Integration with external NHS systems or third-party services  
- Notification mechanisms (email, SMS, or alerts)  
- Distributed messaging or event-driven communication  
- Microservices architecture and service decomposition  