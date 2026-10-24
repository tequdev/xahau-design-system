# Xahau Design System

A framework-free CSS design system for Xahau web apps. Plain CSS custom properties plus `x-` prefixed component classes, no build step, no dependencies. Open `index.html` for a living demo of every component in every theme.

| Blue (default)               | Green (`.theme-green`)         |
| ---------------------------- | ------------------------------ |
| ![Blue theme](docs/blue.png) | ![Green theme](docs/green.png) |

| Yellow (`.theme-yellow`)         | Dark (`.dark`)               |
| -------------------------------- | ---------------------------- |
| ![Yellow theme](docs/yellow.png) | ![Dark theme](docs/dark.png) |

## Themes

- Blue is the default brand (`#183FB7`, hover `#1d4ed8`, light `#7592F7`).
- `.theme-green` (`#197a4b`) and `.theme-yellow` (`#fffd57`, the Xahau logo yellow) remap the brand and gradient tokens. Yellow also sets `--on-brand` and `--glass` to the logo navy `#0e0143`, because white text does not read on it, and uses that navy as the light-mode brand text.
- Brand themes are classes on `<html>`, so they compose with dark mode.
- Dark mode works via `.dark` on `<html>`, `[data-theme="dark"]`, or the OS preference unless `[data-theme="light"]`/`.light` is set.

## Decisions

- Gray scale and accents are a Tailwind-style palette; every component reads semantic vars (`--bg`, `--surface`, `--text`, `--brand`, `--on-brand`, …), so a theme is a block of overrides.
- Fonts are Inter and Source Code Pro. They are not imported by the CSS, link them in `<head>`; fallbacks are system fonts.
- Focus is a 2px outline in the brand text colour, white (or `--on-brand`) on card headers.
- No icon font. Use inline SVG.

## Usage

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Source+Code+Pro:wght@400;500;700&display=swap">
<link rel="stylesheet" href="tokens.css">
<link rel="stylesheet" href="xahau.css">
<html class="dark theme-green"> <!-- both optional; theme-yellow too -->
```

## Components

- `x-container` centered page width with responsive gutters
- `x-topbar`, `x-topbar-row`, `x-brand`, `x-subnav` header with brand and secondary nav
- `x-card`, `x-card-head`, `x-card-sub`, `x-card-body` card with gradient header
- `x-btn` plus `-secondary`, `-warning`, `-glass`, `-sm`, `-lg`; `:disabled` is gray
- `x-badge`, `x-badge-glass` pill label
- `x-box` monospace inset block for addresses and URLs
- `x-tiles`, `x-tiles-2`, `x-tile`, `x-tile-green|blue|purple` stat tiles
- `x-dot`, `x-dot-live`, `x-dot-wait`, `x-state` status indicator
- `x-label`, `x-input` form field
- `x-callout-warn`, `x-callout-error` message blocks
- `x-rows`, `x-row` label, value and action rows
- `x-details`, `x-summary` disclosure with Expand/Collapse chip
- `x-footer`, `x-grid`, `x-stack` layout helpers
