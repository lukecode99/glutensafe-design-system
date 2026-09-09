# GlutenSafe UK — Design System

> Import this repo into **Claude Design** (claude.ai/design → Design system → Import from GitHub).
> Claude Design will build using these tokens and components, and check its output against them
> before you see it. Edit visually in the canvas; the agent side edits here; git keeps both in sync.

## 1. Product & voice
GlutenSafe answers the question community apps dodge: **"where can I eat out that is actually
coeliac-*safe*, not just 'has a gluten-free option'."** The whole brand rests on **honest,
graded trust** — we never overstate safety, and we never merge "has GF" with "coeliac-safe".

**Voice:** calm, factual, reassuring. Never breezy about safety. Every safety claim carries its
source. Copy is plain-English and paraphrased in our own words (never verbatim third-party menus).

## 2. Colour tokens (see `tokens.css` — the single source of truth)
**Neutrals** — ink `#10222b`, muted `#5a6b74`, line `#e3ebee`, bg `#f7fafb`, card `#ffffff`.
**Brand** — teal `#0c7c74` (primary / active / CTA), teal-dark `#075b55` (pressed / links).

**Trust-tier palette — the heart of the product. NEVER collapse these into one "GF" colour:**
- **Gold `#b8860b`** — *Accredited*: Coeliac UK accredited, independently audited. Highest trust.
- **Green `#1a7f37`** — *Coeliac provision*: venue states a cross-contamination safeguard in its
  own words. Not independently verified. **Positive reviews alone NEVER reach green.**
- **Blue `#1f6feb`** — *GF options*: GF items listed, no safeguard claim.
- **Amber `#8a5a00`** — *Caution*: the venue's own wording flags a cross-contamination risk.
- **Grey `#6b7680`** — *No GF found*: we read the menu and it offers nothing GF.
- **Purple `#5b3a9e`** — *Menu not readable*: found the site, couldn't read the menu. **Not a
  judgement either way.** Never conflate with grey.
- **Light-grey `#6b7280`** — *Not yet assessed*: no confirmed website to read yet.

Each tier has a matching `-bg` and `-line` pair in `tokens.css` for badge/panel surfaces.
Red `#c62828` is reserved for errors and the worst hygiene bands.

## 3. Type
System font stack (`--font`): `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, …`.
Scale: title 18 / body 14 / small 12 / micro 10.5. Weights: 400 / 600 / 700 / 800.

## 4. Shape & spacing
Radii: sm 6 · default 10 · lg 12 · pill 999. Spacing step: 4 / 8 / 11 / 16.
Card shadow `0 1px 6px rgba(16,34,43,.06)`. Inputs 1.5px borders, radius 12.

## 5. Components (previews in `components/`)
- **`tier-badges.html`** — the seven trust tiers as badges. The most important component; the
  grammar the whole UI is built on. Positive tiers, caution/absence, unknown states — visually
  distinct groups, never one flat "GF" chip.
- **`venue-card.html`** — the core list unit: tier badge + hygiene badge + breadth badge, title,
  cuisine/location/distance meta, a **signals panel** (tinted to the tier, left-border accent,
  always with an evidence source line), and action links (Book / Menu / Call).
- **`search-filter.html`** — search input, cuisine select, the **safety-bar chip toggle**
  (Coeliac-safe only / +Some GF / Any GF option — *same data, user chooses the threshold*), and
  the Map/List view switch.
- **`header.html`** — shield logo + wordmark (GlutenSafe, "Safe" in teal), Sign-in + Claim CTA,
  and the honesty banner.

## 6. Non-negotiable design rules
1. **Two thresholds, never collapsed** — always surface "GF available" and "coeliac-safe"
   separately. The safety-bar toggle is the product, not a nice-to-have.
2. **Every positive claim shows its source** — the `.evsrc` line is mandatory on green/gold cards.
3. **Unknown ≠ negative** — purple/light-grey states must read as "we don't know", never as a fail.
4. **Gold outranks green outranks blue** — visual weight follows trust rank; don't let a prettier
   blue out-shout a gold.
5. **Never ship a false "safe"** — when in doubt, the design defaults to the lower-trust tier.
