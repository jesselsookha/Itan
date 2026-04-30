# Data Science and Research

*Data science, AI and machine learning, quantitative and qualitative research,
applied science*

---

## What This Field's Readers Most Want to See

Readers of data science and research portfolios — whether technical hiring
managers, research supervisors, or industry data leads — hold a consistent
standard:

> *Does this person understand what their results can and cannot claim?*

This standard is more exacting than it might appear. The ability to run
a model, produce an accuracy metric, and visualise the results is table
stakes. Every data science graduate can do this. What distinguishes
a portfolio entry worth reading is the honest engagement with methodology,
the transparent acknowledgement of limitations, and the precision between
what the findings show and what the analyst claims they show.

Overclaiming — presenting results as more generalisable, more accurate,
or more significant than the evidence supports — is the most serious
credibility failure in research and data science portfolios. It is also
the most common. Readers who spend time with technical work know how to
spot it, and a portfolio that overclaims is remembered for the wrong reasons.

---

## What Belongs in a Data Science and Research Portfolio

### The Research or Project Case Study

The case study for a data science or research project documents the full
intellectual journey: not just what the model produced or what the analysis
found, but the reasoning behind every significant methodological choice,
the honest account of what the approach could not do, and the specific
learning that the project produced.

What the case study must address:

◆ **The research question or problem statement** — stated precisely, in a
  form that makes the scope and criteria for a useful answer clear. A research
  question that is vague at the outset produces results that cannot be
  interpreted clearly at the end. The quality of the question is itself
  evidence of research maturity.

◇ **Data context** — where the data came from, how it was collected or accessed,
  what its known limitations are. Size, representativeness, recency, missing
  values, class imbalance — all of these shape what the analysis can claim,
  and all of them should be acknowledged. Describing data as *"a dataset of
  10,000 records"* without noting that 40% of the target variable was missing
  is a material omission.

◆ **Methodological decisions with alternatives** — why this model architecture,
  this statistical test, this research design, over alternatives. Methodological
  choices in data science and research are decisions with the same structure
  as any other: alternatives existed, a path was chosen, trade-offs were accepted.
  The reasoning should be explicit.

◇ **Results with interpretation, not just metrics** — accuracy, F1, p-values,
  effect sizes, and confidence intervals are not self-interpreting. A portfolio
  entry that reports a 94% accuracy without noting the class distribution of
  the test set, the baseline comparison, or the domain context in which 94%
  is or is not useful, is not yet a result — it is a number.

◆ **Limitations with honesty** — what the project cannot claim, what would
  need to be different to support stronger conclusions, what the next study
  would need to address. Acknowledging limitations is not a sign of weak work.
  It is the mark of a researcher or analyst who understands the relationship
  between evidence and claim.

### Reproducibility and Evidence

◆ **Links to notebooks** — Jupyter notebooks, R Markdown documents, or
  equivalent analytical records are the primary evidence in data science portfolios.
  A portfolio entry that references analysis without linking to it is claiming
  without demonstrating.

◇ **Data links where shareable** — if the data is public, link to it.
  If it is not, describe it specifically and note why it cannot be shared.
  A reader who cannot access the data should still be able to understand
  what it was and what its relevant properties were.

◆ **Visualisations that explain** — charts and figures should be in the
  portfolio because they communicate something specific. A figure without
  a caption explaining what it shows and why it matters is decorative,
  not evidential.

◇ **Code quality as signal** — for technical readers, the code in a
  repository is as much a portfolio item as the results it produces.
  Clean, commented, reproducible code signals professional practice.
  A notebook that runs top-to-bottom without errors signals care.

---

## Platform Guidance

**GitHub** — primary platform for code, notebooks, and documentation.
A data science portfolio without a GitHub presence is missing its primary
evidence layer. Notebooks should be clean, readable, and produce expected
outputs without errors.

**Kaggle** — for data science students, a Kaggle profile with completed
competitions or published notebooks signals community engagement and
practical skill under standardised conditions. High-scoring competition
entries are legitimate portfolio content.

**Hugging Face** — for AI and machine learning students working with
language models or releasing model weights, a Hugging Face profile
demonstrates professional community participation in the ML ecosystem.

