---
title: debugEnabled
description: Utilice el código para habilitar las funciones de depuración en Web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

La propiedad `debugEnabled` le permite habilitar o deshabilitar la depuración mediante código de Web SDK. Es una de las formas disponibles de habilitar la [depuración](/help/collection/use-cases/debugging.md). Habilitar la depuración dentro de la implementación puede ser más conveniente que otros métodos durante el desarrollo del sitio web cuando siempre desea tener la depuración habilitada. Este método de depuración lo permite para todos los visitantes, por lo que no se recomienda para las páginas de producción. Consulte la página del caso de uso [Depuración](/help/collection/use-cases/debugging.md) para obtener más información sobre cómo habilitar la depuración.

Establezca el booleano `debugEnabled` en `true` al ejecutar el comando `configure`. Si omite esta propiedad al configurar SDK, el valor predeterminado es `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Habilitar la depuración mediante la extensión de etiquetas Web SDK

No hay opciones de depuración disponibles de forma nativa mediante la extensión de etiquetas Web SDK. Use un [método de depuración alternativo](/help/collection/use-cases/debugging.md) al configurar su propiedad de etiquetas.
