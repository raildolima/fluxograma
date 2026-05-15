# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Project

No build step. Open `index.html` directly in a browser, or serve with any static server:
```
npx serve .
python -m http.server
```

## Architecture

Single-page app with no framework, no bundler, no backend.

**Key files:**
- `index.html` — production version (Lucide icons, Poppins/Inter fonts)
- `uploads/index.html` — older iteration (Font Awesome, Roboto font); same core logic
- `assets/` — UFMS logos only

**Everything lives in `index.html`:**
- Lines 1–530: HTML structure (sidebar, canvas, panels, tooltip)
- Lines 531–690: Inline CSS (CSS custom properties for UFMS colors)
- Lines 691–1351: Inline JS, organized in numbered sections via comments:
  1. `DADOS` — course database (47 disciplines + 3 institutional, `prerequisites` array)
  2. `PROGRESSO` — localStorage persistence (key: `fluxograma_ufms_cpar_2026`)
  3. `LAYOUT` — node positioning algorithm
  4. `INICIALIZAÇÃO` — Cytoscape.js graph setup and style definitions
  5. `HIGHLIGHT` — prerequisite/dependent visual highlighting
  6. `PAINEL` — right-side detail drawer interactions
  7. `PROGRESSO` — completion toggle logic
  8. `MEU SEMESTRE` — semester filter
  9. `FILTRO` — category filter
  10. `CONTROLES` — reset/fit-view buttons
  11. `MOBILE` — sidebar toggle

## Data Model

```javascript
// Course node
{ id: 's1_1', label: 'Short Name', full: 'Full Name', h: 75, cat: 'basica', sem: 1, ementa: '...' }

// Categories: 'basica' | 'especifica' | 'pratica' | 'institucional'
// Prerequisites: array of { source: 'sX_Y', target: 'sX_Y' }
```

## External Dependencies (CDN only)

- Cytoscape.js v3.26.0 (graph rendering)
- Lucide icons (main) / Font Awesome 6.4.0 (uploads version)
- Google Fonts (Poppins, Inter, JetBrains Mono)

## State Persistence

Progress stored in `localStorage` under key `fluxograma_ufms_cpar_2026`. No server, no login.
