# Sumedh J Jamadagni — portfolio

A single-page personal site for a systems / ML / compilers engineer. Dark, fast, and built
around a live 3D register file.

**Live:** https://optimis3r.github.io/fsd-portfolio-01/

## What it is

A futuristic systems console: a pointer-reactive WebGL register file in the hero, six
projects with real metrics, the stack, the record, and a contact channel. All content is
driven by `src/data/site.ts`.

## Stack

- **Astro 7** — static output, no client framework.
- **Three.js** — one instanced draw call: a 40×40 grid of cells displaced in a vertex
  shader, with pointer raycasting and scroll parallax. Lazy-loaded via `await import('three')`
  so it never blocks first paint.
- **Type** — Space Grotesk (display/UI) and JetBrains Mono (data/HUD labels), Google Fonts.
- **Hosting** — GitHub Pages, built and deployed by GitHub Actions
  (`.github/workflows/deploy.yml`).

The earlier React + Vite + Express assignment build is preserved under [`legacy/`](legacy/)
and is not part of the site.

## Interaction

- Compact custom cursor (20 px reticle) with magnetic buttons, fine pointers only.
- Pointer-tilt project cards with a tracking glare.
- Domain filter on the work grid.
- Scroll progress, section-aware HUD, reveal-on-scroll.
- All of the above are disabled under `prefers-reduced-motion: reduce`; the 3D scene
  renders one static frame, the cursor stays native, and tilt is off.

## Local development

```bash
npm install
npm run dev      # http://localhost:4321/fsd-portfolio-01/
npm run build    # static output in dist/
npm run preview  # serve the built site
npm run check    # Astro + TypeScript checks
```

## Deploying

The workflow builds on every push to `main` and publishes `dist/` to GitHub Pages. In the
repository settings, set **Pages → Source** to **GitHub Actions** once.

`astro.config.mjs` sets:

```js
site: 'https://optimis3r.github.io',
base: '/fsd-portfolio-01',
```

If the repository is renamed (for example to a user site served at the domain root),
update `base` to `'/'`.

## To finish before publishing

- **Contact form** — in `src/components/Contact.astro`, set `FORM_ENDPOINT` to a form
  service endpoint (e.g. `https://formspree.io/f/xxxxxxx`). Until then the form opens the
  visitor's mail app with the message pre-filled, so it works either way.
- **Résumé** — `public/Resume.pdf` is the current PDF. Replace it when the résumé changes.

## Content

All editable content lives in `src/data/site.ts`:

- `identity` — name, role, statement, bio, email, GitHub, location, education, CGPA.
- `stats` — the four hero figures.
- `projects` — six featured builds: summary, metrics, tech, repo URL, motif.
- `moreProjects` — the compact list below the grid.
- `skills` — the five capability groups.
- `timeline` — the record.

## Design

Near-black ground (`#05070a`), one phosphor-mint signal (`#5ef2c0`), cold graphite
surfaces, hairline structure and mono data labels. The page is meant to read like an
instrument panel for the work, not a template. The hero scene is the register file itself:
height is a field, the pointer is a probe, the tall cells light up.
