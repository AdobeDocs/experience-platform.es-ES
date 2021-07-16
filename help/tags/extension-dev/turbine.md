---
title: Variable gratuita turbine
description: Obtenga información sobre el objeto turbine , una variable gratuita que proporciona información y utilidades específicas del tiempo de ejecución de etiquetas de Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 58%

---

# Variable gratuita Turbine

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

El objeto `turbine` es una &quot;variable gratuita&quot; que entra en el ámbito de los módulos de biblioteca de su extensión. Proporciona información y utilidades específicas del tiempo de ejecución de etiquetas de Adobe Experience Platform y siempre está disponible para los módulos de biblioteca sin utilizar `require()`.

## [!DNL buildInfo]

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` es un objeto que contiene información de compilación sobre la biblioteca de tiempo de ejecución de etiquetas actual.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z",
    environment: "development"
}
```

| Propiedad | Descripción |
| --- | --- |
| `turbineVersion` | La versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizada dentro de la biblioteca actual. |
| `turbineBuildDate` | La fecha ISO 8601 en que se creó la versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizada dentro del contenedor. |
| `buildDate` | La fecha ISO 8601 en que se creó la biblioteca actual. |
| `environment` | El entorno para el que se creó esta biblioteca. Los valores aceptados son `development`, `staging` y `production`. |


## [!DNL debugEnabled]

Indica si la depuración de etiquetas está habilitada actualmente.

Si simplemente intenta registrar mensajes, es poco probable que tenga que utilizar este recurso. En su lugar, registre siempre los mensajes utilizando `turbine.logger` para asegurarse de que los mensajes solo se imprimen en la consola cuando la depuración de etiquetas esté habilitada.

### [!DNL getDataElementValue]

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Devuelve el valor de un elemento de datos.

### [!DNL getExtensionSettings] {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Devuelve el objeto de configuración que se guardó por última vez desde la vista de [configuración de la extensión](./configuration.md).

Tenga en cuenta que los valores de los objetos de configuración devueltos pueden proceder de elementos de datos. Por esta razón, realizar llamadas a `getExtensionSettings()` en diferentes momentos puede generar resultados diferentes si los valores de los elementos de datos han cambiado. Para obtener los valores más actualizados, espere el mayor tiempo posible antes de llamar a `getExtensionSettings()`.

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

La propiedad [hostedLibFiles](./manifest.md) se puede definir dentro del manifiesto de extensión para alojar varios archivos junto con la biblioteca de tiempo de ejecución de etiquetas. Este módulo devuelve la URL donde se aloja el archivo de biblioteca determinado.

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Recupera un módulo que se ha compartido desde otra extensión. Si no se encuentra ningún módulo coincidente, se devolverá `undefined`. Consulte [Implementación de módulos compartidos](./web/shared.md) para obtener más información sobre los módulos compartidos.

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

La utilidad de registro se utiliza para registrar mensajes en la consola. Los mensajes solo se mostrarán en la consola si el usuario ha activado la depuración. La manera recomendada de activar la depuración es utilizar la extensión de Chrome [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda) o [ Launch and DTM Switch](https://chrome.google.com/webstore/detail/adobe-dtm-switch/nlgdemkdapolikbjimjajpmonpbpmipk). Como alternativa, el usuario puede ejecutar el siguiente comando `_satellite.setDebug(true)` dentro de la consola del desarrollador del explorador. El registrador tiene los métodos siguientes:

* `logger.log(message: string)`: Registra un mensaje en la consola.
* `logger.info(message: string)`: Registra un mensaje informativo en la consola.
* `logger.warn(message: string)`: Registra un mensaje de advertencia en la consola.
* `logger.error(message: string)`: Registra un mensaje de error en la consola.
* `logger.debug(message: string)`: Registra un mensaje de depuración en la consola. (Solo visible cuando el registro `verbose` está habilitado en la consola del explorador.)

### [!DNL onDebugChanged]

Al pasar una función de llamada de retorno a `turbine.onDebugChanged`, las etiquetas llamarán a la llamada de retorno cada vez que se alterne la depuración. Las etiquetas pasarán un booleano a la función de llamada de retorno que será verdadera si la depuración estaba habilitada o falsa si la depuración estaba deshabilitada.

Si simplemente intenta registrar mensajes, es poco probable que tenga que utilizar este recurso. En su lugar, registre siempre los mensajes utilizando `turbine.logger` y las etiquetas se asegurarán de que los mensajes solo se impriman en la consola cuando la depuración de etiquetas esté habilitada.

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Un objeto que contiene la siguiente configuración definida por el usuario para la propiedad de la biblioteca de tiempo de ejecución de etiquetas actual:

* `propertySettings.domains: Array<String>`

   Matriz de dominios que cubre la propiedad.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Los desarrolladores de extensiones no deben preocuparse por esta configuración.
