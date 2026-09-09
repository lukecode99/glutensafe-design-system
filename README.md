# GlutenSafe Design Bridge

A GitHub-backed sync layer between **Claude Design** (visual canvas, in your browser) and the
**agent** (Nano, building the live app). git is the neutral hand-off — neither side's login blocks it.

## What's here
- `DESIGN.md` — the design-system spec Claude Design imports and builds against.
- `tokens.css` — colour / type / spacing tokens, extracted from the live site (single source of truth).
- `components/*.html` — self-contained component previews. Each starts with a
  `<!-- @dsCard group="…" -->` marker so Claude Design's Design-System pane indexes it as a card.

## The workflow (switch between the two)
1. **Import once:** claude.ai/design → Design system → **Import from GitHub** → this repo.
2. **Design visually:** iterate in the Claude Design canvas — it builds in GlutenSafe's real brand.
3. **Export / commit back** to this repo when you like a change.
4. **Agent picks it up:** Nano pulls, and wires the updated components into the live GlutenSafe app.
5. Repeat. Rough it out with the agent → refine in Claude Design → hand back to the agent to ship.

## Live full two-way sync (optional, full-fat)
Run Claude Code yourself on the MacBook logged into claude.ai — then `/design-sync` gives true
live component-by-component sync. The git bridge above is the works-today version that leans on
the agent for the heavy lifting.

## Source of truth
Tokens mirror `projects/gf-map/build-site.mjs` on the main workspace. If the live site's brand
changes, update `tokens.css` here to match — this repo should never drift from what ships.
