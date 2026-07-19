# NHANES Health Profile: Data Preparation for AI-Driven Guidance

## What this project does

This notebook takes raw health survey data (from NHANES — the National Health and
Nutrition Examination Survey) and cleans, organizes, and analyzes it so it can later
power an AI assistant that gives **personalized, medically-aware health guidance**
instead of generic one-size-fits-all advice.

Think of it as building the assistant's "judgment" before it ever talks to a user:
teaching it which signals matter, and which combinations of signals indicate someone
might need extra care.

## The flow, step by step

**Step 1 — Cleaning the data**
Real survey data is messy. Some answers are missing; others are coded oddly (e.g.
"Refused" or "Don't Know" instead of a number). This step fixes inconsistencies,
fills in a small number of gaps using statistically sound methods (like the median,
which resists distortion from outliers), and checks for relationships between
variables — like whether weight and waist size tend to move together.

**Step 2 — Feature engineering (turning raw numbers into meaningful flags)**
Raw numbers like "BMI = 38" don't mean much on their own. This step translates them
into clear, rule-based categories that mirror how a clinician would think:

- **Physical risk** — e.g. obesity, underweight, or potential pediatric cases
- **Lifestyle risk** — e.g. excessive sedentary time, insufficient sleep
- **Clinical risk** — e.g. depression indicators, diabetes

These flags act as **safety guardrails**: a hard, explainable rule that says "this
person needs special handling," rather than a black-box decision no one can audit.

**Step 3 — Basic visualization**
Simple charts show how common each risk category and flag is across the dataset —
a sanity check that the categories make sense before building on top of them.

**Step 4 — Standardization & PCA (simplifying complexity)**
Many health metrics overlap heavily — weight, BMI, and waist size all largely tell
the same story. This step uses a technique called **PCA (Principal Component
Analysis)** to compress that overlap into a small number of independent factors
(e.g. one factor capturing overall "body composition," another capturing
"lifestyle/mental load"), while still preserving most of the original information
(around 80%). This keeps later analysis efficient without losing the big picture.

## Why this matters

The goal isn't just clean data for its own sake — it's a foundation that lets an AI
system recognize, for example, a likely pediatric or high-risk user and respond with
appropriate caution, rather than treating everyone the same way a generic fitness
chatbot would.

## Current scope

This version focuses on the **rule-based flagging system** (Step 2) as the primary
mechanism for identifying risk groups, with PCA (Step 4) used to simplify the
underlying numeric features for any further analysis. An earlier version of this
project also explored unsupervised clustering (grouping users by patterns the data
reveals on its own) on top of the PCA output, but that approach was set aside in
favor of the more transparent, auditable rule-based flags — which are easier to
explain and trust in a health-related context.
