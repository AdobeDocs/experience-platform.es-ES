---
title: Sincronización de identidades con Audience Manager y Adobe Experience Platform
seo-title: Sincronización de identidades con Audience Manager y Adobe Experience Platform con Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo sincronizar identidades con Adobe Audience Manager con el SDK web Experience Platform
seo-description: Obtenga información sobre cómo sincronizar identidades con Adobe Audience Manager con el SDK web Experience Platform
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Sincronización de identidades

El SDK web de Adobe Experience Platform permite declarar los ID de cliente y sus estados de autenticación mediante el comando [sendEvent](./overview.md#syncing-identities) .

Elija sus Áreas de nombres en las Áreas de nombres [de servicio de](../../identity/../identity-service/namespaces.md) identidad para indicar el contexto con el que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la IU de Áreas de nombres](../../assets/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas las fuentes de datos existentes que utilicen el tipo de ID: Los dispositivos cruzados tienen automáticamente una Área de nombres de identidad correspondiente. Para encontrar la Área de nombres de identidad correspondiente para la fuente de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades.

Cualquier nueva fuente [!DNL Audience Manager] de datos que utilice el tipo de ID: Cross-Device generará una Área de nombres de identidad correspondiente. Actualmente no se admiten la cookie de tipos de ID de fuentes de datos ni el ID de publicidad del dispositivo. Además, cualquier Área de nombres de identidad creada en Adobe Experience Platform generará una fuente [!DNL Audience Manager] de datos correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de Área de nombres.
