---
title: conversación
description: Configure las opciones de chat de Brand Concierge.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge para Web SDK se encuentra actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

El objeto `conversation` contiene opciones de configuración para sesiones de chat de Brand Concierge. Este objeto es compatible con Web SDK versión 2.31.0 o posterior.

## Propiedades

| Propiedad | Tipo | Descripción |
| --- | --- | --- |
| **`collectSources`** | `boolean` | Determina si Web SDK lee el parámetro de cadena de consulta `adobe_brand_concierge_source` y lo incluye en `xdm.channel.referringSource`. El valor predeterminado es `false`. |
| **`stickyConversationSession`** | `boolean` | Determina si Web SDK establece una cookie de sesión para conservar las sesiones de chat de Brand Concierge en las cargas de páginas. El valor predeterminado es `false`. Si se omite o se establece en `false`, el chat de Brand Concierge inicia una nueva sesión en cada carga de página. |

## Ejemplo

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## Configuración de la conversación mediante la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [Brand Concierge settings](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
