---
title: Tipos de elementos de datos para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo de elemento de datos para una extensión de etiqueta en una propiedad web.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 63%

---

# Tipos de elementos de datos para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En las etiquetas de recopilación de datos, los elementos de datos son esencialmente alias a datos de una página. Estos datos se pueden encontrar en parámetros de cadena de consulta, cookies, elementos DOM u otras ubicaciones. Las reglas pueden hacer referencia a un elemento de datos y este puede actuar como una abstracción para acceder a estos fragmentos de datos.

Las extensiones proporcionan los tipos de elementos de datos y permiten a los usuarios configurar elementos de datos para acceder a fragmentos de datos de una forma determinada. Por ejemplo, una extensión podría proporcionar un tipo de elemento de datos &quot;elemento de almacenamiento local&quot; en el que el usuario de podría especificar un nombre de elemento de almacenamiento local. Cuando una regla hace referencia al elemento de datos, la extensión puede buscar el valor del elemento de almacenamiento local utilizando el nombre del elemento de almacenamiento local que el usuario proporcionó al configurar el elemento de datos.

Este documento explica cómo definir los tipos de elementos de datos para una extensión web en Adobe Experience Platform.

>[!IMPORTANT]
>
>Si está desarrollando una extensión edge, consulte la guía sobre [tipos de elementos de datos para extensiones edge](../edge/data-element-types.md) en su lugar.
>
>Este documento también supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones web. Si necesita una introducción, consulte la información general sobre el [formato del módulo de biblioteca](./format.md) antes de volver a esta guía.

Los tipos de elementos de datos suelen consistir en lo siguiente:

1. Se muestra una [vista](./views.md) en la interfaz de usuario de la recopilación de datos que permite a los usuarios modificar la configuración del elemento de datos.
2. Un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y recuperar fragmentos de datos.

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
