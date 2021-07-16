---
title: Tipos de condición para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de condición para una extensión de etiqueta en una propiedad web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 86%

---

# Tipos de condición para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Los módulos de biblioteca de tipos de condición tienen un objetivo: evaluar si algo es verdadero o falso. Lo que evalúan depende de usted.

>[!NOTE]
>
>Este documento describe los tipos de condición para extensiones web. Si va a desarrollar una extensión de Edge, consulte la guía sobre [tipos de condición para extensiones de Edge](../edge/condition-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones de etiquetas. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Por ejemplo, si desea evaluar si el usuario está en el host `example.com`, el módulo puede tener un aspecto similar al siguiente:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Piense ahora en una situación en la que desee que el usuario de Adobe Experience Platform pueda configurar el nombre del host. Puede permitir que el usuario introduzca un nombre de host y, a continuación, guardar el nombre de host en el objeto de configuración. El objeto podría tener este aspecto:

```js
{
  "hostname": "example.com"
}
```

Para poder modificar el nombre de host definido por el usuario, el módulo deberá cambiar a lo siguiente:

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Datos de evento contextual

Se pasa un segundo argumento al módulo que contiene información contextual sobre el evento que activó la regla. Esto puede ser beneficioso en algunos casos y se puede acceder a estos datos de la siguiente manera:

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
