# Inspect — Inspection Job Booking App

## Context & Challenge

- My ex-boss runs a rope and crane inspection business. Before Inspect, every job — request, scheduling, assignment, and status update — was coordinated ad hoc over phone calls and WhatsApp. There was no central system, no scheduling visibility, and no easy way to keep a requestor updated without someone manually messaging them.
- **Key entities**: Job Request → Job → Assignment
- **Personas**: Requestor (the client submitting an inspection request), Admin/"the programmer" (accepts, schedules, and assigns jobs; manages job details), FSP — Field Service Partner (the inspector who carries out the job)
- **Core design tension**: keeping requestors informed and able to track status without requiring them to create an account or log in, while giving admins full control over scheduling and assignment.
- **Strategic constraint**: one-month timeline for the first iteration, designed and built solo.
- **The trigger**: the admin had become the bottleneck — every attachment and contact detail had to be manually forwarded between requestor and FSP, with the admin scrolling back through long WhatsApp threads just to dig up information buried in the conversation. That repeated time sink is what made a proper system worth building.

## My Role & Impact

- **Role**: Design & development, solo — research, UX, UI, and build.
- **Duration**: 1 month (first iteration).
- **Team**: Me (design + dev), business owner as the primary stakeholder and client. I was also training to become an FSP myself during this project, which gave me first-hand insight into what the field-service side actually needs.
- **Key contributions**:
  - Designed and built the end-to-end system from scratch: public request form, admin console, and FSP login.
  - Defined the three-role access model (Requestor / Admin / FSP) and the job lifecycle connecting them.
  - Just wrapped up beta testing on the dev server and opened the production server for real clients to start submitting requests — quantified outcomes still to come.
  - Admin feedback so far: a much clearer picture of the schedule, with visibility into who's doing what job each day, and no more accidentally double-booking an FSP across AM/PM sessions.
  - FSP feedback so far: no more scrolling through WhatsApp to piece together job and contact details — everything now lives in one place.

## Process & Collaboration

- Scoped requirements directly with the business owner and programmer as the client.
- Mapped the job lifecycle across all three roles — request → accept/schedule/assign → field execution → status updates — to identify exactly where a system could replace manual coordination.
- Being trained as an FSP myself gave me direct, first-person exposure to what field inspectors need on the ground, rather than relying on secondhand requirements.
- The main priority was getting a basic, functional version live within the month — the goal being to get requestors, the admin, and FSPs actually using it so we could gather real feedback on what to improve next.
- Cut: automated WhatsApp status update messages. I wasn't familiar with the WhatsApp Business API, and even with AI assistance it would have been too technically involved to ship within the timeline — on top of the time needed for Meta's account verification.
- Cut: in-app assignment acceptance for FSPs. Instead, the admin and FSP still discuss the assignment over WhatsApp, and the admin updates the schedule in the system afterward.
- Neither cut was a dealbreaker, since I'd already designed a workaround: a button on the job details page that opens WhatsApp with a pre-filled message, ready to send.

## Key Design Decisions

### 1. Three scoped roles: Requestor, Admin, FSP

**Situation**: Job coordination happened over phone and WhatsApp, with no separation between who could request a job, who scheduled and assigned it, and who executed it in the field. Everyone touching a job needed a different set of information and actions.

**Options considered**:

- Requiring requestors to sign up for an account before submitting a request — dropped, since that's too much friction for a request that might not even get accepted. Instead, the form asks for only essential info, with the LM and MILL certs marked optional in case the requestor doesn't have them on hand at that moment.
- Building this out as a full CRM to manage clients — out of scope for this first iteration, which was scoped specifically as booking and scheduling, not client management.
- A single shared login for admin and FSP — dropped in favor of separate logins, since FSPs need their own fields (FSP number, joined date, operator level) that don't apply to admins.

**Decision**: Built three scoped experiences: a public-facing form for requestors to submit jobs with no account needed, an admin console for accepting, scheduling, and assigning jobs, and an authenticated login for FSPs that only shows jobs assigned to them.

**Rationale**: Each role only needs to see and do a narrow slice of the job lifecycle. Keeping the request form public removes friction for the client's customers; scoping the FSP view to assigned jobs only keeps the field experience focused and avoids exposing jobs that aren't theirs.

