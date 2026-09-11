# AGENTS.md — print_page

## What this is

Single-page, self-contained HTML app for printing/downloading consignment notes (transport/logistics LR receipts). Company: Bharat Software Pvt Ltd.

## Tech stack

- **Zero tooling**: no build system, no package manager, no bundler, no tests, no linting.
- **Vanilla HTML/CSS/JS** — all inline in `index.html`.
- **External CDN deps** (loaded in `index.html`):
  - Font Awesome 6.5.1
  - html2canvas 1.4.1
  - jsPDF 2.5.1
- PDF generation is client-side only: html2canvas rasterizes the DOM → jsPDF renders A4 PDF.

## How to run

Open `index.html` in a browser. No server needed. Must be online for CDN deps and external images (logo, QR code).

## Key files

| File | Purpose |
|---|---|
| `index.html` | Main application — all HTML, CSS, and JS inline (618 lines) |
| `landing.html` | Draft/test page (not part of the app) |
| `css/` | Empty directory, unused |

## Architecture notes

- Layout uses `display: table` / `table-row` / `table-cell` CSS (not `<table>` elements) for print fidelity.
- `printDocument()` preloads remote images as data URLs before calling `window.print()`.
- `downloadPDF()` uses html2canvas at 2x scale → multi-page jsPDF with overflow handling.
- Images are loaded from external URLs (logo: `newversion.logisticsoftware.in`, QR: `api.qrserver.com`). No fallback if offline.
- Not a git repo. No CI/CD. No tests.
