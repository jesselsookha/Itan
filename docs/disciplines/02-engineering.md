# Engineering

*Mechanical, electrical, civil, systems, and industrial engineering*

---

## What This Field's Readers Most Want to See

Engineering employers and graduate programme selectors share a consistent
expectation when reviewing portfolios: evidence of engineering judgement.

Not just technical competence — the ability to apply a known method correctly.
But judgement — the ability to choose between methods under constraint,
to identify when a solution fails to meet its requirements, to make decisions
that are defensible given incomplete information and real-world limits.

Engineering judgement is difficult to fake and difficult to claim directly.
It is demonstrated through the specific, honest account of how you engaged
with a real problem — what you decided, what you accepted as a trade-off,
and what happened when your design met reality.

A portfolio that demonstrates engineering judgement is more compelling to
a hiring panel than one that lists technical skills. Skills can be taught.
Judgement takes time and real experience to develop — and a portfolio that
provides evidence of it, at student level, signals a graduate worth investing in.

---

## What Belongs in an Engineering Portfolio

### Design and Analysis Documentation

Engineering projects produce artefacts — CAD models, circuit schematics,
structural calculations, simulation results, prototype photographs. These
artefacts are essential portfolio content, but they are not the portfolio
itself. They are the evidence; the case study is the explanation.

What the case study must add to the artefacts:

◆ **The design rationale** — why this form, this material, this configuration,
  this specification. Engineering design involves choices between alternatives
  that are not always obvious from the final design. The rationale makes
  those choices visible.

◇ **Constraint mapping** — the requirements the design had to satisfy
  (performance, cost, safety, manufacturing, regulatory) and how competing
  constraints shaped the solution. Showing that you understood and navigated
  constraint trade-offs is the clearest evidence of engineering judgement.

◆ **Testing and validation evidence** — how the design was tested against
  its requirements. What passed. What failed. What the failure told you.
  Engineering portfolios that show only successful results are less credible
  than those that show the iteration between design, testing, and revision.

◇ **Manufacturing or implementation considerations** — for design projects,
  how the design was or could be manufactured. Cost, process selection,
  material availability, and assembly constraints are legitimate and
  impressive portfolio content that many students omit.

### The Engineering Log Book Connection

The engineering log book — or its modern equivalent — is the primary
source material for a strong engineering case study. If you maintained
a working record of decisions, test results, and revisions during your
project, your case study has specific, dateable material to draw from.

If you are approaching this retrospectively, the artefacts themselves
carry more of the load — but the decision reasoning still needs to come
from memory, and the limits described in
[Part Ⅲ — Retrospective Gathering](../curation/03-retrospective-gathering.md)
apply.

### Supporting Evidence Specific to Engineering

◆ CAD models or technical drawings — with annotation explaining key features  
◇ photographs of prototypes at different stages — not just the final version  
◆ simulation or FEA results with interpretation, not just images  
◇ test data with analysis — what the data shows and what it means  
◆ calculation sheets for significant design decisions — showing the
  analytical basis, not just the result  
◇ cost analysis where relevant to the project's real-world applicability

---

## Platform Guidance

**A personal portfolio site or PDF** — Engineering portfolios are often
presented as PDF documents in application processes, particularly for
graduate schemes. A clean, well-structured PDF that includes case studies,
annotated visuals, and links to artefacts serves most engineering contexts.
A personal site using GitHub Pages or a simple hosting platform provides
a public-facing equivalent.

**GitHub** — for engineering projects with significant software components
(simulation code, data analysis scripts, embedded systems firmware),
GitHub provides the same credibility signal it does for CS portfolios.

**LinkedIn** — professional network for the engineering community.
Particularly relevant for connecting with professional engineering
organisations and graduate recruitment networks.

---

## Annotated Case Study Example

**Project:** Low-power environmental monitoring unit for remote agricultural sites.
*Final-year individual project | 8 months | Embedded systems and hardware design*

---

**Context and problem**

Agricultural monitoring at remote sites typically relies on mains-powered
sensors or periodic manual measurement. For smallholder farmers in areas with
unreliable grid access, neither option is practical. The project brief was
to design a solar-powered, low-power environmental monitoring unit capable
of measuring soil moisture, temperature, and humidity at 30-minute intervals,
transmitting data via LoRaWAN to a base station up to 5km away, and operating
for a minimum of 72 hours without solar input.

**Approach and key decisions**

The central design tension was between measurement frequency and power budget.
The required 30-minute interval for data collection conflicted with a battery
capacity constrained by cost and size targets. Three strategies were evaluated:
reducing processor clock speed during idle periods, duty-cycling the sensors,
and aggressive sleep mode management.

The final design used a combination of all three. The processor (STM32L0
series) was selected for its deep sleep current of under 1µA — significantly
lower than alternatives at a comparable cost point. Sensors were powered down
between measurements rather than left in standby. A hardware timer woke the
system, initiated measurement, transmitted the packet, and returned to sleep
within 800ms of active time per cycle.

Power modelling before implementation predicted an average current draw of
42µA — within the 72-hour backup requirement. Post-implementation measurement
showed 51µA average, a 21% variance from the model, attributable to LoRaWAN
transmission retry events not fully accounted for in the model.

**What was difficult**

LoRaWAN transmission was the primary source of unmodelled power consumption.
Retries occurred when signal conditions degraded — something the bench-test
environment did not replicate. Field testing at 3km range revealed retry
rates of up to 30% under heavy tree cover, adding materially to the average
current budget.

The response was a firmware adjustment: retry limit reduced from three to one,
with failed transmissions flagged for the next cycle rather than retried
immediately. This accepted occasional data gaps in exchange for predictable
power behaviour. The power budget returned to 46µA average under field
conditions — within specification, though the 10% margin over the model
was smaller than I would now design for.

**Outcome**

The unit operated for 89 hours without solar input in field testing — exceeding
the 72-hour requirement. Soil moisture accuracy was within ±3% against
a calibrated reference instrument. Three units were fabricated and deployed
at a partner farm site for a four-week monitoring trial.

Design files, BOM, firmware source, and field test data:
[link to repository]

**Reflection**

The power modelling error was instructive. I modelled the happy path —
good signal, no retries — and treated it as the design case. It should
have been the best case. The design case should have been the realistic
field condition, with margin above it.

This changes how I approach power budgeting: model the realistic operating
condition first, with margin above it, and treat the ideal condition as
validation rather than design input. The firmware adjustment was available
from the beginning — I reached it through a field failure rather than through
design thinking. That order should be reversed.

---

*This case study demonstrates design constraint reasoning, quantitative
validation evidence with honest variance acknowledgement, a specific field
failure with a design-level lesson, and a reflection that produces a portable
change in engineering practice.*

---

[Continue to Design and UX →](03-design-and-ux.md)