**Result**: The admin now has a clear bird's-eye view of all inspection jobs on the planner page, with full job details on the listing page and a record of each FSP's completed and assigned jobs. For FSPs, it's just as straightforward — they see the schedule for the upcoming week and the details for those jobs, with completed jobs out of sight, reducing cognitive load.

### 2. Keeping requestors updated without requiring an account

**Situation**: Requestors are typically construction-industry clients who want a status update, not another account to manage. Requiring login would add friction right where the business needed to look easy to work with.

**Options considered**:

- Email updates — dropped, as it felt old-school and untimely; requestors aren't checking email the way they check WhatsApp.
- WhatsApp — the default choice, since it's the app all parties already use heavily.
- A public link — kept alongside WhatsApp, since it lets a requestor forward status to their own managers or supervisors without pulling them into the same WhatsApp group and pinging them constantly.

**Decision**: Admins send job updates to the requestor either via WhatsApp message or a public shareable link — no login required on the requestor's side.

**Rationale**: This mirrors how the business already communicated with clients (WhatsApp), so it doesn't introduce a new habit. The public link gives a persistent, shareable reference point without the overhead of account creation.

**Result**: To be updated after real clients start using it.

### 3. Capturing accurate job-site location and point-of-contact details

**Situation**: Inspection jobs happen at physical sites — often construction sites — that need a precise location and a point of contact (POC) for the FSP to coordinate with on arrival. Addresses alone aren't always reliable for construction sites, and contact numbers need to be actionable, not just displayed as text.

**Options considered**:

- This wasn't in the initial prototype at all — it only surfaced as essential once we started internal testing and recalled our own frustrations getting to sites.
- An embedded map on the details page — dropped, since it added little value on its own. What actually mattered was a link that opens directly in Google Maps for turn-by-turn driving directions, not a static map view.

**Decision**: Admins can set the actual job location either by typing an address with autocomplete or by dropping a pin manually on Google Maps, for cases where the site doesn't have a clean address. Contact numbers are tap-to-WhatsApp — clicking one opens WhatsApp directly to message or call, rather than showing a plain phone number or routing through native telephony.

**Rationale**: Construction sites often don't resolve cleanly to a mapped address, so manual pin-drop is a necessary fallback to autocomplete. Routing contact numbers straight to WhatsApp matches how the business and its FSPs already communicate, and removes a copy-paste step.

**Result**: With the actual site access location and notes in hand, the FSP can reach the site faster and plan the nearest parking point ahead of time. Previously, without that detail, FSPs had gone to the wrong gate and needed to make a huge detour — wasting time and effort on-site.

### 4. Reference documentation for FSPs

**Situation**: Before a job, FSPs need to know equipment-specific details — the crane's LM (load moment) number certification and the MILL certs for the ropes involved — information that previously had to be tracked down separately.

**Options considered**:

- A shared document repository — dropped, since it meant standing up and managing another piece of software for what's fundamentally a simple need.

**Decision**: Admins upload the relevant LM number cert and MILL certs directly to the job, so FSPs have them on hand as reference before heading to site.

**Rationale**: Attaching certs at the job level keeps everything an FSP needs in one place, tied to the specific job rather than a separate lookup process.

**Result**: FSPs now have one straightforward place to retrieve the docs they need, instead of scrolling back through messages to find them.

## Reflection

- **What I'd do differently**:
  - Reduce repeated information on the details page. Right now some info shows up twice — once as metadata at the top of the section, and again further down — and I'd want to display it clearly without the duplication.
  - Push the visual design further from typical enterprise software — more colour, more personality. The calendar UI on the scheduled job details page is an early example of the direction I'd want to take further.

- **What the system still can't do cleanly**:
  - Send automated WhatsApp status update messages — planned for the 2nd iteration.
  - Accept job requests through an interactive WhatsApp chatbot — planned for a later iteration.

- **What I learned**:
  - Dogfooding the app as a trainee FSP myself meant I could design against what I actually needed on the ground, rather than relying entirely on secondhand feedback — which can sometimes reflect what users wish they wanted rather than what actually works.
  - AI-assisted development can produce overly complex first answers; clear, specific prompting helps a lot, and it often worked better to walk through a problem step-by-step with the AI rather than asking for everything at once, which could get overwhelming.
