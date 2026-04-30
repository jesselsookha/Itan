# CS and IT

*Software development, full-stack engineering, systems, cybersecurity, cloud*

---

## What This Field's Readers Most Want to See

Technical hiring managers, senior developers, and engineering leads have a
specific question when they open a CS or IT portfolio:

> *Does this person understand what they built — not just how to build it?*

This distinction matters. Every CS graduate can describe a project. Very few
can explain, with specificity and honesty, the architectural decisions behind
it, the trade-offs accepted, the failures encountered and diagnosed, and what
they would do differently with what they now know.

That difference — between building and understanding — is what separates
junior developers who are given tasks from junior developers who are given
problems. A portfolio that demonstrates understanding is the one that gets
you into the second conversation.

---

## What Belongs in a CS and IT Portfolio

### The Technical Case Study

The case study is the centrepiece of a CS or IT portfolio entry. It is where
the understanding lives — the reasoning behind decisions, the account of
difficulty, the evidence of growth.

Beyond the universal structure from
[Part Ⅳ](../case-studies/02-universal-structure.md), technical case studies
should specifically address:

◆ **Architecture decisions** — not just what was chosen, but the system-level
  reasoning. What was the architectural pattern and why did it fit this problem?
  What would a different architecture have cost or gained?

◇ **Technology choices in context** — frameworks, languages, databases,
  and deployment choices explained by the problem they were solving, not listed
  as skills. *"We chose PostgreSQL because the data model was relational and
  referential integrity mattered for financial records"* is a technology choice
  in context. *"I used PostgreSQL"* is a technology list.

◆ **System behaviour under real conditions** — how the system performed when
  it met actual load, real users, or production constraints. Projects that
  were only tested in controlled environments have less to say here, but
  the honest acknowledgement of that limitation is itself informative.

◇ **Security and reliability considerations** — not as a compliance checklist,
  but as evidence of professional awareness. Authentication decisions,
  data handling, error states, and failure modes are all legitimate portfolio
  content for CS and IT students.

### The GitHub Profile

For CS and IT students, GitHub is not an optional extra. It is the most
credible technical signal available — and it is almost always the first
thing a technical reader checks after or alongside the portfolio.

A GitHub profile that supports a portfolio:

◆ **Pinned repositories** — selected for relevance, not recency. The repositories
  pinned should be the ones that best demonstrate your current capability
  and professional direction. A first-year tutorial exercise pinned alongside
  a final-year capstone project undermines both.

◇ **READMEs that explain, not just describe** — every significant repository
  should have a README that tells a reader what the project is, what problem
  it solves, what technical decisions shaped it, and how to run or review it.
  A README that says *"A task management app built with Node.js"* is a project
  description. A README that explains the architecture, the key decisions,
  and the known limitations is documentation of thinking.

◆ **A profile README** — a special repository named after your GitHub username
  renders as a profile page. Use it. It should contain your positioning
  statement, your current focus, links to your portfolio and LinkedIn, and
  the technologies you work with most fluently — in context, not as a list.

◇ **Contribution history that means something** — a green contribution graph
  is not inherently meaningful. Consistent commits to projects that matter is.
  A portfolio project updated weekly over a semester tells a more credible
  story than a burst of activity in the final weeks before a submission.

### Supporting Evidence

◆ links to deployed applications — even staging environments  
◇ API documentation where relevant  
◆ architecture diagrams that explain system design visually  
◇ test coverage evidence — not just that tests exist, but that testing
  was part of the development practice  
◆ recorded demonstrations for projects that cannot be publicly deployed

---

## Platform Guidance

**GitHub** — primary platform for technical evidence. Everything important
should be here and maintained.

**A personal portfolio site** — ideally hosted on GitHub Pages, which itself
demonstrates the skill. The site should link to GitHub, to LinkedIn, and
to the strongest case studies. It does not need to be elaborate — clean,
readable, and current matters more than impressive design.

**LinkedIn** — professional network signal. The technical depth lives in
the portfolio and on GitHub. LinkedIn connects it to the professional community.

---

## Annotated Case Study Example

**Project:** Distributed notification service for a university student portal.
*Final-year individual project | 6 months | Backend systems development*

---

**Context and problem**

The university's student portal sent notifications through a single synchronous
process embedded in the main application. Under peak load — registration periods,
results release — the notification queue caused application timeouts affecting
all users simultaneously. The project brief was to design and implement a
decoupled notification service that processed messages asynchronously without
degrading portal performance during high-load periods.

**Approach and key decisions**

The central architectural decision was implementing a message queue using
RabbitMQ rather than a database-polling approach. A polling mechanism would
have been simpler to implement but introduced latency directly proportional
to poll frequency — either slow delivery or high database load. RabbitMQ
added infrastructure complexity but provided genuine decoupling: the portal
publishes events without waiting for delivery confirmation, and the notification
service consumes them independently.

The second significant decision was designing the notification service as
a stateless consumer. Each message carried all state required for delivery —
no shared session, no database lookup on the critical path. This made the
service horizontally scalable without coordination overhead. The accepted
trade-off was message size: payloads were larger than a reference-based
approach, requiring compression for high-volume notification types.

**What was difficult**

Message acknowledgement proved more complex than anticipated. The initial
implementation used automatic acknowledgement — messages were marked as
delivered when received, not when processed. Under failure conditions,
messages could be lost if the service crashed between receipt and delivery.

Diagnosing this required reproducing a failure scenario deliberately in
a test environment — something the original testing approach had not included.
The fix was switching to manual acknowledgement with a dead-letter queue
for failed messages. The lesson was architectural: acknowledgement semantics
should be defined before implementation, not after a failure mode surfaces them.

**Outcome**

Load testing at 3x peak registration traffic showed portal response times
unchanged during sustained notification bursts. The notification service
processed a backlog of 12,000 queued messages without message loss during
a simulated failure-and-recovery sequence.

Repository, architecture documentation, and load test results:
[link to repository]

**Reflection**

The acknowledgement failure changed how I think about distributed system design.
I had understood decoupling as an architectural principle — I now understand
it as a contract that must be specified at the message boundary, not assumed.

What I would change: failure mode testing from the first sprint, not as a
late-stage validation. The dead-letter queue design was available from the
beginning; I reached it through a production-adjacent failure rather than
through design. That order should be reversed.

---

*This case study demonstrates architectural decision reasoning, honest diagnosis
of a real failure, evidence-based outcome claims, and specific reflection that
produces a portable lesson — not a summary of what was learned, but a change
in how future work will be approached.*

---

[Continue to Engineering →](02-engineering.md)
