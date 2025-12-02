---
title: getVisitorId
description: Recupere la instancia de extensión de la etiqueta del servicio de ID de visitante de Experience Cloud.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# `getVisitorId()`

El método `_satellite.getVisitorId()` devuelve una instancia del [servicio Adobe Experience Cloud ID](https://experienceleague.adobe.com/es/docs/id-service/using/home) dentro de su propiedad de etiquetas, **si** tiene instalada y publicada la extensión del servicio de ID. Este método es útil cuando desea acceder directamente a la instancia de ID de visitante para utilizarlo en bloques de código personalizado, en la configuración avanzada de elementos de datos o para solucionar problemas de identidad de visitantes.

>[!IMPORTANT]
>
>Este método solo se aplica a las propiedades que incluyen la extensión de etiqueta de servicio de Experience Cloud ID independiente. No se aplica a las funciones del servicio de ID implícitas disponibles en la extensión de etiquetas de Web SDK. Consulte el comando [`getIdentity`](/help/collection/js/commands/getidentity.md) si necesita obtener una identidad de visitante mediante las funciones del servicio de ID implícitas de Web SDK.

Si llama a este método con la extensión del servicio de ID instalada y publicada, se devuelve un objeto similar al objeto obtenido después de llamar al método [`Visitor.getInstance()`](https://experienceleague.adobe.com/es/docs/id-service/using/id-service-api/methods/getinstance). Si llama a este método cuando no se ha instalado o publicado la extensión del servicio de ID, el método devuelve `null`.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Campos y métodos disponibles

Consulte el servicio de Experience Cloud ID [Métodos](https://experienceleague.adobe.com/es/docs/id-service/using/id-service-api/methods/get-set) en la documentación del servicio de ID de visitante de Experience Cloud para ver qué campos y métodos están disponibles.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
