# AGENT.md — Holograph Design System Implementation Brief
**For: Petunia (OpenClaw agent)**
**Repo: mybotpetunia-maker/petunia-design-system**

This document is your primary implementation reference. Read it before writing any HTML, CSS, or UI code. Every rule here is load-bearing.

---

## 1. Setup

Add to every page `<head>`:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,wght@0,400;0,600;1,400;1,600&family=IBM+Plex+Mono:wght@300;400;500&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

Import tokens.css or inline it in your `<style>` block.

---

## 2. Non-Negotiable Rules

### Typography
- **Bodoni Moda is DISPLAY ONLY.** Minimum 48px. Use for: hero headings, section numbers as visual objects, dramatic short phrases. NEVER for body text, captions, labels, or more than one sentence.
- **IBM Plex Sans** — body copy, UI prose, descriptions, paragraphs.
- **IBM Plex Mono** — labels, annotations, code, data, logs, timestamps, metadata.
- Never use any other typeface.

### Color
- Never hardcode hex values. Always use `var(--token-name)`.
- **Teal (`--brand-teal`) = interactive only.** Links, active states, primary CTAs. Not decoration.
- **Amber (`--status-amber`) = caution/handoff only.** Not decoration.
- **The iris gradient is never static.** Must have `animation: iris-flow 5s linear infinite`.
- Canvas is always `var(--bg-base)` (#080C10). Never pure black (#000) or white (#fff).

### The Mark (Petunia logo)
Use this exact SVG path. Never redraw, simplify, or approximate it. **Never rotate.**

```
Viewbox: 90×90
Path: M45,5 C53,5 63,11 67,19 C69,25 68,33 74,38 C80,43 82,49 79,54 C76,59 69,60 66,67 C63,73 63,80 57,83 C53,86 48,85 45,85 C42,85 37,86 33,83 C27,80 27,73 24,67 C21,60 14,59 11,54 C8,49 10,43 16,38 C22,33 21,25 23,19 C27,11 37,5 45,5 Z
Throat: <circle cx="45" cy="45" r="9" fill="var(--bg-base)"/>
Iris:   <circle cx="45" cy="45" r="4.5" fill="url(#iris-gradient)"/>
Fill:   always the iris gradient, always animated
```

States:
- **Idle**: petals static, dashed iris ring drifts slowly
- **Active/processing**: petals breathe (`petal-wind`), mark sways (`petal-sway` ±1.5°)
- **Done**: petals settle and dim to ~40% opacity

### Motion
- UI feedback: max 300ms. Content reveals: max 600ms.
- Emergence easing: `cubic-bezier(0.16, 1, 0.3, 1)`
- Settle easing: `cubic-bezier(0.34, 1.56, 0.64, 1)`
- Animation must be semantic — it communicates state, never decoration.

### Layout
- All spacing from `var(--space-*)` tokens.
- All border radius from `var(--radius-*)` tokens.
- All borders use `var(--border-*)` tokens. Most common: `1px solid var(--border-subtle)`.

---

## 3. Component Patterns

### Button — Primary
```html
<button style="background:var(--brand-teal);color:var(--bg-base);font-family:var(--font-mono);font-size:var(--text-sm);letter-spacing:var(--tracking-wider);text-transform:uppercase;padding:var(--space-3) var(--space-6);border:none;border-radius:var(--radius-md);cursor:pointer;">Action</button>
```

### Button — Ghost
```html
<button style="background:transparent;color:var(--brand-teal);font-family:var(--font-mono);font-size:var(--text-sm);letter-spacing:var(--tracking-wider);text-transform:uppercase;padding:var(--space-3) var(--space-6);border:1px solid var(--border-teal);border-radius:var(--radius-md);cursor:pointer;">Action</button>
```

### Card
```html
<div style="background:var(--bg-raised);border:1px solid var(--border-subtle);border-radius:var(--radius-lg);padding:var(--space-8);">...</div>
```

### Status Badge
```html
<span style="color:var(--brand-teal);font-family:var(--font-mono);font-size:var(--text-xs);letter-spacing:var(--tracking-wider);text-transform:uppercase;">● Active</span>
<span style="color:var(--status-amber);font-family:var(--font-mono);font-size:var(--text-xs);letter-spacing:var(--tracking-wider);text-transform:uppercase;">⚠ Caution</span>
<span style="color:var(--status-error);font-family:var(--font-mono);font-size:var(--text-xs);letter-spacing:var(--tracking-wider);text-transform:uppercase;">✕ Error</span>
```

### Data Label (mono annotation)
```html
<div style="font-family:var(--font-mono);font-size:var(--text-xs);letter-spacing:var(--tracking-wider);text-transform:uppercase;color:var(--text-tertiary);">Label</div>
<div style="font-family:var(--font-mono);font-size:var(--text-base);color:var(--text-primary);">Value</div>
```

---

## 4. What Not to Do

- Do not use Bodoni for body text or anything read as prose.
- Do not use the iris gradient as a static background.
- Do not rotate the mark.
- Do not use warm colors decoratively — amber is caution only.
- Do not use white (#fff) or black (#000) — use bg/text tokens.
- Do not add text drop shadows — use color contrast instead.
- Do not center-align body copy — left align only.
- Do not animate for decoration — motion communicates state only.

---

## 5. Voice & Tone

When writing any copy or UI text for Petunia:
- First person. She files this about herself.
- Dry. Concise. No exclamation points.
- IBM Plex Mono for system/data text. IBM Plex Sans for prose.
- State facts. Don't explain feelings.

---

## 6. Quick Reference

```
BACKGROUNDS  --bg-base #080C10 / --bg-raised #0D1318 / --bg-surface #111920 / --bg-elevated #16212B
TEXT         --text-primary #E2EBF0 / --text-secondary #B4C8D6 / --text-tertiary #7A97AE
BRAND        --brand-teal #5ECDD8 (interactive) / --brand-violet #A991E2 (secondary)
STATUS       --status-amber #F0A040 (warn) / --status-green #5DB872 (ok) / --status-error #E05040
FONTS        Bodoni Moda (48px+ display only) / IBM Plex Sans (body) / IBM Plex Mono (data/labels)
RADII        3px / 6px / 10px / 16px
MOTION       300ms UI max / 600ms reveal max / ease: cubic-bezier(0.16,1,0.3,1)
```