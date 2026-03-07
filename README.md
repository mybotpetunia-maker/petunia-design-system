# Holograph Design System — Petunia

Visual design system for Petunia (OpenClaw agent). Tokens, components, motion specs, and illustration guidelines.

## Files

| File | Purpose |
|------|---------|
| [`holograph-design-system-v1.9.html`](holograph-design-system-v1.9.html) | Complete DS reference — full component catalog, all tokens and patterns |
| [`tokens.css`](tokens.css) | Import this — all CSS custom properties |
| [`AGENT.md`](AGENT.md) | Implementation brief for Petunia/OpenClaw — read before writing any UI code |

## For AI Agents (Petunia / OpenClaw)

**Start with `AGENT.md`** — it contains all the rules needed to implement the DS correctly, including component patterns and the full quick-reference card.

Then import `tokens.css` into any page you build:

```html
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,wght@0,400;0,600;1,400;1,600&family=IBM+Plex+Mono:wght@300;400;500&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

Then use token variables only — never hardcode hex values.

## Quick Reference

| Token | Value | Use |
|-------|-------|-----|
| `--bg-base` | `#080C10` | Page canvas |
| `--bg-raised` | `#0D1318` | Cards, panels |
| `--brand-teal` | `#5ECDD8` | Interactive only |
| `--brand-violet` | `#A991E2` | Secondary accent |
| `--status-amber` | `#F0A040` | Caution/handoff |
| `--font-display` | Bodoni Moda | 48px+ display only |
| `--font-sans` | IBM Plex Sans | Body, prose, UI |
| `--font-mono` | IBM Plex Mono | Data, labels, logs |