---
description: Obtenga información sobre las cualificaciones de perfil históricas admitidas por los destinos creados con Destination SDK.
title: Calificaciones históricas de perfil
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Calificaciones históricas de perfil

De forma predeterminada, todos los destinos creados mediante Destination SDK admiten las cualificaciones de perfil del historial. Esto significa que, cuando los usuarios configuran por primera vez un flujo de datos de activación para sus destinos, la primera exportación contiene todos los miembros del segmento que alguna vez han cumplido los requisitos para ese segmento.

Este comportamiento se define mediante la variable `"backfillHistoricalProfileData":true` en la configuración de destino.

>[!IMPORTANT]
>
>Las cualificaciones de perfil históricas están habilitadas para todos los destinos creados mediante el Destination SDK y el `backfillHistoricalProfileData` no es configurable por el usuario.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## Pasos siguientes {#next-steps}

Después de leer este artículo, debe saber que el Experience Platform exporta automáticamente una población histórica de todos los perfiles que alguna vez hayan cumplido los requisitos para un segmento activado cuando el segmento se exporta por primera vez al destino. Esta opción no se puede configurar en el Destination SDK ni en la interfaz de usuario del Experience Platform.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Autenticación del cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Configuración por lotes](batch-configuration.md)