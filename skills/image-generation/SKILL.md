---
key: "betaform/image-generation"
---

# Skill: Bild-Prompt für betaform Social-Media-Posts

Wird vom CDO aufgerufen vor jedem `generate-post-image` Plugin-Call.
**Primärquelle Farben/Tokens:** Skill `betaform/betaform-design` (README.md, colors_and_type.css)
**Tonalität/Kanallogik:** Skill `betaform/betaform-voice`

---

## Grundprinzip

Ein Bild ist kein Dekor — es verlängert die Kernaussage des Posts visuell.
Vor dem Prompt-Bauen: Post-Text lesen und die **eine zentrale Idee** identifizieren.
Dann den passenden Bildtyp wählen. Nie das Input→Pfeil→Output Schema erzwingen wenn ein anderes Konzept besser passt.

---

## Schritt 1 — Kanal bestimmen

| Kanal | Titel-Marker |
|---|---|
| `linkedin_personal` | `[LinkedIn Personal]` |
| `linkedin_company` | `[LinkedIn Company]` |
| `instagram` | `[Instagram]` |

---

## Schritt 2 — Bildtyp aus Post-Thema ableiten

Post-Text lesen → Kernidee → Bildtyp:

| Post-Thema | Bildtyp | Beschreibung |
|---|---|---|
| Prozess / Workflow | **Flow-Infografik** | 3–4 Schritte horizontal mit Pfeilen und Labels |
| Vorher/Nachher | **Vergleichskarte** | Zwei Karten nebeneinander, links grau/unstrukturiert, rechts clean/betaform |
| KI / Automation | **Input→Output** | Klassisches Schema: leeres Feld → Pfeil → UI-Ergebnis |
| Design System / Tokens | **Token-Grid** | Farbpalette als Chips, Typografie-Sample, Spacing-Leiter |
| Zahlen / Stats / Ergebnis | **Stat-Karte** | Große Zahl zentriert, kurze Label, betaform Orange Akzent |
| Case Study | **UI-Mockup** | Screenshot-Stil einer konkreten Interface-Komponente |
| Positionierung / Meinung | **Statement-Karte** | Große Typografie, Aurora-Hintergrund, ein Satz |
| GovTech / Komplexität | **Architektur-Diagram** | Vereinfachtes System-Diagramm mit Kästen und Verbindungen |
| Studio-Alltag | **Behind-the-scenes** | Warm, authentisch, Studio-Ästhetik (nur Instagram) |
| Allgemein / kein klarer Fit | **Input→Output** | Fallback |

---

## Schritt 3 — Vollständigen Prompt zusammenbauen

### Farb-Basis (für alle Typen)

```
betaform brand palette:
- Background: warm cream #FAF9F6
- Aurora gradient (subtle, for large backgrounds): dusty rose #f5cec6, peach #ecd5ce, slate-blue #c8d5e4, lavender #e8e4f6, sage #d2e0d8
- Accent: betaform orange #F5943A (sparingly, for active/highlighted elements)
- Cards/surfaces: white #FFFFFF, border-radius 24–32px, soft low-contrast shadow (0 22px 60px -30px rgba(15,23,42,0.18))
- Typography: clean sans-serif, regular weight 400, negative tracking -0.02em
- Dark case surfaces: deep navy #071823, white text
- No glow, no neon, no electric blue, no stock photo elements
```

---

### LinkedIn Personal — Prompt-Templates nach Typ

#### Flow-Infografik
```
Flat vector infographic on warm cream #FAF9F6 background.
Three horizontal steps connected by arrows, each step is a white frosted card (border-radius 28px, subtle shadow):
Step 1: [Label aus Post, max 2 Wörter]
Step 2: [Label aus Post, max 2 Wörter]
Step 3: [Label aus Post, max 2 Wörter]
Arrows between steps in lilac-to-salmon gradient #C4A8F8 → #F7C8C0.
Active/final step card highlighted with betaform orange #F5943A left border.
Clean sans-serif labels, sentence case, no icons, no humans.
Quality: high.
```

#### Vergleichskarte
```
Flat vector split comparison on warm cream #FAF9F6.
Two cards side by side:
Left card (gray #E8E7E2, border-radius 24px): titled "Vorher" — shows messy/unstructured state with scattered small elements, muted colors
Right card (white #FFFFFF, border-radius 28px, subtle shadow): titled "Nachher" — shows clean structured state, betaform orange #F5943A accent, organized layout
Small gradient arrow center pointing right: lilac #C4A8F8 to salmon #F7C8C0.
Sans-serif labels only, max 3 words each. Quality: high.
```

#### Token-Grid (Design System)
```
Flat vector design system overview on warm cream #FAF9F6.
Grid layout with three sections:
1. Color chips row: 5–6 circles in betaform palette (cream, salmon, lavender, slate-blue, orange #F5943A, navy #071823)
2. Typography sample: one large headline "Aa" in regular weight with negative tracking, one body text sample
3. Spacing ruler: 4–5 horizontal bars of increasing width labeled xs/sm/md/lg/xl
White frosted container card (border-radius 28px, subtle shadow) wrapping the grid.
Clean, minimal, professional. Quality: high.
```

#### Stat-Karte
```
Flat vector stat card. Background: warm cream #FAF9F6.
Centered white card (border-radius 32px, soft shadow):
Large number "[Zahl aus Post]" in display size, betaform orange #F5943A
Short label below in gray, small caps
Optional: thin horizontal bar chart or sparkline at bottom in muted lavender
No humans, no icons. Clean, confident. Quality: high.
```

