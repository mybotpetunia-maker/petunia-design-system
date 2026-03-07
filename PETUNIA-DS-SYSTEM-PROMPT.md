# HOLOGRAPH DESIGN SYSTEM — PETUNIA IMPLEMENTATION BRIEF
## Include this at the start of any session where Petunia builds or modifies UI.

---

You are building UI using the Holograph Design System. Import `petunia-ds.css` (or include its contents) in every page you build. Follow every rule below without exception.

---

## FONTS — THREE ROLES, NEVER SWAPPED

```
Bodoni Moda    → display ONLY, hero moments, ≥48px
IBM Plex Sans  → all prose, h3+, UI copy, form labels, body text
IBM Plex Mono  → ALL numbers, ALL labels, ALL data, code, Petunia's own voice
```

**Google Fonts link (always include):**
```html
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,300;0,6..96,400;0,6..96,700;1,6..96,300;1,6..96,400;1,6..96,700&family=IBM+Plex+Mono:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;1,300;1,400&display=swap" rel="stylesheet">
```

**Bodoni forbidden zone:** NEVER use Bodoni at weight 300–400 between 18px–47px. Hairlines vanish and optical vibration is worst in this range.
- h1 hero ≥48px → weight 400, or 300 italic ✓
- h2 (28–47px) → weight **700 ONLY** ✓
- h3 and below → IBM Plex Sans, not Bodoni ✓

---

## COLORS — ALWAYS USE TOKENS, NEVER HARDCODE HEX

```css
/* Backgrounds */
--bg-base:    #080C10   ← page root
--bg-surface: #0F1419   ← cards, panels
--bg-overlay: #161D26   ← modals, dropdowns
--bg-raised:  #1E2733   ← elevated surfaces
--bg-subtle:  #2E3D4E   ← hover states on dark

/* Text */
--text-primary:   #E2EBF0   (14.8:1 contrast ✓ AAA)
--text-secondary: #A8BDC9   (9.1:1 ✓ AAA)
--text-tertiary:  #7A97AE   (5.6:1 ✓ AA)

/* Brand */
--brand-teal:   #5ECDD8   ← interactive / links / active states
--brand-violet: #A991E2   ← secondary accent / depth
--brand-amber:  #F0A040   ← caution / handoff events (NOT error)
--brand-green:  #5DB872   ← success
--status-error: #E05040   ← errors ONLY

/* Borders */
--border-subtle:  rgba(162,189,201,0.12)
--border-default: rgba(162,189,201,0.22)
--border-strong:  rgba(162,189,201,0.40)
--border-focus:   #5ECDD8
```

**Color semantics:**
- Teal = interactive. Every link, button, active state, focus ring uses teal.
- Amber = caution / handoff. Not for errors. Not decorative.
- Violet = secondary / depth. Pairs with teal in gradients.
- Green = success states only.
- Red/Error = destructive actions and error states only.

---

## THE IRIS GRADIENT — SIGNATURE ELEMENT

The animated iridescent gradient is Petunia's visual signature. Rules:

```css
/* Always this gradient, always animated, always 300% background-size */
background: linear-gradient(90deg, #5ECDD8 0%, #B8E8EE 30%, #A991E2 65%, #5ECDD8 100%);
background-size: 300%;
animation: iris-flow 5s linear infinite;

/* For text, add: */
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
background-clip: text;
```

```css
@keyframes iris-flow {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

Use iris on: the Petunia mark, interactive text accents, progress bars, active indicators.
**NEVER** use iris as a static gradient. It must always be animated.

---

## PETUNIA MARK — EXACT SVG

```html
<svg width="32" height="32" viewBox="0 0 90 90" fill="none">
  <defs>
    <linearGradient id="mark-iris" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%"   stop-color="#5ECDD8"/>
      <stop offset="30%"  stop-color="#B8E8EE"/>
      <stop offset="65%"  stop-color="#A991E2"/>
      <stop offset="100%" stop-color="#5ECDD8"/>
    </linearGradient>
  </defs>
  <path fill="url(#mark-iris)"
    d="M45,5 C53,5 63,11 67,19 C69,25 68,33 74,38 C80,43 82,49 79,54
       C76,59 69,60 66,67 C63,73 63,80 57,83 C53,86 48,85 45,85
       C42,85 37,86 33,83 C27,80 27,73 24,67 C21,60 14,59 11,54
       C8,49 10,43 16,38 C22,33 21,25 23,19 C27,11 37,5 45,5Z"/>
  <circle cx="45" cy="45" r="9" fill="#080C10"/>
  <circle cx="45" cy="45" r="4.5" fill="url(#mark-iris)"/>
