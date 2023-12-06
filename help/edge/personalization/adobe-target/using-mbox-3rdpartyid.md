---
title: Sincronización de perfiles en tiempo real para mbox3rdPartyId
description: Aprenda a utilizar mbox3rdPartyId con el SDK web de Adobe Experience Platform.
keywords: personalización;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---

# Qué es `mbox3rdPartyId`

mbox3rdPartyId en Adobe Target es el ID del visitante de su empresa, como el ID de pertenencia para el programa de fidelidad de su empresa.

Cuando un visitante inicia sesión en el sitio de una empresa, esta generalmente crea un ID vinculado a la cuenta del visitante, la tarjeta de fidelidad, el número de pertenencia u otros identificadores aplicables para esa empresa. [Más información](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## Cómo usar `mbox3rdPartyId` con el SDK web

### Paso 1: Configuración de `Target Third Party ID Namespace`

Configure las variables `Target Third Party ID Namespace` en su [Datastream](../../../datastreams/overview.md), usando el área de nombres de ID que desea usar como ID de terceros de mbox.
[Más información sobre Áreas de nombres de ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=es)

![IU de Platform que muestra el campo del área de nombres de ID de terceros de Target.](assets/mbox3rdpartyid.png)

### Paso 2: Envío de la `mbox3rdpartyId` a Target

Envíe el `mbox3rdpartyId` a Target en `sendEvent` , utilizando el área de nombres de ID que configuró en el paso 1.
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
