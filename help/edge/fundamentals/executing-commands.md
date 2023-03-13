---
title: Ejecutar comandos del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo ejecutar comandos de SDK web de Experience Platform
keywords: Ejecutar comandos;commandName;Promesas;getLibraryInfo;objetos de respuesta;consentimiento;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# Ejecutar comandos


Una vez implementado el código base en la página web, puede empezar a ejecutar comandos con el SDK. No es necesario esperar al archivo externo (`alloy.js`) cargarse desde el servidor antes de ejecutar comandos. Si el SDK no ha terminado de cargarse, los comandos se ponen en cola y el SDK los procesa lo antes posible.

Los comandos se ejecutan con la siguiente sintaxis.

```javascript
alloy("commandName", options);
```

El `commandName` indica al SDK qué debe hacer, mientras que `options` son los parámetros y datos que desea pasar a un comando. Dado que las opciones disponibles dependen del comando, consulte la documentación para obtener más detalles sobre cada comando.

## Una nota sobre las promesas

[Promesas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) son fundamentales para la comunicación del SDK con el código de la página web. Una promesa es una estructura de programación común y no es específica de este SDK o incluso JavaScript. Una promesa actúa como un proxy para un valor que no se conoce cuando se crea la promesa. Una vez conocido el valor, la promesa se &quot;resuelve&quot; con el valor. Las funciones de controlador se pueden asociar a una promesa para que se le pueda notificar cuando se haya resuelto la promesa o cuando se haya producido un error en el proceso de resolución de la promesa. Para obtener más información sobre las promesas, lea [este tutorial](https://javascript.info/promise-basics) o cualquiera de los demás recursos de la web.

## Gestión del éxito o el fracaso {#handling-success-or-failure}

Cada vez que se ejecuta un comando, se devuelve una promesa. La promesa representa la eventual finalización del comando. En el ejemplo siguiente, puede utilizar `then` y `catch` métodos para determinar si el comando se ha ejecutado correctamente o no.

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

Si no le importa saber cuándo se ejecuta correctamente el comando, puede quitar la variable `then` llamada.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Del mismo modo, si no le importa saber cuándo falla el comando, puede quitar la variable `catch` llamada.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Objetos Response

Todas las promesas devueltas por los comandos se resuelven con una `result` objeto. El objeto de resultado contendrá datos según el comando y el consentimiento del usuario. Por ejemplo, la información de biblioteca se pasa como propiedad del objeto results en el siguiente comando.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Consentimiento

Si un usuario no ha dado su consentimiento para un fin determinado, la promesa se resolverá; sin embargo, el objeto de respuesta solo contendrá la información que se puede proporcionar en el contexto de lo que el usuario ha consentido.
