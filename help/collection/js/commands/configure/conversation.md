---
title: conversación
description: Configure las opciones de chat de Brand Concierge.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 4%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge para Web SDK se encuentra actualmente en **beta**. La funcionalidad y la documentación están sujetas a cambios.

El objeto `conversation` contiene opciones de configuración para sesiones de chat de Brand Concierge. Este objeto es compatible con Web SDK versión 2.31.0 o posterior.

## Propiedades

| Propiedad | Tipo | Descripción |
| --- | --- | --- |
| **`stickyConversationSession`** | `boolean` | Determina si Web SDK establece una cookie de sesión para conservar las sesiones de chat de Brand Concierge en las cargas de páginas. El valor predeterminado es `false`. Si se omite o se establece en `false`, el chat de Brand Concierge inicia una nueva sesión en cada carga de página. |

## Ejemplo

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    stickyConversationSession: true
  }
});
```

## Configuración de la conversación mediante la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [Brand Concierge settings](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
