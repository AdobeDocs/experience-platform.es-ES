---
title: Tipos de elementos de datos para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de elemento de datos para una extensión de etiqueta en una propiedad web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 70%

---

# Tipos de elementos de datos para extensiones de Edge

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

El propósito de un módulo de biblioteca de tipo de elemento de datos es recuperar un fragmento de datos. El método para esta recuperación es personalizable. Los distintos tipos de elementos de datos permiten a los usuarios de Adobe Experience Platform recuperar datos del almacenamiento local, una cookie o un elemento DOM.

>[!IMPORTANT]
>
>Este documento proporciona información sobre tipos de elementos de datos para extensiones web. Si va a desarrollar una extensión de Edge, consulte la guía sobre [tipos de elementos de datos para extensiones de Edge](../edge/data-element-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones de etiquetas. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Considere una situación en la que desee permitir que los usuarios recuperen un fragmento de datos de un elemento de almacenamiento local denominado `productName`. Es posible que el módulo tenga este aspecto:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Si desea que el usuario de Adobe Experience Platform pueda configurar el nombre del elemento de almacenamiento local, puede permitir que el usuario introduzca un nombre y guardarlo en el objeto `settings` . El objeto podría tener este aspecto:

```js
{
  itemName: "campaignId"
}
```

Para poder utilizar el nombre del elemento de almacenamiento local definido por el usuario, su módulo deberá cambiar a lo siguiente:

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Compatibilidad con valores predeterminados

Tenga en cuenta que los usuarios tienen la opción de configurar un valor predeterminado para cualquier elemento de datos. Si el módulo de la biblioteca de elementos de datos devuelve el valor `undefined` o `null`, este se reemplazará automáticamente por el valor predeterminado que el usuario haya configurado para el elemento de datos.

## Datos de evento contextual

Si el elemento de datos se recupera como resultado de la activación de una regla (por ejemplo, los elementos de datos se utilizan en las condiciones y acciones de la regla), se pasará un segundo argumento al módulo que contiene información contextual sobre el evento que activó la regla. Esto puede ser beneficioso en algunos casos y se puede acceder a estos datos de la siguiente manera:

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
