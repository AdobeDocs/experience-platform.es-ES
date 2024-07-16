---
title: Variable gratuita turbine
description: Obtenga información acerca del objeto turbine, una variable gratuita que proporciona información y utilidades específicas del tiempo de ejecución de la etiqueta de Adobe Experience Platform.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 86%

---

# Variable gratuita Turbine

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

El objeto `turbine` es una &quot;variable gratuita&quot; que entra en el ámbito de los módulos de biblioteca de su extensión. Esta variable proporciona información y utilidades específicas al tiempo de ejecución de la etiqueta de Adobe Experience Platform y siempre está disponible para los módulos de biblioteca sin utilizar `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` es un objeto que contiene información de compilación sobre la biblioteca actual de tiempo de ejecución de etiquetas.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Propiedad | Descripción |
| --- | --- |
| `turbineVersion` | La versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizada dentro de la biblioteca actual. |
| `turbineBuildDate` | La fecha ISO 8601 en que se creó la versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizada dentro del contenedor. |
| `buildDate` | La fecha ISO 8601 en que se creó la biblioteca actual. |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` es un objeto que contiene información sobre el entorno en el que está implementada la biblioteca.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID del entorno. |
| `stage` | El entorno para el que se creó esta biblioteca. Los valores posibles son `development`, `staging` y `production`. |

{style="table-layout:auto"}

## `debugEnabled`

Un valor booleano que indica si la depuración de etiquetas está habilitada actualmente.

Si simplemente intenta registrar mensajes, es poco probable que tenga que utilizar este recurso. En su lugar, registre siempre los mensajes con `turbine.logger` para garantizar que los mensajes se impriman únicamente en la consola cuando la depuración de etiquetas esté habilitada.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Devuelve el valor de un elemento de datos.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Devuelve el objeto de configuración que se guardó por última vez desde la vista de [configuración de la extensión](./configuration.md).

Tenga en cuenta que los valores de los objetos de configuración devueltos pueden proceder de elementos de datos. Por esta razón, realizar llamadas a `getExtensionSettings()` en diferentes momentos puede generar resultados diferentes si los valores de los elementos de datos han cambiado. Para obtener los valores más actualizados, espere lo más tarde posible antes de llamar a `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

La propiedad [hostedLibFiles](./manifest.md) se puede definir dentro del manifiesto de extensión para alojar varios archivos junto con la biblioteca de tiempo de ejecución de etiquetas. Este módulo devuelve la URL donde se aloja el archivo de biblioteca determinado.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Recupera un módulo que se ha compartido desde otra extensión. Si no se encuentra ningún módulo coincidente, se devolverá `undefined`. Consulte [Implementación de módulos compartidos](./web/shared.md) para obtener más información sobre los módulos compartidos.

## `logger`

```js
turbine.logger.error('Error!');
```

Utilidad de registro utilizada para registrar mensajes en la consola. Los mensajes solo se mostrarán en la consola si el usuario ha activado la depuración. La manera recomendada de activar la depuración es usar el [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob). Como alternativa, el usuario puede ejecutar el siguiente comando `_satellite.setDebug(true)` en la consola de desarrollo del explorador. El registrador tiene los métodos siguientes:

* `logger.log(message: string)`: Registra un mensaje en la consola.
* `logger.info(message: string)`: Registra un mensaje informativo en la consola.
* `logger.warn(message: string)`: Registra un mensaje de advertencia en la consola.
* `logger.error(message: string)`: Registra un mensaje de error en la consola.
* `logger.debug(message: string)`: Registra un mensaje de depuración en la consola. (Solo visible cuando el registro `verbose` está habilitado en la consola del explorador.)
* `logger.deprecation(message: string)`: Registra un mensaje de advertencia en la consola, independientemente de si el usuario ha habilitado o no la depuración de etiquetas.

## `onDebugChanged`

Al pasar una función de llamada de retorno a `turbine.onDebugChanged`, las etiquetas se conectarán con la llamada de retorno siempre que se alterne la depuración. Las etiquetas pasarán un valor booleano a la función de llamada de retorno que será verdadero si la depuración estaba habilitada, o falso si la depuración no estaba habilitada.

Si simplemente intenta registrar mensajes, es poco probable que tenga que utilizar este recurso. En su lugar, registre siempre los mensajes con `turbine.logger` y las etiquetas se asegurarán de que los mensajes se impriman únicamente en la consola cuando la depuración de etiquetas esté habilitada.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Objeto que contiene la siguiente configuración definida por el usuario para la propiedad de la biblioteca actual de tiempo de ejecución de etiquetas:

* `propertySettings.domains: Array<String>`

  Matriz de dominios que cubre la propiedad.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

  Los desarrolladores de extensiones no deben preocuparse por esta configuración.
