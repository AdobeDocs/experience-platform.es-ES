---
title: Información general sobre las etiquetas de JavaScript del lado del cliente (_satellite)
description: Obtenga información acerca del objeto _satellite del lado del cliente y las diversas funciones que puede realizar con él en las etiquetas.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Información general sobre las etiquetas de JavaScript del lado del cliente (`_satellite`)

_Estas páginas describen cómo usar el objeto `_satellite`, que le permite administrar y personalizar la lógica de etiquetas mediante JavaScript. Consulte la [extensión de etiquetas Adobe Experience Platform Web SDK](/help/tags/extensions/client/web-sdk/overview.md) para obtener más información sobre cómo configurar la implementación en la IU de recopilación de datos._

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
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
