# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

"סוד מדבר" (MOA Secret) — a static Hebrew (RTL) landing page for a desert retreat accommodation in Moa, Arava region, Israel. No build tools, no JavaScript framework, no package manager.

## Architecture

- **`index.html`** — Single-page site with all content (header, hero, about, accommodation, experience, dark section, dining, footer, restaurant modal)
- **`style.css`** — All styles; uses CSS custom properties defined in `:root` for the color palette and fonts
- **`assets/`** — Images (JPG/PNG) referenced directly from HTML
- **`.github/workflows/pages.yml`** — GitHub Pages deployment on push to `main`

## Development

No build step. Open `index.html` in a browser or use any local server:

```
python3 -m http.server 8000
```

## Key Conventions

- **RTL layout**: `<html lang="he" dir="rtl">` — all layout and text flows right-to-left
- **Fonts**: Heebo (body, Hebrew) + Playfair Display (serif headings) via Google Fonts
- **Color palette**: earthy tones defined as CSS custom properties (`--tobacco`, `--toast`, `--pampas`, `--wafer`, etc.)
- **No JS**: Interactivity is CSS-only (modal open/close via class toggle in inline `onclick`)
- **Responsive**: Three breakpoints — default (desktop), 768px (tablet), 480px (mobile)
- **Images**: Use `loading="lazy"` on below-fold images; aspect ratios set via CSS `aspect-ratio`
