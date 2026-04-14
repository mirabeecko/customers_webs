# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## What This Repo Is

A collection of 13 pre-built, production-ready landing pages for various service industries (hairdresser, law firm, bistro, fitness studio, etc.), hosted as static files on Vercel. There is no build step at the repo level — the React/Vite projects have already been compiled and their output is committed.

## Deployment

```bash
# Deploy to preview
vercel

# Deploy to production
vercel --prod
```

Vercel config (`vercel.json`) enables clean URLs and disables trailing slashes. No environment variables are needed.

## Project Structure

Two types of sites coexist:

### Pre-built React + Vite (reference/01–08)
Each subdirectory under `reference/` is a self-contained static SPA:
- `index.html` — thin shell that loads the bundle
- `assets/index-<hash>.js` — minified React app
- `assets/index-<hash>.css` — bundled styles

**The source code is not in this repo.** These are build artifacts. To modify a React site, you'd need to find its original Vite project, edit it there, rebuild, and replace the `assets/` files here.

### Plain HTML + CSS (root level)
- `index.html` — the master catalog/landing page listing all 13 demos
- `freelancer/index.html`, `kadernictvi/index.html` — standalone pages
- `demo1-web24hodin.html`, `demo2-autoservis.html`, `demo3-ninja-vikend.html` — standalone pages

These are fully editable single-file sites with inline CSS and minimal vanilla JS (scroll animations via IntersectionObserver, accordion toggles).

## Common Patterns in HTML Sites

- Google Fonts loaded via `<link>` (Playfair Display, Inter, Syne)
- Scroll-reveal animations using `IntersectionObserver`
- No external JS dependencies — everything is inline
- Forms are client-side only; no backend or form submission endpoint

## Adding a New Demo Site

1. Create the HTML file (or directory with `index.html`) following existing patterns
2. Add a card for it in the master `index.html` catalog
3. Vercel's `cleanUrls: true` setting will automatically serve it without the `.html` extension