**Observable or Tableau Public** — for data visualisation-heavy work,
interactive published notebooks on Observable or dashboards on Tableau Public
allow readers to engage with the analysis directly. A static screenshot
of a dashboard is significantly less compelling than a dashboard the
reader can explore.

**A personal site or Notion** — for mixed technical and non-technical
audiences, a personal site or Notion-based portfolio that contextualises
the technical work in plain language serves readers who need to understand
the significance of the work without being able to evaluate the technical
implementation directly.

---

## Annotated Case Study Example

**Project:** Predicting student dropout risk in higher education using
administrative and engagement data.
*Honours research project | 6 months | Machine learning, classification*

---

**Context and problem**

Student dropout represents a significant institutional and personal cost
in higher education. Early identification of at-risk students allows
targeted intervention before withdrawal becomes likely. The project
investigated whether administrative and engagement data available in the
first six weeks of semester could predict dropout risk with sufficient
accuracy and lead time to support meaningful intervention.

The data was sourced from a single institution's anonymised student records
(n = 4,200 students across three academic years), combining demographic
variables, first-semester grade performance, library access frequency,
learning management system login counts, and assignment submission timing.
The target variable was dropout within the academic year (12.3% positive class rate).

**Approach and key decisions**

Three classification approaches were evaluated: logistic regression as a
baseline, a gradient boosted tree model (XGBoost), and a neural network
classifier. Logistic regression was retained as the comparison baseline
throughout — interpretability matters in institutional decision-making
contexts where predictions inform human intervention, and a black-box model
that outperforms a transparent one by a small margin is not necessarily
the better institutional choice.

XGBoost was selected as the primary model. It outperformed the neural
network on this dataset size — a neural network's capacity advantage
does not materialise consistently at n < 10,000 with mixed tabular data
and requires more careful regularisation to avoid overfitting on the
minority class. Hyperparameter tuning was conducted with stratified
5-fold cross-validation to avoid data leakage across the class imbalance.

SMOTE was applied to address class imbalance rather than class weighting,
after initial experiments showed that class weighting produced higher
recall on the minority class at the cost of precision rates unacceptable
for a system that would flag students for human review. A high false
positive rate has real costs — staff time, student stigma — and the
threshold was set to optimise F1 rather than recall alone.

**What was difficult**

The most significant methodological challenge was the temporal structure
of the data. Students across three academic years were treated as independent
observations in the initial model, but institutional policy changes between
years introduced distributional shift: dropout rates, assessment structures,
and LMS adoption patterns all changed across the period. Training on earlier
years and testing on the most recent year produced performance substantially
lower than cross-year cross-validation suggested.

The response was restructuring the validation strategy to simulate real
deployment: training exclusively on years one and two, validating on year
three. This reflected the actual use case — a model trained on historical
data deployed in a future period — and produced a more honest estimate of
generalisation. Final AUC on the held-out year was 0.79, compared with
0.87 on within-period cross-validation. The difference is a realistic
estimate of deployment degradation.

**Outcome**

The model achieved AUC 0.79, precision 0.61, and recall 0.58 on the
held-out test year at the selected operating threshold. Logistic regression
baseline achieved AUC 0.71 on the same partition. The 0.08 AUC improvement
represents a meaningful reduction in missed at-risk students for institutional
scale, though the absolute recall of 0.58 means 42% of dropout students
would not be flagged — a limitation with direct intervention implications.

Code, notebooks, and anonymised feature importance analysis:
[link to repository]

**Reflection**

The temporal validation restructuring was the project's most important
methodological contribution — not to the literature, but to my own
understanding of how evaluation design relates to deployment context.

Cross-validation that ignores temporal structure overstates performance.
The gap between 0.87 and 0.79 is not a model failure — it is an honest
estimate. Producing an honest estimate rather than an impressive one is
the more valuable outcome. That distinction — between a metric that looks
good and a metric that means something — is the one I now apply first to
any evaluation design.

---

*This case study demonstrates precise problem framing, honest data description
including class imbalance and temporal structure, methodological decisions with
explicit alternatives, result interpretation with acknowledged limitations, and
reflection that produces a specific change in evaluation practice.*

---

[Continue to Education and Applied Social →](05-education-and-social.md)
