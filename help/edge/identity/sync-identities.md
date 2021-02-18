---
title: Sincronización de identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de plataforma
description: Obtenga información sobre cómo sincronizar identidades entre Audience Manager y Adobe Experience Platform mediante el SDK web de plataforma
seo-description: Obtenga información sobre cómo sincronizar identidades con Adobe Audience Manager con el SDK web Experience Platform
keywords: administrador de audiencias;aam;identities;sync identities;Área de nombres;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Sincronización de identidades entre Audience Manager y Experience Platform

El SDK web de Adobe Experience Platform admite la capacidad de declarar ID de cliente y sus estados de autenticación mediante el comando [sendEvent](./overview.md#syncing-identities).

Elija sus Áreas de nombres en las [Áreas de nombres de servicio de identidad](../../identity/../identity-service/namespaces.md) para indicar el contexto al que se relaciona una identidad, utilizando los valores de la columna Símbolo de identidad:

![Vista de la IU de Áreas de nombres](../../assets/edge_namespaceUI_identity-symbol.png)

Como cliente Audience Manager, todas las fuentes de datos existentes que utilicen el tipo de ID: Los dispositivos cruzados tienen automáticamente una Área de nombres de identidad correspondiente. Para encontrar la Área de nombres de identidad correspondiente para la fuente de datos de Audience Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades.

Cualquier nueva fuente de datos [!DNL Audience Manager] que utilice el tipo de ID: Cross-Device generará una Área de nombres de identidad correspondiente. Actualmente no se admiten la cookie de tipos de ID de fuentes de datos ni el ID de publicidad del dispositivo. Además, cualquier Área de nombres de identidad creada en Adobe Experience Platform generará una fuente de datos [!DNL Audience Manager] correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de Área de nombres.
