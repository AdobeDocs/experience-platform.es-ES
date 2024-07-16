---
title: debugEnabled
description: Utilice código para habilitar las funciones de depuración en el SDK web.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

La propiedad `debugEnabled` le permite habilitar o deshabilitar la depuración mediante código SDK para web. Es una de las formas disponibles de habilitar la [depuración](../../use-cases/debugging.md). Habilitar la depuración dentro de la implementación puede ser más conveniente que otros métodos durante el desarrollo del sitio web cuando siempre desea tener la depuración habilitada. Este método de depuración lo permite para todos los visitantes, por lo que no se recomienda para las páginas de producción.

Consulte la página del caso de uso [Depuración](../../use-cases/debugging.md) para obtener más información sobre cómo habilitar la depuración.

## Habilitar la depuración mediante la extensión de etiqueta del SDK web

No hay opciones de depuración disponibles de forma nativa mediante la extensión de etiqueta del SDK web. Usar un [método de depuración alternativo](../../use-cases/debugging.md).

## Habilitar la depuración mediante la biblioteca JavaScript del SDK web

Establezca el booleano `debugEnabled` en `true` al ejecutar el comando `configure`. Si omite esta propiedad al configurar el SDK, el valor predeterminado es `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
