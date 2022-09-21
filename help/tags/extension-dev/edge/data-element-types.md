---
title: Tipos de elementos de datos para extensiones de Edge
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de elemento de datos para una extensión de etiqueta en una propiedad Edge.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 51%

---

# Tipos de elementos de datos en extensiones perimetrales

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En las etiquetas, los elementos de datos son alias para fragmentos de datos de una página web o móvil, independientemente de dónde se encuentren esos datos dentro del evento recibido por el servidor. Las reglas pueden hacer referencia a un elemento de datos y este puede actuar como una abstracción para acceder a estos fragmentos de datos. Cuando la ubicación de los datos cambie en el futuro (como cambiar la clave de evento que contiene el valor), se puede reconfigurar un solo elemento de datos, mientras que todas las reglas que hacen referencia a ese elemento de datos pueden permanecer sin cambios.

Las extensiones proporcionan los tipos de elementos de datos y el autor de la extensión determina cómo se recupera este fragmento de datos. Por ejemplo, ¿puede utilizar un tipo de elemento de datos para permitir a los usuarios de Adobe Experience Platform recuperar un fragmento de datos de la capa XDM o de su capa de datos personalizada.

Este documento explica cómo definir tipos de elementos de datos para una extensión edge en Adobe Experience Platform.

>[!IMPORTANT]
>
>Si está desarrollando una extensión web, consulte la guía de [tipos de elementos de datos para extensiones web](../web/data-element-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones Edge. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Los tipos de elementos de datos suelen consistir en lo siguiente:

1. Vista que se muestra en la interfaz de usuario del Experience Platform y en la de recopilación de datos y que permite a los usuarios modificar la configuración del elemento de datos.
2. Un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y recuperar fragmentos de datos.

Si desea permitir que los usuarios recuperen un fragmento de datos de la capa de datos personalizada, su módulo puede tener el aspecto de este ejemplo.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Si desea que los usuarios de Adobe Experience Platform puedan configurar los datos devueltos para la capa de datos, puede permitirles introducir un nombre de clave y después que lo guarden en el objeto `settings`. El objeto podría tener este aspecto.

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
