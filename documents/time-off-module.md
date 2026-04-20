# Time Off Module

## Context & Challenge

- OmniHR needed to enhance the time off module with multi-level parallel approvers and a redesigned time off tab.
- Since the release of the first iteration, clients had been requesting for more features in the time off module, with parallel approval flows at the top of the list. Some deals were lost due to the lack of this too. Time was ripe for the 2nd iteration.
- **Key entities**: Approval flows → Submissions → Approvals
- **Personas**: Admin (configures approval flows), Employee (submits time off, tracks approval status), Manager (approves requests)
- **The core design tension**: giving the employees the clarity of their time off balances while maintaining the flexibility to view their time offs visually or not.
- **Strategic constraint**: this module's release needs to meet the timeline pressure and stay consistent with exisitng approval elements - so the tradeoff is the exploration time .

## My Role & Impact

- **Role**: Led design — research, wireframing, interaction design, UI design
- **Duration**: 3 months
- **Team**: 1 Designer (me), 2 PMs, 3 Devs, 2 QAs
- **Key contributions**:
  - While we used the existing approgval status elements taken from the expense module, I proposed a visual tweak to reduce the component variants to save dev/QA time.
  - Proposed the redesign of the time off page, which included calendar/listing toggle, time off summary cards, etc.
  - [YOUR INPUT: Measurable or qualitative outcomes — e.g. did CS tickets about approval confusion drop? Did any customer cite this feature? Did the reduced component variants save dev/QA time? Any adoption data?]

## Process & Collaboration

- Audited all existing time off screens to identify which needed redesigning to support the new parallel approver feature.
- Mapped out all approval progress scenarios — including edge cases where approvers were deleted or dismissed mid-flow — to surface complexity before jumping into screens.
- [YOUR INPUT: What inputs informed your designs? E.g. did you review CS feedback, look at competitor implementations, or reference patterns from the Expense module's approval flow?]
- [YOUR INPUT: How did you validate? E.g. did you review with PMs/devs early? Run through flows with colleagues? Create handoff presentations?]
- Explored various layouts and discussed trade-offs with stakeholders before converging on the final direction.

## Key Design Decisions

### 1. Safety Net for Approval Scoping

**Situation**: Introducing parallel approvers also meant introducing approval scopes — letting admins define which employees are funnelled into which approval flow. This created a new risk: employees who don't match any defined scope would have no approval flow at all.

**Options considered**:

- [YOUR INPUT: What alternatives did you consider? E.g. auto-assigning unscoped employees to a default manager? Blocking submission if no flow matched? Requiring admins to manually cover all employees?]

**Decision**: Created a priority-ordered rule system where each row in the approval flow listing represents a scoped rule. Admins can drag to reorder priority (top = highest). At the bottom sits a permanent "safety net" rule — it catches any employee not matched by the rules above. It cannot be deleted or moved.

**Rationale**:

- [YOUR INPUT: Why this pattern over the alternatives? E.g. did it reduce admin cognitive load? Was it inspired by how firewall rules or CSS cascading work? Did it align with how admins already thought about exceptions?]

**Result**:

- [YOUR INPUT: How was this received? Did it eliminate a class of support tickets? Did admins find it intuitive?]

### 2. Calendar vs. Listing View Toggle

**Situation**: The upgraded approval flow meant employees now needed to see approval status details — but the existing calendar view had no room for this, and the calendar space itself was already compromised by balance cards.

**Options considered**:

- [YOUR INPUT: What alternatives did you explore? E.g. a side panel for status details? Tabs instead of a toggle? An always-visible list below the calendar? Inline status on calendar events?]

**Decision**: Introduced a toggle to switch between calendar and listing views. The calendar view was fully optimised for available space, while the new listing view showed all active (ongoing or upcoming) time off applications with approval status, approver details, and progress.

**Rationale**:

- Employees needed two distinct mental modes: "when am I off" (calendar) vs. "what's the status of my requests" (listing). A toggle lets them switch contexts cleanly rather than cramming both into one view.
- [YOUR INPUT: Any additional reasoning — e.g. did this mirror patterns elsewhere in OmniHR? Was the listing view also useful for managers?]

**Result**:

- Employees now have visibility into the full approval flow — who the approvers are, where it's stuck, and who to follow up with.
- [YOUR INPUT: Any feedback or adoption data?]

### 3. Streamlining the Approver Component

**Situation**: In the Expense module, the approver column had several component variants for different numbers of approvers, creating a maintenance burden for design and development.

**Options considered**:

- [YOUR INPUT: Did you consider keeping the existing multi-variant approach? A fully dynamic/generic component? Something else?]

**Decision**: Streamlined to only 2 variants: single approver and multiple approvers. Pending approvals show the number of approvers and a purple badge on the avatar.

**Rationale**: Two variants cover all cases without the combinatorial explosion of the previous approach. This reduced the maintenance surface for both the design system and front-end code.

- [YOUR INPUT: Any additional reasoning — e.g. did you validate that these 2 variants handled all edge cases across modules?]

**Result**:

- [YOUR INPUT: Did this reduce dev/QA effort? Was the pattern adopted back into the Expense module too?]

### 4. Time Off Page Layout Redesign

**Situation**: The existing time off page had several usability issues: balance cards consumed calendar space, action buttons were hidden below the fold, the calendar legend was hard to reference, and secondary items like "work schedule" and "holiday config" looked out of place.

**Decision**:

- Moved time off balance cards to the top with a refreshed visual style — they're essential context before any action.
- Calendar legend moved up for easier reference.
- Action buttons grouped together and made visible (no more hiding below the fold).
- [YOUR INPUT: How did you handle "work schedule" and "holiday config"? Where did they go?]

**Rationale**:

- Surfaced what's essential (balance, calendar, actions) and toned down what's not — so the page hierarchy matches how employees actually use it.
- [YOUR INPUT: Any additional reasoning — e.g. did you base the hierarchy on usage data or CS feedback?]

**Result**:

- [YOUR INPUT: Any feedback from users, PMs, or CS?]

## Reflection

- **What I'd do differently**:
  - Handle the scenario where approvers are deleted mid-flow, leaving submissions stuck with no recourse. At the time, we decided employees would need to reapply — a known gap we accepted due to [YOUR INPUT: why was this deferred? Timeline? Complexity? Awaiting backend support?].
  - [YOUR INPUT: Anything else you'd approach differently in hindsight?]
- **What the system still can't do cleanly**:
  - Cater for unlimited leave types — instead of showing days available, these should show days taken. This requires a different card treatment.
- **What I learned**:
  - [YOUR INPUT: What's the design principle or insight you took away? E.g. "Designing approval systems taught me that the hardest UX problem isn't the happy path — it's making failure states (deleted approvers, unmatched scopes) visible and recoverable instead of silently broken."]

## Assets
