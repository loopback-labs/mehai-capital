# Sapien Design System

# Darwinbox SDS — UI Kit Handoff

> **Required reading for any design task in this project:** open `CLAUDE.md` first (agent contract), this file (component inventory + utility classes), and `ui-kit.html` (live demos). All three are mandatory before writing HTML.

This kit documents the Darwinbox **Sapien Design System** (SDS) for HTML design work. It is the source of truth for tokens, components, and the contract the code agent uses to translate HTML into Angular/Sapien.

> **Rule #1 — no invented values.** Every new screen must compose its color, type, spacing, radius, elevation, and sizing from the `sds-*` utility classes documented below. Never inline a hex, px, or font-size when an SDS token exists.

> **Rule #2 — primary buttons are always charcoal.** The primary CTA is brand-locked. `sds-btn--primary` uses the charcoal ramp regardless of the active theme. Themes only re-colour the **secondary** button (and only when the designer explicitly opts in with `sds-btn--secondary theme-*`). Do not tint the primary button, a primary icon button, or a primary-tone link to match the theme — that treatment is reserved for secondary/tertiary actions.

---


> The official design system for Darwinbox products.
> _Refreshingly Efficient. Uniquely Yours._

Sapien is the in-house design system that powers the entire **Darwinbox HCM
suite** — a unified library of tokens, components and patterns that gives every
Darwinbox screen, on every platform, a consistent voice and behaviour.

This project is the **HTML/CSS handoff** of Sapien for use inside design
artifacts: prototypes, slides, marketing pages and product mocks.

---

## What is Darwinbox / Sapien?

- **Darwinbox** is a global Human Capital Management (HCM) platform — hire,
  pay, manage, develop and engage employees across the full lifecycle.
- **Sapien** is Darwinbox's design system. It ships as a Figma library
  (`SDS Web — Foundations & Components`) and as code primitives consumed by
  every Darwinbox product team.
- Source: the included `SDS Web` Figma file plus uploaded references
  (`Global Token Variables`, `Alias Tokens`, `Do's & Don'ts`, `Overview`).

## Sapien principles

| Principle    | Idea                                                                              |
|--------------|------------------------------------------------------------------------------------|
| **Human**    | Designs feel natural and empathetic — real people at the center of every decision. |
| **Evolving** | A system that grows, adapts, and improves continuously as the product scales.      |
| **Minimal**  | Simple, clear, purposeful interfaces — remove noise; keep what matters.            |
| **Inclusive**| AA-accessible, multilingual, multi-device — usable for everyone.                   |
| **Trustworthy**| Consistent components, transparent communication, ethical practice.              |

## What changed in this generation of Sapien

1. **Unified component library** — one set of components across web + mobile.
2. **In-house font** — Darwin Sans replaces Circular / Roboto.
3. **Universal design** — multilingual, AA contrast, structured for assistive tech.
4. **Structured navigation** — global header + left-rail pattern across all apps.
5. **Smart Theme** — runtime theming via `theme-*` tokens; logo/colour swap per tenant.
6. **Device responsive** — every component works on phone, tablet, desktop.

---

## Files in this project

| File                          | What it is                                          |
|-------------------------------|------------------------------------------------------|
| `tokens.css`                  | All foundation tokens (color / type / space / radius / shadow). Import this first. |
| `Type.html`                   | Darwin Sans, weights, full type scale, in-the-wild specimens. |
| `Colors.html`                 | Two-tier token system — global ramps + alias mapping. |
| `Spacing.html`                | 8-point grid, radius scale, three-tier elevation.   |
| `Components.html`             | Buttons, inputs, badges, alerts, cards, tabs, tables. |
| `Brand.html`                  | Cover lockup, principles, "what changed", logo, voice. |
| `assets/brand/*`              | Darwinbox + Sapien logos and brand SVGs.            |
| `fonts/*.otf`                 | Darwin Sans family files referenced by `tokens.css`.|
| `SKILL.md`                    | How an agent should use this system in new artifacts.|

---

## Token system — two tiers

Sapien tokens come in two layers:

1. **Global tokens** — raw ramp steps. Named `gl_colors-brand-{ramp}-{step}`,
   exposed in CSS as `--gl-{ramp}-{step}` (e.g. `--gl-charcoal-500`,
   `--gl-blue-500`). Six brand ramps: Charcoal, White, Blue, Green, Red,
   Yellow. Plus eight Custom Theme ramps for Smart Theme.

2. **Alias tokens** — semantic roles that point at global steps. Named
   `{bg|text|border|icon|theme}-{role}-{state}` (e.g. `--bg-primary-default`,
   `--text-neutral-secondary`, `--border-feedback-error`,
   `--theme-bg-active`).

**Always reference aliases in product code.** Reach for globals only for
marketing, illustration, or genuine one-offs.

