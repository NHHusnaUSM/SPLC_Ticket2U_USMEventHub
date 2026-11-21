# Task 4: Lean Waste Auditing & Extreme Programming (XP) Practice Alignment

## 1. Lean Waste Audit & Remedies

## 2. XP Engineering Practices
To eliminate late-night debugging sessions, repetitive manual testing, and coordination bottlenecks across our 5- member USM project team, our group aligns its engineering workflow with three core Extreme Programming (XP) practices: Pair Programming, Test-Driven Development (TDD), and Continuous Integration (CI). 

**1.	Pair Programming**
- Technical Definition & Analogy: Pair Programming involves two developers working together at a single workstation, whereby one acting as the Driver writing the implementation and the other acting as the Navigator reviewing logic and edge cases in real time. Technically, this mirrors dual- core processors sharing a single task for redundancy and efficiency. 
- Application to USM Event Management Hub: Instead of assigning isolated silos where members work alone until the deadline, our group operationalizes our Main + Collaborates On matrix as active Driver–Navigator pairs:
  1. Member D (Acceptance Criteria & XP) pairs with Member C (Requirements) and Member E (V- Model & Governance) when defining validation logic and test rules for event registration capacity limits and QR ticket verification.
  2. Member A (SPEM & Quality) pairs with Member B (RACI & Lean) when aligning system architecture, quality constraints, and MyCSD point- logging workflows.
- Impact on Code Quality & Feedback Loops: Having two sets of eyes on high-risk event workflows catches double-booking edge cases, schema mismatches, and logic bugs immediately during development rather than hours before submission. This eliminates solo late-night troubleshooting and prevents single-point knowledge bottlenecks across the team.

**2.	Test-First Programming / Test-Driven Development (TDD)**
- Technical Definition & Analogy: TDD requires developers to write failing automated tests before writing the minimal production code necessary to pass them. This is directly analogous to writing an assert() statement before implementing the actual function. 
- Application to USM Event Management Hub: Our group links TDD directly to our requirements workflow between Member C and Member D for core features such as student ticket registration and QR code event check-in:
  1. Red (Write Failing Test): Before implementing a feature, Member D translates Member C’s User Stories and Given-When-Then acceptance criteria into failing unit tests using assert() statements (e.g., asserting that registering for a full campus event returns a "Capacity Reached" error or that scanning an already-used QR pass is rejected). 
  2. Green (Minimal Code): The developer writes only the minimal function logic required to pass those assert() checks. 
  3. Refactor: Once the test passes, the developer cleans up internal code structures safely while verifying that the test suite remains green. 
- Impact on Code Quality & Feedback Loops: Automated test suites verify seat availability, duplicate registration prevention, and QR validation in seconds—completely eliminating repetitive manual form-filling and click-testing after every update. Developers receive immediate pass/fail feedback locally within seconds of saving their work.

**3.	Continuous Integration (CI)**
- Technical Definition & Analogy: Continuous Integration mandates that developers integrate and test their code frequently—multiple times a day—rather than holding unmerged changes locally. This functions as an auto-build and test process triggered after every commit to the main branch. 
- Application to USM Event Management Hub: Supervised by Member D (Evidence Lead), all five members (Members A, B, C, D, and E) push small, incremental commits (covering both report artifacts and prototype test specs) to our shared GitHub repository using their individual @student.usm.my email addresses over multiple weeks. We enforce CI through a GitHub Actions workflow that automatically triggers on every push and Pull Request to verify Markdown/file integrity, run linters, and execute our TDD test suite before Member A merges updates into main.
- Impact on Code Quality & Feedback Loops: Frequent integration exposes merge conflicts and "it works on my machine" environment discrepancies within minutes of a commit. This prevents last-minute integration failures and keeps our USM Event Management Hub repository in a clean, verified state at all times. 
