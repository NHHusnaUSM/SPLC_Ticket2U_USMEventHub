# Task 5: Process Tailoring (Münch's 4 Ps) & Human Factors Governance

# 5.1 Tailoring with Münch's 4 Ps

There is no single methodology that fits Ticket2U perfectly. If we used a heavyweight process everywhere, it would create massive waste. If we used a lightweight process everywhere, it would put critical features at risk. We analyze the context of Ticket2U using Münch's process tailoring framework across four factors: Problem, Project, People, and Product. Then, we compare it with our own project, USM Event Hub.  

Based on this analysis, we propose a **hybrid prescriptive approach**:  
*   **Scrum** for rapidly changing front-end work.
*   **Formal V-Model verification gates** for the secure back-end (payment, atomic cart reservation, and automated tier transitions).  

*This analysis of Ticket2U is based on public information (Ticket2U, 2020; Ticket2U, 2023), and where we assume internal practices, we explicitly state so.*

### Table 5.1: Summary of Tailoring Factors

| Factor | Ticket2U (audited company) | USM Event Hub (our project) | Effect on process |
| :--- | :--- | :--- | :--- |
| **Problem** | Many buyers compete for limited tickets at once (Ticket2U, 2023), and organizers ask for new features or ticket tiers at short notice. | Lower stakes, but a set deadline. Requirements change as we learn what USM clubs actually need. | Iterative delivery (Scrum) for evolving requirements. Rigid logic (V-Model) for simultaneous purchases. |
| **Project** | Short release cycles and security compliance requirements *(Assumption: Due to having to integrate multiple e-wallet and FPX payment gateways)*. | Team of 5 students, one-semester deadline, zero budget, and academic grading criteria. | Front-end: Fixed-length Scrum sprints. Backend: V-Model gate checks before release. |
| **People** | A mix of senior developers with experience and junior developers who need guidance *(Assumption: Based on standard tech company structures)*. | Second-year students who need a high level of collaboration and peer learning, and have limited software engineering experience. | Step-by-step V-Model documentation for junior members and Scrum collaboration like Daily Standups. |
| **Product** | Managing payment and inventory where failure is costly, like high-demand ticket sales for stadium audiences of over 100,000 (Ticket2U, 2020; Ticket2U, 2023). | A university event registration system that deals with student user data but has no real money transactions. | Strict V-Model Verification & Validation on Ticket2U's critical back-end. Pure Agile for USM Event Hub. |

### 1. Problem (Complexity, Novelty, and Volatility of Constraints)

**Analysis:** The requirements are volatile because event organizers often want new features or ticket tiers within days of announcing an event. The problem is also complicated: if many buyers are competing for the last tickets at the same moment, the system has to decide fairly who gets them. In USM Event Hub, our requirements altered mid-semester when we learned that students prefer a simplified version over a complex multi-step registration process, requiring us to adjust our UI design.  

**Tailoring:** Volatile requirements require short Scrum iterations where new organizer-facing features can be built and adjusted rapidly. The complex concurrency problem supports the need for more rigid requirements and design in the reservation logic upfront. 

### 2. Project (Team Size, Distribution, Budget, and Schedule)

**Analysis:** We assume that Ticket2U ships features in short cycles and meets the payment security requirements such as FPX gateway standards (Ticket2U, 2020). The USM Event Hub is created by a team of 5 students in one semester with no budget.  

**Tailoring:** We propose front-end features be done in two-week sprints. Before any sprint can go to production, back-end changes have to pass a mandatory V-Model verification gate that includes automated load testing, security testing, and database integrity checks. The QA Lead confirms all checks are passed and the gate is passed.  

### 3. People (Skill Levels, Team Cohesion, Culture, and Turnover)

**Analysis:** Ticket2U likely has both experienced and junior developers *(assumption based on standard tech company structures)*. Senior engineers tend to thrive in the autonomy of self-organizing teams, whereas junior developers need more structure. In USM Event Hub, our team consists of 5 students with different skill levels; two members are strong in backend logic, while the others are stronger in UI/UX, requiring us to pair together to balance the skill.  

**Tailoring:** Scrum events like daily stand-ups and sprint retrospectives promote collaboration. The step-by-step verification documented in the V-Model provides clear guidance for less experienced developers and helps avoid mistakes in sensitive payment logic.  

### 4. Product (Criticality, Reliability, Lifespan, and Security Needs)

**Analysis:** This is very critical as the customer will lose money and trust if a crash happens when buying a ticket that is in high demand, or if the payment is not processed (Ticket2U, 2023). Thus, the back-end should be reliable and secure. The user interface can change more freely.  

