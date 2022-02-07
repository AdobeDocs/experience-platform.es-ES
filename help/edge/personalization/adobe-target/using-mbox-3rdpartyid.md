---
title: Sincronización de perfiles en tiempo real para mbox3rdPartyId
description: Aprenda a utilizar mbox3rdPartyId con el SDK web de Adobe Experience Platform.
keywords: personalización;target;adobe target;renderdecisions;sendEvent;mbox3rdPartyId;
source-git-commit: 86acedc6813a14648848a25e08aa7e65f48d1a2a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 9%

---


# ¿Qué es `mbox3rdPartyId`?

El mbox3rdPartyId de Adobe Target es el ID de visitante de su empresa, como el ID de pertenencia para el programa de fidelidad de su empresa.

Cuando un visitante inicia sesión en el sitio de una empresa, esta generalmente crea un ID vinculado a la cuenta del visitante, la tarjeta de fidelidad, el número de pertenencia u otros identificadores aplicables para esa empresa. [Más información](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## Cómo usar `mbox3rdPartyId` con el SDK web

### Paso 1: Configure las variables `Target Third Party ID Namespace`

Configure las variables `Target Third Party ID Namespace` en su [Datastream](../../fundamentals/datastreams.md), utilizando el espacio de nombres de ID que desea usar como ID de terceros de mbox.
[Más información sobre las áreas de nombres de ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es)

![](assets/mbox3rdpartyid.png)

### Paso 2: Envíe el `mbox3rdpartyId` a Target

Envíe el `mbox3rdpartyId` a Target en el `sendEvent` usando el espacio de nombres de ID que ha configurado en el paso 1.
[Más información sobre el envío de ID](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


