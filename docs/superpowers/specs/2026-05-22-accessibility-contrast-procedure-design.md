---
title: Accessibility — Colour Contrast and Text Size Procedure
tags: accessibility, contrast, wcag, ai-agents, rules, ui
date: 2026-05-22
status: approved
---

# Accessibility — Colour Contrast and Text Size Procedure

## Problem

AI coding agents (Claude Code, Cursor, Gemini, and similar) consistently
misjudge colour contrast when generating or reviewing UI. Two failure
modes dominate:

1. **Wrong comparison background.** The agent compares a foreground colour
   against `body` or `:root` rather than the element's actual opaque
   ancestor (card, modal, header, etc.). This produces both false passes
   (text "passes" against a white body it never sits on) and false fails
   (text flagged against a body background it never touches).
2. **Transparent parents ignored.** When the direct parent has no
   background (`transparent`, unset, or `rgba(_, _, _, 0)`), agents either
   assume the parent IS the background or default to white. They do not
   walk further up the tree.

A third recurring issue is unrelated to contrast but commonly co-occurs:
agents flag legitimate text as "failing accessibility" simply because it
is small, without a clear, project-defined minimum.

The project's existing accessibility rules
(`rules/cursor/ethics-ui.mdc`, `rules/cursor/ethics-review.mdc`,
`rules/claude-code/CLAUDE.md`) reference WCAG 2.1 AA contrast ratios but
do not explain the comparison procedure or define a text-size floor.

## Goals

- Give AI agents an unambiguous procedure for finding the correct
  comparison background when evaluating contrast.
- Define explicit text-size floors (16px primary, 14px secondary) that
  agents can act on without inventing thresholds.
- Keep the change operational: edits live in the rule files that agents
  load, not the high-level principles narrative.
- Preserve existing checklist style and tone in the rule files.

## Non-Goals

- Modify `principles/v2.0.0.md`. The narrative principle stays at the
  level it currently sits.
- Add a new file in `rules/`. Three existing files are sufficient.
- Reproduce the WCAG specification. Reference the relevant ratios and
  point to authoritative sources where appropriate.
- Add tooling or automated checks. This is documentation for AI agents,
  not a linter.

## Files Touched

| File | Change |
|------|--------|
| `rules/cursor/ethics-ui.mdc` | Replace single contrast checklist line with a new "Colour Contrast & Text Size — How to Check" subsection containing the full procedure. |
| `rules/cursor/ethics-review.mdc` | Add one PR-review-shaped line pointing to the procedure. |
| `rules/claude-code/CLAUDE.md` | Insert a compressed inline version of the procedure under "When writing UI components". |
| `CHANGELOG.md` | Add `v2.0.1 — accessibility procedure clarifications` entry. |

## Canonical Procedure (lives in ethics-ui.mdc)

The full block replaces the current line:

> `Text contrast meets WCAG 2.1 AA minimum (4.5:1 body, 3:1 large text)`

with a new subsection appended after the existing Accessibility
checklist (still inside the Accessibility section):

```markdown
### Colour Contrast & Text Size — How to Check

AI agents consistently miscompute contrast by comparing a foreground
colour against the wrong background. Follow this procedure exactly.

1. Identify the element's resolved foreground colour (text colour, icon
   fill, or border colour for affordances).
2. Find the *actual* background by walking up the parent chain:
   - Start at the element's direct parent.
   - If that parent's background is transparent (`transparent`,
     `rgba(_, _, _, 0)`, unset, or inherited from a transparent
     ancestor) — keep walking up.
   - Stop at the first ancestor with an opaque background colour.
   - That ancestor's background is the comparison target.
3. If a semi-transparent overlay sits between the foreground and the
   opaque ancestor, composite the overlay onto the ancestor first, then
   compare against the composited colour.
4. Compute the contrast ratio against THAT colour:
   - Body text: ≥ 4.5:1 (WCAG 2.1 AA)
   - Large text (≥ 24px regular, or ≥ 18.66px bold): ≥ 3:1
   - Non-text UI (icons, focus rings, form borders, meaningful chart
     elements): ≥ 3:1 against adjacent colours
5. Text size floors:
   - Primary / body text: 16px minimum.
   - Secondary text (captions, helper text, badge labels, dense table
     cells): 14px minimum, and must still meet the contrast ratios above.
   - Smaller than 14px is not acceptable for any UI text a user is
     expected to read.

Common mistakes AI agents make:
- Comparing against `body` or `:root` background when the element sits
  inside a card, modal, header, or other container with its own
  background.
- Treating `opacity` on a parent as equivalent to a darker background —
  it isn't; opacity multiplies through every child and breaks in dark
  mode.
- Reducing visual prominence with `opacity: 0.6` on text instead of
  picking a lower-contrast colour token. Use real colour values.
- Skipping the parent-walk when the element has no inline background,
  assuming "no background = white."
- Flagging text as failing accessibility purely because it is small,
  without checking the size floors above.
```

