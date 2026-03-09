# Contributing to Product Ethics Principles

Thank you for engaging with this framework. These principles are meant to be living documents — amended as our understanding deepens, extended as new ethical terrain emerges, and challenged when the existing text is wrong.

Contributions are welcome from practitioners, researchers, educators, and anyone who builds products or studies their social impact.

---

## Table of Contents

- [Community Standards](#community-standards)
- [Types of Contributions](#types-of-contributions)
- [Criteria Every Principle Must Meet](#criteria-every-principle-must-meet)
- [How to Propose an Amendment](#how-to-propose-an-amendment)
- [How to Propose a New Principle](#how-to-propose-a-new-principle)
- [How Versioning Works](#how-versioning-works)
- [What We're Not Looking For](#what-were-not-looking-for)

---

## Community Standards

This project follows a simple code of conduct: engage with ideas on their merits, extend good faith to other contributors, and hold critique to the work — not to the people.

Contributions that demean, harass, or exclude other contributors will not be accepted and may result in removal from the project.

If you experience or witness a conduct issue, contact Spencer Goldade directly via [spencergoldade.ca](https://spencergoldade.ca).

---

## Types of Contributions

| Type | Examples | Version bump |
|---|---|---|
| **Copy fix** | Typo, grammar, broken link, citation correction | Patch (x.x.**1**) |
| **Amendment** | Clarifying or strengthening the definition, In Practice, or Anti-Patterns of an existing principle | Minor (x.**1**.0) |
| **New principle** | Adding a principle not currently in the framework | Major (**3**.0.0) |
| **Case study** | Adding a Failure Mode example to an existing principle | Minor (x.**1**.0) |
| **Structural change** | Reorganizing sections, changing severity levels | Minor or Major, depending on scope |

---

## Criteria Every Principle Must Meet

Before submitting or evaluating any contribution, check it against these criteria. All six structural sections are required; partial submissions will be returned for completion.

### 1. Violable definition
The one-sentence definition must describe a constraint that can be *violated*. A principle that cannot be violated is a declaration, not a principle.

- **Good:** *"The system collects only what it needs and uses data only for the purposes users consented to."* This can be violated by collecting more than needed, or using data for unconsented purposes.
- **Not good:** *"The system respects user privacy."* This is a declaration. It cannot be tested or violated.

Ask: *Can I describe, in concrete terms, what it would look like for a product to fail this?* If yes, the definition is violable.

### 2. Severity level
Every principle must be assigned one of three severity levels, with a rationale:

- **Foundational** — Violations actively harm users. Reserve this for principles where a violation directly causes psychological, physical, financial, or civil harm to real people.
- **Structural** — Violations limit who can participate in or benefit from the system. Use this when the harm is exclusionary or inequitable rather than directly injurious.
- **Aspirational** — The system could do more good than it currently does. Use this when the principle describes a ceiling of positive impact rather than a floor of acceptable behavior.

### 3. All six sections
Every principle must include:

| Section | Purpose |
|---|---|
| **Intent** | The rationale — *why* this matters and what it's trying to prevent |
| **In Practice** | 4–8 concrete, testable compliance criteria |
| **Anti-Patterns** | Named, specific violations with descriptive labels |
| **Failure Modes** | At least one real-world case study with a citation |
| **Connections** | Which other principles this intersects with, and how |
| **For the Builder** | Concrete obligations for the product team |

### 4. Real-world grounding
Failure Modes must cite actual documented cases — published reporting, legal proceedings, academic research, or credible public disclosure. Hypothetical or fabricated examples are not acceptable.

### 5. Practitioner audience
Write for product designers, PMs, and DEI practitioners, not for philosophers or lawyers. Avoid jargon. Use plain language and active voice. If you wouldn't say it in a design crit, don't write it here.

### 6. No overlap without distinction
If a proposed principle substantially overlaps with an existing one, the proposal must clearly articulate what the new principle covers that the existing ones do not. Partial coverage differences belong in **Connections**, not in new principles.

---

## How to Propose an Amendment

An amendment modifies existing text: a definition, a compliance criterion, an anti-pattern label, a failure mode example, or the connections section.

1. **Open an issue first.** Describe what you believe is wrong or incomplete and why. This prevents duplicate work and surfaces whether others share the concern.

2. **Fork the repository** and make your changes in a branch named `amend/<principle-name>` (e.g., `amend/privacy`).

3. **Edit the relevant section** in `principles/v2.0.0.md`. If your amendment changes the one-sentence definition, include a brief explanation of why the current definition is insufficient.

4. **Update `CHANGELOG.md`** with a one-line description of the change under an `Unreleased` section.

5. **Open a pull request** referencing the issue. The PR description should explain:
   - What the current text says
   - What you're changing it to
   - Why the change improves the principle

**Amendments that strengthen** existing text (tighten a definition, add a documented failure mode, name a common anti-pattern) are generally welcomed. **Amendments that weaken** a principle (soften definitions, reduce compliance criteria) require a strong argument and will receive close scrutiny.

---

## How to Propose a New Principle

New principles are a major version change and require a higher bar than amendments.

1. **Open an issue** using the label `new-principle`. The issue should argue:
   - What ethical terrain is not covered by any existing principle
   - Why this terrain constitutes a distinct principle rather than an extension of an existing one
   - At least two documented real-world cases where the absence of this principle caused harm

2. **Write a complete draft** using the standard structure (all six sections, violable definition, severity level, real-world failure modes with citations). Incomplete drafts will not be reviewed.

3. **Fork the repository** and add your draft as `proposals/<principle-name>.md`.

4. **Open a pull request** referencing the issue. Community discussion happens on the PR before any decision is made.

5. **Expect a review period of at least 30 days.** New principles change the scope of the framework and warrant careful consideration.

**New principles that are strong candidates:**
- Cover a domain not addressed by any existing principle
- Are actionable by a product team (not purely regulatory or legal)
- Have documented failure cases in existing products
- Can be written with a genuinely violable definition

**New principles that are unlikely to be accepted:**
- Substantially duplicate existing principles
- Cannot be stated in a single violable sentence
- Require a compliance standard that can't be tested or evaluated
- Are better addressed as an amendment or case study addition to an existing principle

---

## How Versioning Works

This project uses [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`

| Change type | Version component | Example |
|---|---|---|
| Typo, grammar, citation fix | **Patch** | 2.0.0 → 2.0.1 |
| Amendment to an existing principle | **Minor** | 2.0.0 → 2.1.0 |
| New case study or failure mode | **Minor** | 2.0.0 → 2.1.0 |
| Severity level change | **Minor** | 2.0.0 → 2.1.0 |
| New principle added | **Major** | 2.0.0 → 3.0.0 |
| Principle removed or merged | **Major** | 2.0.0 → 3.0.0 |

Each new version is published as a new file in `/principles/` (e.g., `v2.1.0.md`) and noted in `CHANGELOG.md`. The README badge and CLAUDE.md are updated to point to the current version.

---

## What We're Not Looking For

To keep the framework focused and useful:

- **Policy recommendations.** These principles are design heuristics, not regulatory guidance. If your contribution reads like a compliance checklist for a specific law or jurisdiction, it belongs elsewhere.
- **Brand or tool endorsements.** Anti-patterns and In Practice sections should be tool-agnostic.
- **Purely aspirational additions without failure cases.** If you can't point to real-world harm, the principle isn't ready.
- **Process contributions without product relevance.** This framework is specifically about products and the decisions made in building them.

---

*These principles are maintained by Spencer Goldade and licensed CC BY 4.0. Contributions are accepted under the same license.*