### Color cheat-sheet

- **Surface stack:** `--bg-neutralGrey-light2` (page) → `--bg-neutralWhite-default`
  (card) → `--bg-neutralGrey-light4` (hover row).
- **Text stack:** `--text-neutral-default` → `--text-neutral-secondary` →
  `--text-neutral-muted` → `--text-neutral-disabled`.
- **Primary action:** `--bg-primary-active` (charcoal-500) — Sapien's primary
  buttons are charcoal, not coloured.
- **Theme accent:** `--theme-bg-active` — runtime-swappable via Smart Theme;
  defaults to `--gl-blue-500`.
- **Sentiment text:** `--text-feedback-success` / `-error` / `-warning` / `-info`.
- **Sentiment surfaces:** `--bg-feedback-{kind}-{High|Mid|Low}` for filled, soft, lowest tints.

### Type

- Family: **Darwin Sans** (in-house, `.otf` in `fonts/`). Weights: Light 300,
  Book 400, Medium 500, Bold 700, ExtraBold 800 (Book + Medium also italic).
  Web fallback: Mulish → Plus Jakarta Sans → Inter.
- Scale: Display 56/64 · Title L 40/48 · Title M 28/36 · Title S 20/28 ·
  Body L 16/24 · Body M 14/20 · Body S 13/18 · Caption 12/16.
- Weight rules: headings = Medium, body = Book, emphasis = Bold.

### Spacing — 8-point grid

`2 · 4 · 6 · 8 · 12 · 16 · 20 · 24 · 32 · 40 · 48 · 56 · 64 · 80 · 96`.
The 4-unit-and-below tokens are reserved for sub-component nudges.

### Radius

`--radius-xs` 4 · `-s` 8 · `-m` 12 · `-l` 16 · `-xl` 24 · `-pill` 999.
- Buttons / inputs: `--radius-s`.
- Cards / panels: `--radius-m`.
- Modals / hero blocks: `--radius-l`.
- Avatars / pills / chips: `--radius-pill`.

### Elevation

| Level | Use                                            |
|-------|-------------------------------------------------|
| 1     | Cards, dropdowns, tooltips, search bar.         |
| 2     | Alerts, popovers, toasts, callouts.             |
| 3     | Floating panels, modals, FAB, navigation.       |

Stick to the three named shadows. **Never** invent a new one.

---

## Content fundamentals

Sapien is bilingual-by-default and writes with a **plainspoken, direct, calm**
voice — designed to feel like a competent colleague, not a marketer.

- **Use sentence case.** "Apply leave", not "Apply Leave". Title Case is for
  product / module names only.
- **Lead with the verb.** "Request leave", "Submit feedback", "Approve
  request" — not "Click here", "Submit".
- **Numbers stay numerals.** `2 days`, `5 pending`, `28 March 2025`.
- **Dates:** `28 March 2025`, `Mon, 25 Jul 2025`. Time: `10:30 AM`.
- **Empathy over jargon.** "Looks like nothing's here yet." not "No records
  found in resultset."
- **Be specific in errors.** Tell the user what went wrong _and_ what to do.
- **Avoid emoji** in product chrome. Reserve for user-generated content
  (reactions, NPS, celebration moments).
- **Punctuation:** sentence-end periods on full sentences; no period on
  single-line labels, headings or button text.

### Common patterns

| Pattern         | Sapien voice                                            |
|-----------------|----------------------------------------------------------|
| Empty state     | "No leave requests yet. Apply for leave to get started." |
| Confirmation    | "Leave request sent to Britta Seeger."                   |
| Destructive     | "Delete this draft? This can't be undone."               |
| Loading         | "Just a moment…"                                         |
| Success toast   | "Saved."                                                 |
| Permission gate | "You don't have access to this page. Ask your admin."    |

---

## Quick-start

```html
<!doctype html>
<html>
<head>
  <link rel="stylesheet" href="tokens.css" />
</head>
<body>
  <h1 class="t-title-l">Hello, Sapien.</h1>
  <button style="
    background: var(--bg-primary-active);
    color: var(--text-neutral-onBrand);
    padding: var(--space-12) var(--space-24);
    border-radius: var(--radius-s);
    border: 0;
    font: var(--font-weight-medium) var(--font-size-body-m)/1 var(--font-family-base);
    box-shadow: var(--shadow-level-1);
  ">Request leave</button>
</body>
</html>
```

Always layer in this order: **tokens → utilities → components → product code**.

## Sources

- `SDS Web — Foundations & Components` Figma file (Darwinbox internal).
- `Global Token Variables`, `Alias Tokens`, `Do's & Don'ts`, `Overview`,
  `Cover` — uploaded reference pages.
- `uploads/Banner.png`, `uploads/Principles.png`, `uploads/Whats Changes 1-4.png`
  — internal launch deck supplied by the team.
