---
title: Módulos de biblioteca de extensiones web
description: Obtenga información sobre el formato de los módulos de biblioteca para extensiones web en Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: b3754c94843f32ba58aa1e020dface1179372de3
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 94%

---

# Módulos de biblioteca de extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

>[!IMPORTANT]
>
>Este documento describe el formato del módulo de biblioteca para las extensiones web. Si va a desarrollar una extensión de Edge, consulte la guía sobre el [formato de módulos de extensiones web](../edge/format.md).

Un módulo de biblioteca es un fragmento de código reutilizable proporcionado por una extensión que se emite dentro de la biblioteca de tiempo de ejecución de etiquetas en Adobe Experience Platform. A continuación, esta biblioteca se ejecuta en el sitio web del cliente. Por ejemplo, un tipo de evento `gesture` tendrá un módulo de biblioteca que se ejecutará en el sitio web del cliente para detectar los gestos del usuario.

El módulo de biblioteca está estructurado como [módulo CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules). Dentro de un módulo CommonJS, encontrará las siguientes variables disponibles para el uso:

## `require`

Podrá acceder a la función `require`:

1. Módulos principales proporcionados por etiquetas. Se puede acceder a estos módulos utilizando `require('@adobe/reactor-name-of-module')`. Consulte el documento sobre [módulos principales](./core.md) disponibles para obtener más información.
1. Otros módulos dentro de la extensión. Se puede acceder a cualquier módulo de la extensión a través de una ruta relativa. La ruta relativa debe comenzar por `./` o `../`.

Ejemplo de uso:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

Hay disponible una variable gratuita denominada `module` que permite exportar la API del módulo.

Ejemplo de uso:

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

Hay disponible una variable gratuita denominada `exports` que permite exportar la API del módulo.

Ejemplo de uso:

```javascript
exports.sayHello = function(…) { … }
```

Esta es una alternativa a `module.exports`, pero su uso es más limitado. Lea [Explicación de module.export y exportaciones en node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) para comprender mejor las diferencias entre `module.exports` y `exports`, así como las advertencias relacionadas con el uso de `exports`. Cuando tenga dudas, no se complique la vida y utilice `module.exports` en lugar de `exports`.

## Ejecución y almacenamiento en caché

Cuando se ejecute la biblioteca de tiempo de ejecución de etiquetas, los módulos se &quot;instalarán&quot; inmediatamente y sus exportaciones se almacenarán en la caché. Suponga que tiene el módulo siguiente:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` se registrará inmediatamente, mientras que `runs when necessary` solo se registrará cuando el motor de etiquetas haya llamado a la función exportada. Aunque puede que no sea necesario para el propósito de su módulo en particular, puede aprovechar esto realizando la configuración necesaria antes de exportar la función.
