# Time Off Module

## Context & Challenge

- OmniHR needed to enhance the time off module with multi-level parallel approvers and a redesigned time off tab.
- Since the release of the first iteration, clients had been requesting for more features in the time off module, with parallel approval flows at the top of the list. Some deals were lost due to the lack of this too. Time was ripe for the 2nd iteration.
- **Key entities**: Approval flows → Submissions → Approvals
- **Personas**: Admin (configures approval flows), Employee (submits time off, tracks approval status), Manager (approves requests)
- **The core design tension**: giving the employees the clarity of their time off balances while maintaining the flexibility to view their time offs either in visual or listing mode.
- **Strategic constraint**: this module's release needs to meet the timeline pressure and stay consistent with existng approval elements - so the tradeoff is exploration and execution time.

## My Role & Impact

- **Role**: Led design — research, wireframing, interaction design, UI design
- **Duration**: 3 months
- **Team**: 1 Designer (me), 2 PMs, 3 Devs, 2 QAs
- **Key contributions**:
  - Although we used existing approval status elements from the expense module, I proposed some visual tweaks to reduce the component variants to save dev/QA time.
  - Proposed the redesign of the time off page, which included calendar/listing toggle, time off summary cards, etc.
  - After shipping this iteration, we got positive feedback from customers citing the upgraded approval flows and refreshed UIs in the time off tab during the bi-weekly call with the sales and customer success team. It was a good indication that we were shipping features that met customers' needs.

## Process & Collaboration

- Audited all existing time off screens to identify which needed redesigning to support the new parallel approver feature.
- Mapped out all approval progress scenarios — including edge cases where approvers were deleted or dismissed mid-flow — to surface complexity before jumping into screens.
- I looked at competitor implementations for the summary cards, or referenced patterns from the Expense module for the approval statuses in the row items and the details page.
- Explored various layouts and discussed trade-offs with PMs and stakeholders before converging on the final direction. Conducted usability tests with colleagues when deciding between options.

## Key Design Decisions

### 1. Calendar vs. Listing View Toggle

**Situation**: The upgraded approval flow meant employees now needed to see approval status details — but the existing calendar view had no room for this, and the calendar space itself was already compromised by balance cards.

**Options considered**:

- An always-visible list below the calendar: it meant the user needs to scroll down everytime in order to see the statuses, which defeated the purpose of surfacing important things to the top.
- Inline status on calendar events: it meant additional dev effort for customization, which was not possible with tight timeline.
- Tabs instead of toggle: using tabs meant changing the section below the tab element, which was not possible as there are other sections that needs to persist below the calendar.
- Side panel for status details: it meant the user needed to click on the time off requests in order to view the details. Not useful when the events are months into the future; the user needed to toggle the calendar forward until that specific month, which was a hassle just to view the status.

**Decision**: Introduced a toggle to switch between calendar and listing views. The calendar view was fully optimised for available space, while the new listing view showed all active (ongoing or upcoming) time off applications with approval status, approver details, and progress.

**Rationale**:

- Employees needed two distinct mental modes: "when am I off" (calendar) vs. "what's the status of my requests" (listing). A toggle lets them switch contexts cleanly rather than the other options.
- With the calendar view, the user is able to see the upcoming time off for the current month at a glance, and for the next few months couple of clicks away.
- With the listing view, the user is able to see the statuses of all upcoming events in a single page, even if the request is months away.

**Result**:

- Admins now have access to more powerful approval flow, and employees have control over what they wished to see — who the approvers are, where it's stuck, and who to follow up with.
- When doing internal testing with colleagues pre-deployment, the feedback was that they had better clarity about their time off balances and statuses of the upcoming requests.

### 2. Parallel Approver Flow

**Situation**: In the previous version, each approval level could only have a single approver that covered everyone — not powerful enough to cater to the different needs of the organization. On top of that, the time off module has the concept of time off type and policy (where a type can have multiple policies) — a concept that didn't exist in the expense module, so the existing approval flow setup couldn't handle it out of the box.

