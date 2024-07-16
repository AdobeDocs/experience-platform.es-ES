---
title: Sincronización de identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
description: Obtenga información sobre cómo sincronizar identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identidades;identidades de sincronización;área de nombres;
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Sincronización de identidades entre Audience Manager y Experience Platform

El SDK web de Adobe Experience Platform admite la capacidad de declarar los ID de cliente y sus estados de autenticación mediante el comando [sendEvent](./overview.md#syncing-identities).

Elija sus áreas de nombres de [Área de nombres del servicio de identidad](../../identity/../identity-service/features/namespaces.md) para indicar el contexto al que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la interfaz de usuario de Áreas de nombres](../assets/identity/edge_namespaceUI_identity-symbol.png)

Audience Manager Como cliente de, todas las fuentes de datos existentes que utilicen el tipo de ID: entre dispositivos tienen automáticamente un área de nombres de identidad correspondiente. Para buscar el área de nombres de identidad correspondiente a su Source de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades.

Cualquier nuevo Source de datos [!DNL Audience Manager] que utilice el tipo de ID: entre dispositivos generará el área de nombres de identidad correspondiente. Actualmente no se admiten los tipos de ID de Data Source, ni la cookie ni el ID de Device Advertising. Además, cualquier área de nombres de identidad creada en Adobe Experience Platform generará un Source de datos [!DNL Audience Manager] correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de área de nombres.
