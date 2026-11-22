# Task 3: Symmetrical Verification & Validation (V-Model Design)
## V-Model Symmetrical Mapping

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
