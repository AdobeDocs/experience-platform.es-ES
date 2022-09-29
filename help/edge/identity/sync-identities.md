---
title: Sincronización de identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
description: Obtenga información sobre cómo sincronizar identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identidades;sinc. identidades;espacio de nombres;
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Sincronización de identidades entre Audience Manager y Experience Platform

El SDK web de Adobe Experience Platform admite la posibilidad de declarar los ID de cliente y sus estados de autenticación mediante la variable [sendEvent](./overview.md#syncing-identities) comando.

Elija las áreas de nombres en la [Espacios de nombres del servicio de identidad](../../identity/../identity-service/namespaces.md) para indicar el contexto al que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad :

![Vista de la interfaz de usuario de área de nombres](../assets/identity/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas las fuentes de datos existentes que utilicen el tipo de ID: Los dispositivos cruzados tienen automáticamente un área de nombres de identidad correspondiente. Para encontrar el área de nombres de identidad correspondiente a su fuente de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades .

Cualquier nuevo [!DNL Audience Manager] Fuente de datos que utiliza el tipo de ID: Entre dispositivos generará un área de nombres de identidad correspondiente. Los tipos de ID de fuentes de datos, cookies e ID de publicidad de dispositivo no son compatibles actualmente. Además, cualquier área de nombres de identidad creada en Adobe Experience Platform generará un [!DNL Audience Manager] Fuente de datos, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de área de nombres.
