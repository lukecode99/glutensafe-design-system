# GlutenSafe Design Bridge

A GitHub-backed sync layer between **Claude Design** (visual canvas, in your browser) and the
**agent** (Nano, building the live app). git is the neutral hand-off — neither side's login blocks it.

## What's here
- `DESIGN.md` — the design-system spec Claude Design imports and builds against.
- `tokens.css` — colour / type / spacing tokens, extracted from the live site (single source of truth).
- `components/*.html` — self-contained component previews. Each starts with a
  `<!-- @dsCard group="…" -->` marker so Claude Design's Design-System pane indexes it as a card.

## Start from the real, current site
`pages/current-site.html` is a **self-contained snapshot of the live GlutenSafe page** — real header,
banner, filters, map pane and a card for every trust tier — using the live site's own CSS verbatim.
It renders on its own (no API, no login), so it's the starting canvas.

To design changes onto it in Claude Design:
1. Import this repo (below). The page shows up under the **Pages** group as *"Current live site"*.
2. Open it as the frame, then just type the change — e.g. *"make the venue cards more compact and
   move the safety-bar toggle to the top."* Claude Design edits the real layout, not a blank page.
3. When you like it, commit back / tell the agent, and Nano ports the change into `build-site.mjs`.

(No Claude Design import? Same file works as a plain upload/paste, or open it in a browser to eyeball.)

## The workflow (switch between the two)
1. **Import once:** claude.ai/design → Design system → **Import from GitHub** → this repo.
2. **Design visually:** iterate in the Claude Design canvas — it builds in GlutenSafe's real brand,
   starting from `pages/current-site.html`.
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
