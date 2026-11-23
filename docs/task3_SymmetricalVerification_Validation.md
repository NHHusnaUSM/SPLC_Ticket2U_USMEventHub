# Task 3: Symmetrical Verification & Validation (V-Model Design)
## V-Model Symmetrical Mapping
The V-Model above shows the symmetrical Constructive Design and Analytical Testing Phase for our secure payment and ticket reservation functionality. The horizontal arrows do not allow for late stage afterthought testing, with test plans on the right at the same time as specification on the left and all quality attributes and technical constraints are traceable. 

- Requirement specification ↔ Acceptance testing 

Verification (Design): Define core requirements such as secure payments, zero double charging and valid QR acceptance only. 

Validation (Testing): Uses real user sandbox payments and penetration tests to verify that the system is secure and ready for deployment. 

- System Analysis ↔ System Testing 

Verification (Design): Define performance target of a checkout response time of  less than 2.0 seconds under a peak load of 500 concurrent users. 

Validation (Testing): Executes load test with 500 virtual users, measuring the 80th percentile (p80) response time to prove it meets the 2.0s target. 

- Architecture Design ↔ Integration Testing 

Verification (Design): Maps the system's core components, including the Frontend, database (DB), Redis Lock and Bank API. 

Validation (Testing): Testing end to end integration to ensure seamless communication, such as ensuring the frontend processes payments, the DB stores records correctly, and Redis handles timeout locks without deadlocks. 

- Detailed Design ↔ Unit Testing 

Verification (Design): Defines the internal logic and secure routines for payment handling, database queries and transaction scenarios. 

Validation (Testing): Test individual components at the code level, such as ensuring 

invalid QR codes are rejected and payment timeouts are handled gracefully. 

-Coding (Implementation) 

Developers convert the designs into executable code. They write the source code, configure secure environment variables and manage version control via Github. Once implemented, the system undergoes the analytical testing phases to ensure code quality. 

The USM Event Hub and Ticket2U teams ensure that every performance target and security rule created on the left is tested and validated before it goes into production while adhering to this symmetrical mapping and parallel test planning. 

## Quality Attribute & Technical Constraints (Verification And Validation)
-	Non-Functional Quality Attribute: Checkout & Ticket Reservation Response Time (< 2.0 seconds under peak load)
  -	Verification
    -	Static code review and database query plan analysis to confirm indexed lookups
    -	Reviewing connection pool configurations and Redis TTL lock logic during Level 3/4 design inspections to ensure no blocking I/O locks stall the checkout thread.
  -	Validation
    -	Executing automated load tests simulating 500 concurrent USM students booking tickets during a 5 minute flash sale window.
    -	Pass outcome: 80<sup>th</sup>-percentile (p80) API response time remains strictly < 2.0 seconds with zero HTTP 500 errors or deadlocks, confirming the live system meets user speed expectations.
-	Technical Constraint:
  -	Verification
    -	Inspecting source code and security rulesets to confirm that secret keys are loaded from environment variables (never hardcoded) and that webhook handlers enforce constant-time signature comparison.
    -	Running automated unit tests with malformed, expired, and tampered QR payloads to verify rejection logic at the code level.
  -	Validation 
    -	Conducting live sandbox penetration/replay tests where a simulated attacker replays an intercepted FPX callback or scans a screenshot of a modified QR code at a mock DTSP entrance scanner.
    -	Pass outcome: the system rejects all forged/replayed requests (HTTP 401/409), issues zero duplicate tickets, and allows valid student QR codes to scan in under 1 second, proving operational security for event organizers.
