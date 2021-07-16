---
title: Tipos de elementos de datos para extensiones de Edge
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de elemento de datos para una extensión de etiqueta en una propiedad edge.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 59%

---

# Tipos de elementos de datos en extensiones de Edge

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Un módulo de biblioteca de tipo elemento de datos recupera un fragmento de datos. El autor del módulo determina cómo se recupera este fragmento de datos. Por ejemplo, ¿puede utilizar un tipo de elemento de datos para permitir a los usuarios de Adobe Experience Platform recuperar un fragmento de datos de la capa XDM o de su capa de datos personalizada.

>[!IMPORTANT]
>
>Este documento abarca los tipos de elementos de datos para extensiones de Edge. Si está desarrollando una extensión web, consulte la guía sobre [tipos de elementos de datos para extensiones web](../web/data-element-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones de etiquetas. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Si desea permitir que los usuarios recuperen un fragmento de datos de la capa de datos personalizada, su módulo puede tener el aspecto siguiente en este ejemplo.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Si desea que el usuario de Adobe Experience Platform pueda configurar los datos devueltos para la capa de datos, puede permitir que el usuario introduzca un nombre clave y, a continuación, guardar el nombre en el objeto `settings` . El objeto podría tener este aspecto.

```js
{
  keyName: "campaignId"
}
```

Para poder utilizar el nombre del elemento de almacenamiento local definido por el usuario, su módulo deberá cambiar a lo siguiente:

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Contexto del módulo Biblioteca

Todos los módulos de elementos de datos tienen acceso a una variable `context` que se proporciona cuando se invoca el módulo. Puede obtener más información [aquí](./context.md).
