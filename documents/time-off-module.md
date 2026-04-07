# Performance Module

## Overview

- Enhance the time off module with multi-level parallel approvers + redesign of time off tab
- Key entities: Approval flows → Submissions → Approvals
- The personas: Admin, Employee, Manager

## Business Objectives & Design Outcome

- **User case 1**: Demonstrate that OmniHR is constantly enhancing its core modules and address customer requests for the parallel approver feature.
- **Design outcome**: On top of revamping the existing pages to meet the needs of the augmented features, we also took the chance to refine them: surface up what’s essential and tone down what’s not.

## Role & Timeline

- **My Role**: research, wireframing, interaction design, UI design
- **Duration**: 3 months
- **Cross-Functional Team**: 1x Designer, 2x PMs, 3x Devs, 2x QAs

## Process

- Audit the current screens and identify those that needed redesigning to meet the new features
- Explored various layouts and discussed with stakeholders
- **Important**: to map out all the various approval progress scenarios. Need to cover cases where approvers were deleted / dismissed.

## Deep Dive 1: Parallel Approvers

### Intro

- When bringing over parallel approvers to time off module, we did too the approval scope. It allows the admin to define the scope of employees who will be funnelled into a specific approval flow.
- The challenge here is to come up with a solution – **a safety net** – that’s able to catch any employees who managed to fall through all the approval scopes.

### Before

- Admin was able to only create one approval flow that has single approver for multi levels.

### After

- Expanded function to define the employee scope of the approval rule.
- Stacking the conditions to define the criteria for the employee scope.
- While admin can define multiple approvers for each level, where only one is required to approve for that level.
- At the approval flow listing page, each row is a rule that admin can move around to change its priority. Rules at the top has higher priority.
- At the bottom is the "safety net" rule for any employee who doesn’t belong to any of the rules defined above. It can neither be deleted nor moved around.

## Deep Dive 2: Redesign the Time Off Page

### Intro

- Challenge for the upgraded approval flow: Provide the employees a way to see the approval status details apart from the calendar view, and at the same time, optimise the space for the calendar.

### Before

- Space for calendar wasn’t optimised; they were taken up by the balance cards.
- There's no place to display the approval status of the time off submissions.
- The “work schedule” and “holiday config” looked out of place.
- The “add time off type” is pushed out of screen as more cards are added.
- At the Expense module, there were several variants for different # of approvers. It also meant we needed to maintain a component with lots of variants.
- In the time off details card, the employee wasn't able to see the progress of the approval flow.

### After

- Time off balance cards are pretty essential: they are moved to the top with refreshed visual style.
- Calendar legend moved up for easier reference.
- Action buttons are grouped together now (no more hiding below).
- We introduced a toggle to switch between calendar and listing views.
  Calendar fully optimised for the space available (also for the listing view).
- The new listing view of all active time off applications. Active means ongoing or upcoming time offs.
- Pending approvals shows the # of approvers and the purple badge at the avatar.
- We took the chance to streamline the approver col to only 2 variants: single / multiple approvers. Meaning it's now easier to maintain.
- Employee now has visibility of the status of approval flow, and who the approvers are. If the flow is stuck at a level, they can now look for the relevant approvers.

## Reflection

- Things we hope to do in the next iteration:
  - Handle the scenario where the approvers were deleted and got the submission stuck at his level. At that time, we decided to leave it stuck with no recourse; employees need to apply for a new time off.
  - Cater for unlimited leave type. Instead of showing # of days available, we need to show # of days taken.

## Assets
