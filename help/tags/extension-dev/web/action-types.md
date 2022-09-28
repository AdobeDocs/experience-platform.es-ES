---
title: Tipos de acción para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de acción para una extensión de etiqueta en una propiedad web.
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 70%

---

# Tipos de acción para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En el contexto de las etiquetas de recopilación de datos, una acción es algo que se realiza después de que se haya producido un evento de regla y de que todas las condiciones hayan pasado la evaluación.

Por ejemplo, una extensión podría proporcionar un tipo de acción &quot;mostrar chat de asistencia&quot; que puede mostrar un cuadro de diálogo de chat de asistencia técnica para ayudar a los usuarios con problemas para efectuar sus pagos.

Este documento explica cómo definir tipos de acción para una extensión web en Adobe Experience Platform.

>[!IMPORTANT]
>
>Este documento describe los tipos de acción para las extensiones web. Si va a desarrollar una extensión de Edge, consulte la guía sobre [tipos de acción para las extensiones de Edge](../edge/action-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones web. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Los tipos de acción suelen consistir en lo siguiente:

1. A [ver](./views.md) se muestra en la interfaz de usuario del Experience Platform y en la de la recopilación de datos, lo que permite a los usuarios modificar la configuración de la acción.
2. Un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y realizar una acción.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Por ejemplo, para que el mensaje sea configurable por el usuario de Adobe Experience Platform, puede permitir que este introduzca y guarde un mensaje en el objeto de configuración. El objeto tiene un aspecto similar al siguiente:

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

Luego se tendría que pasar un segundo argumento al módulo que contiene la información contextual acerca del evento que activa la regla. Esto puede ser beneficioso en algunos casos y se puede acceder a estos datos de la siguiente manera:

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
