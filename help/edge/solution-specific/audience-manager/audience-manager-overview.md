---
title: Envío de datos al Adobe Audience Manager
seo-title: Envío de datos a Adobe Audience Manager con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Audience Manager con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo enviar datos a Adobe Audience Manager con el SDK web de Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] en el [!DNL Experience Platform Edge Network]

El Adobe Experience Platform [!DNL Web SDK] está integrado con Adobe Audience Manager y admite el envío y la recepción de datos desde los destinos de cookies [!DNL Audience Manager], URL y cookies y la sincronización de ID.

## Habilitación [!DNL Audience Manager]

Para habilitar [!DNL Audience Manager] tendrá que hacer lo siguiente:

- Habilite [!DNL Audience Manager] la configuración [de Edge](../../fundamentals/edge-configuration.md).
- Habilite o deshabilite los destinos de cookies y URL.
- Especifique el Contenedor de sincronización de ID para las sincronizaciones de socios externos (opcional)

## Sincronización de identidades

El Adobe Experience Platform [!DNL Web SDK] admite la capacidad de declarar los ID de cliente y sus estados de autenticación mediante el comando [SyncIdentity](../../fundamentals/identity.md) .

El método syncIdentity utiliza Áreas de nombres [de](../../../identity/../identity-service/namespaces.md) servicio de identidad para indicar el contexto con el que se relaciona una identidad. Como [!DNL Audience Manager] cliente, todas las fuentes de datos existentes que utilicen el tipo de ID: El dispositivo cruzado tendrá automáticamente un [!DNL Identity Namespace]valor correspondiente. Para encontrar el correspondiente [!DNL Identity Namespace] para su [!DNL Audience Manager Data Source], inicie sesión en el Adobe Experience Platform y vaya a la [!DNL Identities] sección .

![Vista de la IU de Áreas de nombres](../../../assets/edge_configuration_identity.png)

Aquí puede buscar la fuente [!DNL Audience Manager] de datos por nombre. El método syncIdentity utiliza el símbolo de identidad para establecer la Área de nombres.

Cualquier nueva fuente [!DNL Audience Manager] de datos que utilice el tipo de ID: Cross-Device generará una Área de nombres de identidad correspondiente. Actualmente no se admiten la cookie de tipos de ID de fuentes de datos ni el ID de publicidad del dispositivo. Además, cualquier Área de nombres de identidad creada en Adobe Experience Platform generará una fuente [!DNL Audience Manager] de datos correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de Área de nombres.
