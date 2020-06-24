---
title: Envío de datos al Adobe Audience Manager
seo-title: Envío de datos a Adobe Audience Manager con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Audience Manager con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo enviar datos a Adobe Audience Manager con el SDK web de Experience Platform
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager en la red Experience Platform Edge

El SDK web de Adobe Experience Platform está integrado con Adobe Audience Manager y admite el envío y la recepción de datos de destinos de Audience Manager, cookies y URL, así como la sincronización de ID.

## Activación del Audience Manager

Para habilitar el Audience Manager, deberá hacer lo siguiente:

- Habilite Audience Manager en la configuración [](../../fundamentals/edge-configuration.md)de Edge.
- Habilite o deshabilite los destinos de cookies y URL.
- Especifique el Contenedor de sincronización de ID para las sincronizaciones de socios externos (opcional)

## Sincronización de identidades

El SDK web de Adobe Experience Platform admite la capacidad de declarar los ID de cliente y sus estados de autenticación mediante el comando [SyncIdentity](../../fundamentals/identity.md) .

El método syncIdentity utiliza Áreas de nombres [de](../../../identity/../identity-service/namespaces.md) servicio de identidad para indicar el contexto con el que se relaciona una identidad. Como cliente Audience Manager, todas las fuentes de datos existentes que utilicen el tipo de ID: El dispositivo cruzado tendrá automáticamente una Área de nombres de identidad correspondiente. Para encontrar la Área de nombres de identidad correspondiente para la fuente de datos de Audience Manager, inicie sesión en el Adobe Experience Platform y vaya a la sección Identidades.

![Vista de la IU de Áreas de nombres](../../../assets/edge_configuration_identity.png)

Aquí puede buscar la fuente de datos de Audience Manager por nombre. El método syncIdentity utiliza el símbolo de identidad para establecer la Área de nombres.

Cualquier nueva fuente de datos de Audience Manager que utilice el tipo de ID: Cross-Device generará una Área de nombres de identidad correspondiente. Actualmente no se admiten la cookie de tipos de ID de fuentes de datos ni el ID de publicidad del dispositivo. Además, cualquier Área de nombres de identidad creada en Adobe Experience Platform generará una fuente de datos de Audience Manager correspondiente, pero tenga en cuenta que el método syncIdentity solo admite símbolos de identidad de Área de nombres.
