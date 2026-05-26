# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository is the source of `jaimeiniesta.com`, the personal portfolio site for Jaime Iniesta (Senior Elixir Engineer). It is built with **Eleventy (11ty)** using **Nunjucks** templates and a local **Tailwind CSS v4** build, deployed to **Netlify**.

## Architecture

- `src/` — source tree (the only place hand-authored content lives).
  - `src/index.njk` — homepage. Uses `layouts/base.njk` and pulls reusable values (email parts, social links, tagline) from `src/_data/site.json`.
  - `src/_includes/layouts/base.njk` — HTML shell: `<head>`, analytics script, the local stylesheet link, and the `{{ content | safe }}` slot.
  - `src/_data/site.json` — shared site data exposed to every template as `site.*`.
  - `src/assets/css/tailwind.css` — Tailwind entry. Single `@import "tailwindcss";` plus `@source` directives for `src/**/*.{njk,md,html}` and a small `@theme` block that defines `--leading-tightest` (the original site uses a `leading-tightest` utility that isn't part of stock Tailwind).
  - `src/img/` — static assets (SVG icons, avatar JPGs). Eleventy passes these through to `_site/img/` unchanged.
- `_site/` — build output. Gitignored. Never edit by hand.
- `.eleventy.js` — Eleventy config (ESM, because `package.json` sets `"type": "module"`). Declares input/output dirs and passthrough copy for images.
- `netlify.toml` — Netlify build config. Runs `npm run build`, publishes `_site`, pins Node 20.

## Commands

- `npm install` — install dependencies.
- `npm run build` — clean, build HTML with Eleventy, then build minified CSS with `@tailwindcss/cli`. Order matters: HTML first so Tailwind's CSS write doesn't get wiped by the Eleventy build cleaning `_site/`.
- `npm run dev` — runs `eleventy --serve` and `@tailwindcss/cli --watch` in parallel for local preview on `http://localhost:8080`.

## Deployment

Netlify builds and deploys `master` automatically via `netlify.toml`. Push to `master` (or open a PR for a deploy preview) — no other deploy step is required.

## Tailwind v4 notes

- No `tailwind.config.js`. All theme extensions live in `src/assets/css/tailwind.css` via `@theme`.
- Tailwind v4 has dropped/renamed a handful of utilities from the old Tailwind 2.x CDN this site used to load. If a class renders differently from the legacy site, add a fix in `tailwind.css` (either a `@theme` token or a small `@layer utilities` block) rather than reaching for a config file.
- `@source` directives in `tailwind.css` tell the CLI which template files to scan for class names.

## Analytics

The Plausible-style script in `base.njk` loads from `marca.lighthous.es` — that is a custom-domain proxy, **not a typo**. Do not "fix" it.

## Email obfuscation

The contact email in `src/index.njk` is assembled at runtime via a small inline `<script>` (`user + "@" + domain`) with a `<noscript>` fallback. The `user`/`domain` values are interpolated from `src/_data/site.json` at build time. Preserve this pattern when editing the contact section.

## Commit conventions

- **Do not add `Co-Authored-By: Claude` (or any other AI attribution) to commit messages.** Per global user preference, commits are authored solely by the human committer regardless of how much was AI-assisted.
- Recent history uses short, lowercase, imperative subjects (e.g. `add Qoolife`, `update links to companies`, `refresh content, add avatar`). Match that style.

## Out of scope (planned follow-ups)

The current site only has a homepage. Future PRs will add `src/projects/` (per-project pages), a `src/posts/` blog with an index, an RSS feed, and a sitemap. Do not scaffold those preemptively.
