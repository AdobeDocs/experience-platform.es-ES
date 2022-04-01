---
title: Interactuar con Adobe Experience Platform
description: Aprenda a utilizar la API de servidor de red perimetral para interactuar con Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: recopilación de datos; salida; analytics; api de red perimetral de Adobe Experience Platform;aep
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# Interactuar con Adobe Experience Platform

## Información general {#overview}

Para habilitar la recopilación de datos del Experience Platform, primero debe [configurar el conjunto de datos](../edge/fundamentals/datastreams.md) para reenviar eventos a conjuntos de datos de Experience Platform.

Una vez configurada, la configuración del conjunto de datos debe incluir ajustes para `com_adobe_experience_platform`, como se muestra en el ejemplo siguiente:


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
