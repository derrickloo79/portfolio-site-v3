# Performance Module

## Overview

- Performance module allows organisations to conduct reviews of their employees’ performance to see how they are progressing.
- **Key entities**: Templates → Cycles → Review phases
- **Personas**: Admin, Reviewee (Employee), Reviewers (Manager, Peers, Subordinates)
- **Visibility matrix**: who sees what, when?
- The core design tension: power for admins vs. clarity for end users
- Why visibility and timing make this uniquely difficult (a reviewee/reviewer seeing the wrong thing at the wrong moment breaks trust in the whole system)

## Business Objectives & Design Outcome

- **User case 1**: Incentivise organisations to jump ship to OmniHR.
- **User case 2**: Encourage stickiness; no need to get a separate appraisal software.
- **Design outcome**: good enough features to meet majority of needs; not aiming to be the best appraisal software → not the key differentiation factor.

## Role & Timeline

- **My Role**: research, competitive analysis, wireframing, interaction design, UI design
- **Duration**: 5 iterations over 2 years (from just 2 to 4 review types to integrating with Goal Setting cycle)
- **Cross-Functional Team**: 1x Designer, 2x PMs, 4x Devs, 2x QAs

## Process

- Competitive research with competitor softwares; note down what we liked and don’t, what was missing in theirs that we can take advantage, what features could we match and not.
- Defined scope for each iteration with stakeholders
- Worked out the user journeys for the end-to-end performance cycle, starting with templates and cycles, to launching the review and viewing the results + some key wireframe screens for initial ideas
- Once we agreed on the strategy, we moved on to Hi-Fi designs and dev hand-off presentations.

## Deep Dive 1: Visibility Rules

### Intro

- When expanding from just Self & Manager Review → Peer & Upward Review, we introduce the Visibility Rules.
- Whose responses can the reviewee & manager see and at what time? Are the peers’ and subordinates’ identities anonymous or visible?
- The challenge is to ensure we cover all the scenarios for the 2 main user roles: reviewee and reviewing managers. We solve it by mapping them all out, and we sped up the process by reusing components.

### Details

- Here’s the new step in the review cycle creation flow.“Can they view results” allows the admin to choose if reviewee and manager can view the results of each persona, and if so, when?
- “Can they view the name of the reviewer” lets the admin choose if they can view the identities of the respondents.
- For certain personas, the options for “Can they view results” affects the options of the 2nd one.
- Two examples of the visibility rules mapping. We use them also to agree on the interactions and views for the various user roles.
- Example of all possible variants of the right-side component, which is nested within the card component. It covers all the scenarios for the various review types, eg. Self review, peer selection, etc..

## Deep Dive 2: Peer & Upward Review

### Intro

- On the same note, previous designs couldn’t simply be edited to meet demands of these 2 new personas.
- Challenge: need to redesign in many places: to-do page, review cycle listing and details page.
- Overcome lack of exploration time by referencing how other softwares did it.

### Before

- In the first iteration, there are only self and manager review to consider for each row item.
- Chip used incorrectly to display the period of the review type.
- Review cards are not fully utilising the available space.

### After

- We need to show the statuses of a max of 5 review types + 2 selection periods.Instead of the 2-col layout, so we revised it to a 2-row layout instead. Row 1: displays essential performance cycle details. Row 2: displays the statuses of the selected reviews for this cycle.
- In event details page, we introduced a progress bar to balance the absolute number and percentage of completion.
- More gap between review period and status -> easier to read.
- New in task page: "My Review" tab to do reviews and view responses that are related to “me”. "Team Review" tab to do reviews and view responses outside of “me” – my subordinates, my peers, my direct manager.

## Reflection

- What you'd do differently:
  - Use a different layout for the My Review and Team Review cards to reduce the wasted space.
- What the system still can't do cleanly:
  - Handle the cases where employees fail to submit before deadlines and to extend deadline for specific ones; required the dev to manipulate via backend.

## Assets
