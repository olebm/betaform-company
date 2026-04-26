# Betaform Design System

> _Form entsteht aus Funktion._

This folder is the **Betaform brand & UI design system** distilled from the
production codebase at `olebm/betaform` (private). It exists so any design or
build agent can produce on-brand artifacts — slides, mocks, prototypes,
production code — without having to spelunk the source repo every time.

## Sources

- **Codebase:** `olebm/betaform@main` — Next.js 16 + Tailwind, App Router.
  Specific files this system was built from:
  - `styles/globals.css` (color tokens, dark-mode mapping, aurora keyframes)
  - `tailwind.config.ts` (color → CSS-var bindings, gradients, font weights)
  - `app/layout.tsx` (Söhne local font wiring, theme bootstrap)
  - `components/app/landing/STYLEGUIDE.md` ⭐ — the single source of truth
    for the marketing site
  - `components/app/landing/landing-theme.ts` (typography, radii, shadows,
    surfaces, gradients, chips, text-link tokens)
  - `content/positioning.ts` (hero copy)
  - `app/(marketing)/landing-sections.tsx` (page composition)
- **Logos in use:** Betaform + 8 client/partner logos (Advanced, Advantic,
  FMK Compare, Magrathea, PPI Media, PPI N3xt, Schwäbisch Media, Skill-Match)
- **Webfonts:** Söhne Buch (400) + Söhne Halbfett (600) — licensed; bundled
  here for prototyping use only.
- **Live site:** https://betaform.io

## Company / product context

**betaform.** is a small German product-design studio (de_DE locale, Hamburg
area) that designs **B2B SaaS products, UI systems, websites and MVPs** for
teams trying to make complex digital products clearer and more effective.
Two-person core team (Carina Gassner & Ole Beekmann); working language is
German. Hero claim: _„Form entsteht aus Funktion.“_ Sub-claim: _„Wir designen
B2B-SaaS-Produkte, die Komplexität in klare Flows und skalierbare UI-Systeme
übersetzen.“_

There is **one product surface** — the marketing site `betaform.io` — with
several sub-areas:

- **Landing** (`/`): hero → process → method → cases → testimonials → blog → CTA
- **Cases** (`/cases`, `/cases/[slug]`): filterable case grid + dark
  case-detail layout (deep navy surfaces over the same aurora chrome)
- **Förderung** (`/foerderung`): funding-check landing with embedded form
- **Content System** (`/content-system`): productized content offering
- **Geo landing pages** (`/geo/[region]`): regional SEO targets
- **Blog** (`/blog`, `/blog/themen/[topic]`)
- **Legal** (`/datenschutz`, `/impressum`)

The studio's services break into four pillars (used as a semantic color
system on cards, see `services-card-colors-0..3`):

| Index | Pillar |
|---|---|
| 0 | Produkt- & UX-Strategie |
| 1 | UX Research & Prototyping |
| 2 | UI Design & Designsysteme |
| 3 | Brand & Corporate Design |

There is also a small **studio app** (`/(app)/app`) — an internal Workbench /
Dashboard used to edit testimonials, cases etc. It is **not** a public
product; the marketing-side `ms-*` component layer is the part to copy.

---

## Visual foundations

### Color
- **Foundation is warm off-white**, not cool gray. `--background = 34 32% 98%`
  (a beige/cream cast), with near-black ink (`0 0% 10%`). Avoid pure white
  surfaces — always lean warm.
- **Accent** is a warm orange `28 88% 65%` (used sparingly).
- **The signature is the aurora** — a slow-drifting multi-stop radial+linear
  gradient mixing five soft pastels: dusty rose `#f5cec6`, peach `#ecd5ce`,
  slate-blue `#c8d5e4`, lavender `#e8e4f6` / `#dcd4f0`, sage `#d2e0d8`,
  blush `#eedde0`. It animates over **40 seconds** on a 500% background-size
  with a gentle ease-in-out (`cubic-bezier(0.45,0,0.55,1)`). Hero, case heroes
  and footer panels all share this gradient (`landingGradients.system`).
- **Service-card gradients** are 4+ pre-mixed pastel blends, indexed by the
  service pillar. Each card has its own subtle 12s drift (`services-card-aurora`).
- **Case-study dark surfaces** use `#071823` and `#0c1520` — deep navy, not
  black — and host white text + glass overlays.
- Dark mode exists and is rigorously remapped (see `globals.css`'s legacy
  remap layer for slate/white utilities → dark equivalents).

### Type
- **Söhne** (Klim Type Foundry) — `--font-sans`. Two weights: 400 Buch and
  600 Halbfett. **Tailwind's font-weight scale is collapsed** so that
  thin/light/normal/medium all resolve to 400 and semibold/bold/extrabold/black
  all resolve to 600 — this is intentional: the system has only two weights.
