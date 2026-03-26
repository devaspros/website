---
layout: post
title: "Haciendo MotoApp: Flexbox en React Native, Intl y Publicar en Expo"
date: 2019-07-07
canonical_url: "https://elcaminodelpro.wordpress.com/2019/07/07/haciendo-motoapp-flexbox-en-react-native-intl-y-publicar-en-expo/"
---

Tercera entrega de la serie MotoApp.

## Flexbox en React Native

La diferencia clave respecto a la web: `flexDirection` tiene valor por defecto `column` (no `row`). Las propiedades se escriben en camelCase. Flexbox Froggy sirve para entender Flexbox, pero aplica para la web — en React Native hay que ajustar las expectativas.

## Problema con Intl de JavaScript

La clase `Intl` no estaba disponible nativamente en algunas plataformas. La solución:

```javascript
import 'intl';
import 'intl/locale-data/jsonp/en.js';
```

## Publicar en Expo

`expo publish` es sencillo pero requiere que los usuarios instalen la app de Expo. Se aceptó esta limitación para evitar la complejidad de Android Studio y Google Play.
