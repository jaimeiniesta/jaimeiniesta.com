# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository is the source of `jaimeiniesta.com`, a single-page personal portfolio site for Jaime Iniesta (Senior Elixir Engineer). It is intentionally a **static site with no build system**.

## Architecture

- `index.html` — the entire site lives in this one file. All content sections (intro, Elixir/Phoenix, Rocket Validator, Ruby/Rails, contact) are hand-authored HTML.
- `img/` — static assets (SVG icons and avatar JPGs) referenced from `index.html` with relative paths (`./img/...`).
- **Styling**: Tailwind CSS 2.0.2 is loaded from `cdnjs.cloudflare.com` (`index.html:8`). There is **no local Tailwind config, no PostCSS, no build pipeline**. Class names must be valid for that CDN-served Tailwind 2.x version.
- **Analytics**: A Plausible-style script is loaded from `marca.lighthous.es` (`index.html:9`) — this is a custom-domain proxy, not a typo. Do not "fix" it.
- **Email obfuscation**: The contact email at `index.html:50-53` is assembled at runtime via inline JS with a `<noscript>` fallback. Preserve this pattern when editing the contact section.

## Working with the site

- **Local preview**: open `index.html` directly in a browser, or serve the directory with any static server (e.g. `python3 -m http.server`). There is no dev server, no hot reload, no tests, no linter configured.
- **Deployment**: deployment is handled outside this repo; commits to `master` are the source of truth.

## Commit conventions

- Per global user preference: **do not add `Co-Authored-By: Claude` or any AI attribution** to commit messages.
- Recent history uses short, lowercase, imperative subjects (e.g. `add Qoolife`, `update links to companies`, `refresh content, add avatar`). Match that style.
