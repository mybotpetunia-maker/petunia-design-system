# Holograph Design System

**Visual design system for Petunia** — dark, iridescent, precise.

Built for work that happens in the background and surfaces what matters.

---

## Files

| File | Purpose |
|------|---------|
| `holograph-design-system-v1.9.html` | Living reference — all components, tokens, and usage examples |
| `petunia-ds.css` | Standalone importable stylesheet — import this into any project |
| `PETUNIA-DS-SYSTEM-PROMPT.md` | Implementation brief for AI agents — include at session start |
| `petunia-visual-language.html` | Visual language specimen collection — illustration, photography, motion, texture, type |

---

## Quick Start

```html
<!-- 1. Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,300;0,6..96,400;0,6..96,700;1,6..96,300;1,6..96,400;1,6..96,700&family=IBM+Plex+Mono:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;1,300;1,400&display=swap" rel="stylesheet">

<!-- 2. Icons -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>

<!-- 3. Design System -->
<link rel="stylesheet" href="https://raw.githubusercontent.com/[YOUR_GITHUB]/holograph-design-system/main/petunia-ds.css">
```

---

## Typography

Three fonts. Three roles. Never swap them.

- **Bodoni Moda** — display only, hero moments, ≥48px
- **IBM Plex Sans** — prose, h3+, UI copy, form labels, body text  
- **IBM Plex Mono** — all numbers, all labels, all data, code

---

## Color

| Token | Value | Role |
|-------|-------|------|
| `--brand-teal` | `#5ECDD8` | Interactive / links / active |
| `--brand-violet` | `#A991E2` | Secondary accent |
| `--brand-amber` | `#F0A040` | Caution / handoff |
| `--brand-green` | `#5DB872` | Success |
| `--status-error` | `#E05040` | Errors |
| `--bg-base` | `#080C10` | Page root |
| `--text-primary` | `#E2EBF0` | Primary text |

---

## For AI Agents

Include `PETUNIA-DS-SYSTEM-PROMPT.md` at the start of any session where an AI is building or modifying UI. It contains every rule in a compact, machine-readable format.

---

## Stack

- CSS custom properties (no preprocessor required)
- [Lucide Icons](https://lucide.dev) — 2px stroke, MIT license
- [Alpine.js](https://alpinejs.dev) — for interactive components (optional)
- Google Fonts — SIL Open Font License, free for commercial use
