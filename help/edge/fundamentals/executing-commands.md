---
title: Ejecución de comandos
seo-title: Ejecución de los comandos del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo ejecutar los comandos del SDK web de la plataforma de experiencia
seo-description: Obtenga información sobre cómo ejecutar los comandos del SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Ejecución de comandos

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Una vez que el código base se haya implementado en la página web, puede empezar a ejecutar comandos con el SDK. No es necesario esperar a que el archivo externo \(`alloy.js`\) se cargue desde el servidor antes de ejecutar los comandos. Si el SDK no ha terminado de cargar el SDK, los comandos se ponen en cola y el SDK los procesa lo antes posible.

Los comandos se ejecutan con la siguiente sintaxis.

```javascript
alloy("commandName", options);
```

El `commandName` indica al SDK qué debe hacer, mientras que `options` son los parámetros y datos que desea pasar a un comando. Dado que las opciones disponibles dependen del comando, consulte la documentación para obtener más detalles sobre cada comando.

## Una nota sobre las promesas

[Las promesas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) son fundamentales para la forma en que el SDK se comunica con el código de la página web. Una promesa es una estructura de programación común y no es específica de este SDK ni de JavaScript. Una promesa actúa como proxy para un valor que no se conoce cuando se crea la promesa. Una vez conocido el valor, la promesa se &quot;resuelve&quot; con el valor. Las funciones de controlador pueden asociarse con una promesa, de modo que se le puede notificar cuando la promesa se haya resuelto o cuando se haya producido un error en el proceso de resolución de la promesa. Para obtener más información sobre las promesas, lea [este tutorial](https://javascript.info/promise-basics) o cualquiera de los otros recursos de la web.

## Gestión de éxito o error

Cada vez que se ejecuta un comando, se devuelve una promesa. La promesa representa la finalización eventual del mando. En el ejemplo siguiente, puede utilizar `then` y `catch` métodos para determinar cuándo el comando se ha ejecutado correctamente o ha fallado.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Si saber cuándo se ejecuta correctamente el comando no es importante para usted, puede eliminar la `then` llamada.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Del mismo modo, si saber cuándo falla el comando no es importante para usted, puede eliminar la `catch` llamada.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## Supresión de errores

Si se rechaza la promesa y no se ha agregado una `catch` llamada, el error &quot;se propaga&quot; y se registra en la consola del desarrollador del explorador, independientemente de si el registro está habilitado en el SDK web de Adobe Experience Platform. Si le preocupa esto, puede establecer la opción de configuración en la `suppressErrors` configuración `true` como se describe en [Configuración del SDK](configuring-the-sdk.md).
