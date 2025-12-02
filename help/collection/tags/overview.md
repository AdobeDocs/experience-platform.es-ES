---
title: Referencia de objeto satélite
description: Obtenga información acerca del objeto _satellite del lado del cliente y las diversas funciones que puede realizar con él en las etiquetas.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# `_satellite` referencia de objeto

El objeto `_satellite` expone varios puntos de entrada admitidos que le ayudarán a interactuar con la biblioteca de etiquetas publicada en el sitio. Todas las implementaciones de etiquetas exponen `_satellite` si la etiqueta del cargador se implementa correctamente. Existen varios casos de uso principales para este objeto:

* Uso dentro de la biblioteca de etiquetas en bloques de código personalizado, lo que le proporciona acceso completo a la propia biblioteca de etiquetas.
* Depuración de la implementación implementada en cualquier entorno (desarrollo, ensayo o producción).
* Implementación directa en el sitio web, lo que le proporciona un control total sobre cuándo entran en déclencheur los eventos o las reglas de etiquetas. Para nuevas implementaciones, Adobe recomienda usar una estrategia más flexible como [Adobe Client Data Layer](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Si llama a `_satellite` desde el código del sitio (por ejemplo, `_satellite.track()`), **proteja cada llamada** para que el sitio no esté perfectamente acoplado a la biblioteca de etiquetas.
>
>El uso de `_satellite` dentro del código personalizado de una propiedad de etiqueta o localmente en la consola del explorador no requiere protección.

## Ejemplos de uso comunes

```js
// Read and write a temporary data element value
const region = _satellite.getVar('user_region');
_satellite.setVar('promo_code', code);

// Local debugging
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');

// Manually trigger a rule configured in your tag property
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}
```
