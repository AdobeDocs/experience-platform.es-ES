---
title: Enlaces de monitorización para Adobe Experience Platform Web SDK
description: Aprenda a utilizar los enlaces de monitorización que proporciona Adobe Experience Platform Web SDK para depurar la implementación y capturar los registros de SDK web.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# Monitorización de vínculos para Web SDK

Adobe Experience Platform Web SDK incluye vínculos de monitorización que puede utilizar para monitorizar varios eventos del sistema. Estas herramientas son útiles para desarrollar sus propias herramientas de depuración y capturar registros de Web SDK.

Web SDK almacena en déclencheur las funciones de supervisión independientemente de si ha habilitado la [depuración](commands/configure/debugenabled.md).

## `onInstanceCreated` {#onInstanceCreated}

Esta función de llamada de retorno se activa cuando se ha creado correctamente una nueva instancia de Web SDK. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.instance` | Función | Función de instancia utilizada para llamar a comandos de Web SDK. |

## `onInstanceConfigured` {#onInstanceConfigured}

Web SDK activa esta función de devolución de llamada cuando el comando [`configure`](commands/configure/overview.md) se resuelve correctamente. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.config` | Objeto | Objeto que contiene la configuración utilizada para la instancia de Web SDK. Estas son las opciones pasadas al comando [`configure`](commands/configure/overview.md) con todos los valores predeterminados agregados. |

## `onBeforeCommand` {#onBeforeCommand}

Web SDK activa esta función de llamada de retorno antes de ejecutar cualquier otro comando. Puede utilizar esta función para recuperar las opciones de configuración de un comando específico. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.commandName` | Cadena | Nombre del comando Web SDK antes del cual se ejecuta esta función. |
| `data.options` | Objeto | Objeto que contiene las opciones pasadas al comando Web SDK. |

## `onCommandResolved` {#onCommandResolved}

Esta función de llamada de retorno se activa al resolver las promesas de comandos. Puede utilizar esta función para ver las opciones y el resultado del comando. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.commandName` | Cadena | Nombre del comando ejecutado de Web SDK. |
| `data.options` | Objeto | Objeto que contiene las opciones pasadas al comando Web SDK. |
| `data.result` | Objeto | Objeto que contiene el resultado del comando Web SDK. |

## `onCommandRejected` {#onCommandRejected}

Esta función de llamada de retorno se activa antes de que se rechace una promesa de comando y contiene información sobre el motivo por el que se rechazó el comando. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.commandName` | Cadena | Nombre del comando ejecutado de Web SDK. |
| `data.options` | Objeto | Objeto que contiene las opciones pasadas al comando Web SDK. |
| `data.error` | Objeto | Objeto que contiene el mensaje de error devuelto por la llamada de red del explorador (`fetch` en la mayoría de los casos), junto con el motivo por el que se rechazó el comando. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Esta función de llamada de retorno se activa antes de que se ejecute una solicitud de red. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.requestId` | Cadena | `requestId` generado por Web SDK para habilitar la depuración. |
| `data.url` | Cadena | La dirección URL solicitada. |
| `data.payload` | Objeto | Objeto de carga de solicitud de red que se convertirá al formato JSON y se enviará en el cuerpo de la solicitud, a través de un método `POST`. |

## `onNetworkResponse` {#onNetworkResponse}

Esta función de llamada de retorno se activa cuando el explorador recibe una respuesta. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.requestId` | Cadena | `requestId` generado por Web SDK para habilitar la depuración. |
| `data.url` | Cadena | La dirección URL solicitada. |
| `data.payload` | Objeto | El objeto de carga útil que se convertirá al formato JSON y se enviará en el cuerpo de la solicitud, a través de un método `POST`. |
| `data.body` | Cadena | El cuerpo de respuesta en formato de cadena. |
| `data.parsedBody` | Objeto | Objeto que contiene el cuerpo de respuesta analizado. Si se produce un error al analizar el cuerpo de respuesta, este parámetro es indefinido. |
| `data.status` | Cadena | El código de respuesta en formato entero. |
| `data.retriesAttempted` | Entero | El número de reintentos realizados al enviar la solicitud. Cero significa que la solicitud se realizó correctamente en el primer intento. |

## `onNetworkError` {#onNetworkError}

Esta función de llamada de retorno se activa cuando falla la solicitud de red. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.requestId` | Cadena | `requestId` generado por Web SDK para habilitar la depuración. |
| `data.url` | Cadena | La dirección URL solicitada. |
| `data.payload` | Objeto | El objeto de carga útil que se convertirá al formato JSON y se enviará en el cuerpo de la solicitud, a través de un método `POST`. |
| `data.error` | Objeto | Objeto que contiene el mensaje de error devuelto por la llamada de red del explorador (`fetch` en la mayoría de los casos), junto con el motivo por el que se rechazó el comando. |

