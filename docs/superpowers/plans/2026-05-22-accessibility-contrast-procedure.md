# Accessibility Contrast & Text-Size Procedure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the three accessibility rule files plus `CHANGELOG.md` so AI agents reliably compare foreground colour against the correct opaque ancestor background and apply consistent text-size floors (16px primary, 14px secondary).

**Architecture:** Documentation-only change across four files. Canonical procedure lives in `rules/cursor/ethics-ui.mdc`. A one-line review check lands in `rules/cursor/ethics-review.mdc`. A compressed inline version lands in `rules/claude-code/CLAUDE.md` (because the Claude Code skill is loaded inline and cross-file references aren't reliably followed during code generation). `CHANGELOG.md` gets a `v2.0.1` entry. No edits to `principles/v2.0.0.md`.

**Tech Stack:** Markdown only. No build step, no tests, no runtime. Verification = `grep` for required strings.

**Note on commits:** Spencer is handling staging and commits manually. Each task's "verify" step replaces the usual TDD commit step. Do **not** run `git add`, `git commit`, or any write-side git command in this plan.

**Spec:** `docs/superpowers/specs/2026-05-22-accessibility-contrast-procedure-design.md`

---

## File Inventory

| File | Operation | Reason |
|------|-----------|--------|
| `rules/cursor/ethics-ui.mdc` | Modify | Canonical procedure lives here; checklist line replaced. |
| `rules/cursor/ethics-review.mdc` | Modify | One new PR-review question under Accessibility. |
| `rules/claude-code/CLAUDE.md` | Modify | Inline procedure under "When writing UI components". |
| `CHANGELOG.md` | Modify | Add `v2.0.1` entry. |

---

## Task 1: Update `rules/cursor/ethics-ui.mdc`

**Files:**
- Modify: `rules/cursor/ethics-ui.mdc:15` (replace single line)
- Modify: `rules/cursor/ethics-ui.mdc` (append new subsection inside Accessibility section, before the `## Representation & Stigma` heading on line 21)

- [ ] **Step 1: Read the current file to confirm line numbers**

Run: `cat -n rules/cursor/ethics-ui.mdc | sed -n '10,25p'`

Expected: line 15 is `- [ ] Text contrast meets WCAG 2.1 AA minimum (4.5:1 body, 3:1 large text)` and line 21 is `## Representation & Stigma (Structural)`. If line numbers differ, locate the equivalent content and adjust.

- [ ] **Step 2: Remove the old contrast checklist line**

Use the Edit tool. Replace the exact string:

```
- [ ] Text contrast meets WCAG 2.1 AA minimum (4.5:1 body, 3:1 large text)
```

with nothing (i.e., remove that line, including its trailing newline so the surrounding list stays tight).

Easiest implementation: Edit `old_string` = the line above plus its leading newline, `new_string` = empty string.

- [ ] **Step 3: Append the new subsection inside the Accessibility section**

The new subsection goes after the last existing Accessibility checklist line (`- [ ] Touch targets are at least 44x44px`, currently line 19) and before the blank line that precedes `## Representation & Stigma (Structural)`.

Use the Edit tool to replace:

```
- [ ] Touch targets are at least 44x44px

## Representation & Stigma (Structural)
```

with:

```
- [ ] Touch targets are at least 44x44px

### Colour Contrast & Text Size — How to Check

AI agents consistently miscompute contrast by comparing a foreground colour against the wrong background. Follow this procedure exactly.

1. Identify the element's resolved foreground colour (text colour, icon fill, or border colour for affordances).
2. Find the *actual* background by walking up the parent chain:
   - Start at the element's direct parent.
   - If that parent's background is transparent (`transparent`, `rgba(_, _, _, 0)`, unset, or inherited from a transparent ancestor) — keep walking up.
   - Stop at the first ancestor with an opaque background colour.
   - That ancestor's background is the comparison target.
3. If a semi-transparent overlay sits between the foreground and the opaque ancestor, composite the overlay onto the ancestor first, then compare against the composited colour.
4. Compute the contrast ratio against THAT colour:
   - Body text: ≥ 4.5:1 (WCAG 2.1 AA)
   - Large text (≥ 24px regular, or ≥ 18.66px bold): ≥ 3:1
   - Non-text UI (icons, focus rings, form borders, meaningful chart elements): ≥ 3:1 against adjacent colours
5. Text size floors:
   - Primary / body text: 16px minimum.
   - Secondary text (captions, helper text, badge labels, dense table cells): 14px minimum, and must still meet the contrast ratios above.
   - Smaller than 14px is not acceptable for any UI text a user is expected to read.

Common mistakes AI agents make:
- Comparing against `body` or `:root` background when the element sits inside a card, modal, header, or other container with its own background.
- Treating `opacity` on a parent as equivalent to a darker background — it isn't; opacity multiplies through every child and breaks in dark mode.
- Reducing visual prominence with `opacity: 0.6` on text instead of picking a lower-contrast colour token. Use real colour values.
- Skipping the parent-walk when the element has no inline background, assuming "no background = white."
- Flagging text as failing accessibility purely because it is small, without checking the size floors above.

## Representation & Stigma (Structural)
```

- [ ] **Step 4: Verify the file**

Run: `grep -c "Colour Contrast & Text Size" rules/cursor/ethics-ui.mdc`
Expected: `1`

Run: `grep -c "Text contrast meets WCAG 2.1 AA minimum" rules/cursor/ethics-ui.mdc`
Expected: `0` (old line is gone)

Run: `grep -c "Walk up the parent chain\|walking up the parent chain" rules/cursor/ethics-ui.mdc`
Expected: `1`

Run: `grep -c "16px minimum" rules/cursor/ethics-ui.mdc`
Expected: `1`

Run: `grep -c "## Representation & Stigma" rules/cursor/ethics-ui.mdc`
Expected: `1` (section header still intact)

If any check fails, re-read the file, find the mismatch, fix in place, re-verify.

---

## Task 2: Update `rules/cursor/ethics-review.mdc`

**Files:**
- Modify: `rules/cursor/ethics-review.mdc:24` (add one line at end of Accessibility section)

- [ ] **Step 1: Read the current Accessibility section**

Run: `cat -n rules/cursor/ethics-review.mdc | sed -n '19,26p'`

Expected: lines 20–24 are the existing five Accessibility bullet points, ending at line 24 with `- Has new UI been tested with a screen reader or automated accessibility tool?`. Line 25 is blank, line 26 is `### Privacy`.

- [ ] **Step 2: Append the new review check**

Use the Edit tool to replace:

```
- Has new UI been tested with a screen reader or automated accessibility tool?

### Privacy
```

with:

```
- Has new UI been tested with a screen reader or automated accessibility tool?
- Is contrast computed against the actual opaque ancestor background, not the page body? Is any new UI text below the 16px primary / 14px secondary floor? See `ethics-ui.mdc` → Colour Contrast & Text Size.

### Privacy
```

- [ ] **Step 3: Verify the file**

Run: `grep -c "opaque ancestor background" rules/cursor/ethics-review.mdc`
Expected: `1`

Run: `grep -c "16px primary / 14px secondary floor" rules/cursor/ethics-review.mdc`
Expected: `1`

Run: `grep -c "^### Privacy" rules/cursor/ethics-review.mdc`
Expected: `1` (the section header that follows the addition is still present)

If any check fails, locate the mismatch and fix.

---

## Task 3: Update `rules/claude-code/CLAUDE.md`

**Files:**
- Modify: `rules/claude-code/CLAUDE.md:126-129` (expand "When writing UI components" subsection)

- [ ] **Step 1: Read the current section**

Run: `cat -n rules/claude-code/CLAUDE.md | sed -n '124,135p'`

Expected: line 126 is `### When writing UI components`, lines 127–129 are the three-line `Check for:` paragraph, line 130 is blank, line 131 begins `### When writing data models or APIs`.

- [ ] **Step 2: Replace the subsection body**

Use the Edit tool to replace:

```
### When writing UI components
Check for: keyboard navigation, color contrast, alt text, motion controls,
inclusive form fields, representative default content, and absence of
dark patterns in all interactive flows.

### When writing data models or APIs
```

with:

```
### When writing UI components
Check for: keyboard navigation, colour contrast, alt text, motion controls,
inclusive form fields, representative default content, and absence of
dark patterns in all interactive flows.

**Colour contrast — measure correctly:**

1. Get the element's resolved foreground colour.
2. Walk up the parent chain; skip every transparent ancestor; stop at the first opaque background. That is your comparison target — not `body` or `:root`.
3. Composite any semi-transparent overlays before comparing.
4. Ratios: ≥ 4.5:1 body, ≥ 3:1 large text (≥ 24px regular / 18.66px bold), ≥ 3:1 non-text UI.

**Text size floors:**

- Primary / body text: 16px minimum.
- Secondary text (captions, helper, badges, dense cells): 14px minimum, contrast ratios still apply.

**Do not** use `opacity` to reduce text prominence — pick a lower-contrast colour token instead. Opacity multiplies through children and breaks in dark mode.

### When writing data models or APIs
```

- [ ] **Step 3: Verify the file**

Run: `grep -c "Colour contrast — measure correctly" rules/claude-code/CLAUDE.md`
Expected: `1`

Run: `grep -c "Walk up the parent chain" rules/claude-code/CLAUDE.md`
Expected: `1`

Run: `grep -c "16px minimum" rules/claude-code/CLAUDE.md`
Expected: `1`

Run: `grep -c "^### When writing data models or APIs" rules/claude-code/CLAUDE.md`
Expected: `1`

Run: `grep -c "^### When writing UI components" rules/claude-code/CLAUDE.md`
Expected: `1`

If any check fails, re-read and fix.

---

## Task 4: Update `CHANGELOG.md`

**Files:**
- Modify: `CHANGELOG.md:3` (prepend `v2.0.1` entry above the existing `v2.0.0` entry)

- [ ] **Step 1: Read the current file**

Run: `cat -n CHANGELOG.md`

Expected: line 1 `# Changelog`, line 2 blank, line 3 `## v2.0.0 — March 2026`.

- [ ] **Step 2: Insert the new entry**

Use the Edit tool to replace:

```
# Changelog

## v2.0.0 — March 2026
```

with:

```
# Changelog

## v2.0.1 — May 2026
- Add explicit colour-contrast measurement procedure for AI agents
  (`rules/cursor/ethics-ui.mdc`, `rules/claude-code/CLAUDE.md`,
  `rules/cursor/ethics-review.mdc`)
- Define text-size floors: 16px primary, 14px secondary
- Document common AI-agent contrast mistakes and the
  opacity-vs-colour anti-pattern

## v2.0.0 — March 2026
```

- [ ] **Step 3: Verify the file**

Run: `grep -c "^## v2.0.1" CHANGELOG.md`
Expected: `1`

Run: `grep -c "^## v2.0.0" CHANGELOG.md`
Expected: `1`

Run: `head -4 CHANGELOG.md`
Expected: shows `# Changelog`, blank line, `## v2.0.1 — May 2026`, then the first bullet.

---

## Task 5: Final cross-file verification

- [ ] **Step 1: Confirm acceptance criteria from the spec**

Run each check; all must pass.

```bash
# ethics-ui.mdc canonical procedure present
grep -q "### Colour Contrast & Text Size — How to Check" rules/cursor/ethics-ui.mdc && echo OK || echo MISS

# old single-line contrast check removed
! grep -q "Text contrast meets WCAG 2.1 AA minimum" rules/cursor/ethics-ui.mdc && echo OK || echo MISS

# ethics-review.mdc new line present
grep -q "opaque ancestor background" rules/cursor/ethics-review.mdc && echo OK || echo MISS

# claude-code/CLAUDE.md inline procedure present
grep -q "Colour contrast — measure correctly" rules/claude-code/CLAUDE.md && echo OK || echo MISS

# CHANGELOG entry present
grep -q "^## v2.0.1 — May 2026" CHANGELOG.md && echo OK || echo MISS

# principles/v2.0.0.md untouched (no contrast procedure language added)
! grep -q "Walk up the parent chain" principles/v2.0.0.md && echo OK || echo MISS

# no new files added under rules/
test "$(find rules/ -type f | wc -l | tr -d ' ')" = "9" && echo OK || echo "CHECK: file count changed"
```

Expected: seven `OK` lines.

- [ ] **Step 2: Confirm git status reflects only the four expected files modified**

Run: `git status --short`

Expected: working tree shows modifications to exactly:
- `CHANGELOG.md`
- `rules/cursor/ethics-ui.mdc`
- `rules/cursor/ethics-review.mdc`
- `rules/claude-code/CLAUDE.md`

Plus whatever was already dirty before the plan started (per session-start `git status`: `.claude/settings.local.json`, `.gitignore`, `docs/essay-draft.md`, and the deleted `.dual-graph/` files). The plan adds the four files above and nothing else.

If anything else changed, identify why and revert the unintended edit.

- [ ] **Step 3: Hand back to Spencer**

Do **not** run `git add`, `git commit`, or `git push`. Report completion with a one-line summary of files touched.

---

## Self-Review (already performed during plan authoring)

- **Spec coverage:** Every spec section maps to a task. Files Touched table covers all four targets. Acceptance Criteria from the spec are verified in Task 5 Step 1.
- **Placeholder scan:** No TBD/TODO. Every Edit shows full before/after strings.
- **Type consistency:** N/A (markdown only). String identifiers (`### Colour Contrast & Text Size — How to Check`, `Colour contrast — measure correctly`, `opaque ancestor background`) are used consistently between the Edit content and the verify-step `grep` patterns.
- **Encoding:** Long em dashes (`—`) appear in the canonical block. Project files already use `—` (e.g., `## v2.0.0 — March 2026`). Safe.
