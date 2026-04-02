---
name: portfolio-visual-design
description: Visual design skill for Quin Robinson's product design portfolio. Enforces the established design system and provides enhancement rules for typography, animation, spacing, accessibility, and dark/light zone treatment.
---

# Portfolio Visual Design Skill

Use this skill whenever making visual design decisions, writing CSS, or enhancing the UI of the portfolio site at `~/Documents/Claude/Product-Design-Portfolio/index.html`.

---

## Design System Tokens

Never introduce new color values. All visual work must use these established tokens:

```css
/* Dark surfaces */
--charcoal:        #111110;   /* primary dark background */
--charcoal-border: rgba(255,255,255,0.09);  /* borders on dark */
--charcoal-muted:  rgba(255,255,255,0.48);  /* secondary text on dark */
--charcoal-subtle: rgba(255,255,255,0.24);  /* tertiary text / labels on dark */

/* Light surfaces */
--white:           #ffffff;
--off-white:       #f5f4f1;   /* warm gray section backgrounds */
--light-border:    #e4e3df;
--ink:             #171715;   /* primary text on light */
--ink-secondary:   #52524e;
--ink-tertiary:    #96958f;
--timeline-line:   #d0cfc9;

/* Accent */
--accent:          #F5975A;   /* warm orange — CTAs, labels, hover states */
--accent-deep:     #E8602C;   /* deeper orange — hover on accent elements */
```

**Typography:** DM Sans (Google Fonts), base weight 300 (light). Use 500 for labels, 600–700 for headings only.

**Zone strategy:** The site alternates between `.zone-dark` (charcoal bg) and light sections (white/off-white). Always maintain this contrast rhythm. Never use accent color as a background fill.

---

## Visual Enhancement Rules

### Typography
- Body line-height: 1.6–1.75. Never below 1.5.
- Max line length for body copy: 65–72 characters (roughly `max-width: 640px`).
- Section leads and headlines: letter-spacing -0.01em to -0.03em for large sizes.
- Small caps / labels: letter-spacing 0.06–0.1em, font-weight 500.
- Never use font-weight below 300 or above 700 in this system.

### Spacing & Rhythm
- Section padding: `5rem 4vw` (established). Don't deviate without cause.
- Use multiples of 4px for spacing values (4, 8, 12, 16, 24, 32, 48, 64).
- Maintain generous whitespace — this is a portfolio, not a dashboard.
- Group related elements tightly; separate distinct sections with space.

### Animation & Motion
- Transitions: `0.2s ease` for hover states, `0.3s ease` for reveals.
- Entrance animations: subtle, fast (200–300ms). Never flashy.
- Always include `prefers-reduced-motion` override:
  ```css
  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { transition: none !important; animation: none !important; }
  }
  ```
- Fade-in on scroll is acceptable; parallax and bounce effects are not on-brand.
- Never animate color changes on body text.

### Dark Zone Enhancements
- Use `--charcoal-border` for all rules and dividers — never white at full opacity.
- Text hierarchy on dark: white (primary) → `--charcoal-muted` (secondary) → `--charcoal-subtle` (tertiary).
- Subtle depth: a `1px` inset border or `box-shadow: 0 0 0 1px var(--charcoal-border)` is preferred over strong drop shadows.
- Hover states on dark: shift text from muted → white, or tint with `--accent`.

### Light Zone Enhancements
- Use `--off-white` (#f5f4f1) for alternating section backgrounds, not pure gray.
- Cards and surfaces: white on off-white backgrounds, with `--light-border` edge.
- Hover states on light: subtle background shift to `--off-white`, or underline with `--accent`.

### Interactive States (all elements)
- Every interactive element must have: hover, focus-visible, and active states.
- Focus rings: `outline: 2px solid var(--accent); outline-offset: 3px;` — never remove outline without a visible replacement.
- Disabled states: 40% opacity, `cursor: not-allowed`.
- Loading states: use opacity pulse (0.4 → 1.0), not spinners unless necessary.

### Accessibility
- Minimum contrast: 4.5:1 for body text, 3:1 for large text and UI components (WCAG AA).
- `--charcoal-muted` (rgba white 48%) on `--charcoal` passes at approximately 4.6:1 — do not reduce opacity further.
- `--accent` (#F5975A) on `--charcoal` (#111110) passes large text contrast. Do not use it for small body text on dark backgrounds.
- All images must have descriptive `alt` attributes. Decorative images: `alt=""`.
- Interactive elements: minimum touch target 44×44px.
- Never rely on color alone to convey state — always pair with text, icon, or shape change.

### Navigation
- Sticky nav: use `backdrop-filter: blur(12px)` with a semi-transparent dark bg rather than fully opaque.
- Active nav state: `--accent` color + optional underline indicator.
- Smooth scroll is already set via `scroll-behavior: smooth` on html — maintain this.

### Performance
- Prefer CSS transitions over JavaScript animations where possible.
- Images: always specify `width` and `height` attributes to prevent layout shift.
- Lazy-load images below the fold: `loading="lazy"`.
- Avoid adding external JS libraries for visual effects — CSS is sufficient for this portfolio's needs.

---

## Style Direction: AI-Native Dark Minimalism

This portfolio's visual identity sits at the intersection of:
- **Swiss/editorial minimalism** — strong grid, generous whitespace, restrained type scale
- **Dark mode premium** — deep charcoal ground, warm orange accent, high-contrast hierarchy
- **AI-native UI signals** — precision, structured content, subtle motion, purposeful data

**Do:** Precise spacing, sharp typographic contrast, warm-cool balance (charcoal + orange), subtle entrance motion, structured layouts.

**Don't:** Gradients (unless very subtle), drop shadows (unless minimal), decorative icons, rounded corners above 8px on cards, animations that call attention to themselves.

---

## Portfolio-Specific Rules

- The work grid (case studies) is the highest-priority visual real estate. Anything that improves scannability and visual weight of the work grid is high value.
- The hero section establishes tone — any changes here should reinforce the "agentic product design" positioning.
- The experience timeline is intentionally restrained — don't over-design it.
- The resume download button is a key CTA — it must always remain high contrast and clearly interactive.
- Never remove the fade-in `.fade-in` animation class behavior — it's used throughout for scroll reveals.
