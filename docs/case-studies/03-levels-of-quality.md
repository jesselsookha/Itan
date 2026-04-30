# Weak, Mid-Level, and Strong

---

## Why Examples Matter Here

The difference between a weak case study and a strong one is difficult to
describe in the abstract. The principles in the previous two documents are
necessary — but reading about specificity is different from seeing what
specificity looks like in practice.

This document uses a single project, documented three times at three
different levels of quality. The underlying project is identical in all
three versions. What changes is the depth of engagement, the honesty of
the account, and the presence of genuine reasoning.

Reading all three versions — in order — makes the standard visible in a
way that description alone cannot.

---

## The Project

**Context:** A final-year IT student group project. The team built a full-stack
task management application for a real client — a small logistics company.
The system includes a REST API backend, a web frontend, and a mobile companion app.
The student writing the case study was responsible for the backend architecture
and API design.

---

## Version Ⅰ — Weak

---

**Task Management System**

*Duration: 8 months | Role: Backend Developer | Technologies: Node.js, Express, MongoDB, React Native*

For my final-year project, I worked on a team that built a task management
application for a client. The system allowed users to create, assign, and
track tasks across desktop and mobile. I worked on the backend and helped
with the API.

We used Node.js and Express for the server, MongoDB for the database, and
React Native for the mobile app. The project was completed on time and the
client was happy with the result.

I learned a lot about full-stack development and working in a team.
It was a challenging project but we managed to deliver a working product.

