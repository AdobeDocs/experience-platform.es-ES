---
title: Módulos compartidos en extensiones web
description: Obtenga información sobre cómo definir los módulos de bibliotecas para extensiones web en Adobe Experience Platform.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 73%

---

# Módulos compartidos en extensiones web

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
