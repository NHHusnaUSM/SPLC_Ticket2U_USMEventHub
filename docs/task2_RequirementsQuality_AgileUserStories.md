# Task 2: Requirements Quality & Agile User Stories (INVEST & GWT)

## 2.1 Agile User Stories & INVEST 

**Feature Backlog Item:** Automatic Ticket Tier Transitions & Real-Time Atomic Cart Reservation System 

The selected feature is to enhance the handling of tickets for high demand events on Ticket2U. The system has two main features: automated ticket-tier transitions for event organizers and temporary ticket reservations for event attendees. The functionalities are designed to reduce manual intervention, improve the ticket buying experience and prevent over-selling of tickets. 

### User Story 1  

**Story:** As an event organizer, I want to be able to automatically move between ticket tiers based on sales quota limits or cut-off times, so that Early Bird tickets are closed and Regular tickets are open automatically without manual intervention or overselling. 

**INVEST Evaluation:** 

| INVEST Criteria | Evaluation | Justification |
| :--- | :--- | :--- |
| **Independent** | Partially | The ticket tier configuration UI can be built separately from the event page for attendees. But the automatic transition mechanism still uses ticket inventory and tier management components |
| **Negotiable** | Yes | The interface design and configuration options like dropdowns, date-time pickers, etc. can be discussed and adjusted with the product owner without changing the main functionality |
| **Valuable** | Yes | This feature decreases the manual effort of the organizer by toggling the ticket tiers automatically. It also stops false ticket availability and enables organizers to better manage high-demand events |
| **Estimable** | Partially | The configuration interface and basic transition logic can be estimated by the development team. However, there are other issues to consider such as quota monitoring, cutoff scheduling and inventory updates |
| **Small** | Partially | The story is about setting up automatic ticket-tier transitions. However, supporting both quota-based and timestamp-based conditions may involve several related development activities |
| **Testable** | Yes | We can then test the system to make sure that when the sales quota or cutoff timestamp is reached, the Early Bird tickets close automatically, and the Regular tickets are available. If 100 tickets have been sold in the Early Bird tier, the Regular ticket tier should be enabled automatically |

### User Story 2  

**Story:** As an event attendee, I want my selected tickets to be held for 10 minutes when I go to checkout so that the tickets aren’t available for anyone else to purchase while I complete my payment. 

**INVEST Evaluation:** 

| INVEST Criteria | Evaluation | Justification |
| :--- | :--- | :--- |
| **Independent** | Partially | The temporary reservation mechanism can be implemented regardless of the payment gateway integration. Still it relies on the ticket inventory and checkout components for proper ticket availability management |
| **Negotiable** | Yes | The length of the reservation like 10 minutes, 15 minutes, etc. is something that can be discussed and adjusted based on business needs and system performance considerations |
| **Valuable** | Yes | Temporary ticket reservations are an excellent way to improve the experience of purchasing tickets. While an attendee is completing the payment process, no other buyers can purchase the reserved tickets |
| **Estimable** | Partially | The dev team can estimate the reservation mechanism. More thought should be given to concurrent handling of reservations, inventory consistency and reservation expiration |
| **Small** | Partially | The story revolves around temporary ticket reservations during checkout. However, this requires a number of related activities like creating reservations, showing the countdown timer, handling ticket availability and releasing expired reservations |
| **Testable** | Yes | We can test the system to make sure reserved tickets are unavailable to other buyers during the reservation period and that they are automatically released when the 10 minute countdown expires without being paid successfully |

---

## 2. Given-When-Then (GWT) & Definition of Done

**USER STORY 1: AUTOMATED TICKET-TIER TRANSITION RULES**

After discussions with the Team Members, our Product Owner (PO) has negotiated with the Event Organizers that in this Sprint, the team will commit to delivering the web portal version of the automated ticket-tier transition rule.

*“As an **EVENT ORGANIZER** using the **TICKET2U WEB PORTAL** on a **DESKTOP** or **LAPTOP**, I want to **CONFIGURE AUTOMATED TICKET-TIER TRANSITION RULES** based on sold-out quota thresholds or cutoff timestamps so that Early Bird tickets close and Regular tickets open automatically without manual intervention or overselling.”*

Acceptance Criteria:

Given: An Event Organizer logged into the Ticket2U Web Portal with an active event containing "Early Bird VIP" (100-ticket quota) linked to "Regular VIP", When: The 100th "Early Bird VIP" ticket payment is confirmed by the payment gateway, Then: The system must automatically update "Early Bird VIP" status to SOLD_OUT within 2 seconds and switch "Regular VIP" from SCHEDULED to ON_SALE on the public event page. 

