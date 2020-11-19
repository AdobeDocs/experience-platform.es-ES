---
title: Ejecución de comandos
seo-title: Ejecución de comandos de Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo ejecutar comandos del SDK web Experience Platform
seo-description: Obtenga información sobre cómo ejecutar comandos del SDK web Experience Platform
keywords: Executing commands;commandName;Promises;getLibraryInfo;response objects;consent;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---


# Ejecución de comandos

Una vez que el código base se haya implementado en la página web, puede empezar a ejecutar comandos con el SDK. No es necesario esperar a que el archivo externo (alloy.js) se cargue desde el servidor antes de ejecutar los comandos. Si el SDK no ha terminado de cargar el SDK, los comandos se ponen en cola y el SDK los procesa lo antes posible.

Los comandos se ejecutan con la siguiente sintaxis.

```javascript
alloy("commandName", options);
```

El `commandName` indica al SDK qué debe hacer, mientras que `options` son los parámetros y datos que desea pasar a un comando. Dado que las opciones disponibles dependen del comando, consulte la documentación para obtener más detalles sobre cada comando.

## Una nota sobre las promesas

[Las promesas](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Reference/Global_Objects/Promise) son fundamentales para la forma en que el SDK se comunica con el código de la página web. Una promesa es una estructura de programación común y no es específica de este SDK ni de JavaScript. Una promesa actúa como proxy para un valor que no se conoce cuando se crea la promesa. Una vez conocido el valor, la promesa se &quot;resuelve&quot; con el valor. Las funciones de controlador pueden asociarse con una promesa, de modo que se le puede notificar cuando la promesa se haya resuelto o cuando se haya producido un error en el proceso de resolución de la promesa. Para obtener más información sobre las promesas, lea [este tutorial](https://javascript.info/promise-basics) o cualquiera de los otros recursos de la web.

## Gestión de éxito o error {#handling-success-or-failure}

Cada vez que se ejecuta un comando, se devuelve una promesa. La promesa representa la finalización eventual del mando. En el ejemplo siguiente, puede utilizar `then` y `catch` métodos para determinar cuándo el comando se ha ejecutado correctamente o ha fallado.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Si saber cuándo se ejecuta correctamente el comando no es importante para usted, puede eliminar la `then` llamada.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Del mismo modo, si saber cuándo falla el comando no es importante para usted, puede eliminar la `catch` llamada.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Objetos de respuesta

Todas las promesas devueltas por los comandos se resuelven con un `result` objeto. El objeto result contendrá datos según el comando y el consentimiento del usuario. Por ejemplo, la información de biblioteca se pasa como una propiedad del objeto results en el siguiente comando.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(results.libraryInfo.version);
  });
```

### Consentimiento

Si un usuario no ha dado su consentimiento para un fin determinado, la promesa se resolverá; sin embargo, el objeto response sólo contendrá la información que se puede proporcionar en el contexto de lo que el usuario haya consentido.