**Tailoring:** The front-end is agile for quick changes. The backend (atomic cart reservation, automated tier transitions, and payment integration) is implemented via the V-Model, where each change to the database schema is verified before its integration.  

### Scope of Validity and Refinement

Only the payment, reservation, and tier-transition components are subject to the V-Model gates. Front-end work uses Scrum. This avoids the chaos of ad-hoc Agile and the over-formalization of a fully linear Waterfall process. We will regularly review this tailoring with feedback from sprint retrospectives. Our group chose this strategy in a Fist-of-Five vote **(refer in Appendix X)**.

# 5.2 Tuckman’s Team Dynamics & Fist-of-Five Governance 

## Tuckman's Team development analysis: 
To ensure our group of 5 students could effectively engineer the process tailoring for Ticker2u and the USM Event Hub, we evaluated our team dynamics using Tuckman's model of group development.

**Forming:** The first phase focused on team ground rules and consenting on the case study (Ticket2U vs. USM Event Hub), as well as identifying team roles with the RACI model. To avoid overlapping of responsibilities and project coordination, each member was given specific tasks to perform according to his/her role and strength. This provided a clear direction and foundation for the team's collaboration.  

**Storming:** There was conflict during the requirements review. Member C suggested implementing a 10 minute checkout timer for User Story 2. Member E responded to this with a technical issue that would result in a "race condition" between the database and the FPX payment gateway, a serious issue.   

**Norming:** The disagreement was not allowed to stop team progress, but was used to discuss and reach a compromise for the options using the 'fist-of-five' consensus approach. The team was able to discuss openly and overcome the technical problem and agree to a new rule for the boundary.  

**Performing:** The team has now overcome the process and requirements conflicts and is in the Performing stage. The members are drafter up with the support of efficient report section drafting, efficient peer reviews, and efficient handling of GitHub commits without the need of constant supervision.  

**Adjourning:** The team will go into the Adjourning stage when submitted. The Group Contribution Log has already been signed to avoid any problems with the handover and avoiding disputes after the project has been completed. 

## Fist-of-Five Consensus Gate 
To formally agree on our process tailoring strategy, we utilized the Fist-of-Five consensus method. This method ensures that every member has voice and prevents false consensus, groupthink, and silent resistance during group decisions. 

Please refer to Appendix D for the proof of Fist-of-Five voting. 

**The Initial Proposal**

Member C offered the team the initial idea for User Story 2, asking them to add a 10 minute countdown timer when checking out. This would automatically cancel the transaction if the timer reached 0 and return the ticket back to the Public Pool. The idea behind this was that the users who abandoned a checkout process without completing payment should not have their tickets reserved indefinitely. 

**The 'Two' and the Vote**

In the first voting round, Members A, B and D scored 5 and 4, representing high levels of support for the proposed 10 minute checkout limit. The other member C also scored the proposal 4. Another member (Member E) who was the QA and Testing Lead however scored a lot lower at 2. 

The governing body rules that a vote of 2 should be a vote to delay decision making until the concern is resolved. Member E raised the concerns that the limit of 10 minutes might present a real race condition. If a user is still on the FPX bank payment screen when the timer expires, the bank may send out the ticket before they are made. One user may buy a ticket when the first user's FPX webhook is received and then another user buy the same ticket 10 seconds later, resulting in the system potentially double-booking the ticket and double-charging the user. 

**The Discussion and Resolution**

The team abandoned the decision making process and discussed the technical risks before proceeding with the original proposal. Member C expressed his appreciation for Member E's concern and called for more suggestions regarding the issue. 

Member E offered an alternative by suggesting an extra 2 minutes grace period added as a Pending Payment grace period in the database. With this new method, users would still be presented with a 10 minute countdown timer on the checkout page but the ticket would be locked in the Redis store for an additional 2 minutes for a total of 12 minutes of reserving time. This would give enough time for the FPX payment webhook to validate the payment before releasing the ticket into the public pool. 

**Final Consensus**

With the discussion the team reached consensus that the proposed 12 minute backend lock, with the 10 minute user-facing countdown, would be a good way to clear the race condition without allowing ticket hoarding. 

Member E then voted from 2 to 5, which meant that the technical issues had been taken care of. The team's Definition of Done was agreed upon with 100% consensus as all 5 members scored 4 or more. This agreement enabled the team to advance to the requirements phase and to transition to the Performing stage without any hassles. 

