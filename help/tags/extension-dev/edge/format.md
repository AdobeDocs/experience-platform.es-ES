---
title: Módulos de biblioteca de extensiones de Edge
description: Formatear módulos de biblioteca para extensiones de etiqueta en una propiedad edge.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 81%

---

# Módulos de biblioteca de extensiones de Edge

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

>[!IMPORTANT]
>
>Este documento describe el formato del módulo de biblioteca para las extensiones de Edge. Si va a desarrollar una extensión web, consulte la guía sobre el [formato de módulos de extensiones web](../web/format.md) en su lugar.

Un módulo de biblioteca es un fragmento de código reutilizable proporcionado por una extensión que se emite dentro de la biblioteca de tiempo de ejecución de etiquetas en Adobe Experience Platform (la biblioteca que se ejecuta en el nodo perimetral). Por ejemplo, un tipo de acción `sendBeacon` tendrá un módulo de biblioteca que se ejecutará en el nodo de Edge y enviará una señalización.

El módulo de biblioteca está estructurado como [módulo CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). Dentro de un módulo CommonJS, encontrará las siguientes variables disponibles para el uso:

## [!DNL require]

Hay una función `require` disponible para que pueda acceder a los módulos de su extensión. Se puede acceder a cualquier módulo de la extensión a través de una ruta relativa. La ruta relativa debe comenzar por `./` o `../`.

Ejemplo de uso:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Hay disponible una variable gratuita denominada `module` que permite exportar la API del módulo.

Ejemplo de uso:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Hay disponible una variable gratuita denominada `exports` que permite exportar la API del módulo.

Ejemplo de uso:

```js
exports.sayHello = (…) => { … }
```

Esta es una alternativa a `module.exports`, pero su uso es más limitado. Lea [Explicación de module.export y exportaciones en node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) para comprender mejor las diferencias entre `module.exports` y `exports`, así como las advertencias relacionadas con el uso de `exports`. Cuando tenga dudas, no se complique la vida y utilice `module.exports` en lugar de `exports`.

## Firma del módulo del lado del servidor

Todos los tipos de módulos (elementos de datos, condiciones o acciones) que proporcione su extensión se solicitarán con los mismos parámetros: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
