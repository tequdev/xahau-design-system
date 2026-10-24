# Xahau Design System

A framework-free CSS design system for Xahau web apps. Plain CSS custom properties plus `x-` prefixed component classes. No build step, no dependencies, two files.

Open `index.html` for a living demo of every component in every theme.

| Blue (default)               | Green (`.theme-green`)         |
| ---------------------------- | ------------------------------ |
| ![Blue theme](docs/blue.png) | ![Green theme](docs/green.png) |

| Yellow (`.theme-yellow`)         | Dark (`.dark`)               |
| -------------------------------- | ---------------------------- |
| ![Yellow theme](docs/yellow.png) | ![Dark theme](docs/dark.png) |

## Usage

```sh
npm i @tequdev/xahau-design-system   # or pnpm add / yarn add
```

With a bundler (Vite, Next.js, webpack), import the stylesheet once at the app entry:

```js
import "@tequdev/xahau-design-system";
```

That is `index.css`, which pulls in `tokens.css` and `xahau.css`. Import the two files separately if you want to swap or extend the tokens:

```js
import "@tequdev/xahau-design-system/tokens.css";
import "./my-tokens.css"; // overrides
import "@tequdev/xahau-design-system/xahau.css";
```

Without a bundler, link the files from a CDN (or copy them next to your page):

```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/@tequdev/xahau-design-system@0.1.0/index.css"
>
```

The CSS does not import fonts. Add Inter and Source Code Pro yourself, or the system falls back to `system-ui` and `ui-monospace`:

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Source+Code+Pro:wght@400;500;700&display=swap"
>
```

Pick a theme with classes on `<html>`. Both are optional and they combine.

```html
<html class="theme-green dark">
```

## Themes

| Theme  | Class           | `--brand` | `--brand-hover` | `--brand-light` | `--on-brand` |
| ------ | --------------- | --------- | --------------- | --------------- | ------------ |
| Blue   | none (default)  | `#183fb7` | `#1d4ed8`       | `#7592f7`       | `#fff`       |
| Green  | `.theme-green`  | `#197a4b` | `#115a36`       | `#51b883`       | `#fff`       |
| Yellow | `.theme-yellow` | `#fffd57` | `#f0ec3a`       | `#fffd57`       | `#0e0143`    |
- A brand theme only remaps the brand tokens: `--brand`, `--brand-hover`, `--brand-light`, `--grad`, and, when the brand is too light for white text, `--on-brand`, `--glass`, `--brand-text`.
- Yellow is the Xahau logo yellow, so its on-brand colour is the logo navy and light-mode headings and links use that navy too.
- Dark mode is `.dark` or `[data-theme="dark"]` on `<html>`. It also follows the OS preference unless `[data-theme="light"]` or `.light` is set. In dark mode brand text switches to `--brand-light`.

### Your own theme

Every component reads semantic tokens, so a theme is one block of overrides on `<html>`:

```css
.theme-purple {
  --brand: #6f23d0;
  --brand-hover: #5c10be;
  --brand-light: #bb87ff;
  --grad: linear-gradient(to right, #6f23d0, #bb87ff);
}
```

## Tokens

Primitives (`--gray-50…900`, `--amber-*`, `--green-*`, `--blue-*`, `--purple-*`, `--red-*`, `--yellow-*`) are a Tailwind-style palette. Components never read them directly; they read the semantic layer below, which the dark and brand blocks override.

