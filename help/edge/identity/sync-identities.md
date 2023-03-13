---
title: Sincronización de identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
description: Obtenga información sobre cómo sincronizar identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identidades;identidades de sincronización;área de nombres;
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Sincronización de identidades entre Audience Manager y Experience Platform

El SDK web de Adobe Experience Platform admite la capacidad de declarar ID de cliente y sus estados de autenticación mediante [sendEvent](./overview.md#syncing-identities) comando.

Elija sus áreas de nombres de la [Áreas de nombres del servicio de identidad](../../identity/../identity-service/namespaces.md) para indicar el contexto al que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la IU de áreas de nombres](../assets/identity/edge_namespaceUI_identity-symbol.png)

Audience Manager Como cliente de, todas las fuentes de datos existentes que utilicen el tipo de ID: entre dispositivos tienen automáticamente un área de nombres de identidad correspondiente. Para buscar el área de nombres de identidad correspondiente a la fuente de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades.

Cualquier nuevo [!DNL Audience Manager] Fuente de datos que utiliza Tipo de ID: Cross-Device generará un área de nombres de identidad correspondiente. Tipos de ID de fuentes de datos Actualmente no se admiten cookies ni ID de publicidad de dispositivo. Además, cualquier área de nombres de identidad creada en Adobe Experience Platform generará un [!DNL Audience Manager] Origen de datos, pero tenga en cuenta que el método syncIdentity sólo admite símbolos de identidad de espacio de nombres.
