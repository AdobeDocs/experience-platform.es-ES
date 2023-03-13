---
title: Módulos de extensión de Edge en contexto
description: Obtenga información acerca del objeto de contexto y la función que desempeña en la interacción con los módulos de biblioteca en las extensiones de las propiedades de Edge.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 97%

---

# Módulos de extensión de Edge en contexto

>[!NOTE]
>
> Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Todos los módulos de biblioteca de las extensiones de Edge reciben un objeto `context` cuando se ejecutan. Este documento describe las propiedades que proporciona el objeto `context` y la función que desempeñan en los módulos de biblioteca.

## Contexto de solicitud de Adobe (arc)

La propiedad `arc` es un objeto que proporciona información sobre el evento que activa la regla. Las secciones siguientes describen las distintas subpropiedades que contiene este objeto.

### [!DNL event]

El objeto `event` representa el evento que activó la regla y contiene los siguientes valores:

```js
logger.log(context.arc.event);
```

| Propiedad | Descripción |
| --- | --- |
| `xdm` | El objeto XDM del evento. |
| `data` | La capa de datos personalizada. |

### [!DNL request]

No debe confundirse con una solicitud del dispositivo cliente, `request` es un objeto ligeramente modificado que procede de Adobe Experience Platform Edge Network.

```js
logger.log(context.arc.request)
```

El objeto `request` tiene dos propiedades de nivel superior: `body` y `head`. La propiedad `body` contiene información del modelo de datos de experiencia (XDM) y se puede inspeccionar en Adobe Experience Platform Debugger cuando se navega a **[!UICONTROL Launch]** y se selecciona la pestaña **[!UICONTROL Rastro de Edge]**.

### [!DNL ruleStash] {#rulestash}

`ruleStash` es un objeto que recopilará todos los resultados de los módulos de acción.

```js
logger.log(context.arc.ruleStash);
```

Cada extensión tiene su propia área de nombres. Por ejemplo: si la extensión tiene el nombre `send-beacon`, todos los resultados de las acciones `send-beacon` se almacenarán en el área de nombres `ruleStash['send-beacon']`.

El área de nombres es única para cada extensión y tiene un valor de `undefined` al principio.

El área de nombres se sobrescribe con el resultado que devuelve cada acción. Por ejemplo, considere una extensión `transform` que contenga dos acciones: `generate-fullname` y `generate-fulladdress`. Estas dos acciones se añaden a continuación a una regla.

Si el resultado de la acción `generate-fullname` es `Firstname Lastname`, la cadena de reglas aparecerá como se muestra a continuación una vez completada la acción:

```js
{
  transform: 'Firstname Lastname'
}
```

Si el resultado de la acción `generate-address` es `3900 Adobe Way`, la cadena de reglas se mostrará como se indica a continuación una vez completada la acción:

```js
{
  transform: '3900 Adobe Way'
}
```

Observe que el &quot;Nombre y apellido&quot; ya no existen dentro de la pila de reglas, porque la acción `generate-address` sobrescribió estos datos con un nuevo valor.

Si desea que `ruleStash` almacene los resultados de ambas acciones dentro del área de nombres `transform`, puede escribir un módulo de acción similar al ejemplo siguiente:

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

La primera vez que se ejecuta esta acción, `ruleStash` comienza como `undefined` y, por lo tanto, se inicializa como objeto vacío. La próxima vez que se ejecute la acción, recibirá el valor `ruleStash` que se devolvió con la llamada anterior a la acción. El uso de un objeto como `ruleStash` permite agregar nuevos datos sin perder los datos que previamente definieron otras acciones de nuestra extensión.

>[!NOTE]
>
>Debe tener cuidado de devolver siempre la cadena de regla de extensión completa al utilizar esta estrategia. Si, en su lugar, solo devolviese un valor, se sobrescribirían las demás propiedades que haya establecido.

## Utilidades

La propiedad `utils` representa un objeto que proporciona utilidades específicas del tiempo de ejecución de la etiqueta.

### [!DNL logger]

La utilidad `logger` permite registrar los mensajes que se mostrarán durante las sesiones de depuración al utilizar [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

El registrador tiene los métodos siguientes, donde `message` es el mensaje que desea registrar:

| Método | Descripción |
| --- | --- |
| `log(message)` | Registra un mensaje en la consola. |
| `info(message)` | Registra un mensaje informativo en la consola. |
| `warn(message)` | Registra un mensaje de advertencia en la consola. |
| `error(message)` | Registra un mensaje de error en la consola. |
| `debug(message)` | Registra un mensaje de depuración en la consola. Esto solo está visible cuando el registro `verbose` está habilitado en la consola del explorador. |

### [!DNL fetch]

Esta utilidad implementa la [API de búsqueda](https://developer.mozilla.org/es-ES/docs/Web/API/Fetch_API). Puede utilizar la función para realizar solicitudes a extremos de terceros.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Esta utilidad devuelve un objeto que contiene información sobre la compilación de la biblioteca de tiempo de ejecución de la etiqueta actual.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

El objeto contiene los valores siguientes:

| Propiedad | Descripción |
| --- | --- |
| `turbineVersion` | La versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) utilizada dentro de la biblioteca actual. |
| `turbineBuildDate` | La fecha ISO 8601 en que se creó la versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) utilizada dentro del contenedor. |
| `buildDate` | La fecha ISO 8601 en que se creó la biblioteca actual. |
| `environment` | El entorno para el que se creó esta biblioteca. Entre los posibles valores se incluyen `development`, `staging` y `production.` |

A continuación se muestra un objeto `getBuildInfo` de ejemplo para demostrar los valores que arroja:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Esta utilidad arroja el objeto `settings` que se guardó por última vez desde la vista de [configuración de la extensión](../configuration.md).

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Esta utilidad arroja el objeto `settings` que se guardó por última vez desde la vista del módulo de biblioteca correspondiente.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Esta utilidad arroja un objeto que contiene información sobre la regla que activa el módulo.

```js
logger.log(context.utils.getRule());
```

El objeto contendrá los valores siguientes:

| Propiedad | Descripción |
| --- | --- |
| `id` | ID de la regla. |
| `name` | Nombre de la regla. |
