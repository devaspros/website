---
layout: post
title: "Haciendo MotoApp: UI en React Native"
date: 2019-04-10
canonical_url: "https://elcaminodelpro.wordpress.com/2019/04/10/haciendo-motoapp-ui-en-react-native/"
---

En esta entrega buscábamos que la app tuviera aspecto nativo Android con Material Design. Descubrimos **React Native Paper**, una colección de componentes que implementan el estándar de Google — exactamente lo que necesitábamos.

## Autenticación con Firebase

```javascript
auth.createUserWithEmailAndPassword(email, password)
  .then(user => this.props.navigation.navigate('Main'))
  .catch(error => this.setState({ errorMessage: error.message }));
```

## Error frustrante

*"Unable to resolve module some-module"* que resultó ser un typo sencillo:

```javascript
// Incorrecto
import algo from 'algo;'

// Correcto
import algo from 'algo';
```

El linter (StandardJS en VS Code) no lo detectó. Una advertencia para tener paciencia con los mensajes de error de React Native — muchas veces el problema es más simple de lo que parece.
