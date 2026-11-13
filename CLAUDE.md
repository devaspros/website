# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
bundle install          # Install dependencies
bundle exec jekyll serve  # Start local dev server at http://localhost:4000
bundle exec jekyll build  # Build static site to _site/
```

## Architecture

This is a **Jekyll static site** for Dev As Pros (devaspros.com), a software development agency. It's built with GitHub Actions and served by GitHub Pages with a custom domain.

**Key directories:**
- `_layouts/` — Page templates: `default.html` (wraps most pages), `post.html` (blog posts), `links.html`
- `_includes/` — Reusable partials (nav, footer, contact form, head tags)
- `_sass/` — SCSS organized by page (`_home.scss`, `_services.scss`, etc.). Each file keeps its responsive rules at the end, after a `// ── Small screens` separator. Compiled with Dart Sass using the module system: every partial that uses variables starts with `@use "variables" as *;` (with `@use` nothing is global, so loading it once in `styles.scss` is not enough). Color helpers go through `sass:color` (`color.adjust(...)`), not the deprecated `darken()`/`lighten()`, and new code must not reintroduce `@import`
- `_projects/` — Casos de éxito as a Jekyll collection, published at `/casos-de-exito/<caso>/` (permalink in `_config.yml`). Each file is front matter + a short body rendered by `_layouts/caso.html`; optional fields (`reto`, `solucion`, `resultados`, `impacto`, `testimonio`, `capturas`, `servicios`, `duracion`) only render when present. Cards come from `_includes/tarjeta_caso.html`; tech names for the "Stack" field from `_data/tecnologias.yml` (no tech-logo section, by design). Old `/projects/...` and `/proyectos/` URLs redirect via `redirect_from` (jekyll-redirect-from). Every caso needs a fixed `date` (publication date) next to `last_modified_at`: without it Jekyll uses the build time, so `datePublished` changes on every deploy. `site.projects` is not sorted explicitly, so it follows `date` (oldest first), then filename.
- `_productos/` — Productos propios de Dev As Pros (Enlacito, Super Menú), no de clientes. Colección publicada en `/productos/<producto>/`, índice en `productos.html`, rendered by `_layouts/producto.html` (reusa las clases de `caso.html`, estilos extra en `_sass/_productos.scss`). Usan los colores de Dev As Pros, no los del producto; solo el logo trae color propio. Ordenados por `orden`. Igual que los casos, cada producto lleva `date` fijo (fecha de publicación). Precios en front matter (`precio`, `planes`, `ofertas` para el JSON-LD) y repetidos en `llms.txt`. Cards reuse `tarjeta_caso.html` with `etiqueta`/`enlace` params. Footer column lists them automatically; not in the top nav, by design
- `_posts/` — Blog posts
- `css/` — `styles.scss` loads every `_sass/` partial with `@use`; `links.scss` is standalone

**Theme:** none. `minima` was removed; every page declares its own layout from `_layouts/`, so a new page without `layout:` renders unstyled.

**Front-end stack:** Bootstrap 4.3.1, jQuery 3.3.1, SCSS compiled to compressed CSS.

**Content language:** Spanish (es).

**Jekyll:** 4.4.1, declared directly in the `Gemfile` (the `github-pages` gem is no longer used). Ruby version comes from `.ruby-version`.

**Jekyll plugins in use:** `jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-redirect-from`. Each must be in both the `Gemfile` (`:jekyll_plugins` group) and `plugins:` in `_config.yml`; nothing arrives implicitly anymore.

**Deployment:** Push to `master` → the `.github/workflows/jekyll.yml` workflow builds with `JEKYLL_ENV=production` and deploys to GitHub Pages (Pages source set to "GitHub Actions"), served at www.devaspros.com. It can also be run manually from the Actions tab. Production-only snippets (e.g. the counter.dev script) only appear when `JEKYLL_ENV=production`, so they are missing from a plain local `jekyll serve`.
