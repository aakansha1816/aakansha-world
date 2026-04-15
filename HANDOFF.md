# aakansha.world — Agent Handoff

## Overview

A **single-page marketing portfolio** for a marketing graduate, built with **Astro 6**, **Tailwind CSS 4**, **GSAP**, and **Lenis** smooth scroll. The site is statically generated (SSG) and designed to be deployed to any static host. The production domain is `https://aakansha.world`.

---

## Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Framework | Astro | ^6.1.6 |
| Styling | Tailwind CSS (via `@tailwindcss/vite`) | ^4.2.2 |
| Animation | GSAP + ScrollTrigger | ^3.15.0 |
| Smooth scroll | Lenis | ^1.3.23 |
| SEO | `@astrojs/sitemap` | ^3.7.2 |
| Node | Required >= 22.12.0 | |

---

## Getting Started

```bash
npm install
npm run dev       # dev server at localhost:4321
npm run build     # production build → ./dist/
npm run preview   # preview the build locally
```

---

## Project Structure

```
aakansha.world/
├── public/
│   ├── images/
│   │   ├── hero-placeholder.svg      ← REPLACE with real hero photo
│   │   └── person-silhouette.svg     ← REPLACE with real silhouette/photo
│   ├── favicon.ico
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── Navbar.astro              ← Fixed header, mobile hamburger menu, scroll-aware
│   │   ├── Hero.astro                ← Full-screen hero with large name typography
│   │   ├── About.astro               ← Skill map with SVG silhouette + GSAP path draw
│   │   ├── Works.astro               ← Project grid from content collection
│   │   ├── Blogs.astro               ← Blog listing from content collection, sorted by date
│   │   ├── Contact.astro             ← Contact form + footer
│   │   └── ScrollAnimations.astro    ← ALL GSAP/Lenis/ScrollTrigger logic lives here
│   ├── content/
│   │   ├── blogs/                    ← 6 markdown blog posts
│   │   └── works/                    ← 7 markdown case studies
│   ├── layouts/
│   │   └── Layout.astro              ← HTML shell, meta tags, fonts, JSON-LD
│   ├── pages/
│   │   ├── index.astro               ← Home (composes all section components)
│   │   ├── blogs/[slug].astro        ← Dynamic blog post detail page
│   │   └── works/[slug].astro        ← Dynamic work/case-study detail page
│   ├── styles/
│   │   └── global.css                ← Tailwind imports, custom theme colors + fonts
│   └── content.config.ts             ← Zod schemas for blogs & works collections
├── astro.config.mjs
├── tsconfig.json
└── package.json
```

---

## Design System

### Colors (defined in `src/styles/global.css` under `@theme`)

| Token | Value | Usage |
|-------|-------|-------|
| `burgundy` | `#560a17` | Primary background throughout |
| `burgundy-light` | `#74162d` | Hover / accent variant |
| `cream` | `#f1e4c6` | Primary text, headings |
| `olive` | `#88a201` | Accent (category labels, links) |
| `dark` | `#0a0a0a` | Unused currently |

### Fonts (loaded via Google Fonts in `Layout.astro`)

- **Headings**: `Playfair Display` (serif) — variable `--font-heading`
- **Body**: `Space Grotesk` (sans-serif) — variable `--font-body`

### Aesthetic

Dark, editorial, luxury feel. Deep burgundy background, warm cream text, olive-green accents. Heavy use of uppercase tracking on labels. Minimalist layout with generous whitespace.

---

## Content Collections

Defined in `src/content.config.ts` using Astro's glob loader.

### `blogs` — `src/content/blogs/*.md`

Frontmatter schema:
```yaml
title: "string"
date: "Mon YYYY"      # e.g. "Mar 2026" — parsed for sorting
excerpt: "string"
```

### `works` — `src/content/works/*.md`

Frontmatter schema:
```yaml
title: "string"
category: "string"        # e.g. "Integrated Campaign"
description: "string"
color: "string"           # Tailwind bg class, e.g. "bg-cream/10"
```

---

## Animations (ScrollAnimations.astro)

