---
title: Tipos de condición para extensiones de Edge
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo condición para una extensión de Edge en Adobe Experience Platform.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 69%

---

# Tipos de condición para extensiones de Edge

>[!NOTE]
>
> Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En una regla de etiqueta, se evalúa una condición después de que se haya producido un evento. Todas las condiciones deben devolver el valor verdadero para que la regla pueda continuar el procesamiento. Las extensiones proporcionan los tipos de condición y evalúan si algo es verdadero o falso, lo que devuelve un valor booleano.

Por ejemplo, una extensión podría proporcionar un tipo de condición &quot;la ventanilla contiene&quot; en la que el usuario de podría especificar un selector CSS. Cuando la condición se evalúa en el sitio web del cliente, la extensión puede encontrar elementos que coincidan con el selector de CSS y devolver si alguno de ellos se incluye en la ventanilla del usuario.

Este documento explica cómo definir tipos de condiciones para una extensión edge en Adobe Experience Platform.

>[!IMPORTANT]
>
>Si está desarrollando una extensión web, consulte la guía sobre [tipos de condición para extensiones web](../web/condition-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones Edge. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Los tipos de condición suelen consistir en lo siguiente:

1. Vista que se muestra en la interfaz de usuario de la recopilación de datos y que permite a los usuarios modificar la configuración de la condición.
2. Módulo de biblioteca emitido en la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y evaluar una condición.

Por ejemplo, si desea evaluar si el usuario está en el host `example.com`, el módulo puede tener un aspecto similar al siguiente.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Si desea que el nombre de host se pueda configurar por el usuario para permitir la entrada de un nombre de host y guardarlo en el objeto de configuración, el objeto podría tener un aspecto similar al de este ejemplo.

```js
{
  "hostname": "example.com"
}
```

Para poder modificar el nombre de host definido por el usuario, el módulo deberá cambiar a lo siguiente:

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Resultado de la condición

El resultado devuelto por un módulo de condición puede ser uno de los siguientes:

1. Un valor booleano (`true` o `false`).
1. Una [promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) que devuelve un valor booleano una vez resuelto.

## Contexto del módulo Biblioteca

Todos los módulos de condición tienen acceso a una variable `context` que se proporciona cuando se invoca el módulo. Puede obtener más información [aquí](./context.md).
