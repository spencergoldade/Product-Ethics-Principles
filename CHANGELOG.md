# Changelog

## v2.0.6 (June 2026)
- Clarified what "AI support" covers. A scope note in README and
  `rules/README.md` distinguishes two things: installing the rule files
  into Cursor or Claude Code, which then read them as they build, versus a
  separate app that runs on Claude underneath. Telling that app to "follow
  the principles" installs nothing, so the framework never reaches it.
- Renamed the README section heading from "With AI coding tools" to
  "Installing into AI coding tools," so the heading itself signals that
  support is an install step.

## v2.0.5 (May 2026)
- Distilled the operationalization layer into the Claude Code and Cursor rules.
  Each principle's named standard now lives in the rules themselves, an
  operationalization reference in `ethics-core.mdc` and `claude-code/CLAUDE.md`,
  with source links in the UI, data, feature, spec, and review rules, so AI
  tools can cite and consult the standard.
- Added per-principle detection cues, run-verbatim Privacy and Security checks
  (closing a client-side sensitive-data gap), a pre-design data-sensitivity
  trigger, plain-language and language-availability checks, and a per-commit
  Foundational checkpoint for agentic builds.

## v2.0.4 (May 2026)
- Added `CI gates by Foundational principle` table to `rules/README.md`. Pairs Foundational and compound-Foundational principles with evidence-named CI tools. Rows without an evidence-named tool point to the relevant standard or review mode.
- Bumped version markers across README, principles, and rules.

## v2.0.3 (May 2026)
- Bind enforcement to severity tiers. Foundational tier: refuse at generation time and warn in CI. Structural tier: flag and explain. Aspirational tier: governance review only. Compound severities apply per sub-case.
- Added preambles to `rules/cursor/ethics-core.mdc` and `rules/claude-code/CLAUDE.md` defining tool behaviour per tier. Sibling `.mdc` files reference the core preamble.
- Add `Severity-driven enforcement` pointer to `rules/README.md`.
- Bump version markers across README, principles, and rules.
- Switch existing changelog headings to parenthesis style for consistency (v2.0.2, v2.0.1, v2.0.0, v1.0.0).

## v2.0.2 (May 2026)
- Add Operationalization line to each of the 18 principles, pointing
  to the closest established measurement or testing standard (WCAG,
  NIST SSDF, GDPR, SCI/ISO 21031, EU AI Act, FTC ROSCA, EU DSA,
  and others); flag principles with no mature standard
- Add vulnerable-populations cross-cut to Review mode in the preface
- Bump version markers across README, principles, and rules

## v2.0.1 (May 2026)
- Add explicit colour-contrast measurement procedure for AI agents
  (`rules/cursor/ethics-ui.mdc`, `rules/claude-code/CLAUDE.md`,
  `rules/cursor/ethics-review.mdc`)
- Define text-size floors: 16px primary, 14px secondary
- Document common AI-agent contrast mistakes and the
  opacity-vs-colour anti-pattern

## v2.0.0 (March 2026)
- Expanded from 12 to 18 principles
- Added: Algorithmic Accountability, Autonomy & Agency,
  Economic Justice, Environmental Sustainability,
  Labor Ethics, Civic Responsibility
- Split Security from Safety; split Stigma & Bias into
  Representation & Stigma and Algorithmic Accountability
- Added Tognazzini-style expansion: Intent, In Practice,
  Anti-Patterns, Failure Modes, Connections, For the Builder
- Added severity tiers: Foundational / Structural / Aspirational
- Added full citation apparatus (28 citations)

## v1.0.0 (October 2020)
- Initial 12 principles published at spencergoldade.ca