---
title: Tipos de acción para extensiones de Edge
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de acción para una extensión de etiqueta en una propiedad edge.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 41%

---

# Tipos de acción para extensiones de Edge

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En una regla de etiqueta, una acción es algo que se realiza después de que las condiciones de la regla hayan pasado la evaluación. Los tipos de acción los proporcionan las extensiones y el autor de la extensión los define por completo.

Por ejemplo, una extensión podría proporcionar un tipo de acción &quot;mostrar chat de asistencia&quot; que puede mostrar un cuadro de diálogo de chat de asistencia técnica para ayudar a los usuarios con problemas para efectuar sus pagos.

Este documento explica cómo definir tipos de acción para una extensión edge en Adobe Experience Platform.

>[!IMPORTANT]
>
>Si va a desarrollar una extensión web, consulte la guía sobre [tipos de acciones para extensiones web](../web/action-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones Edge. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Los tipos de acción suelen consistir en lo siguiente:

1. Vista que se muestra en la interfaz de usuario de la recopilación de datos y que permite a los usuarios modificar la configuración de la acción.
2. Un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y realizar una acción.

Por ejemplo, un módulo para reenviar algunos datos a un extremo de terceros puede tener este aspecto.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Si desea que el punto final sea configurable por el usuario y permitir la entrada y persistencia de un punto final al objeto de configuración dentro del módulo, el objeto tendría un aspecto similar a este.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Para operar en el extremo definido por el usuario, el módulo tendría que cambiar al siguiente ejemplo.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Resultado de la acción

El resultado devuelto por un módulo de acción puede ser cualquier cosa. Si la acción necesita ejecutar una tarea asincrónica, puede devolver una [promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) que devuelve el resultado deseado una vez que se resuelva.

El resultado de la acción se almacena dentro de una clave `ruleStash` que está disponible para todos los módulos a través del parámetro `context` (`context.arc.ruleStash`). Puede obtener más información sobre `ruleStash` [aquí](./context.md#rulestash).
