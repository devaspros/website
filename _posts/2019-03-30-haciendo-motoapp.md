---
layout: post
title: "Haciendo MotoApp"
date: 2019-03-30
canonical_url: "https://elcaminodelpro.wordpress.com/2019/03/30/haciendo-motoapp/"
---

![Tablero Trello de MotoApp](https://elcaminodelpro.wordpress.com/wp-content/uploads/2019/03/tablero-motoapp-terminado.png)

MotoApp es una aplicación para llevar registro de recorridos en moto, desarrollada con React Native + Firebase usando Expo.

## ¿Por qué React Native?

React Native permite crear aplicaciones móviles híbridas escritas en JavaScript/CSS que se exportan a código nativo. Ideal para moverse rápido sin aprender dos plataformas distintas.

## Organización

Usamos Trello con un listado de requerimientos y propuesta de tecnologías antes de escribir una línea de código.

## Expo

Herramienta que simplifica el desarrollo en React Native evitando instalar Android Studio — una diferencia enorme en velocidad de inicio.

## Problema con Firebase

No se podía usar `react-native-firebase` por limitantes de Expo. La solución fue usar el módulo `firebase` directamente:

```bash
yarn add firebase
```

```javascript
import * as firebase from 'firebase';

firebase.initializeApp(config);

export const database = firebase.database();
export const auth = firebase.auth();
export const storage = firebase.storage();
```