## ethics-review.mdc Change

Add one line under the existing accessibility-related review checks:

```markdown
- Is contrast computed against the actual opaque ancestor background,
  not the page body? Is any new UI text below the 16px primary / 14px
  secondary floor? See ethics-ui.mdc → Colour Contrast & Text Size.
```

## claude-code/CLAUDE.md Change

In the "When writing UI components" section (currently around line 127),
replace the single line:

> `Check for: keyboard navigation, color contrast, alt text, motion
> controls, inclusive form fields, representative default content, and
> absence of dark patterns in all interactive flows.`

with an expanded block that keeps the original sweep but adds the
inline contrast/size procedure:

```markdown
### When writing UI components

Check for: keyboard navigation, colour contrast, alt text, motion
controls, inclusive form fields, representative default content, and
absence of dark patterns in all interactive flows.

**Colour contrast — measure correctly:**

1. Get the element's resolved foreground colour.
2. Walk up the parent chain; skip every transparent ancestor; stop at
   the first opaque background. That is your comparison target — not
   `body` or `:root`.
3. Composite any semi-transparent overlays before comparing.
4. Ratios: ≥ 4.5:1 body, ≥ 3:1 large text (≥ 24px regular / 18.66px
   bold), ≥ 3:1 non-text UI.

**Text size floors:**

- Primary / body text: 16px minimum.
- Secondary text (captions, helper, badges, dense cells): 14px minimum,
  contrast ratios still apply.

**Do not** use `opacity` to reduce text prominence — pick a lower-contrast
colour token instead. Opacity multiplies through children and breaks in
dark mode.
```

## CHANGELOG.md Change

Prepend a new entry above `v2.0.0`:

```markdown
## v2.0.1 — May 2026

- Add explicit colour-contrast measurement procedure for AI agents
  (`rules/cursor/ethics-ui.mdc`, `rules/claude-code/CLAUDE.md`,
  `rules/cursor/ethics-review.mdc`).
- Define text-size floors: 16px primary, 14px secondary.
- Document common AI-agent contrast mistakes and the opacity-vs-colour
  anti-pattern.
```

## Acceptance Criteria

- `rules/cursor/ethics-ui.mdc` contains the full "Colour Contrast & Text
  Size — How to Check" subsection with all five numbered procedure steps
  and the "Common mistakes" list.
- The previous single-line contrast checklist item is removed (its content
  is now inside the new subsection).
- `rules/cursor/ethics-review.mdc` contains the one-line review check
  pointing back at the procedure.
- `rules/claude-code/CLAUDE.md` "When writing UI components" section
  contains the compressed inline procedure and the text-size floors.
- `CHANGELOG.md` has the new `v2.0.1` entry.
- No edits to `principles/v2.0.0.md`.
- No new files in `rules/`.

## Open Questions

None — design approved by Spencer 2026-05-22.

## Risks

- Three files duplicate the procedure (full / compressed / one-line).
  Future revisions must update all three. Mitigation: the canonical
  source is `ethics-ui.mdc`; the others link back to it by name.
- The 14px secondary-text floor is a project decision, not a WCAG
  requirement. Some agents may push back against it. The wording calls
  it a project floor, not a standards requirement.