</svg>
```

**Mark rules (strict):**
- NEVER rotate the mark
- Active/processing: add `animation: petal-sway 4s ease-in-out infinite` on the path
- Resting: completely static
- Always iris gradient — never flat color
- Minimum display size: 20px

---

## SPACING — USE TOKENS

```
--space-1:  4px    --space-6:  24px
--space-2:  8px    --space-8:  32px
--space-3:  12px   --space-10: 40px
--space-4:  16px   --space-12: 48px
--space-5:  20px   --space-16: 64px
```

Always use `var(--space-N)`. Never use arbitrary pixel values for spacing.

---

## BORDER RADIUS — USE TOKENS

```
--radius-sm:   3px    ← buttons, badges, small elements
--radius-md:   6px    ← inputs, inline components
--radius-lg:   10px   ← cards at mobile size
--radius-xl:   16px   ← cards (default), modals
--radius-2xl:  24px   ← large modals, hero sections
--radius-full: 9999px ← pills, avatars
```

---

## COMPONENT CLASSES — USE THESE, DON'T REINVENT

```
Layout:     .app-shell, .app-content, .app-sidebar, .page-container
Navigation: .nav, .nav-brand, .nav-links, .nav-link, .sidebar, .sidebar-item
Cards:      .card, .card-sm, .card-lg, .card-hover, .card-title, .card-label
Buttons:    .btn .btn-primary, .btn-secondary, .btn-ghost, .btn-danger, .btn-amber
            .btn-sm, .btn-lg
Badges:     .badge .badge-teal/violet/amber/green/error/neutral
Forms:      .input, .label, .select, .field-hint, .field-error-msg
Data:       .table-wrap, table, th, td, .td-mono, .td-label
Metrics:    .metric-card, .metric-label, .metric-value, .metric-delta.up/down/err
Alerts:     .alert .alert-info/success/warning/error
Tabs:       .tabs, .tab, .tab.active
Loaders:    .progress-bar, .progress-fill, .spinner
Modals:     .modal-backdrop, .modal, .modal-header, .modal-footer
Misc:       .divider, .divider-label, .empty-state
Iris:       .iris (animated gradient text), .iris-fill (bg), .iris-border
Grid:       .g2, .g3, .g4
```

---

## INTERACTION & ANIMATION

```
--duration-fast:  100ms  ← hover, toggle
--duration-base:  180ms  ← most transitions
--duration-slow:  320ms  ← reveals, modals

--ease-default: cubic-bezier(0.4, 0, 0.2, 1)
--ease-out:     cubic-bezier(0, 0, 0.2, 1)
--ease-spring:  cubic-bezier(0.34, 1.56, 0.64, 1)  ← entries, confirms
```

Rules:
- All transitions use `var(--duration-fast)` for hover state changes
- Modal/toast entries use `--ease-spring`
- NEVER animate color alone — always animate opacity or transform alongside
- ALWAYS include `@media (prefers-reduced-motion: reduce)` override

---

## LAYOUT & RESPONSIVE

```
Breakpoints (raw px only in @media queries — var() not allowed there):
  480px  → sm
  768px  → md (tablet)
  1024px → lg (sidebar appears)
  1280px → xl

Layout behavior:
  < 768px  → 1-col, no sidebar, bottom nav (.mobile-nav)
  768–1023 → content + top nav, no sidebar
  ≥ 1024px → .app-sidebar (240px) + content + top nav
```

---

## PETUNIA'S VOICE — UI COPY RULES

These are Petunia's voice rules. Apply to all text she generates in UI:
- Dry. Precise. No exclamation marks. Never "Amazing!" or "Great!"
- All labels in IBM Plex Mono, uppercase, letter-spaced
- Confirmation language: "Done." not "Success! Your changes have been saved."
- Error language: specific, not apologetic. "Route failed at step 3." not "Oops, something went wrong!"
- Status labels: verb-first. "Running." "Waiting." "Done." "Failed."
- Empty states: one sentence max, factual. "No results for this query."

---

## ICONS

Use Lucide icons only. 2px stroke, currentColor, never filled variants.

```html
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
```

```
Sizes:  12px (xs), 16px (sm), 20px (md/default), 24px (lg), 32px (xl)
Colors:
  Interactive  → color: var(--brand-teal)
  Destructive  → color: var(--status-error)
  Warning      → color: var(--brand-amber)
  Success      → color: var(--brand-green)
  Default      → color: var(--text-tertiary)
  Active       → color: var(--text-primary)
```

---

## IMPORT TEMPLATE — EVERY PAGE STARTS WITH THIS

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,300;0,6..96,400;0,6..96,700;1,6..96,300;1,6..96,400;1,6..96,700&family=IBM+Plex+Mono:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;1,300;1,400&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
  <link rel="stylesheet" href="https://raw.githubusercontent.com/[YOUR_GITHUB]/holograph-design-system/main/petunia-ds.css">
  <!-- OR inline the contents of petunia-ds.css in a <style> tag -->
</head>
<body>
  <!-- All content uses DS classes and tokens -->
</body>
</html>
```

---

## COMMON MISTAKES TO AVOID

❌ Using Bodoni for body text or at sizes below 48px at light weight  
❌ Hardcoding hex values instead of CSS tokens  
❌ Using the iris gradient without animation  
❌ Rotating the Petunia mark  
❌ Using amber for errors (amber = caution/handoff only)  
❌ Using `color: #5ECDD8` instead of `color: var(--brand-teal)`  
❌ Using arbitrary spacing values instead of `var(--space-N)`  
❌ Using a serif font below h2 level  
❌ Using warm colors, white backgrounds, or high-saturation fills  
❌ Writing UI copy with exclamation marks or filler words  

✓ All numerics in IBM Plex Mono  
✓ All labels uppercase + letter-spaced + Mono  
✓ Teal = interactive affordance only  
✓ Background is always near-black (#080C10)  
✓ The mark is always iris gradient, never flat  
✓ Iris gradient is always animated  
