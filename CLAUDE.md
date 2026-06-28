# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static marketing/landing site for **Mehai Capital** (financial advisory). No build step — all files are served as-is.

## File format: `.dc.html`

Files use a custom **Design Canvas** format powered by `support.js`:

- Root element is `<x-dc>` — everything inside is the template.
- `<helmet>` block inside `<x-dc>` maps to `<head>` (stylesheets, scripts).
- Templating: `{{ expression }}` for bindings, `<sc-if value="{{ expr }}">` for conditionals.
- Event handlers: `onClick="{{ handlerName }}"`.
- `support.js` is **generated** — do not edit it directly.

## Design system: Sapien (Darwinbox SDS)

All styling uses the **Sapien Design System** loaded from `_ds/sapien-design-system-*/`:
- `tokens.css` — CSS custom properties for color, type, spacing, radius, elevation. Import first.
- `_ds_bundle.js` — component JS bundle.

**Rules:**
- Never use raw hex, px, or font-size values when an SDS token exists. Use `--gl-*` global tokens or `--bg-*` / `--text-*` / `--border-*` alias tokens.
- Color aliases: `--bg-neutralGrey-light2` (page bg) → `--bg-neutralWhite-default` (card) → `--bg-neutralGrey-light4` (hover).
- Text stack: `--text-neutral-default` → `--text-neutral-secondary` → `--text-neutral-muted`.
- Radius: `--radius-s` (buttons/inputs), `--radius-m` (cards), `--radius-l` (modals), `--radius-pill` (avatars/chips).
- Elevation: `var(--shadow-level-1/2/3)` — never invent new shadows.
- Font family: `var(--font-family-base)` (Darwin Sans with Mulish/Inter fallbacks).
- Font weights: `var(--font-weight-bold)` / `--font-weight-medium` / `--font-weight-regular`.

## Key files

| File | Purpose |
|------|---------|
| `index.html` | Main landing page (DC format, uses `<x-dc>`) |
| `mehai-leak-test (1).html` | Self-contained mutual-fund fee-gap diagnostic widget |
| `mehai-leak-test (2).html` | Second variant of the leak-test widget |
| `support.js` | DC runtime — do not edit |
| `_ds/.../tokens.css` | All SDS design tokens |
| `_ds/.../_ds_bundle.js` | SDS component bundle |

## Brand token aliases

`index.html` defines Mehai-specific CSS variables at the root element that alias SDS globals:

```css
--navy:      var(--gl-blue-900)   /* primary brand dark */
--emerald:   var(--gl-green-500)  /* primary brand accent */
--emerald-d: var(--gl-green-600)  /* accent hover */
--ink:       var(--gl-charcoal-500)
--line:      var(--gl-charcoal-50)
--gold:      var(--gl-yellow-500)
```

Use these aliases within `index.html` rather than reaching for raw globals.

## Viewing the site

Open `index.html` directly in a browser — no local server needed. The `support.js` runtime bootstraps the `<x-dc>` template on page load.

The site is deployed on GitHub Pages (see `CNAME` and `.nojekyll`).
