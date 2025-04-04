---
title: Sincronización de identidades entre Audience Manager y Adobe Experience Platform mediante Experience Platform Web SDK
description: Obtenga información sobre cómo sincronizar identidades entre Audience Manager y Adobe Experience Platform mediante Experience Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identidades;identidades de sincronización;área de nombres;
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Sincronización de identidades entre Audience Manager y Experience Platform

Adobe Experience Platform Web SDK admite la capacidad de declarar los ID de cliente y sus estados de autenticación mediante el comando [sendEvent](./overview.md#syncing-identities).

Elija sus áreas de nombres de [Área de nombres del servicio de identidad](../../identity/../identity-service/features/namespaces.md) para indicar el contexto al que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la interfaz de usuario de Áreas de nombres](../assets/identity/edge_namespaceUI_identity-symbol.png)

Como cliente de Audience Manager, todas las fuentes de datos existentes que utilizan el tipo de ID: entre dispositivos tienen automáticamente un área de nombres de identidad correspondiente. Para encontrar el área de nombres de identidad correspondiente a su Source de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades.

Cualquier nuevo Source de datos [!DNL Audience Manager] que utilice el tipo de ID: entre dispositivos generará el área de nombres de identidad correspondiente. Actualmente no se admiten los tipos de ID de Data Source, ni la cookie ni el ID de Device Advertising. Además, cualquier área de nombres de identidad creada en Adobe Experience Platform generará un Source de datos [!DNL Audience Manager] correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de área de nombres.
