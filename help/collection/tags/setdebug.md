---
title: setDebug()
description: Habilite la depuración en el sitio a través de la consola del explorador.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

El método `_satellite.setDebug()` le permite habilitar o deshabilitar la [depuración](../use-cases/debugging.md) en su sitio. Este método está diseñado para ejecutarse localmente en la consola del explorador; Adobe aconseja no llamar a este método dentro de las reglas de etiquetas.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: Habilita [Depuración](../use-cases/debugging.md). Los mensajes generados por la biblioteca de etiquetas (incluido [`_satellite.logger`](logger.md)) se pueden ver en la consola del explorador.
* **`_satellite.setDebug(false);`**: deshabilita la depuración. Los mensajes de la consola generados por la biblioteca de etiquetas no son visibles.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>Los mensajes escritos con el elemento nativo de JavaScript `console.log()` siempre son visibles para cualquiera que tenga DevTools abierto. Adobe recomienda usar [`_satellite.logger`](logger.md) siempre que sea posible.

## Persistencia del modo Debug

Al llamar a este método, el modo de depuración utiliza el ámbito siguiente:

* **Sesión del explorador**: el modo de depuración persiste entre cargas de página. Permanece habilitado hasta que se finaliza la sesión del explorador o se deshabilita explícitamente.
* **Ámbito de origen**: el modo de depuración solo persiste para el mismo sitio (dominio + puerto + protocolo).
* **Por perfil de explorador**: el modo de depuración no es de perfil cruzado.

Otras formas de [depuración](../use-cases/debugging.md) pueden afectar y sobrescribir el modo de depuración mediante el método de consola del explorador.