**Options considered**:

- Reuse existing elements and add a new section to select the time off policies. Lower dev/QA effort.
- Introduce time off policy as a new criteria within the existing element. Higher dev/QA effort.

**Decision**: Reworked the approval flow and introduced time off policy as a new criteria within the existing element.

**Rationale**:

- Initially, we tried using the existing elements from the expense module and created a separate section to select the time off policies range first. We realised it was very difficult to create approval flows for some scenarios. E.g. for specific employees, admins needed to know their time off policies — which meant jumping off to another screen; for specific countries, admins had to select all time off policies, then select the countries. Neither was intuitive.
- Folding policy into the approval flow element itself catered to all the scenarios required, and made configuration easier and faster.

**Result**:

- Reduced approval flow configuration time by 25%.

### 3. Time Off Page Layout Redesign

**Situation**: The existing time off page had several usability issues: balance cards consumed calendar space, action buttons were hidden below the fold, the calendar legend was hard to reference, and secondary items like "work schedule" and "holiday config" looked out of place.

**Decision**:

- Moved time off balance cards to the top with a refreshed visual style — they're essential context before any action.
- Calendar legend moved up for easier reference.
- Action buttons grouped together and made visible (no more hiding below the fold).
- As "work schedule" and "holiday config", they are now repositioned to below the calendar. They are also revised to be consistent with the elements in the Setting module.

**Rationale**:

- Surfaced what's essential (balance, calendar, actions) and toned down what's not — so the page hierarchy matches how employees actually use it.
- I based the redesign on the hierarchy of usage. Employees who accessed this page usually had these few objectives: check balances, submit new requests, and check request statuses. So they should be the centerpiece of the tab.

**Result**:

- A more visually and hierarchically balanced page with essential sections at the top, allowing users the sense of control and full visibility immediately.

### 4. Pending Approval Count Framework

**Situation**: Previously, the time off request details page displayed only the number of days applied for; it lacked essential details like the available and remaining balance, and how many days are pending. The employee couldn't tell immediately if they had enough balances without pausing what they were doing to get those information. Their flow was interrupted.

**Options considered**:

- 1x4 grid; left-aligned
- 1x4 grid; center-aligned
- 2x2 grid; left-aligned
- 2x2 grid; center-aligned
- The center-aligned grids and 2x2 grid were not suitable as broke the reading flow and it used up more space than required.

**Decision**:

- Implement the balance overview section in 1x4 grid format.

**Other additions**:

- We ensured the balance overview section is coherent for every request of the same time off type that are still in pending status.
- When a request is in pending status, details like available balance and amount pending needed to refresh to reflect changes in other requests of the same type, e.g. employee submitted new request, another request got approved or declined, etc.
- Once a request gets approved, balance overview retains only the number of days applied while removing the rest.

**Rationale**:

- It fits the employee's mental model at different points of the time off request.
- When requesting, the **most important thing the employee needs to know is whether she has enough balance**. Which means the calculation in the balance overview section must be clear and complete.
- But once that request got approved, all those numbers didn't matter anymore, except for the number of days applied. Their mind has already moved on to the actual time off.

**Result**:

- A time off details page that provides relevant information at different points of the journey, and one that reflects the user's mental model.

## Reflection

- **What I'd do differently**:
  - Handle the scenario where approvers are deleted mid-flow, leaving submissions stuck with no recourse. At the time, we decided employees would need to reapply — a known gap we accepted due to time constraint and the low probability of occurrence.

- **What the system still can't do cleanly**:
  - Cater for unlimited leave types — instead of showing days available, these should show days taken. This requires a different card treatment.

- **What I learned**:
  - Redesigning modules taught me that the hardest problem isn't just visual refresh – it's about understanding the main outcomes of the user accessing the page and designing for time.
