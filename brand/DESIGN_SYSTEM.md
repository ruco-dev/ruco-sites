# RUCO Design System

> **Version:** 1.0 · **Status:** draft · **Applies to:** all `*.ruco.dev` sites and `style.css`
> **Source of truth:** this file. `style.css` and `ruco-starter.html` are generated from the tokens below.

A restrained **5-colour system**: one signal yellow, a working blue, white, and two greys.
The guiding rule — *yellow marks what matters, blue is reserved for anything clickable, grey and white carry everything else.*

---

## 1. Colour tokens

### Core five

| Token | Name | Hex | RGB | Role |
|---|---|---|---|---|
| `--ruco-yellow` | Ruco Yellow | `#E8B923` | `232 185 35` | Primary · signal accent (one per view) |
| `--ruco-blue` | Ruco Blue | `#2F80ED` | `47 128 237` | Interactive · links & clickable actions |
| `--white` | Signal White | `#FFFFFF` | `255 255 255` | Base · canvas, surfaces |
| `--mist` | Mist Grey | `#9AA1AC` | `154 161 172` | Muted · secondary text, borders |
| `--graphite` | Graphite | `#1E2228` | `30 34 40` | Ink · headlines, dark surfaces |

### Tints & shades (working ramps)

**Yellow** — `50 #FBF4D6` · `100 #F4E08C` · `200 #EECB4E` · **`400 #E8B923` (core)** · `500 #C99D12` (hover) · `600 #9C7A0C` · `700 #6B5407`

**Blue** — `50 #EAF1FE` · `100 #C2D9FB` · `200 #86B2F6` · **`400 #2F80ED` (core)** · `500 #1C63C9` (hover) · `600 #15499A` · `700 #0E3068`

**Neutral** — `0 #FFFFFF` · `50 #F2F3F5` · `100 #E2E4E8` · **`300 #9AA1AC` (mist)** · `500 #6A7280` · `700 #3A4049` · **`900 #1E2228` (graphite)**

### Semantic aliases — *use these in components, never raw hex*

| Alias | Maps to | Use for |
|---|---|---|
| `--color-bg` | `--grey-50` | Page background |
| `--color-surface` | `--white` | Cards, panels |
| `--color-border` | `--grey-100` | Dividers, input borders |
| `--color-text` | `--graphite` | Body & headings |
| `--color-text-muted` | `--grey-500` | Secondary text |
| `--color-text-subtle` | `--mist` | Captions, placeholders |
| `--color-link` | `--ruco-blue` | Links |
| `--color-link-hover` | `--blue-500` | Link hover |
| `--color-accent` | `--ruco-yellow` | The one CTA / signal |
| `--color-accent-hover` | `#F4D24E` | CTA hover |
| `--color-on-accent` | `--graphite` | Text **on** yellow (never white) |
| `--color-ink` | `--graphite` | Dark hero / footer surface |
| `--color-on-ink` | `--white` | Text on dark surface |

---

## 2. Usage rules — the 60 / 30 / 10 split

| Weight | Colours | Where |
|---|---|---|
| **~60%** | White + Mist | Canvas, cards, body text, borders — the quiet majority |
| **~30%** | Graphite | Headlines, footer, code blocks, dark hero sections |
| **~10%** | Blue (clickable) + Yellow (signal) | Links and **one** accent action per view |

**Do**
- Use yellow for exactly one primary action per screen (the thing to notice).
- Use blue **only** for links and inline actions.
- Keep large surfaces neutral; let the accent earn attention by being rare.

**Don't**
- ❌ Put white text on yellow — it fails contrast. Use Graphite (`--color-on-accent`).
- ❌ Use blue as decoration (backgrounds, borders) — it reads as "clickable".
- ❌ Stack two accents competing in the same region.
- ❌ Hard-code hex values in components — reference the semantic aliases.

---

## 3. Accessibility / contrast

| Pair | Ratio | Verdict |
|---|---|---|
| Graphite `#1E2228` on White | ~15.8:1 | ✅ AAA |
| Graphite on Yellow `#E8B923` | ~9.5:1 | ✅ AAA — **the only safe text colour on yellow** |
| Blue `#2F80ED` on White | ~3.9:1 | ✅ AA for links / large text |
| Mist `#9AA1AC` on White | ~2.3:1 | ⚠️ Decorative / large only — not body text |
| White on Graphite | ~15.8:1 | ✅ AAA |

Rule of thumb: **body text is always Graphite on light or White on Graphite.** Mist is for borders and captions, not paragraphs.

---

## 4. Typography

| Token | Value |
|---|---|
| `--font-sans` | `'Segoe UI', system-ui, -apple-system, Arial, sans-serif` |
| `--font-mono` | `ui-monospace, 'SF Mono', Menlo, monospace` |

