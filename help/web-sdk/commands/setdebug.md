---
title: setDebug
description: Habilite o deshabilite la configuración de depuración del SDK web.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

El comando `setDebug` le permite entrar o salir del modo de depuración en el SDK web. Es una de las varias opciones disponibles para [depurar](../use-cases/debugging.md). El Adobe recomienda habilitar el modo de depuración en entornos de desarrollo o solo en el equipo local dentro de entornos de producción.

## Configurar la depuración mediante la extensión de etiqueta del SDK web

La extensión de etiqueta no ofrece la capacidad de alternar las opciones de depuración dentro de la interfaz de usuario. Puede utilizar el editor de código personalizado con la sintaxis de JavaScript o escribir el código de JavaScript en la consola del explorador mientras está en el sitio.

## Configurar la depuración mediante la biblioteca JavaScript del SDK web

Ejecute el comando `setDebug` al llamar a la instancia configurada del SDK web. La única opción en el objeto de configuración es `enabled`, que es un booleano que determina si el modo de depuración está habilitado.

```js
alloy("setDebug", {"enabled": true});
```
