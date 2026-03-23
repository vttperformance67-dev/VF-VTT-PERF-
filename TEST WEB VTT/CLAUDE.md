# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**VTT Performance** — a French bicycle shop web application (Ingwiller, Alsace). It is a single-file vanilla HTML/CSS/JavaScript SPA with no build system.

- Main file: `../INDEX.HTML` (the parent directory `WEB VTT PERFORMANCE/`)
- `TEST WEB VTT/` is a scaffolding directory with empty placeholder files (`index.html`, `script.js`, `style.css`) and an empty `vtt-performance-site/` folder — intended for a future refactored version

## Running the Application

Open `INDEX.HTML` directly in a browser — no build step, no server required.

## Tech Stack

- **Vanilla HTML5 + JavaScript** (no framework)
- **Tailwind CSS v3.4.17** (CDN)
- **Lucide Icons v0.263.0** (CDN)
- **Google Fonts**: Rajdhani (headings), Exo 2 (body)
- All dependencies loaded via CDN — no `package.json`

## Architecture

`INDEX.HTML` is ~1250 lines with everything inline:

1. **HTML structure** — sections: `#accueil`, `#catalogue`, `#rendez-vous`, `#stock`, `#commandes`
2. **Embedded `<style>`** — Tailwind config + custom CSS (dark theme, animations)
3. **Embedded `<script>`** — all application logic

### JavaScript Structure

```
defaultConfig          — UI/store config defaults (store name, slogan, colors)
allRecords []          — data synced from window.dataSdk
cart []                — shopping cart state

// SDK integration hooks
window.elementSdk      — UI/config customization
window.dataSdk         — CRUD persistence (create/update/delete/list)

// Main functions
showSection(id)        — SPA navigation between sections
renderCatalog(filter)  — render product grid (catalog)
renderStockTable()     — render inventory table
renderOrdersList()     — render orders + appointments list
submitStock(e)         — save/update stock item via dataSdk
submitOrder(e)         — submit order via dataSdk
submitAppointment(e)   — submit appointment via dataSdk
showToast(msg, type)   — toast notifications
```

### SDK Integration Pattern

The app is designed to plug into two external SDKs (currently stubs):
- `window.elementSdk.onConfigChange(config)` — fires when store config changes
- `window.dataSdk.create/update/delete/list` — backend persistence
- Without SDK, data is ephemeral (in-memory `allRecords` array)

### Data Model

All records share one flat array (`allRecords`). Records are distinguished by `type`:
- `type: 'stock'` — inventory items (name, category, quantity)
- `type: 'order'` — customer orders (product, customer info, status)
- `type: 'appointment'` — bookings (name, email, date, appointmentType)

## Design System

- **Dark theme**: background `#0a1628`, surface `#0f2341`, accent `#afd5eb`
- **Primary action**: blue gradient (`#2563eb → #0ea5e9`)
- **CTA / status**: orange `#ff6b35`
- Stock status thresholds: `< 5` → low (red), `< 10` → medium (orange), `≥ 10` → high (green)

## Language

All UI text is in **French**.