- Body uses `font-feature-settings: 'ss04', 'ss06'` for stylistic alternates.
- Headlines are **regular weight (400)** with **negative tracking** (`-0.02em`
  for hero, `-0.018em` for sections). Avoid bold display type.
- Hero scale is `clamp(3rem, 6vw, 5.2rem)` desktop / `42px` mobile, leading
  1.04. Section heading: `clamp(1.9rem, 2.2rem+2.9vw, 3.9rem)`.
- Eyebrows are pill-shaped with `0.34em` letterspacing — very airy.

### Spacing & rhythm
- Section vertical rhythm token: `--space-section-y` (clamp ~4–8rem). Use
  `SectionScaffold` in code; replicate via the same clamp in mocks.
- Gutter token: `--space-container-gutter`. Container max-width: 1440px (the
  `2xl` Tailwind breakpoint is overridden to 1440 here).
- Stack gap: `--space-stack-gap` (clamp ~2–4rem).
- Mobile is taken seriously — most components have explicit phone variants.

### Backgrounds & surfaces
- **No flat-color hero backdrops.** It's the aurora gradient or nothing.
- **Glass is the default panel.** `hero-glass-surface` = backdrop-blur 32px
  + saturate 1.6 + ~22% white + ~60% white border. On phones the blur
  drops to 18px (LCP).
- Soft noise overlay on the aurora (`.aurora-surface::after`) — a tiny SVG
  fractal-noise tile at 8% opacity, soft-light blend. This is a hallmark
  texture; reproduce it on any large gradient surface.
- Card surfaces have **four named flavors**: `frosted`, `frostedSoft`,
  `luminous`, `dark` (navy), `softCard`, `panelFrosted`, `chip`.
- **Big radii.** Cards 24–36px (`--radius-lg/xl/2xl/3xl`). Hero cards = 32px.
  A safety net in CSS clamps `rounded-[48/56px]` back down to 32px.

### Shadows & elevation
- **Soft, deep, low-contrast shadows.** Always negative spread, always far
  drop. Examples:
  - `floating`: `0 22px 60px -30px rgba(15,23,42,0.18)`
  - `deep`:     `0 28px 90px -42px rgba(15,23,42,0.28)`
  - `experience`: `0 26px 86px -36px rgba(15,23,42,0.22)`
  - `darkElevation`: 0.45 alpha for dark cards over light bg.
- No inset shadows on cards. No hard 1px shadows.

### Borders
- 1px is default. 1.5px on hero wireframe state and CTA borders.
- Border colors are mostly `var(--color-border-strong)` (12% black) on light
  surfaces, `white/0.18..0.22` on dark.
- Dashed borders only for the brief "wireframe" hero pre-state.

### Animation
- Easing: `cubic-bezier(0.45, 0, 0.55, 1)` for the aurora float, `ease-out`
  200ms for buttons. **No bounces.** No pop/spring.
- Scroll-driven effects via GSAP, but **always** gated by
  `prefers-reduced-motion`.
- **Cards do not lift on hover** — only a subtle background-color shift.
  **Buttons** do (`hover:-translate-y-px`, `active:translate-y-0`).
- Hero has a wireframe → final crossfade on first paint (see `hero-wireframe-*`).

### Press / focus
- Focus: visible ring via `focus-visible`, ring color = `--ring`, with
  ring-offset matched to background.
- Buttons: `solid` hovers to `opacity-80`; `outline` hovers to a slightly
  warmer fill. `HERO_TEXT_CTA_LINK` morphs from transparent to solid white
  on hover (and inverts in dark mode).

### Imagery
- Real photography of the founders (see `betaform-carina-gassner.png`,
  `betaform-ole-beekmann.png` — _not bundled, see Caveats_).
- Time-of-day + weather illustration sets used as adaptive ambient backdrops
  (morning/daytime/evening/night × clear/cloudy/rain/snow).
- Process / case imagery is **warm-toned** (no cool fluorescents), large
  format, often full-bleed inside cards.

### Layout rules
- Fixed elements: floating "Schreib uns" CTA bottom-right (square 48×48
  expanding to 148×48 on hover with MessageCircle icon + label).
- Header logo: 20px tall (`h-5`), footer logo: 56px tall (`h-[56px]`).
- One `<h1>` per page (Hero), every section uses `<h2>` via `MsSectionHeader`.
- Carousels declare `aria-roledescription="carousel"`.

### Transparency / blur
- Hero glass: 32px blur + 22% white. Phone: 18px + lighter saturate.
- Frosted cards: 24px blur + 92% white. Soft cards: nearly opaque (`92%`).
- Inverted chips on dark: `bg-white/10` with `border-white/20`.

---

## Content fundamentals

**Language.** German (de_DE), formal but conversational. The site uses the
informal _du_ form (`„Schreib uns"`, `„Projekt anfragen"`, `„Was machst du
als erstes?"`). README files in the codebase mix English headings with
German body — that's a dev convention, not a content one.

