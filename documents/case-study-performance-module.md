# Performance Module

## Context & Challenge

- OmniHR needed a performance review module to give organisations a reason to consolidate onto the platform — both as a **migration incentive** for new clients and a **retention lever** for existing ones.
- The module allows organisations to create review templates, launch review cycles, and manage multi-directional feedback across employees, managers, peers, and subordinates.
- **Key entities**: Templates → Cycles → Review phases
- **Personas**: Admin, Reviewee (Employee), Reviewers (Manager, Peers, Subordinates)
- **The core design tension**: giving admins powerful configuration options while keeping the experience clear and trustworthy for end users. A reviewee or reviewer seeing the wrong information at the wrong moment breaks trust in the entire system.
- **Strategic constraint**: this module needed to meet the majority of use cases without becoming a standalone appraisal product — so every feature decision was a trade-off between depth and simplicity.

## My Role & Impact

- **Role**: Led design end-to-end — research, competitive analysis, wireframing, interaction design, UI design
- **Duration**: 5 iterations over 2 years, scaling from 2 review types to 4, then integrating with Goal Setting
- **Team**: 1 Designer (me), 2 PMs, 4 Devs, 2 QAs
- **Key contributions**:
  - [Drove the visibility rules framework that became the foundation for how all review responses are surfaced — describe the decision you championed]
  - [Advocated for / pushed back on a specific scope decision — describe what and why]
  - [Outcome: e.g. "X clients cited the module as a migration factor", "reduced admin setup time by Y", "support tickets around review visibility dropped by Z%"]

## Process & Collaboration

- Started with competitive analysis across [X] appraisal tools — identified gaps we could exploit (e.g. [specific gap]) and features we needed to match to be credible.
- Defined scope for each iteration collaboratively with PMs and stakeholders. [Describe a moment where you influenced scope — what did you push to include or cut, and why?]
- Mapped end-to-end user journeys for all personas before jumping into screens. This surfaced edge cases early — particularly around visibility timing — and saved rework downstream.
- [Describe how you validated designs — usability testing, client feedback, support ticket analysis, PM reviews, beta rollouts, etc.]
- Moved to hi-fi designs and created dev handoff presentations to align on interaction details and reduce back-and-forth during implementation.

## Key Design Decisions

### 1. Visibility Rules Framework

**Situation**: Expanding from Self & Manager Review to include Peer & Upward Review introduced a new problem — whose responses can the reviewee and manager see, when, and whether reviewer identities are anonymous.

**Options considered**:
- [Option A — e.g. simple toggle per review type. Why this wasn't enough.]
- [Option B — e.g. the matrix approach you chose. Why this was better.]

**Decision**: Introduced a two-layer visibility configuration in the review cycle creation flow:
1. "Can they view results" — lets the admin choose whether reviewee and manager can view each persona's responses, and when.
2. "Can they view the name of the reviewer" — controls identity anonymity per persona.
- For certain persona combinations, the first setting constrains the options of the second — reducing admin error.

**How we got there**: Mapped out all visibility scenarios across the 2 main user roles (reviewee and reviewing managers). These maps doubled as alignment tools with PMs and devs — we used them to agree on interactions and views before building.

**Rationale**: [Why this approach was the right trade-off — what did it enable that simpler approaches couldn't? What risk did it mitigate?]

**Result**: [Reusable component system that scaled across review types / reduced admin configuration errors / client feedback, etc.]

### 2. Redesigning for Multi-Review Types

**Situation**: The original UI was designed for only self and manager reviews. Adding peer and upward review meant up to 5 review types + 2 selection periods per row — the existing 2-column card layout couldn't accommodate this.

**Options considered**:
- [What other layouts or approaches did you explore? Why were they rejected?]

**Decision**: Revised to a 2-row card layout:
- Row 1: essential performance cycle details
- Row 2: statuses of selected review types for the cycle

Other changes:
- Introduced a progress bar combining absolute numbers and completion percentage on the event details page — giving admins both the "how many" and "how far along" at a glance.
- Increased spacing between review period and status for better scannability.
- Split the task page into "My Review" (reviews and responses about me) and "Team Review" (reviews and responses for subordinates, peers, and direct managers) — separating personal and managerial contexts.

**Rationale**: [Why the 2-row layout won over alternatives. What user need or usability principle drove the My Review / Team Review split?]

**Result**: [How this performed — admin feedback, reduced confusion, scalability for future review types, etc.]

## Reflection

- **What I'd do differently**:
  - Use a different layout for the My Review and Team Review cards to reduce wasted space.
  - [Any other process or collaboration changes?]
- **What the system still can't do cleanly**:
  - Handle cases where employees miss deadlines or need individual deadline extensions — this still requires backend intervention. [What would you propose to fix this? This shows forward-thinking.]
- **What I learned**:
  - [Key takeaway about designing configurable systems, balancing admin power vs. end-user simplicity, working within strategic constraints, etc.]

## Assets
