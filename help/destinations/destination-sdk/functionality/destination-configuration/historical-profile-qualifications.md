---
description: Obtenga información acerca de las cualificaciones de perfil históricas admitidas por los destinos creados con Destination SDK.
title: Cualificaciones históricas del perfil
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# Cualificaciones históricas del perfil

Todos los destinos creados mediante Destination SDK admiten cualificaciones de perfil históricas de forma predeterminada. Esto significa que, cuando los usuarios configuran por primera vez un flujo de datos de activación en sus destinos, la primera exportación contiene todos los miembros de la audiencia que han cumplido los requisitos para ese segmento.

Este comportamiento se define mediante la variable `"backfillHistoricalProfileData":true` en la configuración de destino.

>[!IMPORTANT]
>
>Las cualificaciones de perfil históricas están habilitadas para todos los destinos creados mediante Destination SDK y `backfillHistoricalProfileData` El parámetro no se puede configurar por el usuario.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## Pasos siguientes {#next-steps}

Después de leer este artículo, debe saber que Experience Platform exporta automáticamente una población histórica de todos los perfiles que alguna vez se han clasificado para una audiencia activada cuando la audiencia se exporta por primera vez al destino. Esta opción no se puede configurar en Destination SDK ni en la interfaz de usuario de Experience Platform.

Para obtener más información acerca de los demás componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authorization.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de IU](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación compatibles](supported-mapping-configurations.md)
* [Envío de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)
