# BM Auto-Scheduler Redesign

## Overview of the project

- The users had provided constant feedback that it took way too long and too much effort for them to generate a schedule with our software. By the time the schedule was generated, it was already outdated.
- They also commented that the system was very buggy, generating outputs with incorrect values. It resulted in wasted time and they had to revert to the manual way.
- Solution: We reworked the system and workflow from scratch, and saved the users 63% in time and effort to generate an error-free schedule.

## What the product does, and who the audience is

- BunkerMaestro's primary function is for the bunker suppliers to optimize their bunkering jobs by running them through our proprietary algorithm called Automated Scheduler(AS).
- Secondary function: CRM system to manage the vessels, customers and contacts.
- Main audience: the operation personnel
- Bunker refers to fuel for vessels. You can imagine a car visiting a petrol kiosk when it runs out of petrol. But for vessels, it's the other way round: bunker barges – the pertrol kiosks – visit the vessels to supply them with bunker.

## Business objectives and what needed to be achieved through design

- Increase the user trust of our system to continue using it -> onboard more clients, raise funds for expansion.
- Design outcome: find ways to use the least time on preparing the data to feed the AS and to ensure a error-free output.

## Role & Impact

- **My Role**: Led to end-to-end redesign: discovery, ideation, UX design, data testing, client management
- **Duration**: 2 months
- **Cross-Functional Team**: Monika (Full Stack Developer), Pindar (Full Stack Developer), Timothy (Data Scientist)

### Key Contributions
- Proposed and led the re-design of the AS workflow when bug fixes and patches couldn't resolve the issues of incorrect outputs and time-consuming data preparation.
- Worked with Timothy, the data scientist, on tweaking the AS algorithm to generate the most optimized AS output based on the user's criteria and actual data.
- Did intensive data testing with user's actual data after each refinement to ensure the AS would work for all scenarios.

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

- We broke down this project into small workable chunks to test my hypothesis based on the challenges stated above, starting from the point of entry to getting an AS output.
- My hypothesis: do the user really need to do update all the completed jobs in order to use those ROB values to run the AS? Can we just use the most current value they have from the operators on the ground?  
- Turned out we could, and everything we tested from then on would revolve around that.
- We then worked on the next challenge until the entire re-design is completed.
- We then stress-tested the re-designed system using live client data, before deploying to live server for the client to test it themselves.

## Details

### Ensure only 1 manual ROB entry per barge when running the AS.

- Before: Each time the user manually updated the barge's ROB entry, system would log it down with a timestamp. Sometimes the entry was meant to be for a future event, e.g. the end of job that is one day later.
- All these entries were pulled into algorithm when the user ran the AS, and messed up the algorithm.

- After: We decided that there would be just one entry per barge at the point when the user ran AS, and each time the user ran the AS, its timestamp got updated.
- The users no longer needed to fill up the details for the completed jobs, which means time saved to run the AS.
- What about those values in between? They were no longer important because those jobs were completed; ROB values were crucial only for the upcoming jobs.

### Tackling the Ongoing Jobs

- Before: Many of the issues stemmed from this scenario where there was an ongoing job for a vessel when the user prepared the data to run the AS. 
- The user would provide the estimated post-job ROB with a future timestamp, which in turn messed up the algorithm and generated incorrect output.

- After: We had the users supply the pre-job ROB values of ongoing jobs.
- They didn't even need to enter the timestamp; the system would grab the vessel’s ETA timing to use in the AS.

### “Freeze” the entire AS output until it was applied to the schedule.

- Before: When the user applied the AS output that was generated 4 hours ago, system started applying the data to the upcoming jobs from the point of application. That meant the whole schedule was a mess.

- After: Regardless of the delay between the time AS was run and applied, system would always apply the output to the schedule from the time it was run, not the time it was applied.
- It was as though the schedule and output are frozen in time.

### Surface up errors pre-run

- Before: Errors were highlighted only after the AS starting processing and discovered them. By then, 20-30 mins was already wasted.

- After: System would check and validate all the ROBs pre-AS run for things like having insufficient ROBs or exceeding max capacity, etc., a huge time-saver for the users.

## Moment of Truth

- After weeks of testing and bugs fixing, we were finally ready to push it for production.
- I sent the client a Loom video and Powerpoint presentation of the new procedure. And then we waited.
- The email came eventually. They were very pleased with how the new procedure allowed them to generate the output so much faster, and – more importantly – without errors.
- Our hypothesis worked and our efforts finally paid off!
- As a result of the redesign, the users were able to get an output in about 40 minutes, a **huge savings of over 60%** from the 120 minutes it took previously.
- On top of that, a few other logos started expressing interest to use our software, including Shell and Wilhelmsen. We eventually did a POC with Wilhelmsen on an expanded module of BunkerMaestro.

## Reflections

- In order to locate the source of the problem, we need to trace back to every step of the AS workfolow, questioning each of them using first principles.
- When bug fixes and patches not only don't work but introduce more bugs, it's time for a major overhauls.
- I don't have the solution; I only have a hypothesis of the solution. Once that hypothesis is proved to be true, everything else we tested from then on would revolve around that.
- I was very blessed to have the developers' trust and my management team's backing to pull it off.
