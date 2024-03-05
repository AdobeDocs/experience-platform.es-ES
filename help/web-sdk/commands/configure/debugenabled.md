---
title: debugEnabled
description: Utilice código para habilitar las funciones de depuración en el SDK web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

El `debugEnabled` permite habilitar o deshabilitar la depuración mediante código SDK para web. Es una de las formas disponibles de habilitar [depuración](../../use-cases/debugging.md). Habilitar la depuración dentro de la implementación puede ser más conveniente que otros métodos durante el desarrollo del sitio web cuando siempre desea tener la depuración habilitada. Este método de depuración lo permite para todos los visitantes, por lo que no se recomienda para las páginas de producción.

Consulte la [Depuración](../../use-cases/debugging.md) página de casos de uso para obtener más formas de habilitar la depuración.

## Habilitar la depuración mediante la extensión de etiqueta del SDK web

No hay opciones de depuración disponibles de forma nativa mediante la extensión de etiqueta del SDK web. Utilice un [método de depuración alternativo](../../use-cases/debugging.md).

## Habilitar la depuración mediante la biblioteca JavaScript del SDK web

Configure las variables `debugEnabled` booleano a `true` al ejecutar el `configure` comando. Si omite esta propiedad al configurar el SDK, el valor predeterminado es `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