**Tone.**
- Confident, low-jargon, no marketing froth. Plain claims, not slogans.
- Clear value-first sentences. "Wir designen B2B-SaaS-Produkte, die
  Komplexität in klare Flows und skalierbare UI-Systeme übersetzen."
- "We" voice for the studio (`Wir`), "you/your" voice for the reader (`du`,
  `dein Vorhaben`). Never "Sie".

**Casing.**
- Headlines are **sentence-cased** with intentional line breaks (`\n` in the
  source — see `heroTitle = 'Form entsteht\naus Funktion.'`). Periods at
  the end of sentence-headings.
- Eyebrows are **UPPERCASE** with very wide letterspacing (`0.34em`).
- Buttons are sentence-cased ("Schreib uns", "Projekt anfragen", "Cases ansehen").

**Punctuation.**
- German typography conventions: `„…"` quotes (curly), em-dashes `—`,
  ellipsis `…`. No straight quotes in copy.
- Headlines often use ", " (comma-comma) cadence: _„Produktdesign,
  Strategie, UI-Systeme | betaform."_

**No emoji.** None in marketing copy. Icons are SVGs (see ICONOGRAPHY).

**Numbers.** German number formatting (`1.000`, `2,5x`, `€`-suffix or before
amount). Years as 4-digit. Stat tiles use big numbers + tiny uppercase label
underneath.

**Examples (verbatim from the codebase).**
- Hero title: _„Form entsteht aus Funktion."_
- Hero subtitle: _„Wir designen B2B-SaaS-Produkte, die Komplexität in klare
  Flows und skalierbare UI-Systeme übersetzen."_
- CTA intro: _„Ob Relaunch, MVP oder internes Tool: Wir besprechen kurz dein
  Vorhaben, ordnen den Aufwand ein und sagen dir offen, womit du sinnvoll
  starten kannst."_
- Floating CTA label: _„Schreib uns"_
- Site title: _„Produktdesign, Strategie, UI-Systeme | betaform."_

---

## Iconography

- **Custom service icons** ship as SVGs in `assets/icons/` — a tiny set of
  4 line icons, ~1px stroke, monochrome black, intended at 24–32px:
  - `corporate-design.svg`
  - `produktstrategie.svg`
  - `prototyping.svg`
  - `ux-ui-design.svg`
  Plus `m-black.png` (a dotted "m" mark, used as a small wordmark
  accent).
- **`lucide-react` is the workhorse icon set** for UI iconography (chevrons,
  X, Send, MessageCircle, ArrowRight, Plus, Play, etc). Stroke 1.5–2,
  outline-only, no filled glyphs. Use Lucide via the CDN if recreating outside
  the codebase.
- **No icon font.** No emoji. No unicode glyphs as icons.
- **No decorative SVG illustration** — the brand leans on photography +
  gradient + glass; do not invent line-drawn illustrations.
- **Logos.** All client logos in `assets/logos/` are mono SVGs intended to be
  rendered at 20–32px tall in a horizontal carousel. The CSS class
  `themed-logo-brand` / `themed-logo-partner` inverts them in dark mode via a
  `filter: brightness(0) saturate(100%) invert(96%)` — recreate that if
  using on dark backgrounds.

---

## Index — what's in this folder

```
README.md                  ← you are here
SKILL.md                   ← agent-skill manifest (Claude Code compatible)
colors_and_type.css        ← drop-in CSS variables + base type + utilities
fonts/
  soehne-buch.woff2        ← Söhne 400
  soehne-halbfett.woff2    ← Söhne 600
assets/
  logos/                   ← betaform.svg + 8 client logos (mono SVG)
  icons/                   ← 4 service SVGs + m-black.png mark
  favicon.svg, favicon-32x32.png, app-icon.svg
preview/                   ← Design System tab cards (one HTML each)
ui_kits/
  marketing-site/          ← landing-page UI kit (hero, services,
                             testimonials, footer-CTA, header)
```

> Tip: when building a new betaform artifact, copy `colors_and_type.css` and
> the `assets/` you need into the new file's directory and reference them
> with relative paths. Do _not_ hot-link to this folder.

---

## Caveats

- **Söhne is a licensed font.** It's bundled here only because it lives in
  the repo. **Do not redistribute** these woff2 files outside of betaform's
  own use. For any public-facing third-party deliverable, swap to a free
  similar (Inter, GT America, or Söhne if a license is in place).
- **Founder photography and case imagery were not imported** to keep the
  asset folder small (each is 1–2 MB). Pull from the repo (`public/images/`)
  if needed for a specific deliverable.
- **The studio app** (`/(app)/app`) was not modeled — only the marketing
  surface. If you need to mock the Workbench, ask for a separate pass.
