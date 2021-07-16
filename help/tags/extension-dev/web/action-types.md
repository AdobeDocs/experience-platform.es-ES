---
title: Tipos de acción para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de acción para una extensión de etiqueta en una propiedad web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 65%

---

# Tipos de acción para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Un módulo de biblioteca de tipo de acción está diseñado para realizar una acción predefinida. Lo que dicha acción haga depende de usted. ¿Desea enviar una señalización, mostrar una oferta, dar las gracias al usuario por su visita, guardar una cookie o abrir un chat de asistencia?

>[!IMPORTANT]
>
>Este documento describe los tipos de acción para las extensiones web. Si va a desarrollar una extensión de Edge, consulte la guía sobre [tipos de acción para las extensiones de Edge](../edge/action-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones de etiquetas. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Por ejemplo, para que el mensaje sea configurable por el usuario de Adobe Experience Platform, puede permitir que el usuario introduzca y guarde un mensaje en el objeto de configuración. El objeto tiene un aspecto similar al siguiente:

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Para poder modificar el mensaje definido por el usuario, el módulo deberá cambiar a esto:

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Datos de evento contextual

Luego se tendría que pasar un segundo argumento al módulo que contiene la información contextual sobre el evento que activa la regla. Esto puede ser beneficioso en algunos casos y se puede acceder a estos datos de la siguiente manera:

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

El objeto `event` debe contener las propiedades siguientes:

| Propiedad | Descripción |
| --- | --- |
| `$type` | Cadena que describe el nombre de la extensión y el nombre del evento, unidos mediante un punto. Por ejemplo, `youtube.play`. |
| `$rule` | Objeto que contiene información sobre la regla que se está ejecutando. El objeto debe contener las siguientes propiedades secundarias:<ul><li>`id`: ID de la regla que se está ejecutando.</li><li>`name`: nombre de la regla que se está ejecutando.</li></ul> |

La extensión que proporciona el tipo de evento que activó la regla puede, de manera opcional, añadir cualquier otra información de utilidad a este objeto `event`.
