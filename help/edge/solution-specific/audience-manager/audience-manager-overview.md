---
title: Envío de datos al Administrador de Audiencias de Adobe
seo-title: Envío de datos a Adobe Audiencia Manager con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Audiencia Manager con el SDK web de la plataforma de experiencia
seo-description: Obtenga información sobre cómo enviar datos a Adobe Audiencia Manager con el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: dfe9ea2889b3ba2e74f8b10296bfb2d123ad9d57
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 2%

---


# (Beta) Administrador de Audiencias en la plataforma de experiencia de Edge Network

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

El SDK web de Adobe Experience Platform está integrado con Adobe Audiencia Manager y admite el envío y la recepción de datos desde el Administrador de Audiencias, los destinos de cookies y URL y la sincronización de ID.

## Activación del Administrador de Audiencias

Para habilitar el Administrador de Audiencias deberá hacer lo siguiente:

- Habilite el Administrador de Audiencias en la configuración [](../../fundamentals/edge-configuration.md)de Edge.
- Habilite o deshabilite los destinos de cookies y URL.
- Especifique el Contenedor de sincronización de ID para las sincronizaciones de socios externos (opcional)

## Sincronización de identidades

El SDK web de Adobe Experience Platform admite la capacidad de declarar los ID de cliente y sus estados de autenticación mediante el comando [SyncIdentity](../../fundamentals/identity.md) .

El método syncIdentity utiliza Áreas de nombres [de](../../../identity/../identity-service/namespaces.md) servicio de identidad para indicar el contexto con el que se relaciona una identidad. Como cliente del Administrador de Audiencias, todas las fuentes de datos existentes que utilicen el tipo de ID: El dispositivo cruzado tendrá automáticamente una Área de nombres de identidad correspondiente. Para encontrar la Área de nombres de identidad correspondiente para la fuente de datos de Audiencia Manager, inicie sesión en Adobe Experience Platform y vaya a la sección Identidades.

![Vista de la IU de Áreas de nombres](../../../assets/edge_configuration_identity.png)

Aquí puede buscar la fuente de datos del Administrador de Audiencias por nombre. El método syncIdentity utiliza el símbolo de identidad para establecer la Área de nombres.

Cualquier nueva fuente de datos del Administrador de Audiencias que utilice el tipo de ID: Cross-Device generará una Área de nombres de identidad correspondiente. Actualmente no se admiten la cookie de tipos de ID de fuentes de datos ni el ID de publicidad del dispositivo. Además, cualquier Área de nombres de identidad creada en Adobe Experience Platform generará la correspondiente fuente de datos de Audiencia Manager, pero tenga en cuenta que el método syncIdentity solo admite los símbolos de identidad de Área de nombres.