All animation logic is centralized in `src/components/ScrollAnimations.astro`. This is a `<script>` tag that runs client-side. Key behaviors:

1. **Lenis** smooth scroll is initialized globally and wired to GSAP ticker.
2. **Hero**: staggered entrance animation on page load (navbar fade → name lines slide up → hero image → bottom links).
3. **About**: SVG silhouette path-draw on scroll, skill items animate in from sides.
4. **Works**: heading + cards fade/slide up with stagger.
5. **Blogs**: heading fades up, cards slide in from alternating sides.
6. **Contact**: heading, subtitle, form all fade up in sequence.
7. **Hero parallax**: hero image moves up on scroll.

Anchor links (`href="#section"`) are intercepted and smooth-scrolled via Lenis.

---

## Placeholder Content — What Needs Replacing

The site is scaffolded with placeholder content. Here is everything that needs to be personalized:

### Identity (search for `YOUR NAME`)
- `src/layouts/Layout.astro` — page title, meta description, JSON-LD `name`, `jobTitle`, `sameAs` (LinkedIn URL)
- `src/components/Hero.astro` — the two `<span>` elements showing the name ("YOUR" / "NAME")
- `src/components/Contact.astro` — footer copyright text
- `src/pages/blogs/[slug].astro` — `<title>` tag
- `src/pages/works/[slug].astro` — `<title>` tag

### Logo / Brand Mark (search for `AB.`)
- `src/components/Navbar.astro` — nav brand link text
- `src/components/Contact.astro` — footer brand
- `src/pages/blogs/[slug].astro` — footer brand
- `src/pages/works/[slug].astro` — footer brand

### Links
- `src/components/Hero.astro` — LinkedIn URL (`href="https://linkedin.com"`), Resume link
- `src/components/Contact.astro` — footer LinkedIn, email (`hello@example.com`), Resume link
- `src/layouts/Layout.astro` — `sameAs` array in JSON-LD

### Images
- `public/images/hero-placeholder.svg` — replace with a real hero photo/image
- `public/images/person-silhouette.svg` — replace or keep the SVG silhouette in About section
- `public/images/og-image.png` — **does not exist yet**, needs to be created for Open Graph

### About Section Bio
- `src/components/About.astro` — two `<p>` tags contain lorem ipsum mixed with generic copy

### Blog & Work Content
- All markdown files in `src/content/blogs/` and `src/content/works/` contain a mix of real structure and lorem ipsum filler. The structure/formatting is good; the body text should be replaced with real content.

### Contact Form
- `src/components/Contact.astro` — the `<form>` has `action="#"`. Needs a real backend (Formspree, Netlify Forms, etc.) or client-side handling.

---

## Known Issues / Incomplete Items

1. **No `og-image.png`** — referenced in `Layout.astro` but missing from `public/images/`.
2. **Contact form is non-functional** — `action="#"`, no submission handler.
3. **No 404 page** — Astro supports `src/pages/404.astro`.
4. **Footer is duplicated** — the footer markup is repeated in `Contact.astro`, `blogs/[slug].astro`, and `works/[slug].astro` instead of being a shared component.
5. **No mobile menu close animation** — the hamburger icon doesn't animate to an X.
6. **Blogs date sorting** is brittle — relies on `"Mon YYYY"` string parsing.
7. **No analytics** — no Google Analytics, Plausible, etc.
8. **No sitemap configuration** — the `@astrojs/sitemap` integration is installed but uses defaults.

---

## Suggested Next Steps

1. Replace all placeholder text (`YOUR NAME`, `AB.`, lorem ipsum, URLs).
2. Add real images (hero photo, og-image, optional work thumbnails).
3. Wire up the contact form to a backend service.
4. Extract the footer into a shared `Footer.astro` component.
5. Add a 404 page.
6. Add analytics.
7. Deploy (Vercel, Netlify, or Cloudflare Pages all work with `npm run build`).

---

## Deployment

Astro produces a fully static site in `./dist/`. Any static host works:

```bash
npm run build   # outputs to dist/
```

For Vercel/Netlify, just connect the repo — they auto-detect Astro and use `npm run build` with `dist` as the output directory.
