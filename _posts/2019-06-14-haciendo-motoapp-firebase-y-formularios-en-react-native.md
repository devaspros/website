---
layout: post
title: "Haciendo MotoApp: Guardando Información en Firebase y Formularios en React Native"
date: 2019-06-14
canonical_url: "https://elcaminodelpro.wordpress.com/2019/06/14/haciendo-motoapp-guardando-informacion-en-firebase-y-formularios-en-react-native/"
---

Segunda entrega de la serie MotoApp, cubriendo la integración de Firebase y el manejo de formularios.

## Configuración Firebase

```javascript
import * as firebase from 'firebase';

const config = {
  apiKey,
  authDomain,
  databaseURL,
  projectId,
  storageBucket,
  messagingSenderId
};

firebase.initializeApp(config);

export const database = firebase.database();
export const auth = firebase.auth();
export const storage = firebase.storage();
```

## Formularios en React Native

React Native no tiene elementos de formulario nativos; se usan `View`, `TextInput` y `Button`. La validación es manual (Formik no tiene equivalente sólido en React Native).

Para guardar datos por usuario se usa el UID de Firebase. Para edición, `View` no soporta `onPress` — se usa `TouchableOpacity` en su lugar.