| Element | Size | Weight | Tracking |
|---|---|---|---|
| `h1` | `clamp(2rem, 4vw, 2.75rem)` | 800 | `-0.02em` |
| `h2` | `1.5rem` | 800 | `-0.02em` |
| `h3` | `1.25rem` | 800 | `-0.02em` |
| body | `1rem` / line-height `1.6` | 400 | normal |
| `.eyebrow` | `0.75rem` | 700 | `0.14em`, uppercase, blue |

---

## 5. Spacing, radius & elevation

| Token | Value | Use |
|---|---|---|
| `--radius-sm` | `8px` | Buttons, inputs |
| `--radius-md` | `12px` | Code blocks, small panels |
| `--radius-lg` | `16px` | Cards |
| `--shadow-card` | `0 1px 3px rgba(16,24,40,.08)` | Resting cards |
| `--shadow-lift` | `0 10px 28px rgba(16,24,40,.16)` | Hover / focus lift |

---

## 6. Components

### Button
- **Primary** (`.btn .btn-primary`) — `--color-accent` bg, `--color-on-accent` text. One per view.
- **Secondary** (`.btn .btn-secondary`) — `--ruco-blue` bg, white text. Navigational.
- **Ghost** (`.btn .btn-ghost`) — transparent, `--color-border`, neutral text.
- Padding `.875rem 1.625rem`, radius `--radius-sm`, weight 700.

### Card
`.card` — `--color-surface` bg, `1px solid --color-border`, radius `--radius-lg`, `--shadow-card`, padding `1.75rem`.

### Dark surface
`.surface-ink` — `--color-ink` bg, `--color-on-ink` text; headings stay white, paragraphs drop to Mist. Use for hero & footer.

### Link
`a` — `--color-link`, no underline at rest, underline + `--color-link-hover` on hover, 2px blue focus ring.

### Form
- `.label` — uppercase `0.75rem`, weight 600, `--grey-500`.
- `.input` — white bg, `1.5px solid --color-border`, focus border `--ruco-blue`, placeholder `--mist`.

---

## 7. Machine-readable tokens

> Bots and build tools should parse this block as the canonical token source.

```json
{
  "$schema": "ruco-tokens@1",
  "color": {
    "core": {
      "yellow":   { "hex": "#E8B923", "rgb": [232, 185, 35],  "role": "primary-signal" },
      "blue":     { "hex": "#2F80ED", "rgb": [47, 128, 237],  "role": "interactive-link" },
      "white":    { "hex": "#FFFFFF", "rgb": [255, 255, 255], "role": "base-canvas" },
      "mist":     { "hex": "#9AA1AC", "rgb": [154, 161, 172], "role": "muted-secondary" },
      "graphite": { "hex": "#1E2228", "rgb": [30, 34, 40],    "role": "ink-dark-surface" }
    },
    "ramp": {
      "yellow":  { "50": "#FBF4D6", "100": "#F4E08C", "200": "#EECB4E", "400": "#E8B923", "500": "#C99D12", "600": "#9C7A0C", "700": "#6B5407" },
      "blue":    { "50": "#EAF1FE", "100": "#C2D9FB", "200": "#86B2F6", "400": "#2F80ED", "500": "#1C63C9", "600": "#15499A", "700": "#0E3068" },
      "neutral": { "0": "#FFFFFF", "50": "#F2F3F5", "100": "#E2E4E8", "300": "#9AA1AC", "500": "#6A7280", "700": "#3A4049", "900": "#1E2228" }
    },
    "semantic": {
      "bg": "neutral.50",
      "surface": "white",
      "border": "neutral.100",
      "text": "graphite",
      "text-muted": "neutral.500",
      "text-subtle": "mist",
      "link": "blue",
      "link-hover": "blue.500",
      "accent": "yellow",
      "accent-hover": "#F4D24E",
      "on-accent": "graphite",
      "ink": "graphite",
      "on-ink": "white"
    }
  },
  "font": {
    "sans": "'Segoe UI', system-ui, -apple-system, Arial, sans-serif",
    "mono": "ui-monospace, 'SF Mono', Menlo, monospace"
  },
  "radius": { "sm": "8px", "md": "12px", "lg": "16px" },
  "shadow": {
    "card": "0 1px 3px rgba(16,24,40,.08)",
    "lift": "0 10px 28px rgba(16,24,40,.16)"
  },
  "rules": {
    "accent_per_view": 1,
    "blue_usage": "links-and-inline-actions-only",
    "text_on_yellow": "#1E2228",
    "body_text_min_contrast": "AA",
    "ratio_60_30_10": ["neutral", "graphite", "accent+link"]
  }
}
```

---

## 8. Files in this system

| File | Purpose |
|---|---|
| `DESIGN_SYSTEM.md` | This document — canonical source for humans & bots |
| `style.css` | Drop-in stylesheet (`:root` tokens + base + components) |
| `ruco-starter.html` | Self-contained boilerplate with the CSS embedded + live demo |
| `Ruco Brand Palette.dc.html` | Visual palette reference (click-to-copy swatches) |

---

*Change the palette here first, then regenerate `style.css`. Components reference semantic aliases so a colour change propagates from a single edit.*
