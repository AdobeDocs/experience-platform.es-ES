---
title: setDebug
description: Habilite o deshabilite la configuración de depuración del SDK web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

El `setDebug` permite entrar o salir del modo de depuración en el SDK web. Es una de las varias opciones disponibles para [depuración](../use-cases/debugging.md). El Adobe recomienda habilitar el modo de depuración en entornos de desarrollo o solo en el equipo local dentro de entornos de producción.

## Configurar la depuración mediante la extensión de etiqueta del SDK web

La extensión de etiqueta no ofrece la capacidad de alternar las opciones de depuración dentro de la interfaz de usuario. Puede utilizar el editor de código personalizado con sintaxis de JavaScript o introducir el código JavaScript en la consola del explorador mientras está en el sitio.

## Configurar la depuración mediante la biblioteca JavaScript del SDK web

Ejecute el `setDebug` al llamar a la instancia configurada del SDK web. La única opción del objeto de configuración es `enabled`, que es un booleano que determina si el modo de depuración está habilitado.

```js
alloy("setDebug", {"enabled": true});
```
