# Rules & Skills

AI agent rules and skills for applying the Product Ethics Principles
in your development workflow.

**Scope:** "Supported" means the tool reads these files as it works. That means Cursor and Claude Code only. Other apps, including ones built on Claude, can't load these rules, so the framework doesn't reach them.

---

### Severity-driven enforcement

These rules read severity tags (Foundational, Structural, Aspirational) directly from the principles file and translate them into tool behaviour. See [Enforcement by severity](../principles/v2.0.0.md#enforcement-by-severity) for the canonical mapping.

## CI gates by Foundational principle

Continuous Integration, or "CI," is a software development practice where developers frequently merge their code changes into a central repository. Every time code is merged, automated builds and tests are triggered to verify that the new changes integrate seamlessly without breaking the application

Foundational violations of the Product Ethics Principles should cause a warning in CI. Each row below pairs a principle with the CI tool identified by research evidence. Rows without an evidence-named tool point to the relevant standard or review mode instead.

| # | Principle | Tools named in evidence | What the gate checks | Evidence source |
|---|-----------|-------------------------|----------------------|-----------------|
| 1 | Accessibility | `axe-core`, `pa11y`, `lighthouse` | WCAG 2.2 AA conformance, automated subset (~30-40% of issues) | Empirical report |
| 6 | Privacy | No CI-grade tool named in evidence | Data minimization and consent flows reviewed at design time; secret leakage covered under the Security row | Empirical report; Sciendo 2025 review |
| 7 | Security | `semgrep`; `Dependabot`, `Renovate`, `Snyk` (dependencies); `GitGuardian`, `Trufflehog`, GitHub built-in scanner (secrets); SBOM tooling | Known-bad code patterns, vulnerable dependencies, secret leakage, supply-chain provenance | Empirical report; NIST SSDF |
| 8 | Safety | No CI-grade tool named in evidence | Pre-launch risk assessment (governance review); per-population vulnerability audits | Empirical report; UK ICO Children's Code; US Surgeon General 2023 |
| 10 | Algorithmic Accountability (Foundational sub-case) | Hugging Face model cards at release | Model card present and complete at every model release | Empirical report; FAccT 2024-25 |
| 11 | User Health (Foundational sub-case: deliberate manipulation) | No CI-grade tool named in evidence | Manipulation-pattern review at design time | Empirical report; npj Digital Medicine 2025 |
| 13 | Honesty & Truth (Foundational sub-case: AI disclosure) | C2PA Content Credentials | Provenance metadata present on AI-generated images and video at publish time | Empirical report; Mozilla 2024 |
| 15 | Economic Justice (Foundational sub-case: predatory features) | No CI-grade tool named in evidence | Dark-pattern review using Brignull's taxonomy at design time | Empirical report; FTC 2022; ICPEN 2024 |
| 17 | Labor Ethics | No CI-grade tool named in evidence | Supply-chain labor audit at quarterly governance review | Empirical report; Steiger CHI 2021; Middlesex 2025 |

**Reading the table.** A `No CI-grade tool named in evidence` row is itself a finding, not a placeholder. It means the empirical research base reviewed so far in the creation of the Product Ethics Principles does not name a tool that runs at CI gate time for that principle. Adopters who know of one may wire it, and contributors may recommend it, but the framework does not currently recommend a specific tool for those rows.

**Scope.** This table covers Foundational and compound-Foundational sub-cases only. Structural and Aspirational principles route through review cycles rather than CI gates.

## Cursor Rules

**Location:** `rules/cursor/`

Six `.mdc` rule files for [Cursor](https://cursor.sh). Each targets a
different workflow moment.

| File | Fires when | Purpose |
|------|-----------|---------|
| `ethics-core.mdc` | Always | Core principle reference injected into every session |
| `ethics-ui.mdc` | Editing UI files (jsx, tsx, vue, html, css, scss, svelte) | Accessibility, representation, dark patterns, user health |
| `ethics-data.mdc` | Editing data/API files (models, routes, schema, migrations) | Privacy, security, algorithmic accountability, surveillance |
| `ethics-feature.mdc` | On demand | New feature ethics review — five questions before you build |
| `ethics-review.mdc` | On demand | Full PR/code review ethics audit against all 18 principles |
| `ethics-spec.mdc` | Editing spec/PRD markdown files | Ethics lens for product documents |

### Installation

1. Copy the `rules/cursor/` directory contents into your project:

```bash
mkdir -p your-project/.cursor/rules
cp path/to/Product-Ethics-Principles/rules/cursor/* your-project/.cursor/rules/
```

2. Restart Cursor. The `ethics-core.mdc` rule fires automatically on every
   session. The others fire automatically by file type or when you ask for
   a feature review / ethics audit.

3. To trigger a full ethics audit manually, ask Cursor:
   > "Run a full ethics review of this PR / feature / file"

### Customizing

Each rule file uses standard Cursor `.mdc` frontmatter:
- `alwaysApply: true` — injected into every chat and Cmd+K context
- `globs` — fires when matching files are open or referenced
- No globs + `alwaysApply: false` — agent-requested (you invoke it manually)

Edit the glob patterns to match your project's file structure. The rule
content is yours to adapt under CC BY 4.0 — attribution appreciated.

---

## Claude Code Skill

**Location:** `rules/claude-code/CLAUDE.md`

A `CLAUDE.md` file for [Claude Code](https://claude.ai/code) that tells
Claude to apply the 18 principles throughout its work in your project.

### Installation

Copy the file into your project root or any subdirectory:

```bash
cp path/to/Product-Ethics-Principles/rules/claude-code/CLAUDE.md your-project/CLAUDE.md
```

If your project already has a `CLAUDE.md`, append the contents of this
file to the existing one — Claude Code reads it all.

### What it does

Once installed, Claude Code will:
- Apply the 18 principles framework when writing features, reviewing code,
  and working with data
- Raise Foundational concerns as blockers and Structural concerns as
  required conversations
- Apply specific checks for UI work, data handling, specs, and PRs
- Frame concerns as design problems to solve, not compliance items to log

---

## Using both together

Cursor rules and the Claude Code skill are complementary. Cursor rules
fire automatically during editing and provide in-context checklists.
The Claude Code skill provides the broader reasoning framework for
longer agentic sessions — scaffolding features, reviewing whole files,
writing specs.

Both pull from the same 18 principles. Neither substitutes for dedicated
accessibility testing, legal privacy review, security penetration testing,
or formal algorithmic audits. They raise the issues those functions need
to address.

---

## Version

These rules are calibrated to **Principles v2.0.6** (June 2026).
When the principles are updated, rule files are updated in the same release.
See the root CHANGELOG.md for version history.