- Checklists: This test must pass when tested on:
  - Approved versions of Google Chrome and Microsoft Edge desktop browsers 
  - Automated backend integration tests simulating concurrent final-ticket payments (p95 latency < 2000ms) 
  - Peer code review and static analysis completed with zero critical/high vulnerabilities

Given: An Event Organizer on the Ticket-Tier Configuration page in the Ticket2U Web Portal, When: The Organizer attempts to save a tier rule with a Regular Tier start timestamp earlier than the Early Bird Tier end timestamp, or sets a quota exceeding total venue capacity (1,000 pax), Then: The system must block the save request and display an inline error message: "Tier schedule overlaps with an active tier or exceeds total event capacity (1,000)" while keeping existing live settings unchanged. 

- Checklists: This test must pass when tested on: 
  - Approved versions of Google Chrome and Microsoft Edge desktop browsers 
  - Boundary value unit tests covering quota = 0, quota = 1,001, and overlapping date-time inputs 
  - Database integrity verification confirming zero partial writes occur on failed validation


**USER STORY 2: ATTENDEE ATOMIC CART RESERVATION**

After discussions with the Team Members, our Product Owner (PO) has negotiated that in this Sprint, the team will commit to delivering the real-time cart reservation and countdown timer across both desktop and mobile web browsers. 

*“As an **EVENT ATTENDEE** purchasing tickets on the **TICKET2U WEBSITE** using a **DESKTOP**, **LAPTOP**, or **MOBILE BROWSER**, I want my **SELECTED TICKETS TO BE TEMPORARILY RESERVED WITH A 10-MINUTE COUNTDOWN TIMER** upon clicking checkout so that my tickets are not sold to another buyer while I complete FPX or eWallet payment.”*

Acceptance Criteria: 

Given: An Event Attendee viewing an event on Ticket2U with 5 General Admission tickets remaining in AVAILABLE status, When: The Attendee selects 2 tickets and clicks "Proceed to Checkout", Then: The system must atomically lock 2 tickets under the Attendee's session ID, decrement publicly visible stock to 3 tickets, and display a live 10:00 countdown banner on the payment screen. 

- Checklists: This test must pass when tested on: 
  - Approved versions of Chrome (Desktop & Android) and Safari (iOS) browsers 
  - Load-testing simulations with 2,000 concurrent users confirming atomic row-level locking (< 250ms response time) 
  - Verified FPX and Touch 'n Go eWallet sandbox payment completion within the 10-minute window

Given: An Event Attendee holding 2 tickets in RESERVED status with an active 10-minute checkout timer, When: The 10:00 countdown timer reaches 00:00 before Ticket2U receives a payment confirmation callback, OR two buyers attempt to lock the final 1 remaining ticket within the same millisecond, Then: The system must automatically release expired tickets back to AVAILABLE inventory and redirect the timed-out user with an expiration alert, while blocking the losing concurrent buyer with "Sorry, the last available ticket is currently reserved by another buyer". 

- Checklists: This test must pass when tested on: 
  - Approved versions of Chrome (Desktop & Android) and Safari (iOS) browsers 
  - Automated negative/boundary race-condition tests verifying zero ticket overselling (sold_count <= total_quota) 
  - Background cron/TTL worker verification ensuring expired locks release within 3 seconds of timeout


### DEFINITION OF DONE (DOD) – Ticket2U EVENT TICKETING MODULE ###

To eliminate ambiguity at Sprint closure and reduce the risk of incomplete features reaching live ticket drops, our Agile team enforces a formal Definition of Done (DoD) across all user stories. In alignment with standard Agile governance, a Ticket2U user story is only considered "Done" when it satisfies three core expectation pillars: 
1. Core Acceptance Criteria: All user story-specific Given-When-Then (GWT) scenarios covering positive execution paths as well as invalid input, timeout, and concurrency boundary cases must be fully satisfied. 
2. Process Compliance Guidelines: Mandated engineering standards must be applied universally to all stories, requiring code to be refactored, peer-reviewed, and verified with zero remaining static analysis warnings. 
3. Absolute Integration Verification: All code must be merged and integrated into the staging pipeline, unit and integration tests must pass 100%, and User Acceptance Testing (UAT) must be completed so the increment is fully deployment-ready.

