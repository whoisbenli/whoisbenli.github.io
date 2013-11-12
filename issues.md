Issue Resolution Guide
======================

How to deal with FAILs.

## How to deal with bugs

### Prevention

Don't write bugs in the first place!

Keep things simple. Simpler things are simpler to build and understand
- simpler product design
- simpler implementation architecture
- simple code/logic
- simpler api interfaces

Why?
- simpler code is easier to reason about
- clever code means hard to debug
- be kind to your future self

Engineering Process & Infrastructure
- design, code reviews
- unit tests, harnesses, automated testing

### Failure Mode

Make it easy to triage bugs when they eventually do happen
  
  - logs - make it easy to trace program state and execution
  - keep intermediate info for debugging
  - harnesses - for reproducing and isolating issues in controlled environment
 
## Stages of an Issue

This standardizes the vocabulary around what state an issue is in.

### Filed
Issue has been documented in a ticketing system.

### Reproduced
You are able to consistently reproduce the problem

### Triaged
You know exactly what is going wrong and why, and you know how to fix it.
This means that we can estimate how long it would take to fix the issue AND push the patch to the production. 
As usual, be conservative in your commitment date to customers if CS needs one.

### Review
You have a fix waiting for review in gerrit. Link to the gerrit change.

### Fixed
The change is merged.

### Waiting
We are waiting on some third party to fix something. Usually just assign to Tech Services to follow up.

### Resolved
The fix is in production. Mark a jira as resolved only when it has been released. This tells FQA/CS to verify the fix and communicate that fact to our customers.

### Ignored
Issue is ignored because it is reproducible, or it we won't fix it for whatever reason.

### Test Case
Test cases added

### Verified
Stakeholder/QA verified issue is fixed and test case exists.

### (Process Notes)

Please update JIRA as progress is made
Update Immune system field, if N/A, include good reasons why!, gerrit change url
Include postmortem in the jira. Level of detail should correspond to severity and complexity of issue.

## Priorities

### Critical
Work until fixed, no sleep, detailed postmortem required

### High
Stop and fix
If discovered by customer, eta + daily updates

### Medium
Schedule - e.g. 1 per week. Put it in the plan.

## What you should know or ask about every issue

### Source
How did we find out about the issue?
- automated tests, staging, qa, uat, internal users, customer report?

### Triage Priority
What's the initial priority and criticality?
Is it severe enough to consider a rollback if caused by a recent release?

### Account
What is the errant behavior?
What are the steps taken to reproduce it?
Was there an active modification of the running system? What was the timing and sequence of events?
- Deployments, configuration, migrations, etc.
What is the expected behavior?

### Scope
How does it impact the customer? Which customers?
What parts of the product are affected?
Could this be more of a product design bug?

### Reproduction
Be able to deterministically reproduce the issue
If the issue was found in a prerelease version, is it also found in production?
Make is as easy as possible to reproduce the issue (configure test ads, harnesses, etc)
- This way, colleagues downstream don't have to duplicate work.

### Triage
When was the issue introduced? By who? Who else was involved?
Under what circumstances does it happen, or not happen?

Isolate the issue - what is the smallest case (use harness/unit tests) that reproduces the issue?
Figure out projects affected - client vs server vs console vs db, etc
Eliminate causes by examining scope across dimensions - pubs, ads, integration types, ad types, client platform types
Could it be caused by an external party? Get proof if so, so Tech Services can communicate.

What part of the code is causing the issue and why? Use debugger, logs

*In light of this new information, has the priority changed?

### Fix
What needs to be done to fix the issue? How long will it take? What can we commit to?
Could it potentially introduce other problems? How risky is it?
Is it a symptom of a larger design issue? Should that be fixed as well?
Could the same class of bugs be present elsewhere? Should a more thorough code audit be performed?
Create an automated test case to prevent regressions.

### Postmortem
Was the issue verified to be fixed by the stakeholders?
Why was the issue not caught by our product development process?
Is it the result of a common practice that should be discontinued?
Does everyone know what to do to prevent this from happening again?
Do we need better infrastructure to identify bugs?

### Follow up Actions
How do we change our product development process to ensure that this class of issues do not happen again?
- prd, design review, implementation, unit tests, integration tests, code review, qa, deployment

If longer term effort is required to change the process or introduce new infrastructure, What is being done in the meantime?
