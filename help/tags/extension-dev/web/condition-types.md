---
title: Tipos de condición para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de condición para una extensión de etiqueta en una propiedad web.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 69%

---

# Tipos de condición para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En el contexto de una regla, se evalúa una condición después de que se haya producido un evento. Todas las condiciones deben devolver el valor verdadero para que la regla pueda continuar el procesamiento. La excepción es cuando los usuarios colocan explícitamente condiciones en un bloque de &quot;excepción&quot;, en cuyo caso todas las condiciones dentro del bloque deben devolver false para que la regla siga procesándose.

Por ejemplo, una extensión podría proporcionar un tipo de condición &quot;la ventanilla contiene&quot; en la que el usuario de podría especificar un selector CSS. Cuando la condición se evalúa en el sitio web del cliente, la extensión puede encontrar elementos que coincidan con el selector de CSS y devolver si alguno de ellos se incluye en la ventanilla del usuario.

Este documento explica cómo definir tipos de condiciones para una extensión web en Adobe Experience Platform.

>[!NOTE]
>
>Si va a desarrollar una extensión de Edge, consulte la guía sobre [tipos de condición para extensiones de Edge](../edge/condition-types.md) en su lugar.
>
>Este documento supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones web. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Los tipos de condición suelen consistir en lo siguiente:

1. A [ver](./views.md) se muestra en la interfaz de usuario del Experience Platform y en la de la recopilación de datos, lo que permite a los usuarios modificar la configuración de la condición.
2. Módulo de biblioteca emitido en la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y evaluar una condición.

Un módulo de biblioteca de tipo de condición tiene un objetivo: evalúe si algo es verdadero o falso. Lo que evalúan depende de usted.

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
