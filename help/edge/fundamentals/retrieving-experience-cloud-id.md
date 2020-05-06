---
title: Recuperación del ID de Experience Cloud
seo-title: SDK web de Adobe Experience Platform Recuperación de Experience Cloud ID
description: Obtenga información sobre cómo obtener el ID de Adobe Experience Cloud.
seo-description: Obtenga información sobre cómo obtener el ID de Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# (Beta) Recuperación de Experience Cloud ID

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Adobe Experience Cloud utiliza un ID exclusivo para cada consumidor. Si desea utilizar este ID único, utilice el `getIdentity` comando. `getIdentity` devuelve el ECID existente para el visitante actual. Para los visitantes que no tienen un ECID todavía por primera vez, este comando genera un nuevo ECID.

>[!NOTE]
>
>Este método se utiliza generalmente con soluciones personalizadas que requieren leer el ID de Experience Cloud. No se utiliza en una implementación estándar.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
