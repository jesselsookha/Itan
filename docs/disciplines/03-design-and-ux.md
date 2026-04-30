# Design and UX

*Interface design, user experience, product design, interaction design*

---

## What This Field's Readers Most Want to See

Design hiring managers, creative directors, and UX leads look for one
thing above all others in a design portfolio:

> *Does this person design for people, or do they design for themselves?*

The answer is visible in how a portfolio is structured. A portfolio that
leads with aesthetics — with polished visuals, impressive layouts, and
refined typography — without showing the research, reasoning, and iteration
behind the work, suggests the second. A portfolio that shows how the design
responded to what real users needed, what the research revealed, and how
the design improved through testing, suggests the first.

The design community has a word for beautiful work that does not serve users:
*pretty but broken*. A portfolio that avoids this judgement demonstrates
that the visual skill is in service of a thinking process, not a substitute for it.

---

## What Belongs in a Design and UX Portfolio

### The Process Case Study

Design case studies are process arguments. They do not ask a reader to
admire the outcome — they ask a reader to follow the thinking that produced it.

A design case study without process documentation is a gallery. A design
case study with process documentation is a case study.

What process documentation must show:

◆ **The research foundation** — what you learned about users before designing.
  Surveys, interviews, observation, usability testing, competitive analysis.
  Not the research methodology in academic detail, but the findings that
  mattered — specifically, the findings that changed what you were going to design.

◇ **The problem statement that emerged from research** — not the brief you
  were given, but the design problem you understood after doing the research.
  These are often different. The gap between them is where the most interesting
  design thinking lives.

◆ **Iteration evidence** — early wireframes, mid-fidelity explorations,
  and final designs shown together, with an account of what changed between
  them and why. The visual difference between early and late states is
  compelling only when accompanied by the reasoning that drove the change.

◇ **User feedback and response** — what participants said during usability
  testing or review, and how the design responded. A design that was tested
  and revised based on findings is more credible than one that was tested
  and confirmed. If testing produced no meaningful revision, it is worth
  asking whether the testing was sufficiently challenging.

◆ **Constraint navigation** — accessibility requirements, technical constraints,
  business rules, or time limitations that shaped the design. Showing that
  the design operated within real constraints demonstrates professional practice.

### Visual Presentation

A design portfolio is itself a design artefact. The way it is presented
communicates design sensibility before a single project is opened.

This does not mean it needs to be elaborate. It means it should be consistent,
considered, and appropriate to the professional context you are entering.

Specific considerations:

◆ **Show early states** — sketches, low-fidelity wireframes, rough explorations.
  These signal confidence — a designer willing to show unpolished early work
  is a designer secure in their process. Showing only finals signals either
  that there was no process or that you are afraid to show it.

◇ **Caption everything** — every visual in a design portfolio should be
  captioned with what it shows, what stage it represents, and what decision
  it reflects. Uncaptioned visuals leave interpretation to the reader.

◆ **Interactive where possible** — a Figma prototype that a reader can
  navigate communicates more than any screenshot. Where an interactive
  prototype exists, link to it.

---

## Platform Guidance

**Behance** is the established professional platform for design work.
Publishing on Behance signals community membership — it is where designers
share work, find collaborators, and build reputation. For UI/UX students,
a Behance presence is close to expected in professional applications.

**Dribbble** has a different character — shorter, more visual, less narrative.
It is most useful for building visual presence and connecting with the
design community. Less suited to the full process case study format.

**A personal portfolio site** — built on Webflow, Cargo, Adobe Portfolio,
or similar — gives full control over presentation. For design students,
the site itself is a demonstration of design skill. This raises the stakes:
a poorly designed personal site undermines the portfolio it houses.

**Figma Community** — for groups or individuals whose primary deliverable
is a design system or prototype, publishing to Figma Community allows
readers to interact with the work directly.

---

## Annotated Case Study Example

**Project:** Redesign of a community library's digital catalogue and reservation system.
*Third-year UX project | 12 weeks | User research, interaction design, and prototype testing*

---

**Context and problem**

The public library's existing digital catalogue had been in place for eleven
years. The brief was to assess its usability and propose a redesign. Initial
assumption: the interface was visually outdated and navigation was inefficient.

After conducting six user interviews and two observation sessions with
regular library patrons across three age groups, the assumption required
revision. Navigation was not the primary complaint. The problem was search
behaviour: the system required users to know library classification conventions
(Dewey Decimal subject codes) to search by subject effectively. Casual users
— the majority — were searching by title or author, which the system handled
well, but were unable to discover adjacent titles in the same subject area.
Discovery, not navigation, was the primary unmet need.

**Approach and key decisions**

The redesign reframed the interface around two distinct user behaviours:
*finding* (I know what I want) and *discovering* (I want something like this).
The original system served the first behaviour adequately. The redesign
preserved the existing search for finding while adding a browsing and
recommendation layer for discovery.

The most significant design decision was whether to surface classification
codes visibly or translate them into lay language. Library staff were
resistant to hiding classification codes — they use them daily and feared
a system that obscured professional vocabulary. The resolution was a toggle:
lay language as default for patrons, professional codes accessible on
request. Both audiences were served without compromising either.

Accessibility drove several secondary decisions. The original system failed
WCAG 2.1 AA on contrast ratios in four locations and had no keyboard
navigation for the catalogue grid. These were treated as requirements,
not suggestions — the redesign was validated against both criteria before
prototype testing began.

**What was difficult**

The first round of prototype testing with five participants produced a
finding I had not anticipated: the discovery layer confused users who were
in finding mode. Recommendations appeared alongside search results,
and several participants tried to interact with recommendations when
they were looking for a specific title.

The problem was visual hierarchy — the distinction between search results
and recommendations was not clear enough at first glance. Three interface
iterations followed before a testing session confirmed that users could
reliably distinguish between the two. The final solution used spatial
separation rather than colour or label differentiation — the two behaviours
were given distinct zones on the screen, not just distinct visual treatments
within a shared space.

**Outcome**

Prototype testing with eight participants after the spatial separation
revision showed no confusion between finding and discovery modes. Task
completion time for a standard catalogue lookup was 23% faster than on
the existing system. The redesign was presented to the library board and
accepted for development consideration.

Figma prototype, research documentation, and full testing notes:
[link to Figma] | [link to documentation]

**Reflection**

The assumption error at the start — that navigation was the problem —
would have produced a redesign that looked different and worked the same
way for the users who most needed improvement.

The research phase saved the project from solving the wrong problem. This
is not a lesson I have only read about — it is one I experienced on a
project where the brief pointed in one direction and the users pointed
in another. I now treat the problem statement in any brief as a hypothesis
to be tested, not a problem to be solved.

---

*This case study demonstrates research-driven problem reframing, specific
design decisions with stakeholder constraint navigation, an honest iteration
account tied to a testing finding, quantitative outcome evidence, and a
reflection that produces a specific and portable change in design practice.*

---

[Continue to Data Science and Research →](04-data-science-and-research.md)
