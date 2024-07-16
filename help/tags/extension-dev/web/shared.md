---
title: Módulos compartidos en extensiones web
description: Obtenga información sobre cómo definir los módulos de bibliotecas para extensiones web en Adobe Experience Platform.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 71%

---

# Módulos compartidos en extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Un módulo compartido es un mecanismo mediante el cual puede comunicarse con otras extensiones. Por ejemplo, la extensión A puede cargar un fragmento de datos asincrónicamente y ponerlo a disposición de la extensión B mediante una [promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

En las implementaciones de JavaScript, todas las instancias de los módulos compartidos se crean mediante el método [`getSharedModule`](../turbine.md#shared) que proporciona la variable gratuita `turbine`.

Los módulos compartidos se incluyen en las bibliotecas de etiquetas incluso cuando nunca se les llama desde otras extensiones. Para no incrementar el tamaño de la biblioteca de manera innecesaria, debe tener cuidado con lo que expone como módulo compartido.

Los módulos compartidos no tienen componente de vista.

Al desarrollar su propia extensión de etiqueta, puede definir los módulos compartidos que desea proporcionar. Por ejemplo, puede crear un módulo que cargue un ID de usuario de forma asíncrona y que, a continuación, comparta el ID de usuario con cualquier otra extensión mediante el objeto promise:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

En el [manifiesto de extensión](../manifest.md), debe proporcionar un nombre para este módulo compartido. Si le asigna el nombre `user-id-promise`, otra extensión diferente podría acceder a este módulo compartido como se indica a continuación:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Los módulos compartidos pueden ser cualquier cosa que normalmente puede exportar desde un módulo CommonJS (como funciones, objetos, cadenas, números o valores booleanos).
