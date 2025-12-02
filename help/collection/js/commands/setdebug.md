---
title: setDebug
description: Habilitar o deshabilitar la configuración de depuración de Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

El comando `setDebug` le permite entrar o salir del modo de depuración en Web SDK. Es una de las varias opciones disponibles para [depurar](../../use-cases/debugging.md). Adobe recomienda habilitar el modo de depuración en entornos de desarrollo o solo en el equipo local dentro de entornos de producción.

Ejecute el comando `setDebug` al llamar a la instancia configurada de Web SDK. La única opción en el objeto de configuración es `enabled`, que es un booleano que determina si el modo de depuración está habilitado.

```js
alloy("setDebug", {"enabled": true});
```

## Configurar la depuración mediante la extensión de etiquetas Web SDK

Llame a [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) desde la consola del explorador en una página donde se haya implementado una biblioteca de etiquetas. La extensión de etiquetas Web SDK no ofrece la capacidad de alternar las opciones de depuración dentro de la propia interfaz de usuario de etiquetas.