[GitHub Repository](https://github.com)

---

### What Makes This Weak

◆ **No specific problem.** *"A task management application for a client"*
  tells the reader almost nothing. What was the client's actual problem?
  What were the constraints? Why did it matter?

◇ **No decisions, only technology choices listed.** Naming Node.js, Express,
  and MongoDB is not documenting a decision. A decision has alternatives,
  reasoning, and a trade-off. None appear here.

◆ **Difficulty is generic and unresolved.** *"It was a challenging project"*
  does not tell the reader anything. What was challenging? How was it handled?
  What changed as a result?

◇ **Outcome is vague and unverifiable.** *"The client was happy"* is a claim
  without evidence and without specificity. What was actually delivered?
  What problem did it solve?

◆ **Reflection is a placeholder.** *"I learned a lot about full-stack
  development"* is the most common sentence in student portfolio entries
  across all disciplines. It communicates nothing.

**Overall:** This is a project description — a brief record that the project
happened. A reader learns that this student was on a team, worked on a backend,
and used common technologies. They learn nothing about how this student thinks.

---

## Version Ⅱ — Mid-Level

---

**Task Management System — Logistics Client**

*Final-year group project | 8 months | Role: Backend Developer*

Our final-year project involved building a full-stack task management
application for a small logistics company of twelve staff. The client
was tracking tasks through a shared spreadsheet that caused version
conflicts and missed deadlines. We needed to build a system accessible
on both desktop and mobile with real-time updates.

I was responsible for the backend architecture and REST API design.
We chose Node.js with Express over Python/Django because the team had
stronger JavaScript experience and React Native on the frontend meant
sharing validation logic across the stack was simpler. MongoDB was chosen
over a relational database because the task data model was flexible
and we anticipated schema changes during development.

The main challenge was getting the authentication to work consistently
across both the web and mobile clients. There were issues with token
expiry on mobile that took significant debugging time to resolve.

The final system was deployed and the client confirmed it reduced the
missed deadline rate. The codebase is available on GitHub.

I would approach the authentication architecture earlier in the project —
it became a bottleneck in the later sprints.

---

### What Makes This Mid-Level

◆ **The problem is now specific.** Twelve staff, a shared spreadsheet,
  version conflicts, missed deadlines. A reader understands the context
  and why it warranted a solution. This is a significant improvement.

◇ **Decisions are named with some reasoning.** The Node.js choice has a reason.
  The MongoDB choice has a reason. These are better than a technology list —
  but the reasoning is shallow. Why was shared validation logic across
  the stack actually important? What did the anticipated schema changes
  turn out to be? The decision account is present but not developed.

◆ **Difficulty is specific but thin.** Token expiry issues are named —
  this is better than *"it was challenging."* But *"took significant debugging
  time"* is still vague. What exactly went wrong? What was the diagnosis?
  What was the fix? The reader knows something was difficult but learns
  nothing from how it was handled.

◇ **Outcome has a claim but limited evidence.** *"The client confirmed it
  reduced the missed deadline rate"* is a specific claim — but the percentage,
  the timeframe, and the method of measurement are absent. A link to the
  repository is mentioned but not provided.

◆ **Reflection is present but undeveloped.** *"I would approach authentication
  earlier"* is a genuine lesson — but it stops short. Why? What did the late
  architecture decision cost specifically? What would earlier authentication
  design have changed?

**Overall:** This case study is readable and has genuine content. A reader
learns something about the project, the decisions, and the student's awareness
of what went wrong. But the depth is inconsistent — some elements are developed,
others are stated without evidence or development. It reads as a case study
that stopped short of the standard it was reaching for.

---

## Version Ⅲ — Strong

---

**Task Management System — Logistics Client**

*Final-year group project | 8 months | Backend architecture and API design*

A small logistics firm of twelve staff was coordinating task allocation
through a shared spreadsheet. The result was frequent version conflicts,
tasks assigned to staff who had not been notified, and a missed deadline
rate the operations manager described as "unsustainable." The project
required a system accessible on both desktop and mobile, with real-time
task updates, a minimal learning curve for non-technical staff, and
sufficient reliability for daily operational use.

**Approach and decisions**

The core architectural decision was adopting OAuth 2.0 via a third-party
provider rather than building a custom JWT-based authentication system.
The team initially planned custom token handling, but a stand-up in week
three flagged that none of us had the security expertise to audit it
responsibly. OAuth added constraints — we lost control over the consent
screen UX — but externalised the security responsibility to a provider
whose system had been audited at scale. The accepted trade-off was correct:
the alternative risk was disproportionate to the UX cost.

MongoDB was chosen over PostgreSQL after we sketched the initial data
model and identified that task schemas would likely shift as the client
clarified requirements — which they did three times in the first month.
A flexible document model absorbed those changes with minimal migration
overhead. Had the requirements been stable from the start, PostgreSQL
would have been the stronger choice.

**What was difficult**

After integrating OAuth, access tokens expired silently on the mobile client.
Users were not prompted to re-authenticate — API requests simply failed.
The root cause was a misconfigured refresh token handler that was not
re-issuing tokens after expiry on React Native, despite working correctly
on the web client.

The diagnosis took most of a sprint. The lesson was not a configuration
fix — it was an architectural one: OAuth integration is not uniform across
client surfaces. Each client requires explicit lifecycle management, and
that management needs to be designed and tested per client at integration
stage, not discovered in production.

I now treat per-client authentication lifecycle as a first-week design
consideration on any multi-surface project.

**Outcome**

The system was deployed to the client at the end of semester. After three
months of use, the operations manager reported a 40% reduction in missed
deadlines and confirmed that all staff had adopted the system without
requiring individual training — a measure of the low-friction design
that had been a stated requirement from the first meeting.

The full codebase, API documentation, and a recorded demonstration are
available in the project repository: [link].

**Reflection**

The authentication decision was the project's most instructive moment —
not because it went wrong, but because it forced a precise understanding
of where our team's competence ended. Choosing OAuth was not a shortcut.
It was a justified engineering decision made under real constraints.

What I would change: the per-client token lifecycle should have been a
formal design deliverable in the first sprint, not an assumption tested
in the last. That change would have recovered the sprint lost to debugging
and would have produced a more robust system earlier.

---

### What Makes This Strong

◆ **The problem is specific and evidenced.** The operations manager's language —
  *"unsustainable"* — is not generic. The requirements are stated precisely:
  real-time updates, minimal learning curve, daily operational reliability.
  Every subsequent decision can be evaluated against this stated problem.

◇ **Decisions are developed with real reasoning.** The OAuth decision
  includes the alternatives considered, the risk analysis, the accepted
  trade-off, and a retrospective assessment of whether it was correct.
  The MongoDB decision includes the reason it was chosen and the condition
  under which the alternative would have been better. Both are defensible
  in conversation.

◆ **Difficulty is specific, diagnosed, and instructive.** The token expiry
  problem is named, diagnosed, and resolved — and the resolution produces
  a specific lesson that changes future practice. *"I now treat per-client
  authentication lifecycle as a first-week design consideration"* is a
  real, portable lesson. It could only have been written by someone who
  experienced this specific problem.

◇ **Outcome is evidenced with real data.** 40% reduction in missed deadlines.
  Full staff adoption without individual training. These are specific,
  verifiable claims — not impressions. The link to the repository is present.

◆ **Reflection is specific and forward-facing.** The reflection connects
  to the specific event in the case study (the authentication decision),
  takes a position on it (it was correct, for these reasons), and identifies
  what would be done differently with a specific, actionable change
  (formal first-sprint deliverable for per-client lifecycle design).

**Overall:** A reader who finishes this case study understands what problem
was solved, what decisions were made and why, what went wrong and how it
was diagnosed, what the project produced, and what the student learned.
They have enough material to ask intelligent follow-up questions — and
the student has clearly done the thinking to answer them.

---

## The Pattern Across All Three Versions

The same project. The same duration. The same technologies. The same outcome.

What differs:

| Element | Weak | Mid-level | Strong |
|---|---|---|---|
| Problem | Generic | Specific | Specific and evidenced |
| Decisions | Listed | Named with some reasoning | Developed with alternatives and trade-offs |
| Difficulty | Vague | Named but thin | Diagnosed, resolved, and instructive |
| Outcome | Unverifiable claim | Claim with limited evidence | Specific data and linked artefact |
| Reflection | Placeholder | Present but undeveloped | Specific, portable, forward-facing |

The movement from weak to strong is not more words. It is more honesty,
more specificity, and more willingness to engage with what actually happened
rather than what would look best.

---

!!! tip "Using this for your own work"
    When you finish a draft case study, read it against these three versions.
    Ask honestly: which level does this most resemble?

    If the answer is Weak or Mid-level, identify which element is
    underdeveloped and return to the source material — your Vestigia records,
    your project artefacts, your memory — to find the specificity that
    will move it forward.

    The goal is not Version Ⅲ as a template. It is Version Ⅲ as a standard.

---

[Continue to Documenting Different Project Types →](04-project-types.md)
