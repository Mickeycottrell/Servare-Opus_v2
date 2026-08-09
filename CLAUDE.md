# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A marketing/brochure site for Servare Opus, a fractional executive-assistant-for-CEOs consulting business. Built with [Astro](https://astro.build) as a static site (no server/backend required). Pages: Home, Services, About, Blog, Booking (Cal.com embed), Contact (Formspree form).

## Commands

```
npm install       # install dependencies
npm run dev        # start local dev server (usually http://localhost:4321)
npm run build       # build static site to dist/
npm run preview      # preview the production build locally
```

There is no test suite, linter, or type-checker configured in this repo.

## Architecture

- Astro project using file-based routing under `src/pages/`. Each `.astro` file (or directory with `index.astro`) becomes a route.
- `src/layouts/Layout.astro` is the single shared layout — it renders the `<head>`, site header/nav, footer, and imports `src/styles/global.css`. Every page wraps its content in `<Layout title="..." description="...">`.
- Blog posts are Markdown files in `src/content/blog/`, defined as an Astro Content Collection. The schema (`title`, `description`, `pubDate`, `author`) lives in `src/content/config.ts`. `src/pages/blog/index.astro` lists posts; `src/pages/blog/[...slug].astro` renders individual posts via `getStaticPaths()` + `getCollection('blog')`. Adding a new post is just adding a new `.md` file with the right frontmatter — no route code changes needed.
- Styling is plain CSS, no framework. All design tokens (colors, radius) are CSS custom properties defined at the top of `src/styles/global.css` (`--navy`, `--gold`, `--cream`, etc.). There's no component-scoped styling system in use beyond Astro's default scoped `<style>` blocks where present.
- No client-side JS/interactivity framework is wired in (no React/Vue/Svelte integration in `astro.config.mjs`) — pages are static HTML/CSS.

## Third-party integration placeholders

Two pages currently contain placeholder values that must be swapped for the site to function for real users — check for these before treating booking/contact as "done":

- `src/pages/booking.astro`: Cal.com iframe `src` is `https://cal.com/your-username/discovery-call?embed=true` — needs a real Cal.com booking link.
- `src/pages/contact.astro`: Formspree form `action` is `https://formspree.io/f/YOUR_FORM_ID` — needs a real Formspree form ID.

Both pages render a visible "Setup note" box pointing this out to non-technical users; don't remove those notes unless the real values have been filled in.

## Deployment

Static output (`npm run build` → `dist/`), intended for Netlify or Vercel (build command `npm run build`, publish directory `dist`). `astro.config.mjs` sets `site: 'https://servareopus.com'` for canonical URL/sitemap generation.
