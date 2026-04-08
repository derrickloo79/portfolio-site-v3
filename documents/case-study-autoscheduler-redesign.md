# Performance Module

## Overview of the project

- The users had provided constant feedback that it took way too long and too much effort for them to generate a schedule with our software. By the time the schedule was generated, it was already outdated.
- They also commented that the system was very buggy, generating outputs with incorrect values. It resulted in wasted time and they had to revert to the manual way.
- Solution: We reworked the system and workflow from scratch, and saved the users 63% in time and effort to generate an error-free schedule.

## What the product does, and who the audience is

- BunkerMaestro's pri function is for the bunker suppliers to optimize their bunkering jobs by running them through our proprietary algorithm called Automated Scheduler(AS).
- Sec function: CRM system to manage the vessels, customers and contacts.
- Main audience: the ops personnel
- Bunker refers to fuel for vessels. You can imagine a car visiting a petrol kiosk when it runs out of petrol. But for ships, it's the other way round: bunker vessels – the pertrol kiosk – visit the ships to supply them with bunker.

## Business objectives and what needed to be achieved through design

- Increase the user trust of our system to continue using it -> onboard more clients, raise funds for expansion.
- Design outcome: find ways to use the least time on preparing the data to feed the AS and to ensure a error-free output.

## Role & Timeline

- **My Role**: discovery and ideation, UX design, data testing
- **Duration**: 2 months
- **Cross-Functional Team**: Monika (Full Stack Developer), Pindar (Full Stack Developer), Timothy (Data Scientist)

## Challenges

### Scheduling Data Entry is Time Intensive

- Manual Data Updates: Users must update ETAs, add new jobs, assign barges, and input actual quantities for completed jobs.
- High Effort: Takes ~2+ hours to prepare data before running the Automated Scheduler (AS).
- Error-Prone: Double-checking current ROBs adds complexity; errors delay scheduling further.
- Inefficient System: Even experienced users save only 30-40 minutes, indicating poor usability.
- User Frustration: Negative feedback due to increased workload and time, reducing system value.

### "Time-Travel" ROB Disrupts Schedule Accuracy

- ROB: Bunker remaining on board after a supply job.
- Issue: ROB values used when applying the AS output reflect the application time, not the run time.
- Impact: Leads to negative ROBs for some jobs and over-capacity for others, rendering schedules unusable.
- User Impact: Forces manual rescheduling; users lose trust in the system.
- Attempted Fix: Locking jobs based on time since schedule run failed to cover all edge cases.
- Ongoing Problem: Daily new edge cases trigger client complaints about inaccurate schedules.

## Rethinking the System for Faster, Simpler Scheduling

- Problem: Previous fixes were reactive, patching issues without addressing core user needs.
- New Strategy: Deep dive into root causes to redesign system functionality.
- User Outcome: "As a planner, I want to run the AS using only current ROB values and upcoming jobs to quickly update stakeholders with the new plan.”
- Goal: Minimize manual data entry, reduce errors, and ensure accurate, timely schedules.
- Approach: Build a system that aligns with user needs for speed, simplicity, and reliability.

## Approach

### The design process

- We broke down this project into small workable chunks, starting from the point of entry to getting an AS output.
- Each test built up to the next one until the entire re-design is completed.

## Details

### Ensure only 1 manual ROB entry per barge when running the AS.

- There was just one entry per barge when the user ran AS, and each time the user ran the AS, its timestamp got updated.
- What about those values in between? They were no longer important because those jobs were completed; ROB values were crucial only for the upcoming jobs.

### Tackling the Ongoing Jobs

- We had the users supply the pre-job ROB values of ongoing jobs.
- They didn't even need to enter the timestamp; the system would grab the vessel’s ETA timing to use in the AS.
- Why not use the post-job ROB value? It was because such value required a future timestamp, which would in turn mess up the algorithm and generate errors.

### “Freeze” the entire AS output until it was applied to the schedule.

- This meant that if I ran the output today and only applied it the next, the system would overwrite the schedule from the time it was run, not the time it was applied.
- It was as though the schedule and output are frozen in time.

### Surface up errors pre-run

- System would check the ROBs before the AS run for ongoing and the next upcoming job of each barge, and validate immediately if there were insufficient ROBs or would exceed max capacity, etc..
- AS run could take up to 20 mins or more, so all these would add up to huge time savings.

## Moment of Truth

- After weeks of testing and bugs fixing, we were finally ready to push it for production.
- I sent the client a Loom video and Powerpoint presentation of the new procedure. And then we waited.
- The email came eventually. They were very pleased with how the new procedure allowed them to generate the output so much faster, and, more importantly, it without errors.
- Our hypothesis worked and our efforts finally paid off!
- As a result of the redesign, the users were able to get an output in about 40 minutes, a **huge savings of over 60%** from the 120 minutes it took previously.

## Reflections

- When the fixes are not working, we need to look into the problem deeper;
- Don’t be afraid to make major overhauls when absolutely necessary;
- I don't have the solution; I only have a hypothesis of the solution;
- Start with small, manageable steps and build upon them;
- Help to team see the big picture and the positive impacts they would be making.

## Conclusion

- This is one of the most important and challenging projects I’ve worked on. It required lots of research and delving deep to discover root causes of problem, and it provided real value for the users.
- I was very blessed to have the developers' trust and my management team's backing to pull it off.
