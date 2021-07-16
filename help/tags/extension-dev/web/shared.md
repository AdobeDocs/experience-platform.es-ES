---
title: Módulos compartidos en extensiones web
description: Obtenga información sobre cómo definir módulos de biblioteca compartidos para extensiones web en Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 78%

---

# Módulos compartidos en extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Un módulo compartido es un mecanismo mediante el cual puede comunicarse con otras extensiones. En las implementaciones de JavaScript, todas las instancias de los módulos compartidos se crean mediante el método [`getSharedModule`](../turbine.md#shared) que proporciona la variable gratuita `turbine`.

Al desarrollar su propia extensión de etiquetas, puede definir cualquier módulo compartido que desee que proporcione. Por ejemplo, puede crear un módulo que cargue un ID de usuario de forma asíncrona y que, a continuación, comparta el ID de usuario con cualquier otra extensión mediante el objeto [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise):

```javascript
var userIdPromise = new Promise(/* load user id, then resolve promise */);
module.exports = userIdPromise;
```

En el [manifiesto de extensión](../manifest.md), debe proporcionar un nombre para este módulo compartido. Si le asigna el nombre `user-id-promise`, otra extensión diferente podría acceder a este módulo compartido como se indica a continuación:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Los módulos compartidos pueden ser cualquier cosa que normalmente puede exportar desde un módulo CommonJS (como funciones, objetos, cadenas, números o valores booleanos).