## `onBeforeLog` {#onBeforeLog}

Esta función de llamada de retorno se activa antes de que Web SDK registre algo en la consola. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.componentName` | Cadena | Nombre del componente que generó el mensaje de registro. |
| `data.level` | Cadena | El nivel de registro. Niveles compatibles: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Matriz de cadenas | Los argumentos del mensaje de registro. |


## `onContentRendering` {#onContentRendering}

El componente `personalization` activa esta función de llamada de retorno en varias fases de la representación. La carga útil puede variar según el parámetro `status`. Consulte el ejemplo siguiente para obtener más información sobre los parámetros de función.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.componentName` | Cadena | Nombre del componente que generó el mensaje de registro. |
| `data.payload` | Objeto | El objeto de carga útil que se convertirá al formato JSON y se enviará en el cuerpo de la solicitud, a través de un método `POST`. |
| `data.status` | Cadena | El componente `personalization` notifica al Web SDK del estado de la representación.  Valores compatibles: <ul><li>`rendering-started`: indica que Web SDK está a punto de procesar propuestas. Antes de que Web SDK empiece a procesar una vista o un ámbito de decisión, en el objeto `data` puede ver las propuestas que van a representar el componente `personalization` y el nombre del ámbito.</li><li>`no-offers`: indica que no se recibió carga útil para los parámetros solicitados.</li> <li>`rendering-failed`: indica que Web SDK no pudo procesar una propuesta.</li><li>`rendering-succeeded`: indica que se ha completado el procesamiento para un ámbito de decisión.</li> <li>`rendering-redirect`: indica que Web SDK procesará una propuesta de redirección.</li></ul> |

## `onContentHiding` {#onContentHiding}

Esta función de llamada de retorno se activa cuando se aplica o elimina un estilo de ocultamiento previo.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|----------|
| `data.instanceName` | Cadena | Nombre de la variable global donde se almacena la instancia de Web SDK. |
| `data.componentName` | Cadena | Nombre del componente que generó el mensaje de registro. |
| `data.status` | Cadena | El componente `personalization` notifica al Web SDK del estado de la representación. Valores compatibles: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Cómo especificar los enlaces de monitorización al utilizar el paquete NPM {#specify-monitoring-npm}

Si está usando Web SDK a través del [paquete NPM](install/npm.md), puede especificar vínculos de supervisión en la función `createInstance`, como se muestra a continuación.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Ejemplo {#example}

Web SDK busca una matriz de objetos en una variable global llamada `__alloyMonitors`.

Para capturar todos los eventos de Web SDK, debe definir los vínculos de supervisión antes de cargar el código de Web SDK en la página. Cada método de monitorización captura un evento de SDK web.

Puede definir los vínculos de monitorización *después de* que el código de Web SDK se cargue en su página, pero cualquier vínculo que se haya activado antes de que se cargue la página *no se capturará*.

Al definir el objeto de vínculo de monitorización, solo necesita definir los métodos para los que desea definir una lógica especial.
Por ejemplo, si solo le importa `onContentRendering`, puede definir ese método. No es necesario utilizar todos los ganchos de monitorización a la vez.

Puede definir varios objetos de enlace de monitorización. Se llama a todos los objetos con el método dado cuando se activa el evento correspondiente.

>[!TIP]
>
>Consulte a continuación una página de ejemplo con todos los enlaces de monitorización implementados.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