| Token                                                    | Drives                                                |
| -------------------------------------------------------- | ----------------------------------------------------- |
| `--bg`, `--surface`, `--surface-2`                       | page background, cards and top bar, inset boxes       |
| `--text`, `--muted`, `--border`                          | body text, captions and labels, borders               |
| `--brand`, `--brand-hover`, `--brand-light`              | primary buttons, hover, dark-mode brand text          |
| `--brand-text`, `--on-brand`, `--grad`                   | headings and links, text on brand surfaces, card head |
| `--glass`, `--glass-hover`                               | translucent buttons and badges on the card head       |
| `--btn2-bg`, `--btn2-hover`, `--btn2-text`               | secondary and small buttons, the disclosure chip      |
| `--badge-bg`, `--badge-text`                             | badges                                                |
| `--warn-bg`, `--warn-text`, `--error-bg`, `--error-text` | callouts                                              |
| `--tile-green                                            | blue                                                  | purple(-bg)`, `--tile-label` | stat tiles |
| `--input-border`                                         | inputs                                                |
| `--font-sans`, `--font-mono`                             | Inter, Source Code Pro                                |
| `--radius-sm                                             | md                                                    | lg                           | xl         | full` | 4px, 6px, 8px, 12px, pill |
| `--shadow-card`, `--shadow-bar`                          | card elevation, top bar                               |

## Components

| Class                                                                               | What it is                                        |
| ----------------------------------------------------------------------------------- | ------------------------------------------------- |
| `x-container`                                                                       | centered 80rem page width with 16/24/32px gutters |
| `x-topbar`, `x-topbar-row`, `x-brand`, `x-subnav`                                   | header with brand, actions and a secondary nav    |
| `x-card`, `x-card-head`, `x-card-sub`, `x-card-body`                                | card with gradient header                         |
| `x-btn` + `x-btn-secondary`, `x-btn-warning`, `x-btn-glass`, `x-btn-sm`, `x-btn-lg` | buttons; `:disabled` is gray                      |
| `x-badge`, `x-badge-glass`                                                          | pill label, glass variant for the card head       |
| `x-box`                                                                             | monospace inset for code, URLs and IDs            |
| `x-tiles`, `x-tiles-2`, `x-tile`, `x-tile-green                                     | blue                                              | purple` | stat tiles, 3 or 2 per row, 2 per row under 480px |
| `x-dot`, `x-dot-live`, `x-dot-wait`, `x-state`                                      | status dot with label                             |
| `x-label`, `x-input`                                                                | form field                                        |
| `x-callout-warn`, `x-callout-error`                                                 | message blocks                                    |
| `x-rows`, `x-row`                                                                   | label, value and action rows                      |
| `x-details`, `x-summary`                                                            | disclosure with an Expand/Collapse chip           |
| `x-grid`, `x-stack`, `x-footer`                                                     | 1→2 column grid at 1024px, vertical stack, footer |

### Examples

```html
<button class="x-btn">Primary</button>
<button class="x-btn x-btn-secondary">Secondary</button>
<span class="x-badge">Badge</span>
<span class="x-state"><span class="x-dot x-dot-live"></span>Live</span>
```

```html
<div class="x-card">
  <div class="x-card-head">
    <div>
      <h3>Title <span class="x-badge x-badge-glass">New</span></h3>
      <p class="x-card-sub">Subtitle</p>
    </div>
    <button class="x-btn x-btn-glass">Action</button>
  </div>
  <div class="x-card-body">
    <div class="x-tiles">
      <div class="x-tile x-tile-green"><b>1,234</b>Count</div>
      <div class="x-tile x-tile-blue"><b>42</b>Active</div>
      <div class="x-tile x-tile-purple"><b>v1.0</b>Version</div>
    </div>
  </div>
</div>
```

```html
<label
  ><span class="x-label">Email</span><input class="x-input" type="email"></label
>
<div class="x-callout-warn">Keep this safe<small>Shown once.</small></div>
<div class="x-callout-error" role="alert">Something went wrong.</div>
```

## Conventions

- Focus is a 2px outline in the brand text colour; on the card head it uses `--on-brand`.
- No icon font. Use inline SVG.
- Body text is 16px/1.5 in the sans face; `x-box` and `<code>` use the mono face.

## Development

```sh
python3 -m http.server          # then open http://localhost:8000/
pnpm dlx @biomejs/biome format --write .
```

Screenshots in `docs/` are 1280px wide captures of `index.html` in each theme.

## License

MIT
