---
title: Envío de datos a Adobe Audience Manager
seo-title: Envío de datos a Adobe Audience Manager con Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo enviar datos a Adobe Audience Manager con el SDK web Experience Platform
seo-description: Obtenga información sobre cómo enviar datos a Adobe Audience Manager con el SDK web Experience Platform
translation-type: tm+mt
source-git-commit: b87b1f8a979e028c5ebf57cecf0213a075df90a6
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] en el [!DNL Experience Platform Edge Network]

El Adobe Experience Platform [!DNL Web SDK] está integrado con Adobe Audience Manager y es compatible con el envío y la recepción de datos de destinos de cookies [!DNL Audience Manager], URL y de cookies, así como con la sincronización de ID.

## Habilitación [!DNL Audience Manager]

Para habilitar [!DNL Audience Manager] tendrá que hacer lo siguiente:

- Habilite [!DNL Audience Manager] la configuración [de Edge](../../fundamentals/edge-configuration.md).
- Habilite o deshabilite los destinos de cookies y URL.
- Especifique el Contenedor de sincronización de ID para las sincronizaciones de socios externos (opcional)

## Sincronización de identidades

El SDK web de Adobe Experience Platform permite declarar los ID de cliente y sus estados de autenticación mediante el comando [sendEvent](../../fundamentals/identity.md#syncing-identities) .

Elija sus Áreas de nombres en las Áreas de nombres [de servicio de](../../../identity/../identity-service/namespaces.md) identidad para indicar el contexto con el que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la IU de Áreas de nombres](../../../assets/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas las fuentes de datos existentes que utilicen el tipo de ID: Los dispositivos cruzados tienen automáticamente una Área de nombres de identidad correspondiente. Para encontrar la Área de nombres de identidad correspondiente para la fuente de datos de Audience Manager, inicie sesión en el Adobe Experience Platform y vaya a la sección Identidades.

Cualquier nueva fuente [!DNL Audience Manager] de datos que utilice el tipo de ID: Cross-Device generará una Área de nombres de identidad correspondiente. Actualmente no se admiten la cookie de tipos de ID de fuentes de datos ni el ID de publicidad del dispositivo. Además, cualquier Área de nombres de identidad creada en Adobe Experience Platform generará una fuente [!DNL Audience Manager] de datos correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de Área de nombres.
