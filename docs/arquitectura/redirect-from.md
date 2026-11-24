# Redirects con `redirect_from`

`redirect_from` viene del plugin `jekyll-redirect-from`. Hace falta porque GitHub Pages solo sirve archivos estáticos y no permite configurar redirects en el servidor (no hay `.htaccess` ni reglas de nginx).

## Qué hace

Por cada URL que se pone en `redirect_from`, el plugin genera en el build un archivo HTML adicional en esa ruta vieja, cuyo único trabajo es mandar al visitante a la página nueva.

Por ejemplo, en `nosotros.html`:

```yaml
redirect_from: /nosotros.html
```

Jekyll construye la página normal en `_site/nosotros/index.html`, y el plugin genera además `_site/nosotros.html` con esto:

```html
<!DOCTYPE html>
<html lang="en-US">
  <meta charset="utf-8">
  <title>Redirecting&hellip;</title>
  <link rel="canonical" href="https://www.devaspros.com/nosotros/">
  <script>location="https://www.devaspros.com/nosotros/"</script>
  <meta http-equiv="refresh" content="0; url=https://www.devaspros.com/nosotros/">
  <meta name="robots" content="noindex">
  <h1>Redirecting&hellip;</h1>
  <a href="https://www.devaspros.com/nosotros/">Click here if you are not redirected.</a>
</html>
```

## Qué hace cada parte

- `<script>location=...`: el navegador redirige al instante con JavaScript.
- `<meta http-equiv="refresh" content="0; ...">`: lo mismo sin JavaScript, después de 0 segundos.
- `<link rel="canonical">`: le indica a Google que la URL buena es la nueva.
- `noindex`: evita que la página puente se indexe. Por eso Search Console muestra estas URLs en "Excluded by noindex tag", y eso es lo esperado.
- El enlace "Click here": respaldo por si nada de lo anterior funciona.

## Cómo lo ve Google

El servidor responde 200 con ese HTML, no un 301 real. Aun así, Google trata un meta refresh de 0 segundos como un redirect permanente. Sigue a la URL nueva y le transfiere las señales de la vieja (enlaces externos, historial). Un 301 real sería algo más directo, pero en GitHub Pages esto es lo mejor disponible.

## Uso

- Acepta una URL o una lista:

  ```yaml
  redirect_from:
    - /projects/lupita/
    - /projects/lupita.html
  ```

- Si la ruta termina en `/` (como `/projects/lupita/`), genera `projects/lupita/index.html`. Si termina en `.html`, genera ese archivo tal cual.
- No poner en `redirect_from` una ruta donde ya existe una página real, porque los dos archivos chocan en el build.
- Existe lo contrario, `redirect_to: https://...`, para que una página entera mande a otra URL, incluso de otro sitio.
- Para que funcione, el plugin tiene que estar en el `Gemfile` (grupo `:jekyll_plugins`) y en `plugins:` de `_config.yml`.

## Dónde se usa en este sitio

- URLs `.html` anteriores a `permalink: pretty`: el 20 de agosto de 2026 las URLs pasaron de `/pagina.html` a `/pagina/`. Las páginas, posts y casos que existían antes llevan su URL `.html` vieja en `redirect_from` para que no den 404. Contenido nuevo no lo necesita, porque nunca tuvo URL `.html`.
- Casos de éxito: las URLs viejas `/projects/<caso>/` y `/projects/<caso>.html` redirigen a `/casos-de-exito/<caso>/`.
- `/proyectos/` redirige a `/casos-de-exito/` (en `casos-de-exito.html`).

Contenido eliminado (por ejemplo, un caso que se quitó) no lleva redirect. Un 404 es la respuesta correcta cuando no hay una página equivalente, y redirigir a una página sin relación Google lo trata como un 404 de todos modos.