#### Statement-Karte
```
Flat vector statement card. Background: subtle aurora gradient (dusty rose #f5cec6 to lavender #e8e4f6, diagonal, very soft).
White frosted glass card center (border-radius 32px, backdrop-blur effect suggested via white #FFFFFF at 85% opacity, soft border):
Main statement in large sans-serif, regular weight 400: "[Kernaussage des Posts, max 8 Wörter, sentence case]"
Small betaform orange #F5943A dot or line accent.
Minimal, typographic-driven. No icons, no humans. Quality: high.
```

#### UI-Mockup (Case Study)
```
Flat vector UI mockup on white background.
One browser/app window frame (border-radius 12px, subtle border #E8E7E2):
Inside: simplified B2B interface relevant to the post topic — [konkrete Beschreibung aus Post: z.B. "dashboard with 3 metric cards", "form with 4 fields", "navigation with 5 items"]
betaform orange #F5943A for primary action button or active state.
Clean typography, max 3 words per label, readable at small size.
Deep navy #071823 header bar optional. Quality: high.
```

#### Architektur-Diagram
```
Flat vector system diagram on warm cream #FAF9F6.
Simple boxes-and-arrows architecture:
[Beschreibung der Systemkomponenten aus Post, z.B. "3 connected modules: Input, Process, Output"]
White rounded rectangles (border-radius 12px) for components, thin connecting arrows in slate-blue #c8d5e4.
Key component highlighted with betaform orange #F5943A border.
Short labels only (max 3 words each). No icons, no gradients on arrows. Quality: high.
```

---

### LinkedIn Company — Prompt-Templates

#### Case Study / Portfolio
```
Clean portfolio-quality UI mockup on white or warm cream #FAF9F6.
Professional B2B interface: [konkrete Beschreibung des Deliverables aus Post]
betaform aesthetic: generous whitespace, border-radius 24–28px on cards, soft shadows, orange #F5943A accent for CTA or active element.
Readable labels (max 3 words). No humans, no stock photo elements.
Optional: subtle aurora gradient (dusty rose to lavender) as section background.
Quality: high.
```

#### Methodik / Process
```
Flat vector process diagram on warm cream #FAF9F6.
[3–4 Schritte aus Post als beschriftete Rechtecke mit Pfeilen]
betaform card style: white surfaces, border-radius 24px, soft shadow.
betaform orange #F5943A for key step or final result.
Minimal labels, sentence case, max 3 words each. Quality: high.
```

#### Statement / Positionierung
```
Typographic statement card. Background: aurora gradient (peach #ecd5ce to lavender #e8e4f6).
Frosted white glass card center (border-radius 32px):
"[Kernaussage, max 10 Wörter]" in large clean sans-serif, regular weight.
"betaform." wordmark small bottom right in orange #F5943A.
Minimal, confident, brand-forward. Quality: high.
```

---

### Instagram — Prompt-Templates

#### Behind-the-scenes / Studio
```
Authentic warm studio photography aesthetic (rendered illustration style).
Hamburg studio context: a design workspace, screens with UI work visible, natural warm afternoon light through window.
Soft warm tones, no artificial lighting, no staged setup.
Genuine and human — could be Ole or Carina at work.
Warm cream and wood tones. No text overlays. Quality: high.
```

#### Process / Sketchbook
```
Warm flat illustration of a design process moment:
[konkrete Szene aus Post, z.B. "sketchbook with wireframes", "sticky notes on a wall", "component library on screen"]
Warm natural tones (cream, sand, terracotta). Soft shadows.
Authentic, minimal, not over-designed. Quality: high.
```

---

## Schritt 4 — Prompt personalisieren

Nach dem Basis-Template: **zwei konkrete Angaben aus dem Post-Text einsetzen:**
1. Labels/Beschriftungen direkt aus Post-Inhalt ableiten (nicht generisch "Input/Output")
2. Falls eine Zahl, ein Produkt oder ein konkreter Case im Post erwähnt wird → einbauen

Beispiel: Post über "3 Sprints für MVP" → Stat-Karte mit "3" als große Zahl, Label "Sprints bis MVP"

---

## Schritt 5 — Plugin-Call

```
POST /api/companies/{companyId}/plugins/betaform.paperclaw-dashboard/actions/generate-post-image
{
  "issueId": "{issueId}",
  "companyId": "{companyId}",
  "imagePrompt": "{vollständiger Prompt aus Schritt 3+4}"
}
```

Bild wird fire-and-forget generiert (~60–90s). Nach 2 Minuten Ergebnis prüfen.

---

## CDO-Review: 5-Punkte-Checkliste

| # | Kriterium |
|---|---|
| 1 | Bildtyp passt zur Kernaussage des Posts |
| 2 | betaform Farbpalette erkennbar (Cream, Orange, Pastell) |
| 3 | Kein Stock-Foto-Element (kein Mensch außer Instagram, kein Laptop-Foto) |
| 4 | Text lesbar, max. 3 Wörter pro Label, kein Tippfehler |
| 5 | Kein Glow / Neon / electric blue |

Alle 5 Ja → "Bild freigegeben", Status → `in_review`, Assignee → Ole
Mind. 1 Nein → Prompt neu mit negativer Instruktion für das fehlende Kriterium
Nach 2 Fehlversuchen → Eskalation an Ole mit konkreter Begründung
