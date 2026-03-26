---
layout: post
title: "Haciendo MotoApp: Capturando Errores con Sentry"
date: 2019-07-10
canonical_url: "https://elcaminodelpro.wordpress.com/2019/07/10/haciendo-motoapp-capturando-errores-con-sentry/"
---

Cierre de la serie MotoApp. En esta entrega integramos Sentry para capturar errores automáticamente sin tener que revisar logs manualmente.

## Proceso de integración

1. Registrarse en Sentry y crear un proyecto para obtener el DSN.
2. Instalar la dependencia:

```bash
npm i sentry-expo --save
```

3. Configurar en `App.js`:

```javascript
import Sentry from 'sentry-expo';
Sentry.enableInExpoDevelopment = true;
Sentry.config('AQUIVAELDSN').install();
```

4. Configurar hooks en `app.json` para upload de sourcemaps.

## Error encontrado

Al ejecutar `expo publish` apareció: *"Unable to resolve module sentry-expo"*. La solución fue:

```bash
npm start --reset-cache
expo publish
```

## Aprendizajes de la serie MotoApp

A lo largo de los episodios trabajamos con: Firebase, Expo, React Native, Flexbox, JavaScript Intl y Sentry.
