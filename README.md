# Product Ethics Principles

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](CHANGELOG.md)
[![Principles](https://img.shields.io/badge/principles-18-green.svg)](principles/v2.0.0.md)

A practitioner's reference for building products that are good for the world.

Maintained by [Spencer Goldade](https://spencergoldade.ca) · CC BY 4.0

---

## What this is

A heuristic framework for product designers, product managers, and the
strategists and DEI leaders who work alongside them — in the tradition of
[Nielsen's 10 Usability Heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)
and [Tognazzini's First Principles of Interaction Design](https://asktog.com/atc/principles-of-interaction-design/).

Where those frameworks focus on functional usability, these 18 principles
focus on the **moral, ethical, and social impact** of what we build.

Every principle is written to be *violable* — defining failure as clearly as
success. A principle that can't be violated can't guide a decision.

---

## The 18 Principles

| # | Principle | Severity |
|---|-----------|----------|
| 1 | [Accessibility](principles/v2.0.0.md#1-accessibility) | Foundational |
| 2 | [Diversity](principles/v2.0.0.md#2-diversity) | Structural |
| 3 | [Equity](principles/v2.0.0.md#3-equity) | Structural |
| 4 | [Inclusion](principles/v2.0.0.md#4-inclusion) | Structural |
| 5 | [Belonging](principles/v2.0.0.md#5-belonging) | Structural |
| 6 | [Privacy](principles/v2.0.0.md#6-privacy) | Foundational |
| 7 | [Security](principles/v2.0.0.md#7-security) | Foundational |
| 8 | [Safety](principles/v2.0.0.md#8-safety) | Foundational |
| 9 | [Representation & Stigma](principles/v2.0.0.md#9-representation--stigma) | Structural |
| 10 | [Algorithmic Accountability](principles/v2.0.0.md#10-algorithmic-accountability) | Foundational / Structural |
| 11 | [User Health](principles/v2.0.0.md#11-user-health) | Foundational / Structural |
| 12 | [Autonomy & Agency](principles/v2.0.0.md#12-autonomy--agency) | Structural |
| 13 | [Honesty & Truth](principles/v2.0.0.md#13-honesty--truth) | Foundational / Structural |
| 14 | [False Obsolescence](principles/v2.0.0.md#14-false-obsolescence) | Structural |
| 15 | [Economic Justice](principles/v2.0.0.md#15-economic-justice) | Foundational / Structural |
| 16 | [Environmental Sustainability](principles/v2.0.0.md#16-environmental-sustainability) | Structural |
| 17 | [Labor Ethics](principles/v2.0.0.md#17-labor-ethics) | Foundational |
| 18 | [Civic Responsibility](principles/v2.0.0.md#18-civic-responsibility) | Structural / Foundational |

**Severity levels:**  

- **Foundational** — Violations actively harm users. Non-negotiable.  
- **Structural** — Violations limit who can benefit from the system.  
- **Aspirational** — The system could do more good than it currently does.  

Each principle includes: intent, in-practice criteria, anti-patterns,
real-world failure modes, connections to other principles, and
obligations for the builder team.

→ [Read the full principles document](principles/v2.0.0.md)

---

## How to use this framework

### As a practitioner reference

Read the principles. Apply them during design critique, feature review,
and product audits. The ["at a glance"](principles/v2.0.0.md#the-principles-at-a-glance)
section gives you the one-sentence definition for each.

### With AI coding tools

Drop the rules and skills into your project so your AI tools apply
the framework automatically:

**Cursor** — Copy `rules/cursor/*.mdc` into your project's `.cursor/rules/` directory.
Six rules fire automatically at the right moments: always-on reference,
UI work, data/API work, new features, code review, and spec writing.

**Claude Code** — Copy `rules/claude-code/CLAUDE.md` into your project root.
Claude Code will apply the 18 principles throughout agentic sessions.

→ [Full installation instructions](rules/README.md)

### As an organizational standard

The framework is designed to scale from individual practitioners to
team-level critique criteria to org-level governance standards.
The severity tiers (Foundational / Structural / Aspirational) provide
a triage layer for prioritization.

---

## Applying the principles: six questions

These questions apply to any product decision:

1. Is this accessible to all of our users, or to the users it's easiest to design for?
2. Whose data are we collecting, and what is the minimum we need?
3. Does this default serve the user or the platform?
4. Who is not in the room when this decision is being made, and what would they say?
5. What is the worst reasonable thing someone could do with this feature, and what have we designed to prevent it?
6. Five years from now, what will we wish we had thought of today?

---

## Contributing

This framework is maintained as a living document. Contributions welcome:


- **Amending existing principles** — evidence of real-world failure modes,
  updated anti-patterns, improved in-practice criteria
- **Proposing new principles** — with rationale, full six-section structure,
  and evidence of scope not covered by existing principles
- **Improving the rules/skills** — better Cursor rules, Claude Code
  skill improvements, new tool integrations

→ [Contributing guide](CONTRIBUTING.md)

---

## Further reading

- [Archimedean Oath](https://en.wikipedia.org/wiki/Archimedean_Oath)
- [Universal Ethical Code for Scientists](https://www.gov.uk/government/publications/universal-ethical-code-for-scientists)
- [Nielsen's 10 Usability Heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)
- [Tognazzini's First Principles of Interaction Design](https://asktog.com/atc/principles-of-interaction-design/)
- [WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
- [EU AI Act](https://artificialintelligenceact.eu)
- [EU Digital Services Act](https://digital-markets-act.ec.europa.eu)
- [Deceptive Design](https://www.deceptivedesign.org)
- [Center for Humane Technology](https://www.humanetech.com)
- [Global DEI Benchmarks (GDEIB)](https://www.centerforglobaldiversity.org)

---

## License

[Creative Commons Attribution 4.0 International](LICENSE) —
free to use, adapt, and build on with attribution to Spencer Goldade.
