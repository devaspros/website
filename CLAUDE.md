# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
bundle install          # Install dependencies
bundle exec jekyll serve  # Start local dev server at http://localhost:4000
bundle exec jekyll build  # Build static site to _site/
```

## Architecture

This is a **Jekyll static site** for Dev As Pros (devaspros.com), a software development agency. It's deployed via GitHub Pages with a custom domain.

**Key directories:**
- `_layouts/` — Page templates: `default.html` (wraps most pages), `post.html` (blog posts), `links.html`
- `_includes/` — Reusable partials (nav, footer, contact form, head tags)
- `_sass/` — SCSS organized by page (`_home.scss`, `_services.scss`, etc.). Each file keeps its responsive rules at the end, after a `// ── Small screens` separator
- `_projects/` — Casos de éxito as a Jekyll collection, published at `/casos-de-exito/<caso>/` (permalink in `_config.yml`). Each file is front matter + a short body rendered by `_layouts/caso.html`; optional fields (`reto`, `solucion`, `resultados`, `impacto`, `testimonio`, `capturas`, `servicios`, `duracion`) only render when present. Cards come from `_includes/tarjeta_caso.html`; tech names for the "Stack" field from `_data/tecnologias.yml` (no tech-logo section, by design). Old `/projects/...` and `/proyectos/` URLs redirect via `redirect_from` (jekyll-redirect-from)
- `_productos/` — Productos propios de Dev As Pros (Enlacito, Super Menú), no de clientes. Colección publicada en `/productos/<producto>/`, índice en `productos.html`, rendered by `_layouts/producto.html` (reusa las clases de `caso.html`, estilos extra en `_sass/_productos.scss`). Usan los colores de Dev As Pros, no los del producto; solo el logo trae color propio. Ordenados por `orden`. Precios en front matter (`precio`, `planes`, `ofertas` para el JSON-LD) y repetidos en `llms.txt`. Cards reuse `tarjeta_caso.html` with `etiqueta`/`enlace` params. Footer column lists them automatically; not in the top nav, by design
- `_posts/` — Blog posts
- `css/` — `styles.scss` imports everything from `_sass/`; `links.scss` is standalone

**Theme:** `minima`, set in `_config.yml`. Any page without an explicit layout falls back to it.

**Front-end stack:** Bootstrap 4.3.1, jQuery 3.3.1, SCSS compiled to compressed CSS.

**Content language:** Spanish (es).

**Jekyll plugins in use:** `jekyll-seo-tag`, `jekyll-sitemap`.

**Deployment:** Push to `master` branch → GitHub Pages auto-builds and serves at www.devaspros.com.
