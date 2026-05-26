# jaimeiniesta.com

Source for [jaimeiniesta.com](https://jaimeiniesta.com), Jaime Iniesta's personal site.

Built with [Eleventy](https://www.11ty.dev/) (Nunjucks templates) and [Tailwind CSS v4](https://tailwindcss.com/), deployed to [Netlify](https://www.netlify.com/).

## Develop

```sh
npm install
npm run dev
```

Opens `http://localhost:8080` with HTML and CSS rebuilding on save.

## Build

```sh
npm run build
```

Outputs the production site to `_site/`.

## Layout

- `src/` — source: templates, data, styles, images.
- `src/_data/site.json` — shared site data.
- `src/_includes/layouts/` — Nunjucks layouts.
- `src/assets/css/tailwind.css` — Tailwind entry.
- `src/img/` — static assets (copied through to `_site/img/`).
- `_site/` — build output (gitignored).

## Deploy

Netlify builds and deploys `master` automatically via `netlify.toml`.
