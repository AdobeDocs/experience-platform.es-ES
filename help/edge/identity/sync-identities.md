---
title: Sincronización de identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
description: Obtenga información sobre cómo sincronizar identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de Platform
seo-description: Obtenga información sobre cómo sincronizar identidades con Adobe Audience Manager con el SDK web de Experience Platform
keywords: audience manager;aam;identidades;sinc. identidades;espacio de nombres;
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Sincronización de identidades entre Audience Manager y Experience Platform

El SDK web de Adobe Experience Platform admite la capacidad de declarar ID de cliente y sus estados de autenticación mediante el comando [sendEvent](./overview.md#syncing-identities).

Elija las áreas de nombres de los [Espacios de nombres del servicio de identidad](../../identity/../identity-service/namespaces.md) para indicar el contexto al que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la interfaz de usuario de área de nombres](../images/identity/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas las fuentes de datos existentes que utilicen el tipo de ID: Los dispositivos cruzados tienen automáticamente un área de nombres de identidad correspondiente. Para encontrar el área de nombres de identidad correspondiente a su fuente de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades .

Cualquier fuente de datos [!DNL Audience Manager] nueva que utilice el tipo de ID: Entre dispositivos generará un área de nombres de identidad correspondiente. Los tipos de ID de fuentes de datos, cookies e ID de publicidad de dispositivo no son compatibles actualmente. Además, cualquier área de nombres de identidad creada en Adobe Experience Platform generará una fuente de datos [!DNL Audience Manager] correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de área de nombres.
