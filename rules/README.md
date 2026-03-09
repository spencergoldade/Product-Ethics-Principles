# Rules & Skills

AI agent rules and skills for applying the Product Ethics Principles
in your development workflow.

---

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

These rules are calibrated to **Principles v2.0.0** (March 2026).
When the principles are updated, rule files are updated in the same release.
See the root CHANGELOG.md for version history.
